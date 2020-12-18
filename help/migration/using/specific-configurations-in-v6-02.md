---
solution: Campaign Classic
product: campaign
title: v6.02 特有の設定
description: v6.02 特有の設定
audience: migration
content-type: reference
topic-tags: configuration
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 3%

---


# v6.02 特有の設定{#specific-configurations-in-v6-02}

次の節では、v6.02から移行する際に必要な追加設定について説明します。また、[一般設定](../../migration/using/general-configurations.md)の節で詳しく説明している設定も構成する必要があります。

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

これらのWebアプリケーションを変更し、v7で引き続き使用する場合は、異なるセキュリティゾーンの&#x200B;**allowSQLInjection**&#x200B;オプションを有効にし、アップグレード後の開始を再度行う必要があります。 詳しくは、[SQLData](../../migration/using/general-configurations.md#sqldata)を参照してください。

## 使いやすさ：ホームページとナビゲーション{#user-friendliness--home-page-and-navigation}

>[!IMPORTANT]
>
>v6.02の概要タイプのWebアプリケーションを引き続き使用する場合は、アップグレード後に、異なるセキュリティゾーンで&#x200B;**allowSQLInjection**&#x200B;オプションを有効にする必要があります。 [Web アプリケーション](#web-applications)を参照してください。

バージョン6.02から移行した後は、Adobe Campaignv6.02のホームページは表示されなくなりましたが、引き続きアクセス可能で、Adobe Campaignv7との互換性があります。

v6.02のホームページを引き続き使用するには、移行後に「互換性」パッケージをインストールする必要があります。

これを行うには、互換性パッケージを読み込みます。

**[!UICONTROL ツール/詳細/パッケージの読み込み]**&#x200B;をクリックし、**`\nl\datakit\nms\[Your language]\package\optional`**&#x200B;の&#x200B;**campaignMigration.xml**&#x200B;パッケージを選択します。

v6.02Web アプリケーションタイプインターフェイスへのアクセスを許可するには、**sessionTokenOnly**&#x200B;サーバー構成オプションを&#x200B;**serverConf.xml**&#x200B;ファイルで有効にする必要があります。

```
sessionTokenOnly="true"
```

このオプションを選択すると、インターフェイスの互換性を確保するためにセキュリティレベルが変更されます。

パッケージがインストールされると、Adobe Campaignv7ホームページは、v6.02の古いホームページ完成版で、v7の一般的な設定(青いホームページバナー)に置き換えられます。

![](assets/dashboards.png)

このホームページのリンク上にあるv7画面へのリンクは、リスト(**[!UICONTROL 操作リスト]**、**[!UICONTROL 操作]**&#x200B;の配信トラッキングなど)を除くすべてです。 v6.02の概要（webアプリケーション）へのリンク。

![](assets/dashboards2.png)

v6.02で設定した別の概要を追加する場合は、ダッシュボードからホームページにこの概要を追加する必要があります。 (**[!UICONTROL 管理/アクセス管理/ダッシュボード]**)。

>[!NOTE]
>
>変更を登録するには、必ずコンソールを切断してから再接続してください。

## Message Center {#message-center}

Message Centerコントロールインスタンスの移行後、トランザクションメッセージテンプレートが機能するように、再公開する必要があります。

v7では、実行インスタンスのトランザクションメッセージテンプレート名が変更されました。 現在は、作成元のコントロールインスタンスに対応する演算子名のプレフィックスが付けられます。例えば、**control1_template1_rt**（**control1**&#x200B;は演算子の名前）。 大量のテンプレートがある場合は、コントロールインスタンス上の古いテンプレートを削除することをお勧めします。
