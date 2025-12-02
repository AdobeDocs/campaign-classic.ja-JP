---
product: campaign
title: ステージの設定
description: ステージの設定
feature: Configuration
role: Developer
exl-id: a5ae0b61-3377-46d9-a327-6c897eeda770
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 5%

---

# ステージの設定{#setup-stages}

基本的な原則は、web サイトの特定のページに web トラッキングタグを挿入することです。

タグには次の 2 種類があります。

* **WEB**：このタグは、ページが訪問されたかどうかを示します。
* **トランザクション**:web タグのように動作しますが、生成される取引量に関する情報（取引額、購入した品目の数など）を追加する可能性があります。

これらのタグをセットアップするには、次の手順を適用します。

1. 追跡するページを特定し、そのタイプ（WEB またはトランザクション）を決定します。
1. 収集する追加情報を決定し、この情報の説明を使用して **nms:webTrackingLog** スキーマを拡張します。 デフォルトでは、このスキーマにはトランザクション金額とトランザクションあたりの項目数を格納できます。
1. Web トラッキングタグを作成します。 それには、次の 2 つの方法があります。

   * Adobe Campaign プラットフォームでこれらのページに対応する URL を挿入し、関連する web トラッキングタグを生成して抽出します（クライアントコンソールの **[!UICONTROL キャンペーンの実行/リソース/web トラッキングタグ]** ノードから）。
   * 自分で「その場で作成」モードで web トラッキングタグを作成します。これらのページに対応する URL がAdobe Campaign プラットフォームに自動的に挿入されます。

1. 追跡するページに、これらのタグを静的または動的に追加します。

   >[!NOTE]
   >
   >すべての WEB タイプタグは、サイトのページにそのまま追加できます。 トランザクション タグは、追加情報（金額、項目など）を含めるために、動的に変更または追加する必要があります。

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
