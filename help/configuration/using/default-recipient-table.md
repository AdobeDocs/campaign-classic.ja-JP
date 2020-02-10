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
source-git-commit: 65affa58a66090c3bffc837fdbd85aa46338bd3e

---


# デフォルトの受信者テーブルの使用{#default-recipient-table}

Adobe Campaignの標準搭載された「受信者」テーブルは、データモデルを作成するための良い出発点となります。 拡張が容易な定義済みのフィールドとテーブルリンクが多数あります。 これは、受信者中心の単純なデータモデルに適合するので、主に受信者をターゲットにする場合に特に便利です。

標準的な受信者テーブルを使用する利点は次のとおりです。

* 購読、シードリスト、調査、ソーシャルなどの機能をすぐに使用できます。
* マーケティングデータベースに受信者中心のデータモデルを提供する。
* より迅速な実装。
* サポートとパートナーによる容易な保守

ただし、Recipientテーブルを拡張することは可能ですが、テーブル内のフィールドやリンクの数を減らすことはできません。

>[!IMPORTANT]
>
>受信者テーブルのフィールドは、組み込みモジュールでエラーが発生する可能性があるので、削除しないことをお勧めします。

また、Recipientテーブルは製品の一部なので、製品の変更に伴い、テーブルと関連するフォームの両方が進化します。 したがって、アップグレード時に拡張機能が引き続き有効であるかどうかを確認するには、追加のメンテナンスが必要です。
