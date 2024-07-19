---
product: campaign
title: 移行を開始する前に
description: 移行を開始する前に
feature: Upgrade
audience: migration
content-type: reference
topic-tags: migration-procedure
hide: true
hidefromtoc: true
exl-id: d666bc0b-596a-4908-9364-7df5bb8d68d0
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 2%

---

# 前提条件{#before-starting-migration}



このページでは、移行プロセスを開始する前に実行すべき特定の手順を示します。 また、詳しくは [ このページ ](about-migration.md) を参照する必要があります。

>[!NOTE]
>
>このドキュメントでは、コマンドはサンプルとして提供されています。 設定によって異なる場合があります。

1. Adobe Campaignのバージョンを確認します。移行する前に、使用している現在のバージョンの最新ビルドをインストールします。
1. データをバックアップします。
1. 環境を確認してください。データベースエンジンシステム（DBMS）を変更することはできません。 例えば、PostgreSQL エンジンからOracleエンジンに切り替えることはできません。 ただし、データベースエンジンを最新バージョンに切り替えることはできます。 非 Unicode データベースから Unicode データベースに移行することはできません。

## 移行手順 {#migration-steps}

移行手順は、**すべて** サーバー上で、特定の順序で実行する必要があります。

* **スタンドアロンプラットフォーム** （シングルマシンモード）の場合、アプリケーション全体が移行されます。
* **標準プラットフォーム** （エンタープライズ）の場合、移行手順は次のとおりです。

   1. マーケティングサーバーを移行します。
   1. メールサーバー（mta）を移行します。
   1. リダイレクトサーバーとトラッキングサーバー（Apache/IIS）を移行します。

* **Cloud Messaging プラットフォーム** の場合、実行サーバーはAdobe Campaignでホストされます。 異なるサーバー間の移行を調整するには、Adobe Campaignにお問い合わせください。
* **パワーブースターまたはパワークラスタープラットフォーム** の場合、移行手順は次のとおりです。

   1. リダイレクトサーバーとトラッキングサーバー（Apache/IIS）を移行します。
   1. パワーブースター/クラスターサーバーを移行します。
   1. マーケティングサーバーを移行します。

## ユーザーパスワード {#user-passwords}

v7 では、**internal** および **admin** オペレーター接続はパスワードで保護する必要があります。 これらのアカウントとすべてのオペレーターアカウントに、**移行前** パスワードを割り当てることを強くお勧めします。 **internal** のパスワードを指定していない場合、接続できません。 **internal** にパスワードを割り当てるには、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!CAUTION]
>
>**内部** パスワードは、すべてのトラッキングサーバーで同じである必要があります。 詳しくは、[ 内部識別子 ](../../installation/using/configuring-campaign-server.md#internal-identifier) および [ 権限 ](../../platform/using/access-management.md) の節を参照してください。
