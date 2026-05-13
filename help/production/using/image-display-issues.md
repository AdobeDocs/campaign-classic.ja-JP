---
product: campaign
title: 画像の表示の問題
description: 画像の表示の問題
feature: Monitoring
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 62fa491e-3e83-422b-bcde-2bae2c1b676e
TQID: https://experienceleague.adobe.com/aBPQb0Yp8o7goe2CS4h6ydnZV5gjPYINHMxGcc-d140
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 134
ht-degree: 6%

---

# 画像の表示の問題{#image-display-issues}



送信されたメッセージで画像表示の問題が発生した場合、原因は不正な場所にリンクされている可能性があります。

* 場所が一致しない可能性があります。または、トラッキングサーバーを複製するために画像が正しくプッシュされていない可能性があります。設定を確認してください。
* 画像がマーケティングインスタンスのパブリックリソースフォルダーに存在しない場合があります。問題を解決するには、画像をリソースフォルダーにアップロードします。
* ミッドソーシングアーキテクチャで作業する場合：プルーフの送信時にエラーなしで画像がアップロードされていることを確認します（分析ログに情報が表示されます）。

トラブルシューティング方法：

1. 画像を表示するプルーフを送信します。
1. インスタンス設定のリソース設定が正しいことを検証します。
1. パブリックリソースフォルダーを確認するか、パブリックリソースフォルダーにない場合は、配信で参照されるフォルダーを確認します。
