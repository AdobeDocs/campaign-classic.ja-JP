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
translation-type: ht
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

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

ワークフローテーブル内に含まれるデータは、名前で識別されます。名前は常に、「**targetData**」リンクから構成されます。詳しくは、[ターゲットデータ](../../workflow/using/executing-a-workflow.md#target-data)を参照してください。

さらに、メール配信のフレームワークでは、パーソナライゼーションフィールドで、ターゲティングワークフローステージで実行されるターゲット式のデータを使用できます。以下に例を示します。

![](assets/s_advuser_add_data_email.png)

セグメントコードがターゲティングアクティビティ内に指定されている場合、それらのコードはワークフローテーブルの特定の列に追加され、パーソナライゼーションフィールドと共に提供されます。すべてのパーソナライゼーションフィールドを表示するには、パーソナライゼーションボタン経由でアクセス可能な&#x200B;**[!UICONTROL ターゲット式／その他...]**&#x200B;リンクをクリックします。

![](assets/s_advuser_segment_code_select.png)

## データのエクスポート {#exporting-data}

### ファイルの圧縮または暗号化 {#zipping-or-encrypting-a-file}

Adobe Campaign では、圧縮されたファイルや暗号化されたファイルをエクスポートできます。「**[!UICONTROL データ抽出（ファイル）]**」アクティビティを通じてエクスポートを定義する際にファイルを圧縮または暗号化する後処理を定義できます。

手順は以下のとおりです。

* インストールした Adobe Campaign がアドビによってホストされている場合：必要なユーティリティをサーバーにインストールするよう[サポート](https://support.neolane.net)に依頼します。
* Adobe Campaign のインストールがオンプレミスの場合：使用するユーティリティ（例：GPG、GZIP）およびアプリケーションサーバー上の必要なキー（暗号化キー）をインストールします。

この場合、以下のようなコマンドやコードを使用できます。

```
function encryptFile(file) {  
  var systemCommand = “gpg --encrypt --recipient  recipientToEncryptTo ” + file;  
  var result = execCommand(systemCommand, true); 
}
```

ファイルのインポート時には、ファイルを解凍または復号化することもできます。[処理前のファイルの解凍または復号化](../../workflow/using/importing-data.md#unzipping-or-decrypting-a-file-before-processing)を参照してください。
