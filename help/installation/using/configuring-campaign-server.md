---
solution: Campaign Classic
product: campaign
title: Campaign サーバーの設定
description: Campaign サーバーの設定
audience: installation
content-type: reference
topic-tags: additional-configurations
translation-type: tm+mt
source-git-commit: 6d0ae3d597f9ee30515437d94901cb034d0ca3d5
workflow-type: tm+mt
source-wordcount: '3633'
ht-degree: 4%

---


# Campaign サーバーの設定{#configuring-campaign-server}

以下の節では、お客様のニーズと環境の担当者に合わせて実行できるサーバー側の設定について詳しく説明します。

>[!IMPORTANT]
>
>これらの設定は、管理者と&#x200B;**オンプレミス**&#x200B;ホスティングモデルに対してのみ実行する必要があります。
>
>**ホストされる**&#x200B;デプロイメントの場合、Adobe側の設定はサーバーでのみ構成できます。 ただし、Campaign コントロールパネル内で設定できる設定(IP許可リスト管理やURL権限など)もあります。

詳しくは、次の節を参照してください。

* [コントロールパネルのドキュメント](https://docs.adobe.com/content/help/ja-JP/control-panel/using/control-panel-home.html)
* [モデルのホスティング](../../installation/using/hosting-models.md)
* [Campaign Classicオンプレミスおよびホステッド機能マトリックス](../../installation/using/capability-matrix.md)
* [ハイブリッドモデルとホストモデルの設定手順](../../installation/using/hosting-models.md)

Campaign Classic構成ファイルは、Adobe Campaignのインストールフォルダーの&#x200B;**conf**&#x200B;フォルダーに保存されます。 設定は2つのファイルに分かれています。

* **serverConf.xml**:すべてのインスタンスの一般設定。このファイルは、Adobe Campaignサーバーの技術的なパラメーターを組み合わせたものです。これらはすべてのインスタンスで共有されます。 これらのパラメーターの一部については、以下で詳しく説明します。 この[セクション](../../installation/using/the-server-configuration-file.md)に示す、様々なノードとパラメーター。
* **config-`<instance>`.xml** ( **** instanceはインスタンスの名前):インスタンスの特定の設定。サーバを複数のインスタンス間で共有する場合は、各インスタンスに固有のパラメータを関連ファイルに入力してください。

## セキュリティゾーンの定義{#defining-security-zones}

### セキュリティゾーンについて{#about-security-zones}

各オペレーターは、インスタンスにログオンするためにゾーンにリンクされている必要があります。また、セキュリティゾーンに定義されているアドレスまたはアドレスセットに、オペレーターIPを含める必要があります。 セキュリティゾーンの設定は、Adobe Campaignサーバーの設定ファイルで行われます。

演算子は、コンソールのプロファイル（**[!UICONTROL 管理/アクセス管理/演算子]**&#x200B;ノード）からセキュリティゾーンにリンクされます。 [このセクション](#linking-a-security-zone-to-an-operator)で、ゾーンをキャンペーン演算子にリンクする方法を説明します。

### セキュリティゾーンの作成{#creating-security-zones}

ゾーンは次の方法で定義します。

* 1つ以上のIPアドレスの範囲（IPv4およびIPv6）
* IPアドレスの各範囲にリンクされた技術名

セキュリティゾーンは相互にロックされています。つまり、別のゾーンに新しいゾーンを定義すると、各オペレータに割り当てられる権限を増やしながら、そのゾーンにログオンできるオペレータの数が減ります。

ゾーンは、サーバーの構成時に、**serverConf.xml**&#x200B;ファイルで定義する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

各ゾーンは、次のような権限を定義します。

* HTTPSではなくHTTP接続
* エラー表示（Javaエラー、JavaScript、C++など）
* レポートとWebAppのプレビュー
* ログイン/パスワードによる認証
* 非セキュア接続モード

>[!NOTE]
>
>**各演算子はゾーンにリンクする必要があります**。演算子のIPアドレスがゾーンで定義された範囲に属する場合、演算子はインスタンスにログオンできます。\
>オペレータのIPアドレスは、複数のゾーンで定義できます。 この場合、演算子は各ゾーンに対する使用可能な権限の&#x200B;**set**&#x200B;を受け取ります。

標準搭載の&#x200B;**serverConf.xml**&#x200B;ファイルには、次の3つのゾーンが含まれています。**パブリック、VPN、およびLAN**。

>[!NOTE]
>
>**そのまま使用できる設定は安全です**。ただし、以前のバージョンのAdobe Campaignから移行する前に、新しいルールを移行して承認するために、セキュリティを一時的に低減する必要がある場合があります。

**serverConf.xml**&#x200B;ファイル内にゾーンを定義する方法の例：

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

* **allowDebug**:webAppを「debug」モードで実行できるようにします。
* **allowEmptyPassword**:パスワードを使用しないでインスタンスへの接続を許可します
* **allowHTTP**:HTTPSプロトコルを使用せずにセッションを作成できる
* **allowUserPassword**:セッショントークンは、次の形式を持つことができます。`<login>/<password>`&quot;
* **sessionTokenOnly**:接続URLにセキュリティトークンは不要です
* **showErrors**:サーバー側のエラーが転送され、表示されます

>[!IMPORTANT]
>
>ゾーン定義では、**true**&#x200B;値を持つ各属性によってセキュリティが低下します。

Message Centerを使用する場合、複数の実行インスタンスが存在する場合は、**sessionTokenOnly**&#x200B;属性が&#x200B;**true**&#x200B;に定義された追加のセキュリティゾーンを作成する必要があります。ここでは、必要なIPアドレスのみを追加します。 インスタンスの設定について詳しくは、[このドキュメント](../../message-center/using/creating-a-shared-connection.md)を参照してください。

### セキュリティゾーンのベストプラクティス{#best-practices-for-security-zones}

**lan**&#x200B;セキュリティゾーンの定義では、技術的なアクセスを定義するIPアドレスマスクを追加できます。 この追加により、サーバーでホストされているすべてのインスタンスにアクセスできます。

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

IPアドレスの範囲は、特定のインスタンスにのみアクセスする演算子のインスタンス専用の設定ファイルに直接定義することをお勧めします。

**`config-<instance>.xml`**&#x200B;ファイル内：

```
  <securityZone name="public">
   ...
    <securityZone name="vpn">
      <subNetwork id="cus1" mask="a.b.c.d/xx"/>
```

### セキュリティゾーン{#sub-networks-and-proxies-in-a-security-zone}のサブネットワークとプロキシ

**proxy**&#x200B;パラメーターは、**subNetwork**&#x200B;要素で使用して、セキュリティゾーンでのプロキシの使用を指定できます。

プロキシが参照され、接続がこのプロキシ経由で入る場合（HTTP X-Forwarded-Forヘッダー経由で表示される）、有効なゾーンはプロキシのクライアントのものであり、プロキシのものではありません。

>[!IMPORTANT]
>
>プロキシが設定されていて、そのプロキシを上書きできる場合（または存在しない場合）、テスト対象のIPアドレスは改ざんできます。
>
>さらに、リレーはプロキシと同じように生成されます。 したがって、IPアドレス127.0.0.1は、セキュリティゾーン構成のプロキシのリストに追加できます。
>
>次に例を示します。&quot; `<subnetwork label="Lan 1" mask="192.168.0.0/16" name="lan1" proxy="127.0.0.1,10.100.2.135" />`&quot;と入力します。

様々なケースが発生します。

* サブネットワークはセキュリティゾーンで直接参照され、プロキシは構成されません。サブネットワークのユーザは、Adobe Campaignサーバに直接接続できます。

   ![](assets/8101_proxy1.png)

* セキュリティゾーンのサブネットワークに対してプロキシが指定されています：このサブネットワークのユーザは、このプロキシを介してAdobe Campaignサーバにアクセスできます。

   ![](assets/8101_proxy2.png)

* プロキシは、セキュリティゾーンのサブネットワークに含まれます。接触チャネルに関係なく、このプロキシ経由でアクセスできるユーザーは、Adobe Campaignサーバーにアクセスできます。

   ![](assets/8101_proxy3.png)

Adobe Campaignサーバーにアクセスする可能性の高いプロキシのIPアドレスは、**`<subnetwork>`**&#x200B;と第1レベルのサブネットワーク&#x200B;**`<subnetwork name="all"/>`**&#x200B;の両方に入力する必要があります。 例えば、IPアドレスが10.131.146.102のプロキシの場合、次のようになります。

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

### セキュリティゾーンとオペレーターとのリンク {#linking-a-security-zone-to-an-operator}

ゾーンを定義したら、各演算子を1つのインスタンスにログオンできるように、いずれかの演算子にリンクする必要があります。また、演算子のIPアドレスを、ゾーンで参照されるアドレスまたはアドレスの範囲に含める必要があります。

ゾーンの技術的な構成は、キャンペーンサーバーの構成ファイルで行います。**serverConf.xml**.

これに先立って、**[!UICONTROL セキュリティゾーン]**&#x200B;定義済みリストを設定し、**serverConf.xml**&#x200B;ファイルで定義されたゾーンの内部名にラベルをリンクするように開始する必要があります。

この設定は、キャンペーンエクスプローラーで行います。

1. **[!UICONTROL 管理/プラットフォーム/定義済みリスト]**&#x200B;ノードをクリックします。
1. **[!UICONTROL セキュリティゾーン(securityZone)]**&#x200B;システム定義済みリストを選択します。

   ![](assets/enum_securityzone.png)

1. サーバーの構成ファイルで定義されているセキュリティゾーンごとに、**[!UICONTROL 追加]**&#x200B;ボタンをクリックします。
1. **[!UICONTROL Internal name]**&#x200B;フィールドに、**serverConf.xml**&#x200B;ファイルで定義されているゾーンの名前を入力します。 これは、`<securityzone>`要素の&#x200B;**@name**&#x200B;属性に対応します。 内部名にリンクされているラベルを&#x200B;**ラベル**&#x200B;フィールドに入力します。

   ![](assets/enum_addsecurityvalue.png)

1. 「OK」をクリックし、変更を保存します。

ゾーンを定義し、**[!UICONTROL セキュリティゾーン]**&#x200B;定義済みリストを設定したら、各演算子をセキュリティゾーンにリンクする必要があります。

1. **[!UICONTROL 管理/アクセス管理/演算子]**&#x200B;ノードをクリックします。
1. セキュリティゾーンのリンク先の演算子を選択し、「**[!UICONTROL 編集]**」タブをクリックします。
1. 「**[!UICONTROL アクセス権]**」タブに移動し、「**[!UICONTROL アクセスパラメーターの編集…」をクリックします。]**&#x200B;リンク。

   ![](assets/zone_operator.png)

1. 「**[!UICONTROL Authorized connection zone]**」ドロップダウンリストからゾーンを選択します

   ![](assets/zone_operator_selection.png)

1. 「**[!UICONTROL OK]**」をクリックし、変更を保存してこれらの変更を適用します。

## Tomcatの設定{#configuring-tomcat}

### Tomcat {#default-port-for-tomcat}のデフォルトポート

Tomcatサーバの8080リスニングポートが、設定に必要な別のアプリケーションで既にビジー状態になっている場合は、8080ポートを空きポート（8090など）に置き換える必要があります。 変更するには、Adobe Campaignのインストールフォルダーの&#x200B;**/tomcat-8/conf**&#x200B;ディレクトリに保存されている&#x200B;**server.xml**&#x200B;ファイルを編集します。

次に、JSPリレーページのポートを変更します。 これを行うには、Adobe Campaignインストールディレクトリの&#x200B;**/conf**&#x200B;ディレクトリに保存されている&#x200B;**serverConf.xml**&#x200B;ファイルを変更します。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

```
<serverConf>
   ...
   <web controlPort="8005" httpPort="8090"...
   <url ... targetUrl="http://localhost:8090"...
```

### Tomcat {#mapping-a-folder-in-tomcat}でのフォルダのマッピング

お客様固有の設定を定義するには、**/tomcat-8/conf**&#x200B;コンテキストーに&#x200B;**user_コンテキストー.xml**&#x200B;ファイルを作成します。このフォルダーには、**フォルダー.xml**&#x200B;ファイルも含まれます。

このファイルには、次の種類の情報が含まれます。

```
 <Context path='/foo' docBase='../customers/foo'   crossContext='true' debug='0' reloadable='true' trusted='false'/>
```

必要に応じて、この操作をサーバー側で再生できます。

## 配信パラメータのパーソナライズ{#personalizing-delivery-parameters}

配信パラメーターは、**serverConf.xml**&#x200B;設定ファイルで定義されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

一般的なサーバ設定とコマンドの詳細は、[キャンペーンサーバ設定](../../installation/using/campaign-server-configuration.md)を参照してください。

必要に応じて、次の設定を行うこともできます。

### SMTPリレー{#smtp-relay}

MTAモジュールは、SMTPブロードキャスト用のネイティブメール転送エージェント（ポート25）として機能する。

ただし、セキュリティポリシーで必要な場合は、リレーサーバーで置き換えることができます。 その場合、グローバルスループットは、中継サーバのスループットがAdobe Campaignのスループットより低い場合に限り、中継サーバのスループットとなります。

この場合、これらのパラメーターは&#x200B;**`<relay>`**&#x200B;セクションでSMTPサーバーを設定することで設定されます。 メールの転送に使用するSMTPサーバーのIPアドレス（またはホスト）と、それに関連付けられたポート（デフォルトで25）を指定する必要があります。

```
<relay address="192.0.0.3" port="25"/>
```

>[!IMPORTANT]
>
>この動作モードは、中継サーバ固有の性能（待ち時間、帯域など）が原因でスループットが大幅に低下する可能性があるので、配信に対する重大な制限を意味します。 また、（SMTPトラフィックの分析で検出される）同期配信エラーを認定する能力も限られ、中継サーバが使用できない場合は送信はできません。

### MTA子プロセス{#mta-child-processes}

サーバのCPU電力と使用可能なネットワークリソースに応じてブロードキャストパフォーマンスを最適化するために、子プロセス（デフォルトではmaxSpareServers）の母集団を制御できます。 この設定は、各コンピュータのMTA設定の&#x200B;**`<master>`**&#x200B;セクションで行います。

```
<master dataBasePoolPeriodSec="30" dataBaseRetryDelaySec="60" maxSpareServers="2" minSpareServers="0" startSpareServers="0">
```

[Eメール送信の最適化](../../installation/using/email-deliverability.md#email-sending-optimization)も参照してください。

### アフィニティ{#managing-outbound-smtp-traffic-with-affinities}を使用した送信SMTPトラフィックの管理

>[!IMPORTANT]
>
>アフィニティの設定は、サーバ間で一貫している必要があります。 構成の変更はMTAを実行するすべてのアプリケーションサーバーに複製される必要があるので、アフィニティ設定についてはAdobeにお問い合わせください。

IPアドレスを持つアフィニティを介した送信SMTPトラフィックを改善できます。

それには、次の手順に従います。

1. **serverConf.xml**&#x200B;ファイルの&#x200B;**`<ipaffinity>`**&#x200B;セクションにアフィニティを入力します。

   1つのアフィニティには、複数の異なる名前を付けることができます。区切るには、**;**&#x200B;文字を使用します。

   例：

   ```
    IPAffinity name="mid.Server;WWserver;local.Server">
             <IP address="XX.XXX.XX.XX" heloHost="myserver.us.campaign.net" publicId="123" excludeDomains="neo.*" weight="5"/
   ```

   関連するパラメーターを表示するには、**serverConf.xml**&#x200B;ファイルを参照してください。

1. ドロップダウンリストでアフィニティを選択できるようにするには、**IPAffinity**&#x200B;定義済みリストにアフィニティ名を追加する必要があります。

   ![](assets/ipaffinity_enum.png)

   >[!NOTE]
   >
   >定義済みリストは[このドキュメント](../../platform/using/managing-enumerations.md)で詳しく説明されています。

   次に示すように、タイポロジに使用するアフィニティを選択できます。

   ![](assets/ipaffinity_typology.png)

   >[!NOTE]
   >
   >[配信サーバの設定](../../installation/using/email-deliverability.md#delivery-server-configuration)も参照できます。

## URL へのアクセス権限 {#url-permissions}

Campaign Classic インスタンスの JavaScript コード（ワークフローなど）で呼び出すことができる URL のデフォルトリストは、制限されています。リストに記載されている URL を使用すれば、インスタンスは正常に機能します。

デフォルトでは、インスタンスは外部の URL にアクセスできないようになっています。ただし、許可されたURLのリストに外部URLを追加して、それらのURLにインスタンスを接続することは可能です。 これにより、Campaign インスタンスを SFTP サーバーや Web サイトなどの外部システムと接続して、ファイルやデータの転送が可能になります。

URL を追加すると、該当するインスタンスの設定ファイル（serverConf.xml）で参照されます。

URL権限を管理する方法は、ホスティングモデルに応じて異なります。

* **** Hybridor  **On-premise**:許可するURLを **serverConf.xmlファイルに追加し**&#x200B;ます。詳細は以下の節に記載されています。
* **ホスト**: **Campaign コントロールパネル経由で許可するURLを追加します**。詳しくは、[該当するドキュメント](https://docs.adobe.com/content/help/ja-JP/control-panel/using/instances-settings/url-permissions.html)を参照してください。

**ハイブリッド**&#x200B;と&#x200B;**オンプレミス**&#x200B;のホスティングモデルを使用する場合、管理者は、**serverConf.xml**&#x200B;ファイルで新しい&#x200B;**urlPermission**&#x200B;を参照する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

3 つの接続保護モードがあります。

* **ブロック**:許可リストに属していないURLはすべてブロックされ、エラーメッセージが表示されます。これは、ポストアップグレード後のデフォルトのモードです。
* **権限設定**:許可リストに属していないURLはすべて許可されます。
* **警告**:許可リストに属さないURLはすべて許可されますが、JSインタプリタは警告を出すので、管理者がそれらを収集できます。このモードでは JST-310027 警告メッセージが追加されます。

```
<urlPermission action="warn" debugTrace="true">
  <url dnsSuffix="abc.company1.com" urlRegEx=".*" />
  <url dnsSuffix="def.partnerA_company1.com" urlRegEx=".*" />
  <url dnsSuffix="xyz.partnerB_company1.com" urlRegEx=".*" />
</urlPermission>
```

>[!IMPORTANT]
>
>デフォルトでは、新規顧客のクライアントは&#x200B;**ブロッキングモード**&#x200B;を使用します。 新しいURLを許可する必要がある場合は、管理者に問い合わせて許可リストにURLを追加する必要があります。
>
>移行を行う既存のお客様は、しばらくの間&#x200B;**警告モード**&#x200B;を使用できます。 一方、URLを承認する前に、送信トラフィックを分析する必要があります。 認証済みURLのリストが定義されたら、管理者に連絡して、URLを許可リストに追加し、**ブロックモード**&#x200B;をアクティブにする必要があります。

## 動的なページセキュリティとリレー{#dynamic-page-security-and-relays}

デフォルトでは、すべての動的ページは、Webモジュールが起動したマシンの&#x200B;**ローカル** Tomcatサーバーに自動的に関連付けられます。 この設定は、**ServerConf.xml**&#x200B;ファイルのクエリリレー設定の&#x200B;**`<url>`**&#x200B;セクションに入力されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

**リモート**&#x200B;サーバー上で動的ページの実行を中継するを返します。 これを行うには、**localhost**&#x200B;を、JSPおよびJSSP、Web アプリケーション、レポート、文字列用のリモートコンピューターの名前に置き換える必要があります。

使用可能な様々なパラメーターの詳細については、**serverConf.xml**&#x200B;設定ファイルを参照してください。

JSPページの場合、デフォルト設定は次のとおりです。

```
<url relayHost="true" relayPath="true" targetUrl="http://localhost:8080" urlPath="*.jsp"/>
```

Adobe Campaignでは、次のJSPページを使用します。

* /nl/jsp/**soaprouter.jsp**:クライアントコンソールとWebサービス接続(SOAP API)、
* /nl/jsp/**m.jsp**:ミラーページ、
* /nl/jsp/**logon.jsp**:レポートへのWebベースのアクセスとクライアントコンソールのデプロイメント、
* /nl/jsp/**s.jsp** :クチコミマーケティング（スポンサーおよびソーシャルネットワーク）の使用を参照してください。

Mobile Appチャネルで使用されるJSSPは次のとおりです。

* nms/mobile/1/registerIOS.jssp
* nms/mobile/1/registerAndroid.jssp

**例：**

外部からのクライアントマシン接続を防ぐことができます。 これを行うには、**soaprouter.jsp**&#x200B;の実行を制限し、ミラーページ、クチコミリンク、Webフォームおよびパブリックリソースの実行のみを許可します。

パラメーターは次のとおりです。

```
<url IPMask="<IP_addresses>" deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="*.jsp"/>
<url IPMask="<IP_addresses>" deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="*.jssp"/> 
<url IPMask=""               deny=""     hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080" timeout="" urlPath="m.jsp"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080" timeout="" urlPath="s.jsp"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true" relayPath="true" targetUrl="http://localhost:8080" timeout="" urlPath="webForm.jsp"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/webApp/pub*"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/jssp/pub*"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/strings/pub*"/>
<url IPMask=""               deny=""     hostMask="" relayHost="true"  relayPath="true"  targetUrl="http://localhost:8080" timeout="" urlPath="/interaction/pub*"/>
<url IPMask=""               deny="true" hostMask="" relayHost="false" relayPath="false" targetUrl="http://localhost:8080" timeout="" urlPath="*.jsp"/>
<url IPMask=""               deny="true" hostMask="" relayHost="false" relayPath="false" targetUrl="http://localhost:8080" timeout="" urlPath="*.jssp"/>
```

この例では、**`<IP_addresses>`**&#x200B;値は、このマスクに中継モジュールを使用する権限を持つIPアドレス（comaで区切られたもの）のリストと一致します。

>[!NOTE]
>
>値は、設定とネットワークの制約に従って適合する必要があります。特に、お客様の設置に対して特定の設定が開発されている場合には、その設定が必要です。

## 許可された外部コマンドの制限{#restricting-authorized-external-commands}

>[!NOTE]
>
>次の設定は、オンプレミスでのインストールにのみ必要です。

ビルド8780から、技術管理者は、Adobe Campaignで使用できる認証済みの外部コマンドのリストを制限できます。

そのためには、次のように、使用を禁止するコマンドのリストを含むテキストファイルを作成する必要があります。

```
ln
dd
openssl
curl
wget
python
python3
perl
ruby
sh
```

>[!IMPORTANT]
>
>このリストは完全なものではありません。

サーバー設定ファイルの&#x200B;**exec**&#x200B;ノードで、**blacklistFile**&#x200B;属性で、以前に作成したファイルを参照する必要があります。

**Linuxの場合のみ**:サーバー構成ファイルで、セキュリティ構成を強化するために、外部コマンドの実行専用のユーザーを指定するように再コマンドします。このユーザーは、設定ファイルの&#x200B;**exec**&#x200B;ノードに設定されます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

>[!NOTE]
>
>ユーザーを指定しない場合、すべてのコマンドはAdobe Campaignインスタンスのユーザーコンテキストで実行されます。 ユーザーは、Adobe Campaignを実行しているユーザーとは異なる必要があります。

例：

```
<serverConf>
 <exec user="theUnixUser" blacklistFile="/pathtothefile/blacklist"/>
</serverConf>
```

このユーザーは、「neolane」Adobe Campaign演算子のsudoerリストに追加する必要があります。

>[!IMPORTANT]
>
>カスタムsudoは使用しないでください。 標準のsudoをシステムにインストールする必要があります。

## HTTPヘッダーの管理{#managing-http-headers}

デフォルトでは、すべてのHTTPヘッダーは再生されません。 リレーから送信される返信に、特定のヘッダーを追加できます。 手順は次のとおりです。

1. **serverConf.xml**&#x200B;ファイルに移動します。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。
1. **`<relay>`**&#x200B;ノードで、中継されたHTTPヘッダーのリストに移動します。
1. 追加次の属性を持つ&#x200B;**`<responseheader>`**&#x200B;要素：

   * **name**:header name
   * **value**:値の名前。

   例：

   ```
   <responseHeader name="Strict-Transport-Security" value="max-age=16070400; includeSubDomains"/>
   ```

## 重複した追跡{#redundant-tracking}

リダイレクトに複数のサーバーを使用する場合、リダイレクトするURLからの情報を共有するには、SOAP呼び出しを介して相互に通信できる必要があります。 配信の開始アップ時に、すべてのリダイレクトサーバーが利用できるとは限りません。したがって、同じレベルの情報を持つことはないかもしれません。

>[!NOTE]
>
>標準アーキテクチャまたはエンタープライズアーキテクチャを使用する場合、メインアプリケーションサーバーは、各コンピューター上で追跡情報をアップロードする権限を持っている必要があります。

冗長サーバーのURLは、**serverConf.xml**&#x200B;ファイルを介して、リダイレクトの構成で指定する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

**例：**

```
<spareserver enabledIf="$(hostname)!='front_srv1'" id="1" url="http://front_srv1:8080" />
<spareserver enabledIf="$(hostname)!='front_srv2'" id="2" url="http://front_srv2:8080" />
```

**enableIf**&#x200B;プロパティはオプションです（デフォルトでは空）。結果がtrueの場合にのみ接続を有効にできます。これにより、すべてのリダイレクトサーバーで同じ構成を取得できます。

コンピューターのホスト名を取得するには、次のコマンドを実行します。**hostname -s**.

## パブリックリソースの管理{#managing-public-resources}

パブリックリソースは、[パブリックリソースの管理](../../installation/using/deploying-an-instance.md#managing-public-resources)に記載されています。

これらは、Adobe Campaignインストールディレクトリの&#x200B;**/var/res/instance**&#x200B;ディレクトリに保存されます。

一致するURLは次のとおりです。**http://server/res/instance**&#x200B;ここで&#x200B;**instance**&#x200B;は、トラッキングインスタンスの名前です。

別のディレクトリを指定するには、**conf-`<instance>`.xml**&#x200B;ファイルにノードを追加して、サーバー上のストレージを設定します。 これは、次の行を追加することを意味します。

```
<serverconf>
  <shared>
    <dataStore hosts="media*" lang="fra">
      <virtualDir name="images" path="/var/www/images"/>
     <virtualDir name="publicFileRes" path="$(XTK_INSTALL_DIR)/var/res/$(INSTANCE_NAME)/"/>
    </dataStore>
  </shared>
</serverconf>
```

この場合、デプロイメントウィザードのウィンドウ上部に表示されるパブリックリソースの新しいURLは、このフォルダーを指す必要があります。

## 高可用性ワークフローとアフィニティ{#high-availability-workflows-and-affinities}

複数のワークフローサーバー(wfserver)を設定し、2台以上のマシンに配布できます。 この種のアーキテクチャを選択する場合は、Adobe Campaignアクセスに応じてロードバランサーの接続モードを設定します。

Webからのアクセスの場合は、**ロードバランサー**&#x200B;モードを選択して接続時間を制限します。

Adobe Campaignコンソールからアクセスする場合は、**ハッシュ**&#x200B;または&#x200B;**スティッキーip**&#x200B;モードを選択します。 これにより、リッチクライアントとサーバー間の接続を維持し、例えばインポート操作やエクスポート操作中にユーザーセッションが中断されるのを防ぐことができます。

特定のマシン上でワークフローまたはワークフローアクティビティを強制的に実行するよう選択できます。 これを行うには、関連するワークフローまたはアクティビティに対して1つ以上のアフィニティを定義する必要があります。

1. ワークフローまたはアクティビティのアフィニティを作成するには、**[!UICONTROL アフィニティ]**&#x200B;フィールドに入力します。

   アフィニティ名は自由に選択できます。 ただし、スペースや句読点は使用しないでください。 別のサーバーを使用する場合は、別の名前を指定します。

   ![](assets/s_ncs_install_server_wf_affinity01.png)

   ![](assets/s_ncs_install_server_wf_affinity02.png)

   ドロップダウンリストには、以前に使用したアフィニティが含まれています。 時間の経過と共に異なる入力値で完了します。

1. **nl6/conf/config-`<instance>.xml`**&#x200B;ファイルを開きます。
1. **[!UICONTROL wfserver]**&#x200B;モジュールに一致する行を次のように変更します。

   ```
   <wfserver autoStart="true" affinity="XXX,"/>
   ```

   複数のアフィニティを定義する場合は、コンマで区切ってスペースを入れないでください。

   ```
   <wfserver autoStart="true" affinity="XXX,YYY,"/>
   ```

   アフィニティが定義されていないワークフローを実行するには、アフィニティ名の後のカンマが必要です。

   アフィニティが定義されているワークフローのみを実行する場合は、アフィニティのリストの最後にカンマを追加しないでください。 例えば、次のように行を変更します。

   ```
   <wfserver autoStart="true" affinity="XXX"/>
   ```

## 自動プロセス再開{#automatic-process-restart}

デフォルトでは、異なるAdobe Campaignプロセスは、毎日午前6時（サーバー時間）に自動的に再起動します。

ただし、この設定は変更できます。

これを行うには、インストール先の&#x200B;**conf**&#x200B;リポジトリにある&#x200B;**serverConf.xml**&#x200B;ファイルに移動します。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

このファイルに設定された各プロセスには、**processRestartTime**&#x200B;属性があります。 この属性の値を変更して、各プロセスの再開時間をニーズに合わせて調整できます。

>[!IMPORTANT]
>
>この属性は削除しないでください。 すべてのプロセスは毎日再起動する必要があります。

## アップロード可能ファイルの制限{#limiting-uploadable-files}

新しい属性&#x200B;**uploadWhiteList**&#x200B;を使用すると、Adobe Campaignサーバーでアップロードできるファイルタイプを制限できます。

この属性は、**serverConf.xml**&#x200B;ファイルの&#x200B;**dataStore**&#x200B;要素内で使用できます。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

この属性のデフォルト値は&#x200B;**です。+**&#x200B;に置き換え、任意のファイルタイプをアップロードできます。

使用可能な形式を制限するには、有効なJava正規式で属性値を置き換える必要があります。 複数の値をコンマで区切って入力できます。

次に例を示します。**uploadWhiteList=&quot;.*.png,.*.jpg&quot;**&#x200B;を使用すると、PNG形式とJPG形式をサーバにアップロードできます。 その他の形式は使用できません。

>[!IMPORTANT]
>
>Internet Explorerでは、完全なファイルパスを正規式で検証する必要があります。

## プロキシ接続の構成{#proxy-connection-configuration}

例えば、**ファイル転送**&#x200B;ワークフローアクティビティを使用して、キャンペーンサーバーをプロキシ経由で外部システムに接続できます。 これを行うには、特定のコマンドを使用して&#x200B;**serverConf.xml**&#x200B;ファイルの&#x200B;**proxyConfig**&#x200B;セクションを設定する必要があります。 **serverConf.xml**&#x200B;で使用できるすべてのパラメーターは、この[セクション](../../installation/using/the-server-configuration-file.md)に一覧表示されます。

次のプロキシ接続が可能です。HTTP、HTTPS、FTP、SFTP。 20.2キャンペーンリリース以降、HTTPおよびHTTPSプロトコルのパラメーターは&#x200B;**使用できなくなりました**。 これらのパラメーターは、9032を含む以前のビルドで引き続き使用できるので、以下に説明します。

>[!CAUTION]
>
>基本認証モードのみがサポートされています。 NTLM認証はサポートされていません。
>
>SOCKSプロキシはサポートされていません。


次のコマンドを使用できます。

```
nlserver config -setproxy:[protocol]/[serverIP]:[port]/[login][:‘https’|'http’]
```

プロトコルのパラメータには、「http」、「https」、「ftp」のいずれかを使用できます。

HTTP/HTTPSトラフィックと同じポートにFTPを設定する場合は、次を使用できます。

```
nlserver config -setproxy:http/198.51.100.0:8080/user
```

「http」および「https」オプションは、プロトコルパラメータが「ftp」の場合にのみ使用され、指定したポートでのトンネリングがHTTPSまたはHTTPを使用して実行されるかどうかを示します。

プロキシサーバー経由のFTP/SFTPとHTTP/HTTPSトラフィックに異なるポートを使用する場合は、「ftp」プロトコルパラメーターを設定する必要があります。


例：

```
nlserver config -setproxy:ftp/198.51.100.0:8080/user:’http’
```

次に、パスワードを入力します。

HTTP接続は、proxyHTTPパラメーターで定義します。

```
<proxyConfig enabled=“1” override=“localhost*” useSingleProxy=“0”>
<proxyHTTP address=“198.51.100.0" login=“user” password=“*******” port=“8080”/>
</proxyConfig>
```

HTTPS接続は、proxyHTTPSパラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyHTTPS address=“198.51.100.0” login=“user” password=“******” port=“8080"/>
</proxyConfig>
```

FTP/FTPS接続は、proxyFTPパラメーターで定義されます。

```
<proxyConfig enabled=“1" override=“localhost*” useSingleProxy=“0">
<proxyFTP address=“198.51.100.0” login=“user” password=“******” port=“5555" https=”true”/>
</proxyConfig>
```

複数の接続タイプで同じプロキシを使用する場合、proxyHTTPのみがuseSingleProxyを&quot;1&quot;または&quot;true&quot;に設定して定義されます。

プロキシを経由する必要がある内部接続がある場合は、それらをoverrideパラメーターに追加します。

プロキシ接続を一時的に無効にする場合は、有効なパラメーターを「false」または「0」に設定します。
