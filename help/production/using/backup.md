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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2a11a73b0679c0a65dc10f71869bf2a6c6efc008

---


# バックアップ{#backup}

マシン上の問題（物理またはシステムに関連する問題）が発生した場合にデータが失われるのを防ぐために、バックアップは不可欠です。

データは2つの異なる場所に保存されます。

* 物理ファイルは、Adobe Campaignのディレクトリに保存され、
* その他のデータはデータベースに格納されます。

ほとんどのデータはデータベース内にあります。 これは、バックアップする情報の99%を表します。

## 物理ファイル {#physical-files}

ファイルは、次のカテゴリに分類されます。

* 設定ファイル( **nl6/conf内)**

   これにより、Adobe Campaignを非常に迅速に再設定できます。

* リダイレクトファイル** nl6/var/`<instancename>`/redir**

   これらはトラッキング（「フロント」とも呼ばれる）サーバー上にあり、以前のキャンペーンのリダイレクトがすべて含まれます。 以前のキャンペーンでも引き続き使用されます。

* ログファイル： **nl6/var/`<instancename>`/log**

   これらは問題の追跡に使用できます。

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

この操作は、ホスティング会社とそのデータベース管理者が担当します。
