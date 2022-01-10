---
product: campaign
title: 移行を開始する前に
description: 移行を開始する前に
audience: migration
content-type: reference
topic-tags: migration-procedure
exl-id: d666bc0b-596a-4908-9364-7df5bb8d68d0
source-git-commit: 8610d29a3df1080f1622a2cb3685c0961fb40092
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 2%

---

# 前提条件{#before-starting-migration}

![](../../assets/v7-only.svg)

このページでは、移行プロセスを開始する前に実行する必要のある特定の手順を示します。 また、 [このページ](about-migration.md) を参照してください。

>[!NOTE]
>
>このドキュメントでは、コマンドをサンプルとして提供します。 設定によって異なる場合があります。

1. Adobe Campaignのバージョンを確認する：移行する前に、使用している現在のバージョンの最新ビルドをインストールします。
1. データをバックアップします。
1. 環境の確認：データベースエンジンシステム (DBMS) は変更できません。 例えば、PostgreSQL エンジンからエンジンエンジンに切り替えることはできませんOracle。 ただし、データベースエンジンの最新バージョンに切り替えることができます。 Unicode 以外のデータベースから Unicode データベースに移動することはできません。

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
>この **内部** パスワードは、すべてのトラッキングサーバーで同一である必要があります。 詳しくは、 [内部識別子](../../installation/using/configuring-campaign-server.md#internal-identifier) および [権限](../../platform/using/access-management.md) セクション。
