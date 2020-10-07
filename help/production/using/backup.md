---
title: バックアップ
seo-title: バックアップ
description: バックアップ
seo-description: null
page-status-flag: never-activated
uuid: 50134154-a671-4534-b48d-a9e2c42e8f1a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: data-processing
discoiquuid: 870ab0f2-1bd7-42e7-8d83-a08a520b6587
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---


# バックアップ{#backup}

マシン上の問題（物理的な問題でもシステム関連の問題でも）のイベントにデータが失われないように、バックアップは不可欠です。

データは、次の2つの場所に別々に保存されます。

* 物理ファイルはAdobe Campaignディレクトリに格納され、
* その他のデータはデータベースに格納されます。

データの大部分はデータベースにあります。 これは、バックアップする情報の99%を表します。

## 物理ファイル {#physical-files}

ファイルは、次の複数のカテゴリーに分けられます。

* 構成ファイル( **nl6/conf内)**

   これにより、Adobe Campaignを非常に迅速に再設定できます。

* リダイレクトファイル** nl6/var/`<instancename>`/redir**

   これらはトラッキング（「前頭」と呼ばれることが多い）サーバー上にあり、以前のキャンペーンのリダイレクトがすべて含まれます。 これらは、以前のキャンペーンでも引き続き使用されます。

* ログファイル： **nl6/var/`<instancename>`/log**

   これらは、問題を追跡するために使用できます。

したがって、バックアップするディレクトリは次のとおりです。

* nl6/conf

* nl6/var/`<instanceName>`/redir（各インスタンスに対して）

* nl6/var/`<instanceName>`/log（オプション）

* nl6/var/`<instanceName>`/relay（オプション）

>[!CAUTION]
>
>データベースをバックアップする必要があります。

## データベース {#database}

データベースには、Adobe Campaignリッチクライアントコンソールに表示されるすべての情報と、すべての基幹業務データが含まれます。

この操作は、ホスティング会社とそのデータベース管理者が行います。
