---
product: campaign
title: ダイレクトメールコンテンツの定義
description: ダイレクトメールのコンテンツを定義する方法を学ぶ
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Direct Mail
role: User
hide: true
exl-id: 585b2017-9408-4953-8505-2f6d9db8032f
TQID: https://experienceleague.adobe.com/LybEpDwVDNAGQg5CA2nZ3IkNoyHFiYvNuKm-VXYW4s4
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 192
ht-degree: 100%

---

# ダイレクトメールコンテンツの定義{#defining-the-direct-mail-content}

## 抽出ファイル {#extraction-file}

抽出したデータを格納するファイルの名前は、「**[!UICONTROL ファイル]**」フィールドで定義します。 フィールドの右にあるボタンを使用すると、ファイルネームを生成するためのパーソナライゼーションフィールドを指定できます。

抽出ファイルは、デフォルトではサーバー上に作成され、格納されますが、 コンピューター上に保存することもできます。 そのためには、「**[!UICONTROL 配信の分析後に、生成されたファイルをダウンロードする]**」をオンにします。 この場合、ローカルストレージディレクトリのアクセスパスおよびファイル名を指定する必要があります。

![](assets/s_ncs_user_mail_delivery_local_file.png)

ダイレクトメール配信の場合、抽出するデータのコンテンツは「**[!UICONTROL 抽出ファイルのフォーマットを編集]**」リンクを使用して定義します。

![](assets/s_ncs_user_mail_delivery_format_link.png)

このリンクをクリックすると、抽出アシスタントにアクセスして、出力ファイルにエクスポートする情報（列）を定義できます。

![](assets/s_ncs_user_mail_delivery_format_wz.png)

抽出ファイルには、パーソナライズした URL を挿入することができます。 詳しくは、[この節](../../web/using/publishing-a-web-form.md)を参照してください。

>[!NOTE]
>
>このアシスタントには、[はじめに](../../platform/using/executing-export-jobs.md)の節で説明されているエクスポートアシスタントの手順が含まれています。
