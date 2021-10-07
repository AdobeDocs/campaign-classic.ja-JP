---
product: campaign
title: v6.02 特有の設定
description: v6.02 特有の設定
audience: migration
content-type: reference
topic-tags: configuration
exl-id: 7e8f8488-f3ef-4b64-9981-335d67caf372
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 3%

---

# v6.02 特有の設定{#specific-configurations-in-v6-02}

![](../../assets/v7-only.svg)

次の節では、v6.02 からの移行時に必要な追加設定について詳しく説明します。[ 一般設定 ](../../migration/using/general-configurations.md) の節で詳しく説明する設定も行う必要があります。

## web アプリケーション {#web-applications}

v6.02 から移行する場合、概要タイプの Web アプリケーションに関するエラーログが表示されることがあります。 エラーメッセージの例：

```
[PU-0006] Entity of type : 'xtk:entityBackupNew' and Id 'nms:webApp|taskOverview', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'xtk:formDictionary' and Id 'nms:webApp|lastTasks', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'nms:webApp' and Id 'taskOverview', expression '[SQLDATA[' was found : '...@owner-id] IN ([SQLDATA[select iGroupid...'. (iRc=-1)
```

これらの Web アプリケーションは SQLData を使用しており、セキュリティが高まるため v7 との互換性がありません。 これらのエラーは、移行エラーを引き起こします。

これらの Web アプリケーションを使用しなかった場合は、次のクリーンアップスクリプトを実行し、ポストアップグレードを再実行します。

```
Nlserver javascript -instance:[instance_name] -file [installation_path]/datakit/xtk/fra/js/removeOldWebApp.js
```

これらの Web アプリケーションを変更し、v7 で引き続き使用する場合は、別のセキュリティゾーンで **allowSQLInjection** オプションを有効にし、アップグレード後に再び開始する必要があります。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata) の節を参照してください。

## 使いやすさ：ホームページとナビゲーション {#user-friendliness--home-page-and-navigation}

>[!IMPORTANT]
>
>v6.02 の概要タイプの Web アプリケーションを引き続き使用する場合は、アップグレード後に、別のセキュリティゾーンで **allowSQLInjection** オプションを有効にする必要があります。 [Web アプリケーション ](#web-applications) を参照してください。

バージョン 6.02 から移行した後は、Adobe Campaign v6.02 のホームページは表示されなくなりましたが、引き続きアクセス可能で、Adobe Campaign v7 と互換性があります。

v6.02 ホームページを引き続き使用するには、移行後に「互換性」パッケージをインストールする必要があります。

それには、互換性パッケージをインポートします。

**[!UICONTROL ツール/詳細設定/パッケージをインポート]** をクリックし、**`\nl\datakit\nms\[Your language]\package\optional`** で **campaignMigration.xml** パッケージを選択します。

v6.02 Web アプリケーションタイプのインターフェイスへのアクセスを許可するには、**sessionTokenOnly** サーバー設定オプションを **serverConf.xml** ファイルで有効にする必要があります。

```
sessionTokenOnly="true"
```

このオプションは、インターフェイスの互換性を確保するためにセキュリティレベルを変更します。

パッケージがインストールされると、Adobe Campaign v7 ホームページは、古い v6.02 ホームページに置き換えられ、v7（青いホームページバナー）の一般的な設定が完了します。

![](assets/dashboards.png)

このホームページ上のすべてのリンクは、リスト（**[!UICONTROL 操作リスト]**、**[!UICONTROL 操作の配信トラッキング]** など）を除き、v7 画面にリンクします。 v6.02 の概要（web アプリケーション）へのリンク

![](assets/dashboards2.png)

v6.02 で設定した別の概要を追加する場合は、ダッシュボードからホームページに追加する必要があります。 （**[!UICONTROL 管理/アクセス管理/ダッシュボード]**）。

>[!NOTE]
>
>変更を登録するには、必ずコンソールを切断してから再接続します。

## Message Center {#message-center}

Message Center コントロールインスタンスの移行後、移行をおこなうには、トランザクションメッセージテンプレートを再公開する必要があります。

v7 では、実行インスタンス上のトランザクションメッセージテンプレートの名前が変更されました。 現在は、作成元のコントロールインスタンスに対応する演算子名が先頭に付いています。例えば、**control1_template1_rt**（**control1** は演算子の名前）。 大量のテンプレートがある場合は、コントロールインスタンスで古いテンプレートを削除することをお勧めします。
