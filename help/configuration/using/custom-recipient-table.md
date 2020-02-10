---
title: Adobe Campaign Classicデータモデルについて
description: このドキュメントでは、Adobe Campaign Classicデータモデルの基本について説明します。
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


# カスタム受信者テーブルの使用{#custom-recipient-table}

Adobe Campaignデータモデルをデザインする際は、標準搭載の受信者テーブルを使用するか [](../../configuration/using/default-recipient-table.md)、マーケティングプロファイルを保存する非標準の受信者テーブルを作成することができます。

実際、データモデルが受信者中心の構造に適合しない場合は、他のテーブルをAdobe Campaign内のターゲットディメンションとして設定できます。 例えば、単なる受信者ではなく、世帯、アカウント（携帯電話など）、会社/サイトをターゲットにする必要がある場合に、これが重要になります。

>[!NOTE]
>
>この場合、新しいターゲットマッピングを作成する必要 [があります](../../configuration/using/target-mapping.md)。

カスタム受信者テーブルを使用する際に必要なすべての原則と手順について、この節で詳しく説 [明します](../../configuration/using/about-custom-recipient-table.md)。

カスタム受信者テーブルを使用する利点は次のとおりです。

## 柔軟なデータモデル {#flexible-data-model}

「受信者」(Recipient)テーブルのフィールドのほとんどが不要な場合や、データモデルが受信者中心でない場合は、そのまま使用できる「受信者」(Recipient)テーブルは役に立ちません。

## 拡張性 {#scalability}

大量のボリュームを使用する場合は、効率的なデザインを実現するために、数個のフィールドを備えた合理化されたテーブルが必要です。 標準搭載の受信者テーブルには、役に立たないフィールドが多すぎるので、パフォーマンスと効率に影響を与える可能性があります。

## データの場所 {#data-location}

データが既存の外部マーケティングデータベースに存在する場合は、標準搭載の受信者テーブルを使用するのに多くの労力が必要になる場合があります。 既存の構造に基づいて新しい構造を作成する方が簡単です。

## 容易な移行 {#easy-migration}

アップグレード時に、すべての拡張機能が引き続き有効であることを確認するために、メンテナンスは必要ありません。

>[!IMPORTANT]
>
>カスタム受信者テーブルの使用は上級ユーザー向けに用意されており、一部の制限があります。 詳しくは、この節を参照してください。
