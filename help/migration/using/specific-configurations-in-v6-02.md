---
title: v6.02 特有の設定
seo-title: v6.02 特有の設定
description: v6.02 特有の設定
seo-description: null
page-status-flag: never-activated
uuid: ea072af3-fdc1-4828-ad13-d4327de1eaf8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: configuration
discoiquuid: 87a6cbda-54a6-4dae-8224-e06dc217f4fc
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---


# v6.02 特有の設定{#specific-configurations-in-v6-02}

次の節では、v6.02から移行する際に必要な追加設定について詳しく説明します。 [一般設定](../../migration/using/general-configurations.md) 節で詳しく説明している設定も行う必要があります。

## Web アプリケーション {#web-applications}

v6.02から移行する場合、概要タイプのWebアプリケーションに関するエラーログが表示される場合があります。 エラーメッセージの例：

```
[PU-0006] Entity of type : 'xtk:entityBackupNew' and Id 'nms:webApp|taskOverview', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'xtk:formDictionary' and Id 'nms:webApp|lastTasks', expression '[SQLDATA[' was found : '...)) or (@id IN ([SQLDATA[select 
[PU-0006] Entity of type : 'nms:webApp' and Id 'taskOverview', expression '[SQLDATA[' was found : '...@owner-id] IN ([SQLDATA[select iGroupid...'. (iRc=-1)
```

これらのWebアプリケーションはSQLDataを使用しており、セキュリティが高まるためv7との互換性がありません。 これらのエラーは、移行エラーを引き起こします。

これらのWebアプリケーションを使用しなかった場合は、次のクリーンアップスクリプトを実行し、アップグレード後に再実行します。

```
Nlserver javascript -instance:[instance_name] -file [installation_path]/datakit/xtk/fra/js/removeOldWebApp.js
```

これらのWebアプリケーションを変更し、v7で引き続き使用する場合は、異なるセキュリティゾーンで **allowSQLInjection** オプションをアクティブ化し、アップグレード後の開始を再度行う必要があります。 詳細は、 [SQLData](../../migration/using/general-configurations.md#sqldata) の節を参照してください。

## 使いやすさ：ホームページとナビゲーション {#user-friendliness--home-page-and-navigation}

>[!IMPORTANT]
>
>v6.02の概要タイプのWebアプリケーションを引き続き使用する場合は、アップグレード後の前に、様々なセキュリティゾーンで **allowSQLInjection** オプションをアクティブにする必要があります。 Refer to [Web applications](#web-applications).

バージョン6.02から移行した後は、Adobe Campaignv6.02のホームページは表示されなくなりましたが、引き続きアクセス可能で、Adobe Campaignv7との互換性があります。

v6.02のホームページを引き続き使用するには、移行後に「互換性」パッケージをインストールする必要があります。

これを行うには、互換性パッケージを読み込みます。

**[!UICONTROL ツール/アドバンスト/パッケージの読み込みをクリックし]** 、で **campaignMigration.xml** パッケージを選択し **`\nl\datakit\nms\[Your language]\package\optional`**&#x200B;ます。

v6.02Web アプリケーションタイプインターフェイスへのアクセスを許可するには、sessionTokenOnly **server設定オプションを** serverConf.xml **** ファイルで有効にする必要があります。

```
sessionTokenOnly="true"
```

このオプションを選択すると、インターフェイスの互換性を確保するためにセキュリティレベルが変更されます。

パッケージがインストールされると、Adobe Campaignv7ホームページは、v6.02の古いホームページ完成版で、v7の一般的な設定(青いホームページバナー)に置き換えられます。

![](assets/dashboards.png)

このホームページ上のすべてのv7画面へのリンクは、リスト(**[!UICONTROL 操作リスト]**、操作の **[!UICONTROL 配信追跡]**&#x200B;など)を除き、 v6.02の概要（webアプリケーション）へのリンク。

![](assets/dashboards2.png)

v6.02で設定した別の概要を追加する場合は、ダッシュボードからホームページにこの概要を追加する必要があります。 (**[!UICONTROL 管理/アクセス管理/ダッシュボード]**)。

>[!NOTE]
>
>変更を登録するには、必ずコンソールを切断してから再接続してください。

## Message Center {#message-center}

Message Centerコントロールインスタンスの移行後、トランザクションメッセージテンプレートが機能するように、再公開する必要があります。

v7では、実行インスタンスのトランザクションメッセージテンプレート名が変更されました。 現在、これらの文字には、作成元のコントロールインスタンスに対応する演算子名のプレフィックスが付きます。例えば、 **control1_template1_rt** ( **control1** は演算子の名前)です。 大量のテンプレートがある場合は、コントロールインスタンス上の古いテンプレートを削除することをお勧めします。
