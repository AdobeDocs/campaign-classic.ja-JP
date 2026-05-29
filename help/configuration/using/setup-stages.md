---
product: campaign
title: ステージの設定
description: ステージの設定
feature: Configuration
role: Developer
exl-id: a5ae0b61-3377-46d9-a327-6c897eeda770
TQID: https://experienceleague.adobe.com/1Euw5OREQLbcjZLR0g-QKzU3tOI9041En4Z7Uf-NTy8
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 244
ht-degree: 5%

---

# ステージの設定{#setup-stages}

基本原則は、web サイトの特定のページにweb トラッキングタグを挿入することです。

タグには2つの種類があります。

* **WEB**：このタグは、ページが訪問されたかどうかを示します。
* **TRANSACTION**: web タグのように動作しますが、生成される業務量（トランザクション金額、購入済みアイテム数など）に関する情報を追加する可能性があります。

これらのタグを設定するには、次の手順を適用します。

1. トラッキングするページを特定し、そのタイプ（WEBまたはトランザクション）を決定します。
1. 収集する追加情報を決定し、この情報の説明とともに&#x200B;**nms:webTrackingLog** スキーマを拡張します。 デフォルトでは、このスキーマはトランザクションごとのトランザクション金額と項目数を保存できます。
1. Web トラッキングタグの作成。 それには、次の 2 つの方法があります。

   * これらのページに対応するURLをAdobe Campaign プラットフォームに挿入し、関連するweb トラッキングタグを生成して抽出します（クライアントコンソールの&#x200B;**[!UICONTROL Campaign実行/リソース/web トラッキングタグ]** ノードから）。
   * Web トラッキングタグを「オンザフライ作成」モードで作成すると、これらのページに対応するURLがAdobe Campaign プラットフォームに自動的に挿入されます。

1. これらのタグは、追跡するページに静的または動的に追加します。

   >[!NOTE]
   >
   >すべてのWEB タイプのタグは、サイトのページにそのまま追加できます。 トランザクションタグは、追加情報（金額、項目など）を含めるには、動的に変更または追加する必要があります。

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
