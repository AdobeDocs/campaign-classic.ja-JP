---
product: campaign
title: 画像の表示の問題
description: 画像の表示の問題
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 62fa491e-3e83-422b-bcde-2bae2c1b676e
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# 画像の表示の問題{#image-display-issues}



送信されたメッセージで画像の表示に関する問題が発生した場合、原因が次のように不適切な場所に関係している可能性があります。

* 場所が一致しないか、画像が重複したトラッキングサーバーに正しくプッシュされていない可能性があります。設定を確認します。
* 画像は、マーケティングインスタンス上のパブリックリソースフォルダーに存在しない可能性があります。問題を解決するには、画像をリソースフォルダーにアップロードします。
* ミッドソーシングアーキテクチャで作業する場合：配達確認の送信時に、画像がエラーなしでアップロードされていることを確認します（情報は分析ログに表示されます）。

トラブルシューティング方法：

1. 画像を表示する配達確認を送信します。
1. インスタンス設定のリソース設定が正しいことを検証します。
1. パブリックリソースフォルダー、またはパブリックリソースフォルダーにない場合は配信で参照されるフォルダーを確認します。
