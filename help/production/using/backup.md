---
product: campaign
title: バックアップ
description: バックアップ
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: data-processing
exl-id: e5ef6aba-dc22-4c8d-9fbb-13d507181b65
TQID: https://experienceleague.adobe.com/ZCExecNbs9DnWVoQLpvzlrH7k2eGhBNq7pEiybyQdi4
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: a075b2c1-7748-4328-b7f6-343aa314616a
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 232
ht-degree: 14%

---

# バックアップ{#backup}

バックアップは、マシン上で（物理的またはシステム関連の）問題が発生した場合にデータが失われるのを防ぐために不可欠です。

データは、次の2つの場所に保存されます。

* 物理ファイルはAdobe Campaignディレクトリに保存され，
* その他のデータはデータベースに保存されます。

データの大半はデータベースにある。 これは、バックアップする情報の99%を表します。

## 物理ファイル {#physical-files}

ファイルはいくつかのカテゴリに分けられます。

* **nl6/conf**&#x200B;に保存されている設定ファイルを使用すると、Adobe Campaignをすばやく再設定できます。

* **nl6/var/`<instance-name>`/redir**&#x200B;に保存されているリダイレクションファイルは、トラッキング（「frontal」と呼ばれることが多い）サーバー上にあり、以前のすべてのキャンペーンリダイレクトが含まれています。 以前のキャンペーンでも使用されています。

* **nl6/var/`<instance-name>`/log**&#x200B;に保存されているログファイルを使用して、問題を追跡できます。

したがって、バックアップするディレクトリは次のとおりです。

* nl6/conf

* nl6/var/`<instance-name>`/redir （各インスタンスについて）

* nl6/var/`<instance-name>`/log （オプション）

* nl6/var/`<instance-name>`/relay （オプション）


## データベース {#database}

>[!IMPORTANT]
>
>データベースをバックアップすることが不可欠です。


データベースには、Adobe Campaign リッチクライアントコンソールに表示されるすべての情報と、すべての事業部門データが含まれます。

ホスティング会社、特にそのデータベース管理者がこの操作を担当します。
