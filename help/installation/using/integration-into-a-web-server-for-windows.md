---
product: campaign
title: Windows 用 web サーバーへの統合
description: Windows 用 web サーバーへの統合
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html" tooltip="Applies to on-premise and hybrid deployments only"
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
exl-id: 041c4431-baae-4e64-9e9a-0daa5123bd8a
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 4%

---

# Windows 用 web サーバーへの統合{#integration-into-a-web-server-for-windows}



Adobe Campaignには、HTTP（および SOAP）を介してアプリケーションサーバー内のエントリポイントとして機能する Apache Tomcat が含まれています。

この統合 Tomcat サーバーを使用して、HTTP リクエストを処理できます。

この場合、次のようになります。

* デフォルトのリスニングポートは 8080 です。 変更するには、 [この節](../../installation/using/configure-tomcat.md).
* クライアントコンソールは次のような URL を使用して接続します。 ```https:// `<computer>`:8080```.

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピューターがインターネットに公開され、ネットワーク外のコンソールにアクセスする場合は、専用の Web サーバーを HTTP トラフィックのメインエントリポイントとして使用することをお勧めします。

また、Web サーバーを使用すると、HTTPs プロトコルでデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合は Web サーバーを使用する必要があります。この機能は、Web サーバー拡張モジュールとしてのみ使用できます。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、Apache または IIS の標準インストールを実行し、Campaign にリダイレクトできます。 トラッキング Web サーバー拡張モジュールは不要です。

## IIS Web サーバーの設定 {#configuring-the-iis-web-server}

IIS Web サーバーの設定手順は、ほとんどグラフィカルです。 Web サイト（作成済みまたは作成保留中）を使用して、Adobe Campaignサーバーのリソースにアクセスする必要があります。Java(.jsp) ファイル、スタイルシート (.css、.xsl)、画像 (.png)、リダイレクト用の ISAPI DLL など。

次の節では、IIS 7 での設定について詳しく説明します。 IIS8 の設定は基本的に同じです。

Web IIS サーバーがまだコンピューターにインストールされていない場合は、 **[!UICONTROL [ 追加 ] > [ プログラムの削除 ] > [Windows の機能を有効または無効にする ]]** メニュー

IIS 7 では、標準のサービスに加えて、ISAPI 拡張機能と ISAPI フィルターをインストールする必要があります。

![](assets/s_ncs_install_iis7_isapi.png)

### 設定の手順 {#configuration-steps}

次の設定手順を実行します。

1. を使用して IIS を開きます。 **[!UICONTROL コントロールパネル/管理ツール/サービス]** メニュー
1. ネットワークのパラメーター（TCP 接続ポート、DNS ホスト、IP アドレス）に応じて、サイト (Adobe Campaignなど ) を作成および設定します。

   ![](assets/s_ncs_install_iis7_add_site.png)

   少なくともサイトの名前と仮想ディレクトリへのアクセスパスを指定する必要があります。 Web サイトディレクトリにアクセスするためのパスは使用されないので、次のディレクトリを使用できます。

   ```
   C:\inetpub\wwwroot
   ```

   ![](assets/s_ncs_install_iis7_parameters_step1.png)

1. A **VBS** スクリプトを使用すると、先ほど作成した仮想ディレクトリ上でAdobe Campaignサーバーが使用するリソースを自動的に設定できます。 起動するには、 **iis_neolane_setup.vbs** 次の場所にあるファイル： `[INSTALL]\conf` フォルダー、ここで `[INSTALL]` は、Adobe Campaignインストールフォルダーにアクセスするためのパスです。

   ![](assets/s_ncs_install_iis7_parameters_step2.png)

   >[!NOTE]
   >
   >Windows Server 2008/IIS7 のインストールの場合、VBS スクリプトを実行するか、管理者としてスクリプトを実行するには、管理者としてログインする必要があります。

   クリック **[!UICONTROL OK]** Web サーバーがトラッキングリダイレクションサーバーとして使用されている場合は、 **[!UICONTROL キャンセル]**.

   複数のサイトが既に Web サーバー上で設定されている場合は、インストールを適用する Web サイトを指定する中間ページが表示されます。サイトにリンクされた番号を入力し、 **[!UICONTROL OK]**.

   ![](assets/s_ncs_install_iis7_parameters_step3.png)

   確認メッセージが表示されます。

   ![](assets/s_ncs_install_iis7_parameters_step7.png)

1. 内 **[!UICONTROL コンテンツ表示]** 「 」タブで、Web サイトがAdobe Campaignのリソースで正しく設定されていることを確認します。

   ![](assets/s_ncs_install_iis7_parameters_step6.png)

   ツリーが表示されない場合は、IIS を再起動します。

### 権限の管理 {#managing-rights}

次に、ISAPI DLL と、Adobe Campaignインストールディレクトリ内のリソースのセキュリティ設定を構成する必要があります。

それには、次の手順に従います。

1. を選択します。 **[!UICONTROL 機能ビュー]** タブをクリックし、 **認証** リンク。

   ![](assets/s_ncs_install_iis7_parameters_step8.png)

1. 内 **ディレクトリセキュリティ** 「 」タブで、匿名アクセスが有効になっていることを確認します。 必要に応じて、 **[!UICONTROL 編集]** リンクをクリックして設定を変更します。

   ![](assets/s_ncs_install_iis7_parameters_step9.png)

### Web サーバーの起動と設定のテスト {#launching-the-web-server-and-testing-the-configuration}

次に、設定が正しいかどうかをテストする必要があります。

これをおこなうには、次の手順に従います。

1. を使用して IIS サーバーを再起動します。 **iisreset** コマンドラインを使用します。

1. Adobe Campaignサービスを起動し、実行中であることを確認します。

1. 次の URL を Web ブラウザーに挿入して、トラッキングモジュールをテストします。

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

また、ISAPI DLL が正しく読み込まれていることを確認することもできます。

それには、次の手順に従います。

1. Adobe Campaignサイトの ISAPI フィルターを編集するには、 **[!UICONTROL ドライバーマッピング]** アイコン
1. ISAPI フィルターの内容を確認します。

   ![](assets/s_ncs_install_iis7_parameters_step11.png)

## その他の設定 {#additional-configurations}

### アップロードファイルのサイズ制限の変更 {#changing-the-upload-file-size-limit}

IIS Web サーバーを設定する場合、サーバーにアップロードされる設定ファイルに対しては、自動的に約 28 MB の制限が適用されます。

Adobe Campaignでは特に、この制限を超えるファイルをアップロードする場合、この変更は影響を受ける可能性があります。

例えば、 **データ読み込み（ファイル）** 50 MB のファイルをインポートするワークフローに「 」アクティビティを入力すると、エラーが発生し、ワークフローの正常な実行が停止します。

この場合、この制限を引き上げる必要があります。

1. を使用して IIS を開きます。 **[!UICONTROL スタート/（コントロールパネル）/管理ツール]** メニュー
1. 内 **接続** ウィンドウで、インストール用に作成したサイトをAdobeし、 **リクエストのフィルター** をクリックします。
1. 内 **アクション** ペイン、選択 **フィーチャ設定を編集** 値を **許可された最大コンテンツサイズ（バイト）** フィールドに入力します。

   例えば、50 MB のファイルのアップロードを許可するには、「52428800」バイトを超える値を指定する必要があります。

>[!NOTE]
>
>この IIS オプションの詳細については、 [公式ドキュメント](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits).

### HTTP エラーメッセージ表示の設定 {#configuring-http-error-message-display}

6.1 バージョンの IIS サーバーを使用している場合、メッセージに望ましくないHTMLコードが表示されるので、生成されたエラーメッセージを読み取るのが困難な場合があります。

この問題を修正してエラーを正しく表示するには、次の設定を適用します。

1. を使用して IIS を開きます。 **[!UICONTROL スタート/Campaign コントロールパネル/管理ツール]** メニュー
1. 内 **接続** ウィンドウで、Adobe Campaignインストール用に作成されたサイトを選択し、ダブルクリックします。 **設定エディター** をクリックします。
1. 内 **セクション** ドロップダウンリストで、「 **system.webServer** > **httpErrors**.
1. を選択します。 **PassThrough** 値を **existingResponse** 行

![](assets/ins_iis_httperrors.png)
