---
product: campaign
title: 一時ファイル
description: 一時ファイル
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: e77800f5-c0ae-446d-8ff3-bc8a18c97dbd
TQID: https://experienceleague.adobe.com/eZnGm-WK-etrLLbJ-aeuSqakYAfPNBQd2q3JlEd4rE8
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
feature_v2: []
subfeature_v2: id: c03a11ff-bdf9-4e5b-b279-f468b4293464id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 164
ht-degree: 21%

---

# 一時ファイル{#temporary-files}



システムが実稼動環境に入ると、次のようなエラーメッセージが（特に配信ログに）表示されることがあります。

*ファイル &#39;/tmp/tmp0000.tmp&#39;の名前を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません；（errno=18、無効なクロスデバイスリンク） （iRc=-52）*

原因は次のとおりです。

Adobe Campaignは&#x200B;**/tmp**&#x200B;の下に一時ファイルを生成し、名前を変更して&#x200B;**/usr/local/neolane/nl6/var**&#x200B;に移動します。 このエラーは、フォルダー（**/tmp**&#x200B;と&#x200B;**/usr/local/neolane/nl6/var**）の両方が異なるデバイスに対応している場合に発生します。実際には、これは&#x200B;**/var/nl6**&#x200B;へのシンボリックリンクです。 検証には、**df** コマンドが使用されます。

この問題を修正するには、一時ファイルを宛先と同じデバイスで生成する必要があります。

例えば、次のコマンドを実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```
