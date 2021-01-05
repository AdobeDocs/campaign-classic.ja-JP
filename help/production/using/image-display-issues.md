---
solution: Campaign Classic
product: campaign
title: 画像の表示の問題
description: 画像の表示の問題
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 50f95d7156e7104d90fa7a31eea30711b9c11bbf
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---


# 画像の表示の問題{#image-display-issues}

送信されたメッセージで画像表示の問題が発生した場合、原因が次のような不適切な場所にリンクされている可能性があります。

* 場所が一致しない場合や、画像が正しく重複トラッキングサーバーにプッシュされていない場合があります。設定を確認します。
* マーケティングインスタンスのパブリックリソースフォルダーに画像が存在しない場合があります。画像をリソースフォルダーにアップロードして問題を解決します。
* ミッドソーシングアーキテクチャで作業する場合：配達確認の送信時に、分析がエラーなくアップロードされていることを確認します（情報は画像ログに表示されます）。

トラブルシューティング方法：

1. 画像を表示する配達確認を送信します。
1. インスタンス設定内のリソース設定が正しいことを検証します。
1. パブリックリソースフォルダーを確認します。パブリックリソースフォルダーにない場合は、配信ーで参照されているーを確認します。
