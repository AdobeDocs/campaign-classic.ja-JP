---
product: campaign
title: セキュリティゾーンの設定
description: セキュリティゾーンの構成方法を説明します
audience: installation
content-type: reference
topic-tags: additional-configurations
source-git-commit: e719c8c94f1c08c6601b3386ccd99d250c9e606b
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 29%

---

# セキュリティゾーンの定義（オンプレミス）{#defining-security-zones}

![](../../assets/v7-only.svg)

インスタンスにログオンするには、各オペレーターがゾーンにリンクされている必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレスセットにオペレーターの IP が含まれている必要があります。セキュリティゾーンの設定は、Adobe Campaign サーバーの設定ファイルで実行されます。

オペレーターは、クライアントコンソールでオペレーターのプロファイルからセキュリティゾーンにリンクされます。オペレーターのプロファイルは、**[!UICONTROL 管理／アクセス管理／オペレーター]**&#x200B;ノードでアクセスできます。[詳細情報](#linking-a-security-zone-to-an-operator)。

>[!NOTE]
>
>この手順は、**オンプレミス** のデプロイメントに制限されます。
>
>**ホスト** のお客様は、[ キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja) にアクセスできる場合、セキュリティゾーンセルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html?lang=ja)
>
>その他の **ハイブリッド/ホスト型** のお客様は、Adobeに IP を追加するために、サポートチームに連絡する必要があ許可リストります。

## セキュリティゾーンの作成 {#creating-security-zones}

ゾーンは次の方法で定義します。

* 1 つ以上の IP アドレス範囲（IPv4 および IPv6）
* IP アドレスの各範囲に関連付けられた技術的な名前

セキュリティゾーンは相互にロックされています。つまり、別のゾーン内に新しいゾーンを定義すると、各オペレーターに割り当てられる権限を増やしながら、そのゾーンにログオンできるオペレーターの数が減ります。

ゾーンは、サーバーの設定時に **serverConf.xml** ファイルで定義する必要があります。 **serverConf.xml** で使用できるすべてのパラメーターは、[ この節 ](../../installation/using/the-server-configuration-file.md) に記載されています。

各ゾーンは、次のような権限を定義します。

* HTTPS ではなく HTTP 接続
* エラー表示 (Java エラー、JavaScript、C++など )
* レポートと Web アプリのプレビュー
* ログイン/パスワードによる認証
* 非セキュア接続モード

>[!NOTE]
>
>**各オペレーターは、ゾーン**&#x200B;にリンクされている必要があります。オペレーターの IP アドレスがゾーンで定義された範囲に属している場合、オペレーターはインスタンスにログオンできます。\
>オペレーターの IP アドレスは、複数のゾーンに定義できます。 この場合、各ゾーンに対して使用可能な権限の **set** を受け取ります。

標準の **serverConf.xml** ファイルには、次の 3 つのゾーンが含まれています。**public、VPN、LAN**。

>[!NOTE]
>
>**標準設定は安全です**。ただし、以前のバージョンのAdobe Campaignから移行する前に、新しいルールを移行して承認するために、セキュリティを一時的に低減する必要が生じる場合があります。

**serverConf.xml** ファイルでのゾーンの定義方法の例：

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

ゾーンを定義するすべての権限は次のとおりです。

* **allowDebug**:webApp を「デバッグ」モードで実行できるようにします。
* **allowEmptyPassword**:パスワードなしでインスタンスへの接続を許可する
* **allowHTTP**:HTTPS プロトコルを使用せずにセッションを作成できる
* **allowUserPassword**:セッショントークンは、「`<login>/<password>`」の形式を使用できます。
* **sessionTokenOnly**:接続 URL にセキュリティトークンは必要ありません
* **showErrors**:サーバー側のエラーが転送され、表示されます

>[!IMPORTANT]
>
>ゾーン定義では、**true** 値を持つ各属性によってセキュリティが低下します。

Message Center を使用する場合、複数の実行インスタンスがある場合は、**sessionTokenOnly** 属性を **true** に定義し、必要な IP アドレスのみを追加するセキュリティゾーンを追加する必要があります。 インスタンスの設定について詳しくは、[ このドキュメント ](../../message-center/using/configuring-instances.md) を参照してください。

## セキュリティゾーンのベストプラクティス {#best-practices-for-security-zones}

**lan** セキュリティゾーンの定義では、テクニカルアクセスを定義する IP アドレスマスクを追加できます。 この追加により、サーバーでホストされるすべてのインスタンスにアクセスできます。

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

IP アドレスの範囲は、特定のインスタンスにのみアクセスするオペレーター向けの、インスタンス専用の設定ファイルで直接定義することをお勧めします。

**`config-<instance>.xml`** ファイル内：

```
  <securityZone name="public">
   ...
    <securityZone name="vpn">
      <subNetwork id="cus1" mask="a.b.c.d/xx"/>
```

## セキュリティゾーンのサブネットワークとプロキシ {#sub-networks-and-proxies-in-a-security-zone}

**proxy** パラメーターは、**subNetwork** 要素で使用して、セキュリティゾーンでのプロキシの使用を指定できます。

プロキシが参照され、接続がこのプロキシ経由で入る（HTTP X-Forwarded-For ヘッダー経由で表示される）場合、検証されたゾーンはプロキシのクライアントのゾーンであり、プロキシのクライアントのゾーンではありません。

>[!IMPORTANT]
>
>プロキシが設定され、上書きできる場合（または存在しない場合）は、テスト対象の IP アドレスを偽造できます。
>
>さらに、リレーはプロキシのように生成されます。 したがって、IP アドレス 127.0.0.1 をセキュリティゾーン設定のプロキシのリストに追加できます。
>
>例：&quot; `<subnetwork label="Lan 1" mask="192.168.0.0/16" name="lan1" proxy="127.0.0.1,10.100.2.135" />`&quot;

様々なケースが発生する可能性があります。

* サブネットワークはセキュリティゾーンで直接参照され、プロキシは設定されません。サブネットワークのユーザーは、Adobe Campaignサーバーに直接接続できます。

   ![](assets/8101_proxy1.png)

* セキュリティゾーンのサブネットワークにプロキシが指定されています：このサブネットワークのユーザーは、このプロキシ経由でAdobe Campaignサーバーにアクセスできます。

   ![](assets/8101_proxy2.png)

* プロキシは、セキュリティゾーンのサブネットワークに含まれます。このプロキシを通じてアクセスできるユーザーは、接続元に関係なく、Adobe Campaignサーバーにアクセスできます。

   ![](assets/8101_proxy3.png)

Adobe Campaignサーバーにアクセスする可能性が高いプロキシの IP アドレスは、該当する **`<subnetwork>`** と第 1 レベルのサブネットワーク **`<subnetwork name="all"/>`** の両方に入力する必要があります。 例えば、IP アドレスが 10.131.146.102 のプロキシの場合：

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

## セキュリティゾーンをオペレーターにリンクする {#linking-a-security-zone-to-an-operator}

ゾーンを定義したら、各オペレーターをいずれかのオペレーターにリンクして、インスタンスにログオンできるようにする必要があります。また、ゾーンで参照されるアドレスまたはアドレスの範囲に、オペレーターの IP アドレスを含める必要があります。

ゾーンの技術的な設定は、Campaign サーバーの設定ファイルで実行します。**serverConf.xml** です。

まず、標準の **[!UICONTROL セキュリティゾーン]** 列挙を設定して、**serverConf.xml** ファイルで定義されたゾーンの内部名にラベルをリンクする必要があります。

この設定は、Campaign エクスプローラーでおこないます。

1. **[!UICONTROL 管理/プラットフォーム/列挙]** ノードをクリックします。
1. **[!UICONTROL セキュリティゾーン (securityZone)]** システム列挙を選択します。

   ![](assets/enum_securityzone.png)

1. サーバーの構成ファイルで定義された各セキュリティゾーンに対して、**[!UICONTROL Add]** ボタンをクリックします。
1. 「**[!UICONTROL 内部名]**」フィールドに、**serverConf.xml** ファイルで定義したゾーンの名前を入力します。 `<securityzone>` 要素の **@name** 属性に対応します。 **ラベル** フィールドに、内部名にリンクされたラベルを入力します。

   ![](assets/enum_addsecurityvalue.png)

1. 「OK」をクリックし、変更を保存します。

ゾーンを定義し、**[!UICONTROL セキュリティゾーン]** 列挙を設定したら、各オペレーターをセキュリティゾーンにリンクする必要があります。

1. **[!UICONTROL 管理/アクセス管理/オペレーター]** ノードをクリックします。
1. セキュリティゾーンをリンクするオペレーターを選択し、「**[!UICONTROL 編集]**」タブをクリックします。
1. 「**[!UICONTROL アクセス権]**」タブに移動し、「**[!UICONTROL アクセスパラメーターを編集…」をクリックします。]** リンク。

   ![](assets/zone_operator.png)

1. 「**[!UICONTROL 許可された接続ゾーン]**」ドロップダウンリストからゾーンを選択します。

   ![](assets/zone_operator_selection.png)

1. 「**[!UICONTROL OK]**」をクリックし、変更を保存して変更を適用します。



## 推奨事項

* subNetwork でリバースプロキシが許可されていないことを確認します。許可されている場合は、**すべての**&#x200B;トラフィックがこのローカル IP から来ているものとして検出され、信頼されます。

* sessionTokenOnly=&quot;true&quot; の使用は最小限に抑えます。

   * 警告：この属性が true に設定されている場合、オペレーターは **CRSF 攻撃** にさらされる可能性があります。
   * また、 sessionToken Cookie に httpOnly フラグが設定されていないので、一部のクライアント側 JavaScript コードで読み取ることができます。
   * ただし、複数の実行セルで Message Center が sessionTokenOnly を必要とします。新しいセキュリティゾーンを作成し、sessionTokenOnly を true に設定して、**必要な IP のみ**&#x200B;をこのゾーンに追加します。

* 可能な場合は、allowHTTP と showErrors をすべて false に設定し（localhost ではない）、確認します。

   * allowHTTP = &quot;false&quot;：オペレーターは HTTPS を使用することを強制されます。
   * showErrors = &quot;false&quot;：技術的エラー（SQL エラーなど）を非表示にします。これにより、表示される情報の量を抑えられますが、マーケターが（管理者に追加情報を要求することなしに）問題を解決することが難しくなります。

* 調査、webApp、レポートを作成（実際にはプレビュー）する必要があるマーケティングユーザーまたは管理者が使用する IP に対してのみ、allowDebug を true に設定します。このフラグを使用すると、これらの IP でリレールールが表示され、デバッグできるようになります。

* allowEmptyPassword、allowUserPassword、allowSQLInjection は決して true に設定しないでください。これらの属性は、v5 や v6.0 からの移行のためだけにあります。

   * **allowEmptyPassword** を使用すると、オペレーターは空のパスワードを設定できます。この属性を使用する場合、すべてのオペレーターに所定の期限までにパスワードを設定するよう通知してください。この期限を経過したら、この属性を false に設定します。

   * **allowUserPassword** を使用すると、オペレーターは資格情報をパラメーターとして送信できます（この情報は、Apache、IIS、プロキシでログに記録されます）。この機能は、以前に API の使用を簡素化するために使用されていました。クックブック（または仕様）で、サードパーティのアプリケーションがこれを使用していないかをチェックできます。使用されている場合、API の使用方法を変更して、なるべく早くこの機能を削除するよう通知する必要があります。

   * **allowSQLInjection** を使用すると、ユーザーは古い構文を使用した SQL インジェクションを実行できます。[ このページ ](../../migration/using/general-configurations.md) で説明されている修正を、できるだけ早く行い、この属性を false に設定できるようにします。 /nl/jsp/ping.jsp?zones=true を使用すると、セキュリティゾーン設定をチェックできます。このページには、現在の IP のセキュリティ対策のアクティブステータス（これらのセキュリティフラグで計算）が表示されます。

* HttpOnly cookie／useSecurityToken：**sessionTokenOnly** フラグを参照してください。

* に追加される IP を最小許可リスト化：標準では、セキュリティゾーンに、プライベートネットワーク用の 3 つの範囲を追加しました。 通常、これらの IP アドレスをすべて使用することはありません。そのため、必要なもののみを保持するようにしてください。

* webApp／内部オペレーターを更新して、localhost でのみアクセス可能となるようにしてください。
