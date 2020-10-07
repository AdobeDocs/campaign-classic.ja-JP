---
title: ステージの設定
seo-title: ステージの設定
description: ステージの設定
seo-description: null
page-status-flag: never-activated
uuid: 4111a805-95ab-4e26-be51-2db1e5c20f57
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 76174374-af73-4da0-b62b-6979bca0102b
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 6%

---


# ステージの設定{#setup-stages}

基本原則は、Webサイトの特定のページにWebトラッキングタグを挿入することです。

タグには2種類あります。

* **WEB**:このタグは、ページが訪問されたかどうかを示します。
* **TRANSACTION**:Webタグのように機能しますが、生成されたビジネス量（取引額、購入した商品数など）に関する情報が追加される可能性があります。

次の手順を適用して、これらのタグを設定します。

1. 追跡するページを識別し、そのタイプ（WEBまたはトランザクション）を判断します。
1. 収集する追加情報を決定し、 **nms:webTrackingLog** スキーマを拡張して、この情報の説明を入力します。 デフォルトでは、このスキーマには、トランザクション金額とトランザクションあたりの品目数が格納されます。
1. Webトラッキングタグーの作成 それには、次の 2 つの方法があります。

   * これらのページに対応するURLをAdobe Campaignプラットフォームに挿入し、関連するWebトラッキングタグーを生成して抽出します(クライアントコンソールの **[!UICONTROL キャンペーン実行/リソース/Web トラッキングタグ]** )。
   * Webトラッキングタグを自分で「オンザフライ作成」モードで作成します。これらのページに対応するURLは、Adobe Campaignプラットフォームに自動的に挿入されます。

1. これら追加のタグは、トラッキング対象のページで静的または動的に設定します。

   >[!NOTE]
   >
   >すべてのWEBタイプタグは、そのままサイトのページに追加できます。 TRANSACTIONタグは、追加情報（量、項目など）を含めるために、動的に変更または追加する必要があります。

**例**：

```
<script type="text/javascript">
var _f = "nmsWebTracking"
var _t = window.location.href.match(/.*://[^/]*(/[^?#&]*)/)[1] + "|w|" + _f
document.write("<img height='0' width='0' alt='' src='" +
window.location.protocol + "//tsupport/r/" +
Math.random().toString() + "?tagid=" + escape(_t) + "'/>")
</script>
```

