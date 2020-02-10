---
title: 画像表示の問題
seo-title: 画像表示の問題
description: 画像表示の問題
seo-description: null
page-status-flag: never-activated
uuid: 8fc51459-ee46-4c05-8011-f0651e6b451b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: dfccfe8c-b826-4648-9a0b-23d7e6a4808a
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# 画像表示の問題{#image-display-issues}

送信されたメッセージで画像表示の問題が発生した場合、不適切な場所にリンクされている可能性があります。

* 場所が一致しないか、画像が重複したトラッキングサーバーに正しくプッシュされない可能性があります。設定を確認します。
* イメージは、マーケティングインスタンスのパブリックリソースフォルダーに存在しない場合があります。画像をリソースフォルダーにアップロードして、問題を解決します。
* ミッドソーシング・アーキテクチャで作業する場合：校正の送信時に、画像が誤りなくアップロードされているかどうかを確認します（分析ログに情報が表示されます）。

トラブルシューティング方法：

1. 画像を表示する校正を送信します。
1. インスタンス設定内のリソース設定が正しいことを検証します。
1. パブリックリソースフォルダを確認します。パブリックリソースフォルダにない場合は、配信で参照されているフォルダを確認します。

