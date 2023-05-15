---
product: campaign
title: バックアップ
description: バックアップ
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
badge-v7-prem: label="on-premise & hybrid" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=en" tooltip="Applies to on-premise and hybrid deployments only"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: e5ef6aba-dc22-4c8d-9fbb-13d507181b65
source-git-commit: a5762cd21a1a6d5a5f3a10f53a5d1f43542d99d4
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---

# バックアップ{#backup}



マシン上の問題（物理的な問題でもシステム関連の問題でも）が発生した場合にデータが失われるのを防ぐために、バックアップは不可欠です。

データは次の 2 つの場所に保存されます。

* 物理ファイルは、 Adobe Campaignディレクトリに格納されます。
* その他のデータは、データベースに格納されます。

ほとんどのデータはデータベースに格納されています。 これは、バックアップする情報の 99%を表します。

## 物理ファイル {#physical-files}

ファイルは、次のように複数のカテゴリに分類されます。

* 設定ファイル： **nl6/conf**

   これにより、Adobe Campaignを非常に迅速に再設定できます。

* リダイレクトファイル** nl6/var/`<instancename>`/redir**

   これらはトラッキング（「フロント」とも呼ばれる）サーバー上にあり、以前のキャンペーンのリダイレクトをすべて含みます。 これらは、以前のキャンペーンでも引き続き使用されます。

* ログファイル： **nl6/var/`<instancename>`/log**

   これらは、問題を追跡するために使用できます。

バックアップするディレクトリは次のようになります。

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
