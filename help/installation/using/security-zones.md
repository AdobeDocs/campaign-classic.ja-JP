---
product: campaign
title: セキュリティゾーンの設定
description: セキュリティゾーンの構成方法を説明します
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 67dda58f-97d1-4df5-9648-5f8a1453b814
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 27%

---


# セキュリティゾーンの定義（オンプレミス）{#defining-security-zones}

インスタンスにログオンするには、各オペレーターをゾーンにリンクする必要があります。また、セキュリティゾーンに定義されているアドレスまたはアドレスセットにオペレーターのIPを含める必要があります。 セキュリティゾーンの設定は、Adobe Campaignサーバーの設定ファイルで実行されます。

オペレーターは、コンソール内のプロファイルからセキュリティゾーンにリンクされ、**[!UICONTROL 管理/アクセス管理/オペレーター]**&#x200B;ノードでアクセスできます。 [詳細情報](#linking-a-security-zone-to-an-operator)。

>[!NOTE]
>
>この手順は、**オンプレミス**&#x200B;デプロイメントに制限されます。
>
>**ホスト**&#x200B;のお客様は、[キャンペーンCampaign コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/control-panel-home.html?lang=ja)にアクセスできる場合、セキュリティゾーンセルフサービスインターフェイスを使用できます。 [詳細情報](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/ip-allow-listing-instance-access.html?lang=ja)
>
>その他の&#x200B;**ハイブリッド/ホスト型**&#x200B;のお客様は、Adobeサポートチームに連絡して、許可リストにIPを追加する必要があります。


## セキュリティゾーンの作成{#creating-security-zones}

ゾーンは、次の方法で定義します。

* 1つ以上のIPアドレスの範囲（IPv4およびIPv6）
* IPアドレスの各範囲に関連付けられた技術的な名前

セキュリティゾーンは相互にロックされています。つまり、別のゾーン内に新しいゾーンを定義すると、各オペレーターに割り当てられる権限を増やしながら、そのゾーンにログオンできるオペレーターの数が減ります。

ゾーンは、サーバーの設定時に&#x200B;**serverConf.xml**&#x200B;ファイルで定義する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、[この節](../../installation/using/the-server-configuration-file.md)に記載されています。

各ゾーンは、次のような権限を定義します。

* HTTPSではなくHTTP接続
* エラー表示(Javaエラー、JavaScript、C++など)
* レポートとWebアプリのプレビュー
* ログイン/パスワードによる認証
* 非セキュア接続モード

>[!NOTE]
>
>**各オペレーターは、ゾーンにリンクされている必要があります**。オペレーターのIPアドレスがゾーンで定義された範囲に属する場合、オペレーターはインスタンスにログオンできます。\
>オペレーターのIPアドレスは、複数のゾーンに定義できます。 この場合、オペレーターは各ゾーンに対して使用可能な権限の&#x200B;**set**&#x200B;を受け取ります。

標準搭載の&#x200B;**serverConf.xml**&#x200B;ファイルには、次の3つのゾーンが含まれています。**public、VPN、およびLAN**。

>[!NOTE]
>
>**標準設定は安全です**。ただし、以前のバージョンのAdobe Campaignから移行する前に、新しいルールを移行して承認するために、セキュリティを一時的に低減する必要が生じる場合があります。

**serverConf.xml**&#x200B;ファイルでのゾーンの定義方法の例：

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

* **allowDebug**:webAppを「デバッグ」モードで実行できるようにします。
* **allowEmptyPassword**:パスワードを使用せずにインスタンスへの接続を許可する
* **allowHTTP**:HTTPSプロトコルを使用せずにセッションを作成できる
* **allowUserPassword**:セッショントークンは、「`<login>/<password>`」の形式を使用できます。
* **sessionTokenOnly**:接続URLにセキュリティトークンは不要です
* **showErrors**:サーバー側のエラーが転送され、表示されます

>[!IMPORTANT]
>
>ゾーン定義では、**true**&#x200B;値を持つ各属性によってセキュリティが低下します。

Message Centerを使用する場合、複数の実行インスタンスがある場合は、**sessionTokenOnly**&#x200B;属性を&#x200B;**true**&#x200B;に定義して追加のセキュリティゾーンを作成する必要があります。この場合、必要なIPアドレスのみを追加します。 インスタンスの設定について詳しくは、[このドキュメント](../../message-center/using/configuring-instances.md)を参照してください。

## セキュリティゾーンのベストプラクティス{#best-practices-for-security-zones}

**lan**&#x200B;セキュリティゾーンの定義では、テクニカルアクセスを定義するIPアドレスマスクを追加できます。 この追加により、サーバーでホストされるすべてのインスタンスにアクセスできます。

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

特定のインスタンスにのみアクセスするオペレーターには、そのインスタンス専用の設定ファイルでIPアドレス範囲を直接定義することをお勧めします。

**`config-<instance>.xml`**&#x200B;ファイル内：

```
  <securityZone name="public">
   ...
    <securityZone name="vpn">
      <subNetwork id="cus1" mask="a.b.c.d/xx"/>
```

## セキュリティゾーン{#sub-networks-and-proxies-in-a-security-zone}のサブネットワークとプロキシ

**proxy**&#x200B;パラメーターは、**subNetwork**&#x200B;要素で使用して、セキュリティゾーンでのプロキシ使用を指定できます。

プロキシが参照され、接続がこのプロキシ経由で入る（HTTP X-Forwarded-Forヘッダー経由で表示される）場合、検証されたゾーンはプロキシのクライアントのゾーンではなく、プロキシのクライアントのゾーンです。

>[!IMPORTANT]
>
>プロキシが設定され、上書き可能な場合（または存在しない場合）は、テスト対象のIPアドレスを改ざんできます。
>
>さらに、リレーはプロキシのように生成されます。 したがって、IPアドレス127.0.0.1をセキュリティゾーン設定のプロキシのリストに追加できます。
>
>例：&quot; `<subnetwork label="Lan 1" mask="192.168.0.0/16" name="lan1" proxy="127.0.0.1,10.100.2.135" />`&quot;と入力します。

様々なケースが発生する可能性があります。

* サブネットワークはセキュリティゾーンで直接参照され、プロキシは設定されません。サブネットワークのユーザーは、Adobe Campaignサーバーに直接接続できます。

   ![](assets/8101_proxy1.png)

* セキュリティゾーンのサブネットワークに対してプロキシが指定されています。このサブネットワークのユーザーは、このプロキシを介してAdobe Campaignサーバーにアクセスできます。

   ![](assets/8101_proxy2.png)

* プロキシは、セキュリティゾーンのサブネットワークに含まれます。このプロキシを通じてアクセスできるユーザーは、接続元に関係なく、Adobe Campaignサーバーにアクセスできます。

   ![](assets/8101_proxy3.png)

Adobe Campaignサーバーにアクセスする可能性が高いプロキシのIPアドレスは、該当する&#x200B;**`<subnetwork>`**&#x200B;と第1レベルのサブネットワーク&#x200B;**`<subnetwork name="all"/>`**&#x200B;の両方に入力する必要があります。 例えば、IPアドレスが10.131.146.102のプロキシの場合は、次のようになります。

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

## セキュリティゾーンをオペレーター{#linking-a-security-zone-to-an-operator}にリンクする

ゾーンを定義したら、各オペレーターをいずれかのオペレーターにリンクして、インスタンスにログオンできるようにする必要があります。また、ゾーンで参照されるアドレスまたはアドレスの範囲に、オペレーターのIPアドレスを含める必要があります。

ゾーンの技術的な設定は、Campaignサーバーの設定ファイルで実行されます。**serverConf.xml**&#x200B;と入力します。

これをおこなう前に、あらかじめ用意されている&#x200B;**[!UICONTROL セキュリティゾーン]**&#x200B;列挙を設定し、**serverConf.xml**&#x200B;ファイルで定義されているゾーンの内部名にラベルをリンクする必要があります。

この設定は、Campaignエクスプローラーでおこないます。

1. **[!UICONTROL 管理/プラットフォーム/列挙]**&#x200B;ノードをクリックします。
1. **[!UICONTROL セキュリティゾーン(securityZone)]**&#x200B;システム列挙を選択します。

   ![](assets/enum_securityzone.png)

1. サーバーの設定ファイルで定義されたセキュリティゾーンごとに、「**[!UICONTROL 追加]**」ボタンをクリックします。
1. 「**[!UICONTROL 内部名]**」フィールドに、**serverConf.xml**&#x200B;ファイルで定義したゾーンの名前を入力します。 `<securityzone>`要素の&#x200B;**@name**&#x200B;属性に対応します。 **ラベル**&#x200B;フィールドに、内部名にリンクされたラベルを入力します。

   ![](assets/enum_addsecurityvalue.png)

1. 「 OK 」をクリックして、変更を保存します。

ゾーンを定義し、**[!UICONTROL セキュリティゾーン]**&#x200B;列挙を設定したら、各オペレーターをセキュリティゾーンにリンクする必要があります。

1. **[!UICONTROL 管理/アクセス管理/オペレーター]**&#x200B;ノードをクリックします。
1. セキュリティゾーンをリンクするオペレーターを選択し、「**[!UICONTROL 編集]**」タブをクリックします。
1. 「**[!UICONTROL アクセス権]**」タブに移動し、「**[!UICONTROL アクセスパラメーターを編集…」をクリックします。]**&#x200B;リンクをクリックします。

   ![](assets/zone_operator.png)

1. 「**[!UICONTROL 許可された接続ゾーン]**」ドロップダウンリストからゾーンを選択します。

   ![](assets/zone_operator_selection.png)

1. 「**[!UICONTROL OK]**」をクリックし、変更を保存して変更を適用します。



## 推奨事項

* subNetwork でリバースプロキシが許可されていないことを確認します。許可されている場合は、**すべての**&#x200B;トラフィックがこのローカル IP から来ているものとして検出され、信頼されます。

* sessionTokenOnly=&quot;true&quot; の使用は最小限に抑えます。

   * 警告：この属性がtrueに設定されている場合、オペレーターは&#x200B;**CRSF攻撃**&#x200B;にさらされる可能性があります。
   * さらに、sessionToken cookie に httpOnly フラグが設定されていないので、一部のクライアント側 JavaScript コードがこれを読み取れる可能性があります。
   * ただし、複数の実行セルで Message Center が sessionTokenOnly を必要とします。新しいセキュリティゾーンを作成し、sessionTokenOnly を true に設定して、**必要な IP のみ**&#x200B;をこのゾーンに追加します。

* 可能な場合は、allowHTTPとshowErrorsをすべてfalseに設定し（localhostではない）、確認します。

   * allowHTTP = &quot;false&quot;：オペレーターは HTTPS を使用することを強制されます。
   * showErrors = &quot;false&quot;：技術的エラー（SQL エラーなど）を非表示にします。これにより、表示される情報の量を抑えられますが、マーケターが（管理者に追加情報を要求することなしに）問題を解決することが難しくなります。

* 調査、webApp、レポートを作成（実際にはプレビュー）する必要があるマーケティングユーザーまたは管理者が使用する IP に対してのみ、allowDebug を true に設定します。このフラグを使用すると、これらの IP でリレールールが表示され、デバッグできるようになります。

* allowEmptyPassword、allowUserPassword、allowSQLInjection は決して true に設定しないでください。これらの属性は、v5 や v6.0 からの移行のためだけにあります。

   * **allowEmptyPassword** を使用すると、オペレーターは空のパスワードを設定できます。この属性を使用する場合、すべてのオペレーターに所定の期限までにパスワードを設定するよう通知してください。この期限を経過したら、この属性を false に設定します。

   * **allowUserPassword** を使用すると、オペレーターは資格情報をパラメーターとして送信できます（この情報は、Apache、IIS、プロキシでログに記録されます）。この機能は、以前に API の使用を簡素化するために使用されていました。クックブック（または仕様）で、サードパーティのアプリケーションがこれを使用していないかをチェックできます。使用されている場合、API の使用方法を変更して、なるべく早くこの機能を削除するよう通知する必要があります。

   * **allowSQLInjection** を使用すると、ユーザーは古い構文を使用した SQL インジェクションを実行できます。この属性をfalseに設定できるように、[このページ](../../migration/using/general-configurations.md)で説明されている修正をできるだけ早く実行します。 /nl/jsp/ping.jsp?zones=true を使用すると、セキュリティゾーン設定をチェックできます。このページには、現在の IP のセキュリティ対策のアクティブステータス（これらのセキュリティフラグで計算）が表示されます。

* HttpOnly cookie／useSecurityToken：**sessionTokenOnly** フラグを参照してください。

* 許可リストに追加する IP を最小限に抑える：セキュリティゾーンには、既にプライベートネットワーク用の 3 つの範囲が追加されています。通常、これらの IP アドレスをすべて使用することはありません。そのため、必要なもののみを保持するようにしてください。

* webApp／内部オペレーターを更新して、localhost でのみアクセス可能となるようにしてください。
