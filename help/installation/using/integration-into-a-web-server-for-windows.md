---
product: campaign
title: Windows 用 web サーバーへの統合
description: Windows 用 web サーバーへの統合
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 041c4431-baae-4e64-9e9a-0daa5123bd8a
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 4%

---

# Windows 用 web サーバーへの統合{#integration-into-a-web-server-for-windows}

Adobe Campaignには、HTTP（およびSOAP）を介してアプリケーションサーバーのエントリポイントとして機能するApache Tomcatが含まれています。

この統合Tomcatサーバーを使用して、HTTPリクエストを処理できます。

この場合、次のようになります。

* デフォルトのリスニングポートは8080です。 これを変更するには、[この節](../../installation/using/configure-tomcat.md)を参照してください。
* 次に、クライアントコンソールは、[https:// `<computer>`:8080](https://myserver.adobe.com:8080)のようなURLを使用して接続します。

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネット上で公開され、ネットワーク外のコンソールにアクセスする場合は、専用のWebサーバーをHTTPトラフィックのメインエントリポイントとして使用することをお勧めします。

また、Webサーバーを使用すると、HTTPプロトコルによるデータの機密性を保証できます。

同様に、Webサーバーは、Webサーバー拡張モジュールとしてのみ使用可能なトラッキング機能を使用する場合に使用する必要があります。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、ApacheまたはIISの標準インストールを実行し、Campaignにリダイレクトできます。 トラッキングWebサーバー拡張モジュールは不要です。

## IIS Webサーバー{#configuring-the-iis-web-server}の設定

IIS Webサーバーの設定手順は、ほとんどグラフィカルです。 Adobe Campaignサーバーのリソースにアクセスするには、Webサイト（作成済みまたは作成保留中）を使用する必要があります。Java(.jsp)ファイル、スタイルシート(.css、.xsl)、画像(.png)、リダイレクト用のISAPI DLLなど

以下の節では、IIS 7での設定について詳しく説明します。 IIS8の設定は基本的に同じです。

Web IISサーバーがまだコンピューターにインストールされていない場合は、**[!UICONTROL 追加/プログラムの削除/ Windows機能を有効または無効にする]**&#x200B;メニューを使用してインストールできます。

IIS 7では、標準のサービスに加えて、ISAPI拡張とISAPIフィルターをインストールする必要があります。

![](assets/s_ncs_install_iis7_isapi.png)

### 設定の手順 {#configuration-steps}

次の設定手順を実行します。

1. **[!UICONTROL コントロールパネル/管理ツール/サービス]**&#x200B;メニューからIISを開きます。
1. ネットワークのパラメーター（TCP接続ポート、DNSホスト、IPアドレス）に応じて、サイト(Adobe Campaignなど)を作成および設定します。

   ![](assets/s_ncs_install_iis7_add_site.png)

   少なくとも、サイトの名前と仮想ディレクトリへのアクセスパスを指定する必要があります。 Webサイトディレクトリにアクセスするためのパスは使用されないので、次のディレクトリを使用できます。

   ```
   C:\inetpub\wwwroot
   ```

   ![](assets/s_ncs_install_iis7_parameters_step1.png)

1. **VBS**&#x200B;スクリプトを使用すると、先ほど作成した仮想ディレクトリ上でAdobe Campaignサーバーが使用するリソースを自動的に構成できます。 起動するには、`[INSTALL]\conf`フォルダーにある&#x200B;**iis_neolane_setup.vbs**&#x200B;ファイルをダブルクリックします。`[INSTALL]`は、Adobe Campaignのインストールフォルダーにアクセスするパスです。

   ![](assets/s_ncs_install_iis7_parameters_step2.png)

   >[!NOTE]
   >
   >Windows Server 2008/IIS7をインストールした場合、VBSスクリプトを実行するか、スクリプトを管理者として実行するには、管理者としてログインする必要があります。

   Webサーバーをトラッキングリダイレクトサーバーとして使用する場合は「**[!UICONTROL OK]**」を、使用しない場合は「**[!UICONTROL キャンセル]**」をクリックします。

   複数のサイトが既にWebサーバー上で構成されている場合は、インストールを適用するWebサイトを指定する中間ページが表示されます。サイトにリンクする番号を入力し、「**[!UICONTROL OK]**」をクリックします。

   ![](assets/s_ncs_install_iis7_parameters_step3.png)

   確認メッセージが表示されます。

   ![](assets/s_ncs_install_iis7_parameters_step7.png)

1. 「**[!UICONTROL コンテンツビュー]**」タブで、WebサイトがAdobe Campaignのリソースで正しく設定されていることを確認します。

   ![](assets/s_ncs_install_iis7_parameters_step6.png)

   ツリーが表示されない場合は、IISを再起動します。

### 権限の管理 {#managing-rights}

次に、ISAPI DLLとAdobe Campaignインストールディレクトリ内のリソースのセキュリティ設定を構成する必要があります。

それには、次の手順に従います。

1. 「**[!UICONTROL 機能ビュー]**」タブを選択し、「**認証**」リンクをダブルクリックします。

   ![](assets/s_ncs_install_iis7_parameters_step8.png)

1. Webサイトの「**ディレクトリのセキュリティ**」タブで、匿名アクセスが有効になっていることを確認します。 必要に応じて、**[!UICONTROL 編集]**&#x200B;リンクをクリックして設定を変更します。

   ![](assets/s_ncs_install_iis7_parameters_step9.png)

### Webサーバーの起動と設定のテスト{#launching-the-web-server-and-testing-the-configuration}

次に、設定が正しいかどうかをテストする必要があります。

これをおこなうには、次の手順に従います。

1. **iisreset**&#x200B;コマンドラインを使用してIISサーバーを再起動します。
1. 次のURLをWebブラウザーに挿入して、トラッキングモジュールをテストします。

   ```
   https://<computer>/r/test
   ```

   ブラウザーには次の応答が表示されます。

   ```
   <redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='myserver.mydomain.com' localHost='localhost'/>
   ```

リダイレクトモジュールの有無をテストするには、次のコマンドラインを実行します。

```
nlserver pdump
```

次の情報を返す必要があります。

```
12:00:33 >   Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
webmdl@default (1644) - 18.2 Mo
```

また、ISAPI DLLが正しく読み込まれていることを確認することもできます。

それには、次の手順に従います。

1. **[!UICONTROL ドライバーマッピング]**&#x200B;アイコンをクリックして、Adobe CampaignサイトのISAPIフィルターを編集します。
1. ISAPIフィルターの内容を確認します。

   ![](assets/s_ncs_install_iis7_parameters_step11.png)

## その他の設定 {#additional-configurations}

### アップロードファイルのサイズ制限{#changing-the-upload-file-size-limit}の変更

IIS Webサーバーを設定する場合、サーバーにアップロードされる設定ファイルに対して、約28 MBの制限が自動的に適用されます。

これは、Adobe Campaignで特に、この制限を超えるファイルをアップロードする場合に、影響を及ぼす可能性があります。

例えば、ワークフローで「**データ読み込み（ファイル）**」タイプアクティビティを使用して50 MBのファイルをインポートすると、エラーによってワークフローの正常な実行が停止されます。

この場合、次の制限を引き上げる必要があります。

1. **[!UICONTROL スタート/（コントロールパネル）/管理ツール]**&#x200B;メニューからIISを開きます。
1. **Adobe**&#x200B;ウィンドウで、接続のインストール用に作成したサイトを選択し、メインウィンドウの「**リクエストのフィルタリング**」をダブルクリックします。
1. **アクション**&#x200B;ウィンドウで、「**機能設定を編集**」を選択して、「**許可されたコンテンツの最大サイズ（バイト）**」フィールドの値を編集できます。

   例えば、50 MBのファイルのアップロードを承認するには、「52428800」バイトを超える値を指定する必要があります。

>[!NOTE]
>
>このIISオプションの詳細については、[公式ドキュメント](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits)の「使い方」の節を参照してください。

### HTTPエラーメッセージ表示{#configuring-http-error-message-display}の設定

6.1バージョンのIISサーバーを使用している場合、メッセージに望ましくないHTMLコードが表示されるので、生成されたエラーメッセージを読み取るのが困難な場合があります。

この問題を修正し、エラーを正しく表示するには、次の設定を適用します。

1. **[!UICONTROL スタート/Campaign コントロールパネル/管理ツール]**&#x200B;メニューからIISを開きます。
1. **接続**&#x200B;ウィンドウで、Adobe Campaignのインストール用に作成したサイトを選択し、メインウィンドウで&#x200B;**設定エディター**&#x200B;をダブルクリックします。
1. 「**セクション**」ドロップダウンリストで、**system.webServer**/**httpErrors**&#x200B;を選択します。
1. **existingResponse**&#x200B;行で&#x200B;**PassThrough**&#x200B;値を選択します。

![](assets/ins_iis_httperrors.png)
