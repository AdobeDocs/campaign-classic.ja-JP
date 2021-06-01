---
product: campaign
title: ステージの設定
description: ステージの設定
audience: configuration
content-type: reference
topic-tags: setting-up-web-tracking
exl-id: a5ae0b61-3377-46d9-a327-6c897eeda770
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 5%

---

# ステージの設定{#setup-stages}

基本的な原則は、Webサイトの特定のページにWebトラッキングタグを挿入することです。

タグには、次の2つのタイプがあります。

* **WEB**:このタグは、ページが訪問されたかどうかを示します。
* **トランザクション**:はWebタグのように機能しますが、例えば、生成されるビジネス量に関する情報（トランザクション量、購入品目数など）を追加できます。

次の手順に従って、これらのタグを設定します。

1. 追跡するページを特定し、そのタイプ（WEBまたはTRANSACTION）を特定します。
1. 収集する追加情報を決定し、**nms:webTrackingLog**&#x200B;スキーマをこの情報の説明と共に拡張します。 デフォルトでは、このスキーマにトランザクションの金額とトランザクションごとの品目数を保存できます。
1. Webトラッキングタグを作成します。 それには、次の 2 つの方法があります。

   * これらのページに対応するURLをAdobe Campaignプラットフォームに挿入し、関連するWebトラッキングタグを生成して抽出します（クライアントコンソールの&#x200B;**[!UICONTROL キャンペーンの実行/リソース/Webトラッキングタグ]**&#x200B;ノードから）。
   * 「オンザフライ作成」モードで、Webトラッキングタグを自分で作成します。これらのページに対応するURLは、Adobe Campaignプラットフォームに自動的に挿入されます。

1. これらのタグを、静的に、または追跡するページに動的に追加します。

   >[!NOTE]
   >
   >すべてのWEBタイプタグは、そのままサイトのページに追加できます。 TRANSACTIONタグは、追加情報（金額、品目など）を含めるために、動的に変更または追加する必要があります。

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
