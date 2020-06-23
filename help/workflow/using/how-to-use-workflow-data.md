---
title: ワークフローデータの使用方法
seo-title: ワークフローデータの使用方法
description: ワークフローデータの使用方法
seo-description: null
page-status-flag: never-activated
uuid: ed03f14b-1b53-426e-9213-22cb2f3deb19
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: -general-operation
discoiquuid: ec3844ca-8d80-4ddc-b08c-f18a6919bb28
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: bb35d2ae2d40aaef3bb381675d0c36ffb100b242
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 52%

---


# ワークフローデータの使用方法{#how-to-use-workflow-data}

## データベースの更新 {#updating-the-database}

収集したすべてのデータは、データベースを更新するために、または配信内で使用できます。例えば、メッセージのコンテンツのパーソナライゼーション機能をエンリッチメントすること（メッセージ内に契約件数を含める、過去 1 年間のショッピングカートの平均購入額を指定するなど）や、母集団のターゲティングを詳細におこなうこと（契約の共有者にメッセージを送る、オンラインサービスの高額契約者上位 1,000 人をターゲティングするなど）ができます。このデータは、リストにエクスポートまたはアーカイブできます。

### リストおよびダイレクト更新 {#lists-and-direct-updates}

Adobe Campaign データベースのデータおよび既存のリストは、2 つの専用アクティビティを使用して更新できます。

* 「**[!UICONTROL リスト更新]**」アクティビティを使用して、データリスト内に作業用テーブルを保存できます。

   既存のリストを選択するか、新規リストを作成することができます。ここでは、名前が自動生成されます（場合によってはレコードフォルダーも）。

   ![](assets/s_user_create_list.png)

   [リストの更新](../../workflow/using/list-update.md)を参照してください。

* **[!UICONTROL データを更新]**&#x200B;アクティビティでは、データベースのフィールドを一括で更新します。

   詳しくは、[データを更新](../../workflow/using/update-data.md)を参照してください。

### 購読／購読解除の管理 {#subscription-unsubscription-management}

ワークフロー経由で受信者の情報サービスの購読を登録および解除する方法については、[購読サービス](../../workflow/using/subscription-services.md)を参照してください。

## ワークフロー経由での送信 {#sending-via-a-workflow}

### 配信アクティビティ {#delivery-activity}

配信アクティビティについて詳しくは、[配信](../../workflow/using/delivery.md)を参照してください。

### 配信のエンリッチメントとターゲティング {#enriching-and-targeting-deliveries}

コンテンツまたはターゲット母集団の選択のフレームワークをカスタマイズするために、配信はワークフロー内のデータを処理できます。

例えば、直接メール配信のフレームワーク内では、ワークフロー内で実行されるデータ操作から取り出した追加データを、抽出ファイルに含めることができます。

![](assets/s_advuser_add_data_postal_mail.png)

通常のパーソナライゼーションフィールドに加えて、ワークフローステージからのパーソナライゼーションフィールドを、配信コンテンツに追加できます。以下の例に示すように、ワークフローアクティビティ内で定義された追加データは、直接メール配信のフレームワーク内で出力ファイルの名前を定義するために、配信ウィザード内に保持され、アクセスできるようになります。

![](assets/s_advuser_using_additional_data.png)

ワークフローテーブル内に含まれるデータは、名前で識別されます。名前は常に、「**targetData**」リンクから構成されます。詳しくは、[ターゲットデータ](../../workflow/using/data-life-cycle.md#target-data)を参照してください。

さらに、メール配信のフレームワークでは、パーソナライゼーションフィールドで、ターゲティングワークフローステージで実行されるターゲット式のデータを使用できます。以下に例を示します。

![](assets/s_advuser_add_data_email.png)

セグメントコードがターゲティングアクティビティ内に指定されている場合、それらのコードはワークフローテーブルの特定の列に追加され、パーソナライゼーションフィールドと共に提供されます。すべてのパーソナライゼーションフィールドを表示するには、パーソナライゼーションボタン経由でアクセス可能な&#x200B;**[!UICONTROL ターゲット式／その他...]**&#x200B;リンクをクリックします。

![](assets/s_advuser_segment_code_select.png)

## データのエクスポート {#exporting-data}

### ファイルの圧縮または暗号化 {#zipping-or-encrypting-a-file}

Adobe Campaign では、圧縮されたファイルや暗号化されたファイルをエクスポートできます。「**[!UICONTROL データ抽出（ファイル）]**」アクティビティを通じてエクスポートを定義する際にファイルを圧縮または暗号化する後処理を定義できます。

手順は以下のとおりです。

1. コント [ロールパネルを使用して、インスタンス用のGPGキーペアをインストールします](https://docs.adobe.com/content/help/en/control-panel/using/instances-settings/gpg-keys-management.html#encrypting-data)。

   >[!NOTE]
   >
   >コントロールパネルは、AWSでホストされるすべてのお客様が利用できます（自分のマーケティングインスタンスをオンプレミスでホストするお客様を除く）。

1. Adobe Campaignのインストールがアドビによってホストされている場合は、アドビカスタマーケアに連絡して、必要なユーティリティをサーバーにインストールしてもらいます。
1. Adobe Campaignのインストールがオンプレミスの場合は、使用するユーティリティをインストールします(例： GPG、GZIP)と、アプリケーションサーバー上の必要なキー（暗号化キー）。

その後、アクティビティの「 **[!UICONTROL スクリプト]** 」タブまたはJavaScriptコード **** アクティビティでコマンドまたはコードを使用できます。 次の使用例に例を示します。

**関連トピック：**

* [処理前のファイルの解凍または復号化](../../workflow/using/importing-data.md#unzipping-or-decrypting-a-file-before-processing)
* [データ抽出（ファイル）アクティビティ](../../workflow/using/extraction--file-.md).

### 使用例： コントロールパネルにインストールされたキーを使用して、データを暗号化およびエクスポートする {#use-case-gpg-encrypt}

この場合、コントロールパネルにインストールされたキーを使用してデータを暗号化およびエクスポートするためのワークフローを構築します。

この使用例を実行する手順は次のとおりです。

1. GPGユーティリティを使用してGPGキーペア（公開/秘密）を生成し、公開キーをコントロールパネルにインストールします。 詳細な手順は、 [コントロールパネルのドキュメントで確認できます](https://docs.adobe.com/content/help/en/control-panel/using/instances-settings/gpg-keys-management.html#encrypting-data)。

1. Campaign Classicで、データを書き出すワークフローを作成し、コントロールパネルからインストールされた秘密鍵を使用して書き出します。 これを行うには、次のようにワークフローを構築します。

   ![](assets/gpg-workflow-encrypt.png)

   * **[!UICONTROL クエリ]** アクティビティ: この例では、クエリを実行して、エクスポートするデータベースのデータをターゲットします。
   * **[!UICONTROL データ抽出（ファイル）]** アクティビティ: データをファイルに抽出します。
   * **[!UICONTROL JavaScriptコード]** アクティビティ: 抽出するデータを暗号化します。
   * **[!UICONTROL ファイル転送]** アクティビティ: データを外部ソース（この例ではSFTPサーバー）に送信します。

1. データベースから必要なデータをターゲットする **[!UICONTROL クエリ]** アクティビティを設定します。 詳しくは、[この節](../../workflow/using/query.md)を参照してください。

1. データ **[!UICONTROL 抽出（ファイル）]** アクティビティを開き、必要に応じて設定します。 この節では、アクティビティの設定方法に関するグローバルな概念について説明 [します](../../workflow/using/extraction--file-.md)。

   ![](assets/gpg-data-extraction.png)

1. JavaScriptコード **[!UICONTROL アクティビティを開き]** 、次のコマンドをコピー&amp;ペーストして、抽出するデータを暗号化します。

   >[!IMPORTANT]
   >
   >コマンドの **指紋** （指紋）の値は、コントロールパネルにインストールされた公開鍵の指紋に置き換えてください。

   ```
   var cmd='gpg ';
   cmd += ' --trust-model always';
   cmd += ' --batch -yes';
   cmd += ' --recipient fingerprint';
   cmd += ' --encrypt --output ' + vars.filename + '.gpg ' + vars.filename;
   execCommand(cmd,true);
   vars.filename=vars.filename + '.gpg'
   ```

   ![](assets/gpg-script.png)

1. 「 **[!UICONTROL ファイル転送]** 」アクティビティを開き、ファイルの送信先のSFTPサーバーを指定します。 この節では、アクティビティの設定方法に関するグローバルな概念について説明 [します](../../workflow/using/file-transfer.md)。

   ![](assets/gpg-file-transfer.png)

1. これで、ワークフローを実行できます。 実行後、クエリによるデータターゲットは、暗号化された.gpgファイルにSFTPサーバにエクスポートされます。

   ![](assets/gpg-sftp-encrypt.png)
