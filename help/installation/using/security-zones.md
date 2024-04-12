---
product: campaign
title: セキュリティゾーンの設定
description: セキュリティゾーンの設定方法を学ぶ
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 67dda58f-97d1-4df5-9648-5f8a1453b814
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 15%

---

# セキュリティゾーンの定義（オンプレミス）{#defining-security-zones}



インスタンスにログオンするには、各オペレーターがゾーンにリンクされている必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットにオペレーターの IP が含まれている必要があります。セキュリティゾーンの設定は、Adobe Campaign サーバーの設定ファイルで実行されます。

オペレーターは、クライアントコンソールでオペレーターのプロファイルからセキュリティゾーンにリンクされます。オペレーターのプロファイルは **[!UICONTROL 管理/ アクセス管理/ オペレーター]** ノード。 [詳細情報](#linking-a-security-zone-to-an-operator)。

>[!NOTE]
>
>この手順は、次の場合に制限されます **オンプレミス** のデプロイメント。
>
>As a **hosted** 顧客（アクセス可能な場合） [キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)セキュリティーゾーンのセルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html?lang=ja)
>
>その他 **ハイブリッド/ホスト** お客様は、Adobe許可リストに加える サポートチームに連絡して、IP をチームに追加する必要があります。
>

## セキュリティゾーンの作成 {#creating-security-zones}

ゾーンは、次の方法で定義されます。

* 1 つまたは複数の IP アドレスの範囲（IPv4 および IPv6）
* ip アドレスの各範囲に関連付けられた技術名

セキュリティゾーンは連動しています。つまり、別のゾーン内に新しいゾーンを定義すると、そのゾーンにログオンできるオペレーターの数が減るとともに、各オペレーターに割り当てられる権限が増えます。

ゾーンは、サーバーの構成時に、次で定義する必要があります **serverConf.xml** ファイル。 で使用できるすべてのパラメーター **serverConf.xml** の一覧を次に示します [この節](../../installation/using/the-server-configuration-file.md).

各ゾーンでは、次のような権限を定義します。

* HTTPS ではなく HTTP 接続
* エラー表示（Java エラー、JavaScript、C++など）
* レポートと web アプリのプレビュー
* ログイン/パスワードによる認証
* 非セキュア接続モード

>[!NOTE]
>
>**各演算子はゾーンにリンクされている必要があります**. オペレーターの IP アドレスがゾーンで定義された範囲に属する場合、オペレーターはインスタンスにログオンできます。\
>オペレーターの IP アドレスは、複数のゾーンで定義できます。 この場合、オペレーターは次を受け取ります **set** （各ゾーンで使用可能な権限）。

標準搭載 **serverConf.xml** ファイルには、次の 3 つのゾーンが含まれています。 **パブリック、VPN、および LAN**.

>[!NOTE]
>
>**標準提供の設定はセキュリティで保護されています**. ただし、以前のバージョンのAdobe Campaignから移行する前に、新しいルールを移行して承認するために、セキュリティを一時的に軽減する必要が生じる場合があります。

でのゾーンの定義方法の例 **serverConf.xml** ファイル：

```
<securityZone allowDebug="false" allowHTTP="false" label="Public Network" name="public">
<subNetwork label="All addresses" mask="*" name="all"/>

<securityZone allowDebug="true" allowHTTP="false" label="Private Network (VPN)"
              name="vpn" showErrors="true">

  <securityZone allowDebug="true" allowEmptyPassword="true" allowHTTP="true"
                allowUserPassword="false" label="Private Network (LAN)" name="lan"
                sessionTokenOnly="true" showErrors="true">
    <subNetwork label="Lan 1" mask="192.168.0.0/16" name="lan1"/>
    <subNetwork label="Lan 2" mask="172.16.0.0/12" name="lan2"/>
    <subNetwork label="Lan 3" mask="10.0.0.0/8" name="lan3"/>
    <subNetwork label="Localhost" mask="127.0.0.1/16" name="locahost"/>
    <subNetwork label="Lan (IPv6)" mask="fc00::/7" name="lan6"/>
    <subNetwork label="Localhost (IPv6)" mask="::1/128" name="localhost6"/>
  </securityZone>

</securityZone>
</securityZone>
```

ゾーンを定義する権限は次のとおりです。

* **allowDebug**:web アプリを「デバッグ」モードで実行できるようにします
* **allowEmptyPassword**：パスワードを使用せずにインスタンスへの接続を認証します
* **allowHTTP**:HTTPS プロトコルを使用せずにセッションを作成できます
* **allowUserPassword**：セッショントークンの形式は次のとおりです」`<login>/<password>`“
* **sessionTokenOnly**：接続 URL にセキュリティトークンは必要ありません
* **showErrors**：サーバーサイドのエラーは転送され、表示されます

>[!IMPORTANT]
>
>ゾーン定義では、各属性は **true** 値を指定するとセキュリティが低下します。

Message Center を使用していて、複数の実行インスタンスがある場合は、 **sessionTokenOnly** 属性の定義： **true**&#x200B;を使用する場合は、必要な IP アドレスのみ追加されます。 インスタンスの設定について詳しくは、次を参照してください： [このドキュメント](../../message-center/using/configuring-instances.md).

## セキュリティゾーンのベストプラクティス {#best-practices-for-security-zones}

の定義 **lan** セキュリティゾーン。技術的なアクセスを定義する IP アドレスマスクを追加できます。 この追加により、サーバーでホストされているすべてのインスタンスにアクセスできるようになります。

```
<securityZone allowDebug="true" allowEmptyPassword="false" allowHTTP="true"
                    allowUserPassword="false" label="Private Network (LAN)" name="lan"
                    sessionTokenOnly="true" showErrors="true">
        <subNetwork label="Lan 1" mask="192.168.0.0/16" name="lan1"/>
        <subNetwork label="Lan 2" mask="172.16.0.0/12" name="lan2"/>
        <subNetwork label="Lan 3" mask="10.0.0.0/8" name="lan3"/>
        <subNetwork label="Localhost" mask="127.0.0.1/16" name="locahost"/>
        <subNetwork label="Lan (IPv6)" mask="fc00::/7" name="lan6"/>
        <subNetwork label="Localhost (IPv6)" mask="::1/128" name="localhost6"/>
  
        <!-- Customer internal IPs -->
        <subNetwork id="internalNetwork" mask="a.b.c.d/xx"/>

      </securityZone>
```

特定のインスタンスにのみアクセスするオペレーター向けに、インスタンス専用の設定ファイルで IP アドレスの範囲を直接定義することをお勧めします。

が含まれる **`config-<instance>.xml`** ファイル：

```
  <securityZone name="public">
   ...
    <securityZone name="vpn">
      <subNetwork id="cus1" mask="a.b.c.d/xx"/>
```

## セキュリティゾーン内のサブネットワークとプロキシ {#sub-networks-and-proxies-in-a-security-zone}

この **委任状** パラメーターは、 **subNetwork** セキュリティゾーンでのプロキシの使用を指定する要素。

プロキシが参照され、このプロキシ経由で（HTTP X-Forwarded-For ヘッダーを介して表示される）接続が入ると、検証されたゾーンは、プロキシのクライアントのゾーンであり、プロキシのゾーンではありません。

>[!IMPORTANT]
>
>プロキシが設定されていて、それを上書きできる（または存在しない場合に上書きする）場合、テストされる IP アドレスは偽造される可能性があります。
>
>さらに、プロキシと同様にリレーが生成されるようになりました。 したがって、IP アドレス 127.0.0.1 をセキュリティゾーン設定のプロキシのリストに追加できます。
>
>例：&quot; `<subnetwork label="Lan 1" mask="192.168.0.0/16" name="lan1" proxy="127.0.0.1,10.100.2.135" />`」と入力します。

次のような様々なケースが発生する可能性があります。

* サブネットワークはセキュリティゾーンで直接参照され、プロキシは設定されません。サブネットワークのユーザーは、Adobe Campaign サーバーに直接接続できます。

  ![](assets/8101_proxy1.png)

* セキュリティゾーンのサブネットワークにプロキシが指定されています。このサブネットワークのユーザーは、このプロキシを介してAdobe Campaign サーバーにアクセスできます。

  ![](assets/8101_proxy2.png)

* プロキシは、セキュリティゾーンサブネットワークに含まれます。接触チャネルに関係なく、このプロキシを通じてアクセスできるユーザーは、Adobe Campaign サーバーにアクセスできます。

  ![](assets/8101_proxy3.png)

Adobe Campaign サーバーにアクセスする可能性があるプロキシの IP アドレスは、次の両方に入力する必要があります **`<subnetwork>`** 関心のある第 1 レベルのサブネットワーク **`<subnetwork name="all"/>`**. 例えば、IP アドレスが 10.131.146.102 のプロキシの場合、次のようになります。

```
<securityZone allowDebug="false" allowHTTP="false" label="Public Network" 
                      name="public">
    <subNetwork label="All addresses" mask="*" name="all"
                      proxy="10.131.146.102,127.0.0.1, ::1"/>

    <securityZone allowDebug="true" allowHTTP="false" label="Private Network (VPN)" 
                      name="vpn" showErrors="true">
        <securityZone allowDebug="true" allowEmptyPassword="false" allowHTTP="true" 
                      allowUserPassword="false" label="Private Network (LAN)" 
                      name="lan" sessionTokenOnly="true" showErrors="true">
            <subNetwork label="Lan proxy" mask="10.131.193.182" name="lan3" 
                      proxy="10.131.146.102,127.0.0.1, ::1"/>
            <subNetwork label="Lan 1" mask="192.168.0.0/16" name="lan1" 
                      proxy="127.0.0.1, ::1"/>

        </securityZone>
    </securityZone>
</securityZone>
```

## セキュリティゾーンのオペレーターへのリンク {#linking-a-security-zone-to-an-operator}

ゾーンを定義したら、インスタンスにログオンできるようにするには、各オペレーターをそのうちの 1 つにリンクする必要があります。また、オペレーターの IP アドレスを、ゾーンで参照されるアドレスまたはアドレスの範囲に含める必要があります。

ゾーンの技術的な設定は、Campaign サーバーの設定ファイルで実行されます。 **serverConf.xml**.

この前に、すぐに使用できる設定から始める必要があります **[!UICONTROL セキュリティゾーン]** で定義されているゾーンの内部名にラベルをリンクするための列挙 **serverConf.xml** ファイル。

この設定は、Campaign エクスプローラーで行います。

1. 「」をクリックします **[!UICONTROL 管理/ プラットフォーム /列挙]** ノード。
1. 「」を選択します **[!UICONTROL セキュリティゾーン （securityZone）]** システム列挙。

   ![](assets/enum_securityzone.png)

1. サーバーの構成ファイルで定義された各セキュリティゾーンに対して、 **[!UICONTROL 追加]** ボタン。
1. が含まれる **[!UICONTROL 内部名]** フィールドに、で定義されたゾーンの名前を入力します。 **serverConf.xml** ファイル。 これは **@name** 属性 `<securityzone>`  要素。 内の内部名にリンクされているラベルを  **ラベル**&#x200B;フィールド。

   ![](assets/enum_addsecurityvalue.png)

1. 「OK」をクリックして、変更を保存します。

ゾーンを定義し、 **[!UICONTROL セキュリティゾーン]** 定義済みリストが設定されています。各演算子をセキュリティゾーンにリンクする必要があります。

1. 「」をクリックします **[!UICONTROL 管理/ アクセス管理/ オペレーター]** ノード。
1. セキュリティゾーンのリンク先となるオペレーターを選択し、 **[!UICONTROL 編集]** タブ。
1. に移動します **[!UICONTROL アクセス権]** tab キーを押しながら **[!UICONTROL アクセスパラメーターを編集…]** リンク。

   ![](assets/zone_operator.png)

1. 「」からゾーンを選択 **[!UICONTROL 許可された接続ゾーン]** ドロップダウンリスト

   ![](assets/zone_operator_selection.png)

1. クリック **[!UICONTROL OK]** 変更を保存して、これらの変更を適用します。



## 推奨事項

* のリバースプロキシが subNetwork で許可されていないことを確認してください。 許可されている場合は、**すべての**&#x200B;トラフィックがこのローカル IP から来ているものとして検出され、信頼されます。

* sessionTokenOnly=&quot;true&quot;の使用を最小限に抑える

   * 警告：この属性を true に設定すると、演算子を **CRSF 攻撃**.
   * さらに、sessionToken cookie は httpOnly フラグで設定されていないので、一部のクライアントサイド JavaScript コードは読み取ることができます。
   * ただし、複数の実行セルで Message Center が sessionTokenOnly を必要とします。新しいセキュリティゾーンを作成し、sessionTokenOnly を true に設定して、**必要な IP のみ**&#x200B;をこのゾーンに追加します。

* 可能な場合は、すべての allowHTTP、showErrors を false に設定し（localhost の場合ではない）、それらを確認します。

   * allowHTTP = &quot;false&quot;：オペレーターは HTTPS を使用することを強制されます。
   * showErrors = &quot;false&quot;：技術的なエラー（SQL エラーを含む）を非表示にします。 これにより、表示される情報の量を抑えられますが、マーケターが（管理者に追加情報を要求することなしに）問題を解決することが難しくなります。

* allowDebug を true に設定するのは、調査、web アプリ、レポートを（実際にプレビューで）作成する必要があるマーケティングユーザーや管理者が使用する IP のみです。 このフラグを使用すると、これらの IP でリレールールが表示され、デバッグできるようになります。

   * allowDebug を false に設定すると、次のように出力されます。

     ```
     <redir status='OK' date='...' sourceIP='...'/>
     ```

   * allowDebug を true に設定すると、出力は次のようになります。

     ```
     <redir status='OK' date='...' build='...' OR version='...' sha1='...' instance='...' sourceIP='...' host='...' localHost='...'/>
     ```

* allowEmptyPassword、allowUserPassword、allowSQLInjection を true に設定しないでください。

   * **allowEmptyPassword** オペレーターが空のパスワードを持つことができます。 その場合は、すべてのオペレーターに通知して、期限を設定したパスワードの設定を依頼してください。 この期限を経過したら、この属性を false に設定します。

   * **allowUserPassword** オペレーターは、資格情報をパラメーターとして送信できます（これにより、オペレーターは Apache/IIS/プロキシに記録されます）。 この機能は、API の使用を簡素化するために以前に使用されていました。 クックブック（または仕様）で、サードパーティのアプリケーションで使用されているかどうかを確認できます。 使用されている場合、API の使用方法を変更して、なるべく早くこの機能を削除するよう通知する必要があります。

   * **allowSQLInjection** ユーザーは古い構文を使用して SQL 挿入を実行できます。 この属性は false に設定する必要があります。 /nl/jsp/ping.jsp?zones=true を使用して、セキュリティゾーンの設定を確認できます。 このページには、現在の IP のセキュリティ対策のアクティブステータス（これらのセキュリティフラグで計算）が表示されます。

* HttpOnly cookie／useSecurityToken：**sessionTokenOnly** フラグを参照してください。

* 許可リストに追加する IP を最小限に抑える^標準搭載のセキュリティゾーンでは、プライベートネットワーク用に 3 つの範囲を追加しました。 これらの IP アドレスをすべて使用することはほとんどありません。 そのため、必要なもののみを保持するようにしてください。

* webApp／内部オペレーターを更新して、localhost でのみアクセス可能となるようにしてください。
