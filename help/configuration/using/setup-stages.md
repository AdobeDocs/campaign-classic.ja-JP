---
title: 設定ステージ
seo-title: 設定ステージ
description: 設定ステージ
seo-description: null
page-status-flag: never-activated
uuid: 4111a805-95ab-4e26-be51-2db1e5c20f57
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
discoiquuid: 76174374-af73-4da0-b62b-6979bca0102b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 設定ステージ{#setup-stages}

基本的な原則は、Webサイトの特定のページにWebトラッキングタグを挿入することです。

タグには2種類あります。

* **WEB**:このタグは、ページが訪問されたかどうかを知らせます。
* **TRANSACTION**:はWebタグのように機能しますが、生成された業務量（取引額、購入した品目数など）に関する情報が追加される可能性があります。

次の手順を適用して、これらのタグを設定します。

1. 追跡するページを識別し、そのタイプ（WEBまたはTRANSACTION）を決定します。
1. 収集する追加情報を決定し、 **** nms:webTrackingLogスキーマをこの情報の説明と共に拡張します。 デフォルトでは、このスキーマにはトランザクション金額とトランザクションあたりの品目数を格納できます。
1. Webトラッキングタグの作成 それには、次の 2 つの方法があります。

   * これらのページに対応するURLをAdobe Campaignプラットフォームに挿入し、関連するWebトラッキングタグを生成して抽出します(クライアントコンソールの **[!UICONTROL Campaign execution>Resources>Web tracking tags]** ノードから)。
   * Webトラッキングタグを「その場で作成」モードで自分で作成します。これらのページに対応するURLは、Adobe Campaignプラットフォームに自動的に挿入されます。

1. これらのタグは、静的または動的に、追跡するページに追加します。

   >[!NOTE]
   >
   >すべてのWEBタイプタグは、そのままサイトのページに追加できます。 TRANSACTIONタグは、追加情報（金額、項目など）を含めるために、動的に変更または追加する必要があります。

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

