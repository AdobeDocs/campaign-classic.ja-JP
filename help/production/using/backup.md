---
product: campaign
title: バックアップ
description: バックアップ
audience: production
content-type: reference
topic-tags: data-processing
exl-id: e5ef6aba-dc22-4c8d-9fbb-13d507181b65
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---

# バックアップ{#backup}

![](../../assets/v7-only.svg)

マシン上の問題（物理的な問題やシステム関連の問題）が発生した場合にデータが失われないように、バックアップは不可欠です。

データは次の 2 つの場所に保存されます。

* 物理ファイルは、Adobe Campaignディレクトリに格納されます。
* その他のデータはデータベースに保存されます。

ほとんどのデータはデータベースに格納されています。 これは、バックアップする情報の 99%を表します。

## 物理ファイル {#physical-files}

ファイルは、次の複数のカテゴリに分類されます。

* **nl6/conf** にある設定ファイル

   これにより、Adobe Campaignを非常に迅速に再設定できます。

* リダイレクトファイル** nl6/var/`<instancename>`/redir**

   これらは追跡（「前方」とも呼ばれる）サーバー上にあり、以前のキャンペーンのリダイレクトをすべて含みます。 以前のキャンペーンでも引き続き使用されます。

* ログファイル：**nl6/var/`<instancename>`/log**

   これらは問題を追跡するのに使用できます。

したがって、バックアップするディレクトリは次のとおりです。

* nl6/conf

* nl6/var/`<instanceName>`/redir （各インスタンスに対して）

* nl6/var/`<instanceName>`/log （オプション）

* nl6/var/`<instanceName>`/relay （オプション）

>[!IMPORTANT]
>
>データベースをバックアップする必要があります。

## データベース {#database}

データベースには、Adobe Campaignのリッチクライアントコンソールに表示されるすべての情報と、すべての事業部門データが含まれています。

この操作は、ホスティング会社と、特にデータベース管理者が担当します。
