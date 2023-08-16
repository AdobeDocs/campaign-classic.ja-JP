---
product: campaign
title: 画像の表示の問題
description: 画像の表示の問題
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 62fa491e-3e83-422b-bcde-2bae2c1b676e
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 11%

---

# 画像の表示の問題{#image-display-issues}



送信されたメッセージで画像の表示に関する問題が発生した場合、原因が次のように不適切な場所に関係している可能性があります。

* 場所が一致しないか、画像が重複トラッキングサーバーに正しくプッシュされていない可能性があります。設定を確認してください。
* 画像は、マーケティングインスタンス上のパブリックリソースフォルダーに存在しない場合があります。問題を解決するには、画像をリソースフォルダーにアップロードします。
* ミッドソーシングアーキテクチャで作業している場合：配達確認の送信時に画像がエラーなしでアップロードされていることを確認します（情報は分析ログに表示されます）。

トラブルシューティング方法：

1. 画像を表示する配達確認を送信します。
1. インスタンス設定のリソース設定が正しいことを検証します。
1. パブリックリソースフォルダー、またはパブリックリソースフォルダーにない場合は配信で参照されるフォルダーを確認します。
