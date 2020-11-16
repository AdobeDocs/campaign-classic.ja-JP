---
title: Windows 用 Web サーバーへの統合
seo-title: Windows 用 Web サーバーへの統合
description: Windows 用 Web サーバーへの統合
seo-description: null
page-status-flag: never-activated
uuid: a5042221-44fe-46a6-9322-288b108396e2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: installing-campaign-in-windows-
discoiquuid: a4f2ae0e-e631-4ab6-934e-8298e4ce6f2c
translation-type: tm+mt
source-git-commit: 6d6f63fb6ac99c3a9e58a8670bc9bc59e6cfd420
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 5%

---


# Windows 用 Web サーバーへの統合{#integration-into-a-web-server-for-windows}

Adobe Campaignには、HTTP（およびSOAP）を介してアプリケーションサーバーのエントリポイントとして機能するApache Tomcatが含まれます。

この統合Tomcatサーバーを使用して、HTTP要求を処理できます。

この場合、次のようになります。

* デフォルトのリスニングポートは8080です。 変更する方法については、「Tomcatの [設定](../../installation/using/configuring-campaign-server.md#configuring-tomcat)」を参照してください。
* 次に、クライアントコンソールはhttps:// [:8080 `<computer>`などのURLを使用して接続します](https://myserver.adobe.com:8080)。

ただし、セキュリティと管理上の理由から、Adobe Campaignを実行しているコンピュータがインターネット上に公開され、ネットワーク外のコンソールにアクセスする場合は、HTTPトラフィックのメインエントリポイントとして専用のWebサーバを使用することをお勧めします。

また、Webサーバーでは、HTTPsプロトコルを使用してデータの機密性を保証できます。

同様に、トラッキング機能を使用する場合はWebサーバを使用する必要があります。この機能は、Webサーバ拡張モジュールとしてのみ使用できます。

>[!NOTE]
>
>トラッキング機能を使用しない場合は、ApacheまたはIISの標準インストールを実行し、キャンペーンへのリダイレクトを行うことができます。 追跡用Webサーバー拡張モジュールは不要です。

## IIS Webサーバーを構成する {#configuring-the-iis-web-server}

IIS Webサーバーの構成手順は、ほとんどグラフィカルです。 Webサイト（既に作成済みまたは保留中の作成）を使用してAdobe Campaignサーバーのリソースにアクセスする必要があります。Java (.jsp)ファイル、スタイルシート(.css、.xsl)、画像(.png)、リダイレクト用のISAPI DLLなど。

次の節では、IIS 7での設定について詳しく説明します。 IIS8の設定は基本的に同じです。

Web IISサーバーがまだコンピューターにインストールされていない場合は、 **[!UICONTROL 追加/プログラムを削除/Windows機能を有効または無効にする]** メニューを使用してインストールできます。

IIS 7では、標準のサービスに加えて、ISAPI拡張機能とISAPIフィルターをインストールする必要があります。

![](assets/s_ncs_install_iis7_isapi.png)

### 設定の手順 {#configuration-steps}

次の設定手順を実行します。

1. コントロールパネル/ **[!UICONTROL 管理ツール/サービス]** メニューから、IISを開きます。
1. ネットワークのパラメーター（TCP接続ポート、DNSホスト、IPアドレスなど）に応じて、サイト(Adobe Campaignなど)を作成し、構成します。

   ![](assets/s_ncs_install_iis7_add_site.png)

   サイトの名前と、仮想ディレクトリへのアクセスパスを少なくとも指定する必要があります。 Webサイトディレクトリにアクセスするパスは使用されないので、次のディレクトリを使用できます。

   ```
   C:\inetpub\wwwroot
   ```

   ![](assets/s_ncs_install_iis7_parameters_step1.png)

1. VBS **** スクリプトを使用すると、先ほど作成した仮想ディレクトリでAdobe Campaignサーバが使用するリソースを自動的に構成できます。 起動するには、重複がフォルダ内にある **iis_neolane_setup.vbs** ファイルをクリックします。 `[INSTALL]\conf` は、Adobe Campaignインストールフォルダにアクセスするためのパス `[INSTALL]` です。

   ![](assets/s_ncs_install_iis7_parameters_step2.png)

   >[!NOTE]
   >
   >Windows Server 2008/IIS7をインストールする場合、VBSスクリプトを実行するか、スクリプトを管理者として実行するには、管理者としてログインする必要があります。

   Webサーバーがトラッキングリダイレクトサーバーとして使用されている場合は **[!UICONTROL [OK]** ]をクリックし、それ以外の場合は[ **[!UICONTROL キャンセル]**]をクリックします。

   ウェブサーバ上で複数のサイトが既に構成されている場合は、中間ページが表示され、インストールを適用するウェブサイトを指定します。サイトにリンクされている番号を入力し、「 **[!UICONTROL OK]**」をクリックします。

   ![](assets/s_ncs_install_iis7_parameters_step3.png)

   確認メッセージが表示されます。

   ![](assets/s_ncs_install_iis7_parameters_step7.png)

1. 「 **[!UICONTROL コンテンツ表示]** 」タブで、WebサイトにAdobe Campaignリソースが正しく設定されていることを確認します。

   ![](assets/s_ncs_install_iis7_parameters_step6.png)

   ツリーが表示されない場合は、IISを再起動します。

### 権限の管理 {#managing-rights}

次に、ISAPI DLLおよびAdobe Campaignインストールディレクトリ内のリソースのセキュリティ設定を構成する必要があります。

それには、次の手順に従います。

1. 「 **[!UICONTROL 機能の表示]** 」タブを選択し、「 **認証** 」リンクを重複クリックします。

   ![](assets/s_ncs_install_iis7_parameters_step8.png)

1. Webサイトの「 **ディレクトリセキュリティ** 」タブで、匿名アクセスが有効になっていることを確認します。 必要に応じて、「 **[!UICONTROL 編集]** 」リンクをクリックして設定を変更します。

   ![](assets/s_ncs_install_iis7_parameters_step9.png)

### Webサーバーの起動と設定のテスト {#launching-the-web-server-and-testing-the-configuration}

次に、設定が正しいかどうかをテストする必要があります。

これを行うには、次の手順を適用します。

1. iisresetコマンドラインを使用してIISサーバーを **再起動します** 。
1. 次のURLをWebブラウザーに挿入して、トラッキングモジュールをテストします。

   ```
   https://<computer>/r/test
   ```

   ブラウザーに次の応答が表示されます。

   ```
   <redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='myserver.mydomain.com' localHost='localhost'/>
   ```

リダイレクトモジュールの存在をテストするには、次のコマンドラインを実行します。

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

1. [ **[!UICONTROL Driver mapping]** ]アイコンをクリックして、Adobe CampaignサイトのISAPIフィルターを編集します。
1. ISAPIフィルタの内容を確認します。

   ![](assets/s_ncs_install_iis7_parameters_step11.png)

## 任意の追加設定 {#additional-configurations}

### アップロードするファイルのサイズ制限の変更 {#changing-the-upload-file-size-limit}

IIS Webサーバーを構成する場合、サーバーにアップロードされる設定ファイルの上限は、自動的に約28 MBになります。

これは、特にこの制限を超えるファイルをアップロードする場合に、Adobe Campaignに影響を及ぼす可能性があります。

例えば、ワークフローで **データ読み込み（ファイル）** 型のアクティビティを使用して50 MBのファイルを読み込むと、エラーが発生してワークフローの正しい実行が停止します。

この場合、次の制限を増やす必要があります。

1. 開始/（コントロールパネル）/管理ツール **** /メニューから、IISを開きます。
1. 「 **Connections** 」ペインで、Adobeのインストール用に作成したサイトを選択し、メインペインの「 **Request Filtering** 」を重複クリックします。
1. 「 **アクション** 」ペインで、「 **機能設定を編集** 」を選択して、許可されたコンテンツの **最大サイズ（バイト）** フィールドの値を編集できます。

   例えば、50 MBのファイルのアップロードを承認するには、「52428800」バイトを超える値を指定する必要があります。

>[!NOTE]
>
>このIISオプションの詳細については、 [公式ドキュメントの「使い方」の節を参照してください](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits)。

### HTTPエラーメッセージ表示の設定 {#configuring-http-error-message-display}

6.1バージョンのIISサーバーを使用している場合は、メッセージに不適切なHTMLコードが表示されるので、生成されたエラーメッセージを読み取るのが困難な場合があります。

この問題を修正し、エラーを正しく表示するには、次の設定を適用します。

1. [ **[!UICONTROL 開始] > [Campaign コントロールパネル] > [管理ツール]** ]メニューでIISを開きます。
1. 「 **Connections** 」ペインで、Adobe Campaignのインストール用に作成したサイトを選択し、メインペインの「 **Configuration editor** 」を重複クリックします。
1. 「 **セクション** 」ドロップダウンリストで、 **system.webServer** / **httpErrorsを選択します**。
1. **既存のResponse** 行でPassThrough **** 値を選択します。

![](assets/ins_iis_httperrors.png)

