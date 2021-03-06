---
product: campaign
title: ステージの設定
description: ステージの設定
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: a5ae0b61-3377-46d9-a327-6c897eeda770
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# ステージの設定{#setup-stages}

![](../../assets/v7-only.svg)

基本的な原則は、Web サイトの特定のページに Web トラッキングタグを挿入することです。

タグには次の 2 つのタイプがあります。

* **WEB**:このタグは、ページが訪問されたかどうかを示します。
* **トランザクション**:は Web タグのように機能しますが、例えば、生成されたビジネスボリュームに関する情報（トランザクション数、購入した品目の数など）を追加できるようになります。

次の手順に従って、これらのタグを設定します。

1. 追跡するページを特定し、そのタイプ（WEB または TRANSACTION）を決定します。
1. 収集する追加情報を決定し、 **nms:webTrackingLog** スキーマとこの情報の説明。 デフォルトでは、このスキーマにトランザクションの金額とトランザクションごとの品目数を保存できます。
1. Web トラッキングタグの作成。 それには、次の 2 つの方法があります。

   * これらのページに対応する URL をAdobe Campaignプラットフォームに挿入し、関連する Web トラッキングタグを ( **[!UICONTROL キャンペーンの実行/リソース/Web トラッキングタグ]** クライアントコンソールのノード )。
   * Web トラッキングタグを「オンザフライ作成」モードで自分で作成します。これらのページに対応する URL は、Adobe Campaignプラットフォームに自動的に挿入されます。

1. これらのタグを、静的に、または、追跡するページに動的に追加します。

   >[!NOTE]
   >
   >すべての WEB タイプタグは、そのままサイトのページに追加できます。 TRANSACTION タグは、追加情報（金額、項目など）を含めるために、動的に変更または追加する必要があります。

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
