---
title: ダイレクトメールコンテンツの定義
seo-title: ダイレクトメールコンテンツの定義
description: ダイレクトメールコンテンツの定義
seo-description: null
page-status-flag: never-activated
uuid: eac69f58-5ecb-4884-8806-edb16e6dece8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: sending-direct-mail
discoiquuid: 443689f4-4c82-490f-ad96-22446f649a07
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# ダイレクトメールコンテンツの定義{#defining-the-direct-mail-content}

## 抽出ファイル {#extraction-file}

抽出したデータを格納するファイルの名前は、「**[!UICONTROL ファイル]**」フィールドで定義します。フィールドの右にあるボタンを使用すると、ファイルネームを生成するためのパーソナライゼーションフィールドを指定できます。

抽出ファイルは、デフォルトではサーバー上に作成され、格納されますが、コンピューター上に保存することもできます。そのためには、「**[!UICONTROL 配信の分析後に、生成されたファイルをダウンロードする]**」をオンにします。この場合、ローカルストレージディレクトリのアクセスパスおよびファイル名を指定する必要があります。

![](assets/s_ncs_user_mail_delivery_local_file.png)

ダイレクトメール配信の場合、抽出するデータのコンテンツは「**[!UICONTROL 抽出ファイルのフォーマットを編集]**」リンクを使用して定義します。

![](assets/s_ncs_user_mail_delivery_format_link.png)

このリンクをクリックすると、抽出ウィザードにアクセスして、出力ファイルに抽出する情報（列）を定義できます。

![](assets/s_ncs_user_mail_delivery_format_wz.png)

抽出ファイルには、パーソナライズした URL を挿入することができます。詳しくは、[Web 機能](../../web/using/publishing-a-web-form.md)を参照してください。

>[!NOTE]
>
>このウィザードには、[はじめに](../../platform/using/exporting-data.md#export-wizard)の節で説明されているエクスポートウィザードの手順が含まれています。
