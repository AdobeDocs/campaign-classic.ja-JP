---
title: 移行を開始する前に
seo-title: 移行を開始する前に
description: 移行を開始する前に
seo-description: null
page-status-flag: never-activated
uuid: b9325510-2fa5-4be4-9cf0-f37232bbbd8c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: migration-procedure
discoiquuid: d8877378-fb43-4f32-91c6-60f2f788f916
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---


# 移行を開始する前に{#before-starting-migration}

>[!NOTE]
>
>このドキュメントでは、データベースにリンクされたコマンドを例として示します。 これらは、設定によって異なります。 データベース管理者に問い合わせてください。

## 警告 {#warnings}

### インストール済みバージョン {#installed-version}

移行する前に、使用している最新バージョンの最新ビルドをインストールする必要があります。

nlserver pdump **[!UICONTROL コマンドを使用して、クライアントコンソールの]** ヘルプ/バージョン情報 **(About** )メニューに移動し、サーバーのバージョンを確認します。

### データバックアップ {#data-backup}

移行プロセスを開始する前に、データをバックアップする **必要があります** 。

### 環境 {#environment}

* データベースエンジンタイプ(DBMS)は変更できません。 例えば、PostgreSQLエンジンからOracleエンジンに切り替えることはできません。 ただし、Oracle 8エンジンからOracle 10エンジンに切り替えることができます。
* 非UnicodeデータベースからUnicodeデータベースに移動することはできません。

### 推奨事項 {#recommendation}

移行手順は特に機密性が高いので、手順を開始する前に、このドキュメントを十分に読むことをお勧めします。

## 移行手順 {#migration-steps}

移行手順は、 **すべてのサーバーで特定の順序で実行する必要があります** 。

* ス **タンドアロンプラットフォーム** （シングルマシンモード）の場合は、アプリケーション全体が移行されます。
* 標 **準プラットフォーム** （エンタープライズ）の場合の移行手順は次のとおりです。

   1. マーケティングサーバーを移行します。
   1. メールサーバー(mta)を移行します。
   1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。

* Cloud Messagingプラットフォームの場合 ****、実行サーバーはAdobe Campaignでホストされます。 Adobe Campaignに問い合わせて、異なるサーバ間の移行を調整してください。
* パワー・ブースターまたは **パワー・クラスタ・プラットフォームの場合**、移行手順は次のとおりです。

   1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。
   1. パワー・ブースタ/クラスタ・サーバを移行します。
   1. マーケティングサーバーを移行します。

>[!NOTE]
>
>v6.02マーケティングサーバーとv7 Cloud MessagingまたはPower Booster/Clusterサーバー間の通信は可能です。 ただし、v6.02マーケティングサーバーを維持する場合は、Cloud MessagingまたはPower Booster/Clusterに移行する前に、最新のv6.02ビルドでこのバージョンを更新する必要があります。

## ユーザーパスワード {#user-passwords}

v7では、 **内部** / **管理** 演算子の接続は、パスワードで保護する必要があります。 移行 **前に、これらのアカウントおよびすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧め**&#x200B;します。 **内部用のパスワードを指定していない場合**、接続できません。 パスワードを **内部に割り当てるには**、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>内 **** 部パスワードは、すべてのトラッキングサーバーで同一にする必要があります。 詳しくは、 [内部識別子](../../installation/using/campaign-server-configuration.md#internal-identifier) 、権限に [ついての節を参照してください](../../platform/using/access-management.md#about-permissions) 。

