---
product: campaign
title: 移行を開始する前に
description: 移行を開始する前に
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migration-procedure
hide: true
exl-id: d666bc0b-596a-4908-9364-7df5bb8d68d0
TQID: https://experienceleague.adobe.com/FBbSwRfACqdgT1S9aXlDvR4tqqBOuv1BnMYqASi4OoQ
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 323
ht-degree: 2%

---

# 前提条件{#before-starting-migration}



このページでは、移行プロセスを開始する前に実行する特定の手順を示します。 詳細なガイダンスについては、[このページ ](about-migration.md)も参照してください。

>[!NOTE]
>
>このドキュメントでは、コマンドはサンプルとして提供されています。 設定によって異なる場合があります。

1. Adobe Campaignのバージョンを確認する：移行する前に、使用中の最新バージョンの最新ビルドをインストールします。
1. データのバックアップ：
1. 環境を確認してください：データベース エンジン システム （DBMS）を変更することはできません。 例えば、PostgreSQL エンジンからOracle エンジンに切り替えることはできません。 ただし、データベースエンジンの最新バージョンに切り替えることができます。 Unicode以外のデータベースからUnicode データベースに移行することはできません。

## 移行手順 {#migration-steps}

移行手順は、**all** サーバーで、特定の順序で実行する必要があります。

* **スタンドアロンプラットフォーム** （シングルマシンモード）の場合、アプリケーション全体が移行されます。
* **標準プラットフォーム** （エンタープライズ）の場合、移行手順は次のとおりです。

   1. マーケティングサーバーの移行。
   1. メールサーバー（mta）を移行します。
   1. リダイレクトおよびトラッキングサーバー（Apache/IIS）を移行します。

* **Cloud Messaging Platform**&#x200B;の場合、実行サーバーはAdobe Campaignでホストされます。 異なるサーバー間の移行を調整するには、Adobe Campaignにお問い合わせください。
* **Power BoosterまたはPower Cluster プラットフォーム**&#x200B;の場合、移行手順は次のとおりです。

   1. リダイレクトおよびトラッキングサーバー（Apache/IIS）を移行します。
   1. Power Booster/Cluster サーバーを移行します。
   1. マーケティングサーバーの移行。

## ユーザーパスワード {#user-passwords}

v7では、**internal**&#x200B;および&#x200B;**admin**&#x200B;のオペレーター接続はパスワードで保護する必要があります。 移行前&#x200B;**にこれらのアカウントとすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧めします**。 **internal**&#x200B;のパスワードを指定していない場合は、接続できません。 パスワードを&#x200B;**internal**&#x200B;に割り当てるには、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!CAUTION]
>
>**internal** パスワードは、すべてのトラッキングサーバーで同じである必要があります。 詳細については、[内部識別子](../../installation/using/configuring-campaign-server.md#internal-identifier)および[権限](../../platform/using/access-management.md)の節を参照してください。
