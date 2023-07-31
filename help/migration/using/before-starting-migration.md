---
product: campaign
title: 移行を開始する前に
description: 移行を開始する前に
feature: Upgrade
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
audience: migration
content-type: reference
topic-tags: migration-procedure
hide: true
hidefromtoc: true
exl-id: d666bc0b-596a-4908-9364-7df5bb8d68d0
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 2%

---

# 前提条件{#before-starting-migration}



このページでは、移行プロセスを開始する前に実行する特定の手順を示します。 また、 [このページ](about-migration.md) を参照してください。

>[!NOTE]
>
>このドキュメントでは、コマンドをサンプルとして提供します。 設定によって異なる場合があります。

1. Adobe Campaignのバージョンを確認します。移行する前に、使用している現在のバージョンの最新ビルドをインストールします。
1. データをバックアップします。
1. 環境を確認してください。データベースエンジンシステム (DBMS) は変更できません。 例えば、PostgreSQL エンジンからエンジンエンジンに切り替えることはできませんOracle。 ただし、データベースエンジンの最新バージョンに切り替えることができます。 Unicode 以外のデータベースから Unicode データベースに移動することはできません。

## 移行手順 {#migration-steps}

移行手順は、次の場所で実行する必要があります。 **すべて** サーバーと特定の順序で送信されます。

* の場合、 **スタンドアロンプラットフォーム** （シングルマシンモード）、アプリケーション全体が移行されます。
* の場合、 **標準プラットフォーム** （エンタープライズ）移行手順は、次のとおりです。

   1. マーケティングサーバーを移行します。
   1. メールサーバー (mta) を移行します。
   1. リダイレクトとトラッキングサーバー (Apache/IIS) を移行します。

* の場合、 **Cloud Messaging プラットフォーム**&#x200B;に設定されていない場合、実行サーバーはAdobe Campaignでホストされます。 異なるサーバー間の移行を調整するには、Adobe Campaignにお問い合わせください。
* の場合、 **パワーブースターまたはパワークラスタープラットフォーム**&#x200B;移行手順は次のとおりです。

   1. リダイレクトとトラッキングサーバー (Apache/IIS) を移行します。
   1. パワーブースター/クラスターサーバーを移行します。
   1. マーケティングサーバーを移行します。

## ユーザーパスワード {#user-passwords}

v7 では、 **内部** および **admin** オペレーターの接続は、パスワードで保護する必要があります。 これらのアカウントおよびすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧めします。 **移行前**. パスワードを指定していない場合は、 **内部**&#x200B;接続できなくなります。 パスワードをに割り当てるには **内部**、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!CAUTION]
>
>The **内部** パスワードは、すべてのトラッキングサーバーで同一である必要があります。 詳しくは、 [内部識別子](../../installation/using/configuring-campaign-server.md#internal-identifier) および [権限](../../platform/using/access-management.md) セクション。
