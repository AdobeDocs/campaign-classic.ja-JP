---
product: campaign
title: バックアップ
description: バックアップ
audience: production
content-type: reference
topic-tags: data-processing
exl-id: e5ef6aba-dc22-4c8d-9fbb-13d507181b65
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---

# バックアップ{#backup}

マシン上の問題（物理的な問題でもシステム関連の問題でも）が発生した場合にデータが失われないように、バックアップは不可欠です。

データは次の2つの場所に保存されます。

* 物理ファイルはAdobe Campaignディレクトリに格納されます。
* その他のデータは、データベースに格納されます。

ほとんどのデータはデータベースに格納されます。 これは、バックアップする情報の99%を表します。

## 物理ファイル{#physical-files}

ファイルは、次の複数のカテゴリに分類されます。

* **nl6/conf**&#x200B;にある設定ファイル

   これにより、Adobe Campaignを非常に迅速に再設定できます。

* リダイレクトファイル** nl6/var/`<instancename>`/redir**

   これらは、追跡（多くの場合、「前方」と呼ばれる）サーバー上にあり、以前のキャンペーンのリダイレクトをすべて含みます。 これらは、以前のキャンペーンでも引き続き使用されます。

* ログファイル：**nl6/var/`<instancename>`/log**

   これらは、問題を追跡するために使用できます。

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
