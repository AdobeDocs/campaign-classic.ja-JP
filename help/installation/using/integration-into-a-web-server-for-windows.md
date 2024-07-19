---
product: campaign
title: Windows 用 Web サーバーへの統合
description: Windows 用 Web サーバーへの統合
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 041c4431-baae-4e64-9e9a-0daa5123bd8a
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 3%

---

# Windows 用 Web サーバーへの統合 {#integration-into-a-web-server-for-windows}

Adobe Campaignには、HTTP （およびSOAP）を介してアプリケーションサーバーへのエントリポイントとして機能する Apache Tomcat が含まれています。

この統合 Tomcat サーバーを使用して、HTTP リクエストを提供できます。

この場合の解決策は、次のとおりです。

* デフォルトのリスニングポートは 8080 です。 変更するには、[ この節 ](../../installation/using/configure-tomcat.md) を参照してください。
* その後、クライアントコンソールは ```https:// `<computer>`:8080``` などの URL を使用して接続します。

ただし、セキュリティおよび管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネットに公開され、ネットワークの外部にあるコンソールにアクセスする場合は、HTTP トラフィックの主なエントリポイントとして専用の web サーバーを使用することをお勧めします。

また、web サーバーを使用すると、HTTP プロトコルでデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合は、web サーバーを使用する必要があります。この機能は、web サーバー拡張機能モジュールとしてのみ使用できます。

## IIS Web サーバーの設定 {#configuring-the-iis-web-server}

Microsoft IIS Web サーバーの設定手順は、ほとんどがグラフィカルです。 Web サイトを使用して、Adobe Campaign サーバーのリソース（Java （.jsp） ファイル、スタイルシート（.css、.xsl）、画像（.png）、リダイレクト用の ISAPI DLL など）にアクセスする必要があります。


### 設定の手順 {#configuration-steps}

Adobe CampaignをMicrosoft IIS web サーバーと統合するには、次の手順に従います。

1. Microsoft IIS を開きます。
1. ネットワークのパラメーター（TCP 接続ポート、DNS ホスト、IP アドレス）に応じて、サイト（Adobe Campaignなど）を作成し、設定します。

   少なくとも、サイトの名前と仮想ディレクトリへのアクセスパスを指定する必要があります。 Web サイトディレクトリにアクセスするためのパスは使用されないので、次のディレクトリを使用できます。

   ```
   C:\inetpub\wwwroot
   ```

   ![](assets/s_ncs_install_iis7_parameters_step1.png)

1. **VBS** スクリプトを使用すると、Adobe Campaign サーバーが使用するリソースを、作成した仮想ディレクトリに自動的に設定できます。 起動するには、`[INSTALL]\conf` フォルダーにある **iis_neolane_setup.vbs** ファイルをダブルクリックします。ここで、`[INSTALL]` はAdobe Campaign インストールフォルダーにアクセスするためのパスです。

   >[!NOTE]
   >
   >VBS スクリプトを実行するには、管理者としてログインするか、スクリプトを管理者として実行する必要があります。

   Web サーバーをトラッキング リダイレクト サーバーとして使用する場合は [**[!UICONTROL OK]**] をクリックし、使用しない場合は [**[!UICONTROL キャンセル]**] をクリックします。

   Web サーバー上に複数のサイトが既に構成されている場合は、インストールの適用先となる Web サイトを示す中間ページが表示されます。サイトにリンクされている番号を入力し、[**[!UICONTROL OK]**] をクリックします。

1. 「**[!UICONTROL コンテンツビュー]**」タブで、web サイトがAdobe Campaign リソースで正しく設定されていることを確認します。

   ツリーが表示されない場合は、Microsoft IIS を再起動します。

### 権限の管理 {#managing-rights}

次に、ISAPI DLL とAdobe Campaign インストールディレクトリ内のリソースのセキュリティ設定を行う必要があります。

それには、次の手順に従います。

1. **[!UICONTROL 機能ビュー]** タブを選択し、**認証** リンクをダブルクリックします。

   ![](assets/s_ncs_install_iis7_parameters_step8.png)

1. Web サイトの [**Directory Security**] タブで、匿名アクセスが有効になっていることを確認します。 必要に応じて、「**[!UICONTROL 編集]** リンクをクリックして設定を変更します。

   ![](assets/s_ncs_install_iis7_parameters_step9.png)

### Web サーバーの起動と設定のテスト {#launching-the-web-server-and-testing-the-configuration}

設定が正しいかどうかをテストする必要があります。

それには、次の手順を適用します。

1. **iisreset** コマンドラインを使用して、Microsoft IIS サーバーを再起動します。

1. Adobe Campaign サービスを起動し、実行中であることを確認します。

1. Web ブラウザーに次の URL を挿入して、トラッキングモジュールをテストします。

   ```
   https://<computer>/r/test
   ```

   ブラウザーには、次の応答が表示されます。

   ```
   <redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='myserver.mydomain.com' localHost='localhost'/>
   ```

リダイレクトモジュールが存在するかどうかをテストするには、次のコマンドラインを実行します。

```
nlserver pdump
```

次の情報を返す必要があります。

```sql
HH:MM:SS >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
webmdl@default (1644) - 18.2 Mo
```

また、ISAPI DLL が正しく読み込まれていることを確認することもできます。

それには、次の手順に従います。

1. **[!UICONTROL ドライバーマッピング]** アイコンをクリックして、Adobe Campaign サイトの ISAPI フィルターを編集します。
1. ISAPI フィルターの内容を確認します。


## アップロードファイルのサイズ制限の変更 {#changing-the-upload-file-size-limit}

IIS Web サーバーを設定する場合、サーバーにアップロードされる設定ファイルには、自動的に約 28 MB の制限が適用されます。

これは、Adobe Campaignに影響を与える可能性があります。特に、この制限を超えるファイルをアップロードする場合に影響が大きくなります。

例えば、ワークフローで **データ読み込み（ファイル）** タイプのアクティビティを使用して 50 MB のファイルを読み込むと、エラーにより、ワークフローが正しく実行されなくなります。

この場合、この制限を増やす必要があります。

このMicrosoft IIS オプションについて詳しくは、[Microsoft ドキュメント ](https://learn.microsoft.com/en-us/iis/configuration/system.webServer/security/requestFiltering/requestLimits/){target="_blank"} の操作方法の節を参照してください。

