---
title: ファイルの添付
seo-title: ファイルの添付
description: ファイルの添付
seo-description: null
page-status-flag: never-activated
uuid: a4dc1908-a6ef-4bc8-a310-605fc80c34ca
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-emails
discoiquuid: f3666c12-5e6f-452e-b1d6-b69a7e9f6f6e
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b60b5fad24c1237981f66315e7cf585c79f82641
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 88%

---


# ファイルの添付{#attaching-files}

## E メールの添付ファイルについて {#about-email-attachments}

E メール配信には 1 つまたは複数のファイルを添付できます。

>[!NOTE]
>
>パフォーマンスの問題を回避するために、1つの電子メールに複数の添付ファイルを含めないことをお勧めします。 推奨しきい値は、Campaign Classicオプション [のリストから設定でき](../../installation/using/configuring-campaign-options.md#delivery)ます。

次の 2 つの場合が考えられます。

* ファイルを選択し、そのまま配信に添付する。
* 添付ファイルのコンテンツを受信者ごとにパーソナライズする。この場合、**計算済み添付ファイル**&#x200B;を作成する必要があります。添付ファイルの名前は、各メッセージの送信時に、受信者に応じて自動生成されます。また、**Variable Digital Printing** オプションがインストールされている場合は、コンテンツをパーソナライズし、配信時に PDF 形式に変換して添付することもできます。

>[!NOTE]
>
>多くの場合、このタイプの設定は配信テンプレートを使用して実行されます。詳しくは、[テンプレートについて](../../delivery/using/about-templates.md)を参照してください。

## ローカルファイルの添付 {#attaching-a-local-file}

ローカルファイルを配信に添付するには、以下の手順に従います。

>[!NOTE]
>
>配信には複数個のファイルを添付できます。添付ファイルは、任意のフォーマット（zip 形式を含む）で指定できます。

1. 「**[!UICONTROL 添付ファイル]**」リンクをクリックします。
1. 「**[!UICONTROL 追加]**」ボタンをクリックします。
1. [ **[!UICONTROL ファイル…]** ]をクリックして、配信に添付するファイルを選択します。

   ![](assets/s_ncs_user_wizard_email_attachement.png)

また、配信の「**[!UICONTROL 添付ファイル]**」フィールドにファイルを直接ドラッグ＆ドロップしたり、配信ウィザードのツールバーから&#x200B;**[!UICONTROL 添付]**&#x200B;アイコンを使用したりできます。

![](assets/s_ncs_user_wizard_add_file_ico.png)

配信の際に利用できるよう、選択したファイルは、ただちにサーバー上へとアップロードされます。「**[!UICONTROL 添付ファイル]**」フィールドに一覧表示されます。

![](assets/s_ncs_user_wizard_email_attachement_e.png)

## 計算済み添付ファイルの作成 {#creating-a-calculated-attachment}

計算済み添付ファイルを作成する際には、各メッセージの分析または配信時にファイル名を生成させることができ、受信者に応じて異なるファイル名を付けることができます。また、内容をパーソナライズして PDF に変換することもできます。

![](assets/s_ncs_user_wizard_attachment.png)

パーソナライズされた添付ファイルを作成するには、次の手順に従います。

1. 「**[!UICONTROL 添付ファイル]**」リンクをクリックします。
1. 「**[!UICONTROL 追加]**」ボタンをクリックし、「**[!UICONTROL 計算済み添付ファイル]**」を選択します。
1. **[!UICONTROL タイプ]**&#x200B;ドロップダウンリストから、使用する計算のタイプを選択します。

![](assets/s_ncs_user_wizard_email01_136.png)

次のオプションを使用できます。

* **配信テンプレートの作成時にファイル名を生成**
* **メッセージの配信中にファイルのコンテンツはパーソナライズされて PDF に変換**
* **配信分析時にファイル名を生成（受信者プロファイルは利用不可）**
* **メッセージの配信中にファイル名を生成（受信者プロファイルを利用可）**

### ローカルファイルの添付 {#attach-a-local-file}

添付ファイルがローカルファイルの場合は、「**[!UICONTROL 配信テンプレートの作成時にファイル名を生成]**」オプションを選択します。ファイルはローカルで選択され、サーバーにアップロードされます。次の手順に従います。

1. アップロードするファイルを、「**[!UICONTROL ローカルファイル]**」フィールドで選択します。
1. 必要な場合はラベルを指定します。このラベルは、メッセージングシステム上でファイル名の代わりに表示されます。指定しない場合はデフォルトでファイル名が表示されます。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_02.png)

1. 必要に応じて、「**[!UICONTROL ファイルをサーバーにアップロード]**」を選択し、「**[!UICONTROL サーバーで更新]**」をクリックして転送を開始します。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_01.png)

このファイルは、サーバー上で、このテンプレートから作成された別の配信に添付できるようになります。

### パーソナライズ済みメッセージの添付 {#attach-a-personalized-message}

The option **[!UICONTROL The file content is personalized and converted into PDF format at the time of delivery for each message]** lets you select a file with personalization fields, such as the last name and first name of the intended recipient.

![](assets/s_ncs_user_wizard_email_calc_attachement_06.png)

このタイプの添付ファイルについては、次の設定手順に従います。

1. アップロードするファイルを選択します。

   >[!NOTE]
   >
   >ソースファイルは LibreOffice で作成する必要があります。インスタンスは、[この節](../../installation/using/before-starting.md)で説明されている前提条件に沿って設定されている必要があります。

1. 必要な場合はラベルを指定します。
1. 「**[!UICONTROL ファイルをサーバーにアップロード]**」を選択し、「**[!UICONTROL サーバーで更新]**」をクリックして転送を開始します。
1. プレビューを表示するには、受信者を選択します。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_07.png)

1. 配信を分析し、開始します。

   各受信者に、配信に添付されたパーソナライズ済み PDF が届きます。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_08.png)

>[!NOTE]
>
>パフォーマンスの問題を回避するために、パーソナライズされたURLからその場でダウンロードされた画像を添付ファイルとして含める場合、デフォルトで各画像サイズが100,000バイトを超えないようにする必要があります。 この推奨しきい値は、Campaign Classicオプション [のリストから設定でき](../../installation/using/configuring-campaign-options.md#delivery)ます。

### 計算済みファイルの添付 {#attach-a-calculated-file}

配信の準備中に添付ファイルの名前を計算できます。これをおこなうには、「**[!UICONTROL 配信分析時にファイル名を生成（受信者プロファイルは利用不可）]**」オプションを選択します。

>[!NOTE]
>
>このオプションは、配信が外部のプロセスまたはワークフローによって送信される場合にのみ使用されます。

1. 添付ファイルに適用するラベルを指定します。
1. 定義ウィンドウで、ファイルのパスと正確な名前を指定します。

   >[!IMPORTANT]
   >
   >ファイルはサーバー上に置かれている必要があります。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_04.png)

1. 配信を分析し、開始します。

   ファイル名の処理は分析ログに記録されます。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_05.png)

### パーソナライズ済みファイルの添付 {#attach-a-personalized-file}

添付ファイルを選択するときに、「**[!UICONTROL メッセージの配信中にファイル名を生成（受信者プロファイルを利用可）]**」オプションを選択できます。その後、送信するファイル名と受信者のパーソナライズデータをマップできます。

>[!NOTE]
>
>このオプションは、配信が外部のプロセスまたはワークフローによって送信される場合にのみ使用されます。

1. 添付ファイルに適用するラベルを指定します。
1. 定義ウィンドウで、ファイルのパスと正確な名前を指定します。ファイル名をパーソナライズする場合は、パーソナライゼーションフィールドを使用して適切な値を取得できます。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_010.png)

   >[!IMPORTANT]
   >
   >ファイルはサーバー上に置かれている必要があります。

1. 配信を分析し、開始します。

   下の例では、結合フィールドを使用して定義されたファイル名に基づいて添付ファイルを選択しています。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_011.png)

### 添付ファイルの設定 {#attachment-settings}

1 番目と 2 番目のオプションについては、「**[!UICONTROL ファイルをサーバーにアップロード]**」を選択し、適切なオプションを設定します。「**[!UICONTROL サーバーで更新...]**」リンクをクリックすると、アップロードが開始されます。

![](assets/s_ncs_user_wizard_email01_137.png)

ファイルがアップロードされていることを示す、次のようなメッセージが表示されます。

![](assets/s_ncs_user_wizard_email01_1371.png)

ファイルが変更されている場合は、次のような警告メッセージが表示されます。

![](assets/s_ncs_user_wizard_email01_1372.png)

「**[!UICONTROL 詳細設定]**」タブでは、添付ファイルについて次のような詳細設定オプションを指定できます。

* フィルターオプションを指定すると、添付ファイルの送り先とする受信者を限定できます。「**[!UICONTROL 添付ファイルを受信する受信者のフィルターを有効にする]**」オプションを選択すると、受信者選択用スクリプトを記述するための入力フィールドが有効になります。このスクリプトは JavaScript で記述する必要があります。
* ファイル名をパーソナライズするためのスクリプトを指定できます。

   ウィンドウにテキストを入力し、ドロップダウンリストから使用可能なパーソナライゼーションフィールドを選択します。次の例では、ファイル名がパーソナライズされ、今日の日付と受信者の名前が含まれています。

   ![](assets/s_ncs_user_wizard_email_calc_attachement_09.png)
