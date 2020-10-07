---
title: 画像の表示の問題
seo-title: 画像の表示の問題
description: 画像の表示の問題
seo-description: null
page-status-flag: never-activated
uuid: 8fc51459-ee46-4c05-8011-f0651e6b451b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: dfccfe8c-b826-4648-9a0b-23d7e6a4808a
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 8%

---


# 画像の表示の問題{#image-display-issues}

送信されたメッセージで画像表示の問題が発生した場合、原因が次のような不適切な場所にリンクされている可能性があります。

* 場所が一致しない場合や、画像が重複トラッキングサーバーに正しくプッシュされていない場合があります。設定を確認します。
* イメージは、マーケティングインスタンスのパブリックリソースフォルダーに存在しない場合があります。画像をリソースフォルダーにアップロードして問題を解決します。
* ミッドソーシングアーキテクチャで作業する場合：配達確認の送信時に、分析がエラーなくアップロードされていることを確認します（情報は画像ログに表示されます）。

トラブルシューティング方法：

1. 画像を表示する配達確認を送信します。
1. インスタンス設定内のリソース設定が正しいことを検証します。
1. パブリックリソースフォルダーを確認します。パブリックリソースフォルダーにない場合は配信ーで参照されているー。

