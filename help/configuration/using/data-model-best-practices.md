---
title: Adobe Campaign Classic Recipientテーブルの使用
description: Adobe Campaign Classicでデータモデルをデザインする際に、あらかじめ用意されている受信者テーブルを使用する方法を説明します。
page-status-flag: never-activated
uuid: faddde15-59a1-4d2c-8303-5b3e470a0c51
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: schema-reference
discoiquuid: 5957b39e-c2c6-40a2-b81a-656e9ff7989c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 620724e283215df1fb3f10bd0211652b36284b57

---


# データモデルのベストプラクティス{#data-model-best-practices}

大きなテーブルと複雑な結合を使用してデータモデルを設計する際に従うべきベストプラクティスを以下に示します。

* 追加のカスタム受信者テーブルを使用する場合は、各配信マッピングに対して専用のログテーブルがあることを確認します。
* 特に未使用の列を識別することで、列の数を減らします。
* 複数の条件や複数の列に対する結合など、複雑な結合を避け、データモデルの関係を最適化します。
* 結合キーには、文字列ではなく常に数値データを使用します。
* ログ保存の深さをできるだけ減らします。 より深い履歴が必要な場合は、計算を集計したり、カスタムログテーブルを処理してより大きな履歴を保存したりできます。

データベースデザインを大量に最適化する方法に関する詳細なベストプラクティスについては、 [Campaign Classic Data Model Best practicesを参照してください](https://helpx.adobe.com/campaign/kb/acc-data-model-best-practices.html)。
