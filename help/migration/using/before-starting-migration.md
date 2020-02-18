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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9f7cf3d530f141a661df5fcc8cbcf0bb4c8d3e89

---


# 移行を開始する前に{#before-starting-migration}

>[!NOTE]
>
>このドキュメントでは、データベースにリンクされたコマンドの例を示します。 これらは設定によって異なります。 データベース管理者に問い合わせてください。

## 警告 {#warnings}

### インストール済みバージョン {#installed-version}

移行する前に、使用している最新バージョンの最新ビルドをインストールする必要があります。

nlserver pdumpコマンドを使用して、クライアントコンソールのメ **[!UICONTROL Help> About]** ニューに移動し、サーバー上のバージョ **ンを確認し** ます。

### データバックアップ {#data-backup}

移行プロセスを開始する前に、データをバ **ックアップ** する必要があります。

### 環境 {#environment}

* データベースエンジンタイプ(DBMS)を変更することはできません。 例えば、PostgreSQLエンジンからOracleエンジンに切り替えることはできません。 ただし、Oracle 8エンジンからOracle 10エンジンに切り替えることができます。
* 非UnicodeデータベースからUnicodeデータベースに移動することはできません。

### 推奨 {#recommendation}

移行手順は特に慎重に行う必要があるので、手順を開始する前に、このドキュメントを十分に読むことを強くお勧めします。

## 移行手順 {#migration-steps}

移行手順は、すべてのサーバーで特 **定の順序** で実行する必要があります。

* スタンドアロンプラットフォ **ーム** （シングルマシンモード）の場合、アプリケーション全体が移行されます。
* 標準プラットフォーム **** （エンタープライズ）の場合、移行手順は次のとおりです。

   1. マーケティングサーバーを移行します。
   1. メールサーバー(mta)を移行します。
   1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。

* クラウドメッセージングプラット **フォームの場合**、実行サーバーはAdobe Campaignでホストされます。 異なるサーバー間の移行を調整するには、Adobe Campaignにお問い合わせください。
* パワーブースターまたはパワーク **ラスタプラットフォームの場合**、移行手順は次のとおりです。

   1. リダイレクトサーバーとトラッキングサーバー(Apache/IIS)を移行します。
   1. パワーブースタ/クラスタサーバを移行します。
   1. マーケティングサーバーを移行します。

>[!NOTE]
>
>v6.02マーケティングサーバーとv7クラウドメッセージングまたはパワーブースター/クラスターサーバー間の通信が可能です。 ただし、v6.02マーケティングサーバーを維持する場合は、Cloud MessagingまたはPower Booster/Clusterに移行する前に、最新のv6.02ビルドで更新する必要があります。

## ユーザーパスワード {#user-passwords}

v7では、内部と **管理者の****演算子の接続は** 、パスワードで保護する必要があります。 移行前に、これらのアカウントとすべての演算子アカウントにパスワードを割り当てることを強 **くお勧めしま**&#x200B;す。 内部用のパスワードを指定しな **いと**、接続できません。 内部にパスワードを割り当てる **には**、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>内部パ **スワードは** 、すべてのトラッキングサーバーで同じにする必要があります。 詳しくは、「内部識別子」および「権限に [ついて](../../installation/using/campaign-server-configuration.md#internal-identifier) 」の節を [参照してください](../../platform/using/access-management.md#about-permissions) 。

