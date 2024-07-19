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
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---

# バックアップ{#backup}

マシン上で（物理またはシステムに関連する）問題が発生した場合にデータが失われないようにするには、バックアップが不可欠です。

データは、次の 2 つの異なる場所に保存されます。

* 物理ファイルは、Adobe Campaign ディレクトリに格納されます。
* その他のデータはデータベースに保存されます。

ほとんどのデータはデータベースに入っています。 これは、バックアップ対象の情報の 99% を表します。

## 物理ファイル {#physical-files}

ファイルはいくつかのカテゴリに分類されます。

* **nl6/conf** に格納される設定ファイルを使用すると、Adobe Campaignを非常に迅速に再設定できます。

* **nl6/var/`<instance-name>`/redir** に保存されるリダイレクトファイルは、トラッキング（「フロント」と呼ばれることが多い）サーバー上にあり、以前の campaign リダイレクトをすべて含みます。 以前のキャンペーンでも引き続き使用されます。

* **nl6/var/`<instance-name>`/log** に保存されるログファイルを使用して問題をトレースできます。

したがって、バックアップするディレクトリは次のようになります。

* nl6/conf

* nl6/var/`<instance-name>`/redir （各インスタンスに対して）

* nl6/var/`<instance-name>`/log （オプション）

* nl6/var/`<instance-name>`/relay （オプション）


## データベース {#database}

>[!IMPORTANT]
>
>データベースをバックアップする必要があります。


このデータベースには、Adobe Campaign リッチクライアントコンソールに表示されるすべての情報と、すべての事業部門データが含まれています。

ホスティング会社、特にデータベース管理者が、この操作を担当します。
