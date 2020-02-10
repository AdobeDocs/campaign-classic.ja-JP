---
title: v6.02での具体的な設定
seo-title: v6.02での具体的な設定
description: v6.02での具体的な設定
seo-description: null
page-status-flag: never-activated
uuid: ea072af3-fdc1-4828-ad13-d4327de1eaf8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: configuration
discoiquuid: 87a6cbda-54a6-4dae-8224-e06dc217f4fc
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# v6.02での具体的な設定{#specific-configurations-in-v6-02}

次の節では、v6.02からの移行時に必要な追加設定について詳しく説明します。また、「一般設定」セクションで詳しく説明されている設定も [行う必要があります](../../migration/using/general-configurations.md) 。

## Web アプリケーション {#web-applications}

v6.02から移行する場合、概要タイプのWebアプリケーションに関するエラーログが表示される場合があります。 エラーメッセージの例：

```
[PU-0006] Entity of type : 'xtk:entityBackupNew' and Id 'nms:webApp|taskOverview', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'xtk:formDictionary' and Id 'nms:webApp|lastTasks', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'nms:webApp' and Id 'taskOverview', expression '[SQLDATA[' was found : '...@owner-id] IN ([SQLDATA[select iGroupid...'. (iRc=-1)
```

これらのWebアプリケーションはSQLDataを使用していたので、高いセキュリティを確保したため、v7との互換性がありません。 これらのエラーは、移行エラーを引き起こします。

これらのWebアプリケーションを使用しなかった場合は、次のクリーンアップスクリプトを実行し、アップグレード後の処理を再実行します。

```
Nlserver javascript -instance:[instance_name] -file [installation_path]/datakit/xtk/fra/js/removeOldWebApp.js
```

これらのWebアプリケーションを変更し、v7で引き続き使用する場合は、異なるセキュリティゾーンで **allowSQLInjection** オプションを有効にし、アップグレード後に再起動する必要があります。 詳細は [SQLData](../../migration/using/general-configurations.md#sqldata) の節を参照してください。

## 使いやすさ：ホームページとナビゲーション {#user-friendliness--home-page-and-navigation}

>[!CAUTION]
>
>v6.02の概要タイプのWebアプリケーションを引き続き使用する場合は、アップグレード後に、様々なセキュリティゾーンで **allowSQLInjection** オプションをアクティブにする必要があります。 「 [Webアプリケーション](#web-applications)」を参照。

バージョン6.02から移行した後、Adobe Campaign v6.02のホームページは表示されなくなりましたが、引き続きアクセス可能で、Adobe Campaign v7との互換性が維持されます。

v6.02のホームページを引き続き使用するには、移行後に「互換性」パッケージをインストールする必要があります。

これを行うには、互換性パッケージを読み込みます。

をクリ **[!UICONTROL Tools > Advanced > Import package]** ックし、 **campaignMigration.xmlパッケージを** 「」で選択しま **`\nl\datakit\nms\[Your language]\package\optional`**&#x200B;す。

v6.02 webアプリケーションタイプインターフェイスへのアクセスを許可するには、 **sessionTokenOnly** server設定オプションをserverConf.xmlファイルで有効にする必要が **あります** 。

```
sessionTokenOnly="true"
```

このオプションは、インターフェイスの互換性を確保するためにセキュリティレベルを変更します。

パッケージがインストールされると、Adobe Campaign v7のホームページは、v6.02の古いホームページの完成ページに置き換えられ、v7（青いホームページバナー）の一般的な設定になります。

![](assets/dashboards.png)

このホームページ上のすべてのリンクは、リスト（、など）を除くv7 **[!UICONTROL operation list]**&#x200B;画面に **[!UICONTROL delivery tracking in operations]**&#x200B;リンクします。v6.02の概要（Webアプリケーション）へのリンク。

![](assets/dashboards2.png)

v6.02で設定した別の概要を追加する場合は、ダッシュボードからホームページに追加する必要があります。(**[!UICONTROL Administration > Access management > Dashboard]**)。

>[!NOTE]
>
>変更を登録するには、必ずコンソールを切断してから再接続してください。

## Message Center {#message-center}

Message centerコントロールインスタンスの移行後、機能させるには、トランザクションメッセージテンプレートを再公開する必要があります。

v7では、実行インスタンス上のトランザクションメッセージテンプレートの名前が変更されました。 現在、これらの変数の先頭には、作成元の制御インスタンスに対応する演算子名が付きます。例えば、 **control1_template1_rt** ( **control1** は演算子の名前)です。 大量のテンプレートがある場合は、コントロールインスタンスの古いテンプレートを削除することをお勧めします。
