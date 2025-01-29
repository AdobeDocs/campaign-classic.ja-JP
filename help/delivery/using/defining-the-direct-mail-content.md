---
product: campaign
title: ダイレクトメールコンテンツの定義
description: ダイレクトメールのコンテンツを定義する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Direct Mail
role: User
exl-id: 585b2017-9408-4953-8505-2f6d9db8032f
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 100%

---

# ダイレクトメールコンテンツの定義{#defining-the-direct-mail-content}

## 抽出ファイル {#extraction-file}

抽出したデータを格納するファイルの名前は、「**[!UICONTROL ファイル]**」フィールドで定義します。フィールドの右にあるボタンを使用すると、ファイルネームを生成するためのパーソナライゼーションフィールドを指定できます。

抽出ファイルは、デフォルトではサーバー上に作成され、格納されますが、コンピューター上に保存することもできます。そのためには、「**[!UICONTROL 配信の分析後に、生成されたファイルをダウンロードする]**」をオンにします。この場合、ローカルストレージディレクトリのアクセスパスおよびファイル名を指定する必要があります。

![](assets/s_ncs_user_mail_delivery_local_file.png)

ダイレクトメール配信の場合、抽出するデータのコンテンツは「**[!UICONTROL 抽出ファイルのフォーマットを編集]**」リンクを使用して定義します。

![](assets/s_ncs_user_mail_delivery_format_link.png)

このリンクをクリックすると、抽出アシスタントにアクセスして、出力ファイルに抽出する情報（列）を定義できます。

![](assets/s_ncs_user_mail_delivery_format_wz.png)

抽出ファイルには、パーソナライズした URL を挿入することができます。詳しくは、[こちらの節](../../web/using/publishing-a-web-form.md)を参照してください。

>[!NOTE]
>
>このアシスタントには、[はじめに](../../platform/using/executing-export-jobs.md)の節で説明されているエクスポートアシスタントの手順が含まれています。
