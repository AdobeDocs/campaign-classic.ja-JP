---
title: スキーマの再生成
seo-title: スキーマの再生成
description: スキーマの再生成
seo-description: null
page-status-flag: never-activated
uuid: 455c37f1-cbaf-4503-b2e9-5eec7fad6e97
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: editing-schemas
discoiquuid: 0f7c835e-b429-422b-87ae-1234c7dd8fe6
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e7ff12260d875b85256c8678fa8d100fd355398e

---


# スキーマの再生成{#regenerating-schemas}

スキーマを変更して変更を保存すると、拡張スキーマが自動的に生成されます。 ただし、変更を適用するには、スキーマを手動で再生成する必要がある場合があります。 手順は次のとおりです。

1. 再生成する必要のあるスキーマを選択します。
1. 右クリックし、を選択しま **[!UICONTROL Actions > Regenerate selected schemas...]** す。
1. をクリック **[!UICONTROL OK]** して、プロセスを確定し、起動します。

生成されたスキーマの構造は、「プレビュー」タブと「ドキュメント」タブで確認できます。 For more on this, refer to the [Principles](../../configuration/using/data-schemas.md#principles) section.

>[!NOTE]
>
>例えば、逆リンクの依存関係の問題を解決するために、すべてのスキーマを強制的に再生成する必要がある場合は、Adobe Campaignアプリケーションサーバーから次のコマンドを起動できます。

>**nlserver config -postupgrade -instance:`&lt;インスタンス名>&#39; -force**

>その後、Adobe Campaignアプリケーションサーバーを再起動し、クライアントコンソールから切断/再接続する必要があります。

