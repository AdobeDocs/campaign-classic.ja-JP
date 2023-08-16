---
product: campaign
title: バックアップ
description: バックアップ
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: e5ef6aba-dc22-4c8d-9fbb-13d507181b65
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 12%

---

# バックアップ{#backup}

マシン上の問題（物理的な問題でもシステム関連の問題でも）が発生した場合にデータが失われるのを防ぐために、バックアップは不可欠です。

データは次の 2 つの場所に保存されます。

* 物理ファイルは、 Adobe Campaignディレクトリに格納されます。
* その他のデータは、データベースに格納されます。

ほとんどのデータはデータベースに格納されています。 これは、バックアップする情報の 99%を表します。

## 物理ファイル {#physical-files}

ファイルは、次のように複数のカテゴリに分類されます。

* 設定ファイル（に保存） **nl6/conf**&#x200B;を使用すると、Adobe Campaignを非常にすばやく再設定できます。

* リダイレクトファイル（に保存）  **nl6/var/`<instance-name>`/redir**&#x200B;は、トラッキング（多くの場合、「フロント」と呼ばれます）サーバー上にあり、以前のキャンペーンのリダイレクトをすべて含みます。 これらは、以前のキャンペーンでも引き続き使用されます。

* ログファイル（に保存） **nl6/var/`<instance-name>`/log**&#x200B;を使用して、問題を追跡できます。

バックアップするディレクトリは次のようになります。

* nl6/conf

* nl6/var/`<instance-name>`/redir （各インスタンスに対して）

* nl6/var/`<instance-name>`/log （オプション）

* nl6/var/`<instance-name>`/relay （オプション）


## データベース {#database}

>[!IMPORTANT]
>
>データベースをバックアップする必要があります。


データベースには、Adobe Campaignのリッチクライアントコンソールに表示されるすべての情報と、すべての事業部門データが含まれています。

この操作は、ホスティング会社と、特にデータベース管理者が担当します。
