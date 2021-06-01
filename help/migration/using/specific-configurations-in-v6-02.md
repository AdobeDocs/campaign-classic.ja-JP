---
product: campaign
title: v6.02 特有の設定
description: v6.02 特有の設定
audience: migration
content-type: reference
topic-tags: configuration
exl-id: 7e8f8488-f3ef-4b64-9981-335d67caf372
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 3%

---

# v6.02 特有の設定{#specific-configurations-in-v6-02}

次の節では、v6.02から移行する際に必要な追加設定について詳しく説明します。[一般設定](../../migration/using/general-configurations.md)の節で詳しく説明している設定も構成する必要があります。

## web アプリケーション {#web-applications}

v6.02から移行する場合、概要タイプのWebアプリケーションに関するエラーログが表示される場合があります。 エラーメッセージの例：

```
[PU-0006] Entity of type : 'xtk:entityBackupNew' and Id 'nms:webApp|taskOverview', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'xtk:formDictionary' and Id 'nms:webApp|lastTasks', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'nms:webApp' and Id 'taskOverview', expression '[SQLDATA[' was found : '...@owner-id] IN ([SQLDATA[select iGroupid...'. (iRc=-1)
```

これらのWebアプリケーションはSQLDataを使用しており、セキュリティが高まるため、v7との互換性がありません。 これらのエラーは、移行エラーを引き起こします。

これらのWebアプリケーションを使用しなかった場合は、次のクリーンアップスクリプトを実行し、ポストアップグレードを再実行します。

```
Nlserver javascript -instance:[instance_name] -file [installation_path]/datakit/xtk/fra/js/removeOldWebApp.js
```

これらのWebアプリケーションを変更済みで、v7で引き続き使用する場合は、別のセキュリティゾーンで&#x200B;**allowSQLInjection**&#x200B;オプションを有効にし、アップグレード後に再開する必要があります。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata)の節を参照してください。

## 使いやすさ：ホームページとナビゲーション{#user-friendliness--home-page-and-navigation}

>[!IMPORTANT]
>
>v6.02の概要タイプのWebアプリケーションを引き続き使用する場合は、アップグレード後に、別のセキュリティゾーンで&#x200B;**allowSQLInjection**&#x200B;オプションを有効にする必要があります。 [Webアプリケーション](#web-applications)を参照してください。

バージョン6.02から移行した後、Adobe Campaign v6.02のホームページは表示されなくなりましたが、引き続きアクセス可能で、Adobe Campaign v7との互換性があります。

v6.02ホームページを引き続き使用するには、移行後に「互換性」パッケージをインストールする必要があります。

これをおこなうには、互換性パッケージをインポートします。

**[!UICONTROL ツール/詳細設定/パッケージをインポート]**&#x200B;をクリックし、**`\nl\datakit\nms\[Your language]\package\optional`**&#x200B;で&#x200B;**campaignMigration.xml**&#x200B;パッケージを選択します。

v6.02 Webアプリケーションタイプインターフェイスへのアクセスを許可するには、**sessionTokenOnly**&#x200B;サーバー設定オプションを&#x200B;**serverConf.xml**&#x200B;ファイルで有効にする必要があります。

```
sessionTokenOnly="true"
```

このオプションは、インターフェイスの互換性を確保するためにセキュリティレベルを変更します。

パッケージがインストールされると、Adobe Campaign v7ホームページは、v7の一般的な設定（青いホームページバナー）を含む古いv6.02ホームページに置き換えられます。

![](assets/dashboards.png)

このホームページ上のすべてのリンクは、リスト（**[!UICONTROL 操作リスト]**、**[!UICONTROL 操作の配信トラッキング]**&#x200B;など）を除き、v7 screensにリンクします。 v6.02の概要（webアプリケーション）へのリンク

![](assets/dashboards2.png)

v6.02で設定した別の概要を追加する場合は、ダッシュボードからホームページに追加する必要があります。 （**[!UICONTROL 管理/アクセス管理/ダッシュボード]**）。

>[!NOTE]
>
>変更を登録するには、必ずコンソールを切断してから再接続します。

## Message Center {#message-center}

Message Centerコントロールインスタンスの移行後、移行をおこなうには、トランザクションメッセージテンプレートを再公開する必要があります。

v7では、実行インスタンス上のトランザクションメッセージテンプレートの名前が変更されました。 現在、作成元のコントロールインスタンスに対応する演算子名が先頭に付きます。例えば、**control1_template1_rt**（ここで&#x200B;**control1**&#x200B;は演算子の名前）。 大量のテンプレートがある場合は、コントロールインスタンス上の古いテンプレートを削除することをお勧めします。
