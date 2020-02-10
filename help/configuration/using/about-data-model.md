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
source-git-commit: 2ce2a1a55e244180a4e62d6f3b5a5ed5bb8aff6e

---


# Campaign Classicデータモデルについて{#about-data-model}

ここでは、Campaignの組み込み表とそのインタラクションについてより深く理解するために、Adobe Campaign Classicデータモデルの基本について説明します。

Adobe Campaignデータベースの概念データモデルは、一連の組み込みテーブルとそのインタラクションで構成されます。

各テーブルの説明にアクセスするには、に進み、リ **[!UICONTROL Admin > Configuration > Data schemas]**&#x200B;ストからリソースを選択して、タブをクリック **[!UICONTROL Documentation]** します。

![](assets/data-model_documentation-tab.png)

デフォルトのCampaign Classicデータモデルの詳細については、このドキュメントを参照して [ください](https://final-docs.campaign.adobe.com/doc/AC/en/technicalResources/_Datamodel_Description_of_the_main_tables.html)。

アプリケーションに格納されるデータの物理的な構造と論理的な構造は、XMLで記述されます。 スキーマと呼ばれるAdobe Campaign固有の文法に従います。 Adobe Campaignスキーマについて詳しくは、この節を参照してく [ださい](../../configuration/using/about-schema-reference.md)。

## 概要 {#data-model-overview}

Adobe Campaignは、相互にリンクされたテーブルを含むリレーショナルデータベースに依存しています。

Adobe Campaignデータモデルの基本構造は、次のとおりです。

## 受信者テーブル {#recipient-table}

データモデルは、デフォルトでRecipientテーブル(**NmsRecipient**)のメインテーブルに依存しています。 この表では、すべてのマーケティングプロファイルを保存できます。

「受信者」テーブルの詳細については、この節を参照して [ください](../../configuration/using/default-recipient-table.md)。

## 配信テーブル {#delivery-table}

また、データモデルには、すべてのマーケティングアクティビティを保存するための部分も含まれます。 通常は、配信テーブル(**NmsDelivery**)です。 このテーブルの各レコードは、配信アクションまたは配信テンプレートを表します。 ターゲット、コンテンツなどの配信を実行するために必要なすべてのパラメーターが含まれます。

## ログテーブル {#log-tables}

データモデルの別の部分では、キャンペーンの実行に関連付けられたすべてのログを一時的に保存できます。

配信ログは、すべてのチャネルを通じて受信者またはデバイスに送信されるすべてのメッセージです。 メインの配信ログテーブル(**NmsBroadLog**)には、すべての受信者の配信ログが格納されます。
メインのトラッキングログテーブル(**NmsTrackingLog**)には、すべての受信者のトラッキングログが格納されます。 トラッキングログは、電子メールの開封数やクリック数など、受信者の反応を表します。 各反応はトラッキングログに対応します。
配信ログとトラッキングログは、Adobe Campaignで指定され、変更可能な特定の期間の経過後に削除されます。 したがって、ログを定期的に書き出すことを強くお勧めします。

## 技術表 {#technical-tables}

最後に、データモデルの一部は、演算子やユーザー権限(**NmsGroup**)、フォルダー(**XtkFolder**)など、アプリケーションプロセスで使用される技術データで構成されます。