---
product: campaign
title: ファイルの解凍または復号化
description: 処理を行う前に Campaign でファイルを展開または復号化する方法について説明します
feature: Workflows, Encryption
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
exl-id: 1a79da3b-2abc-4bfc-a0ee-8471c478638d
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: ht
source-wordcount: '733'
ht-degree: 100%

---


# ファイルの解凍または復号化 {#unzipping-or-decrypting-a-file-before-processing}

Adobe Campaign では、圧縮されたファイルや暗号化されたファイルをインポートできます。[データ読み込み（ファイル）](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/data-loading-file.html?lang=ja){target="_blank"}アクティビティで読み取る前にファイルを解凍または復号化する前処理を定義できます。

>[!IMPORTANT]
>
>4 Gb を超える圧縮されたファイルは解凍できません。

手順は以下のとおりです。

1. ファイルの復号化を可能にするために、[コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/gpg-keys-management.html?lang=ja#decrypting-data)を使用して公開鍵と秘密鍵のペアを生成します。

   >[!NOTE]
   >
   >コントロールパネルは、すべての管理者ユーザーがアクセスできます。 ユーザーに管理者アクセス権を付与する手順については、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html?lang=ja#discover-control-panel)で詳しく説明しています。
   >
   >インスタンスは AWS でホストされ、[最新の GA ビルド](../../rn/using/rn-overview.md)でアップグレードされている必要があります。バージョンを確認する方法については、[この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照してください。インスタンスが AWS でホストされているかどうかを確認するには、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/faq.html?lang=ja)に記載されている手順に従います。

1. Adobe Campaign のインストールがオンプレミスの場合：使用するユーティリティ（例：GPG、GZIP）およびアプリケーションサーバー上の必要なキー（暗号化キー）をインストールします。

   インストールした Adobe Campaign がアドビでホストされている場合は、必要なユーティリティをサーバーにインストールするよう[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に依頼します。

次に、目的の前処理コマンドをワークフローで使用します。

1. ワークフローに「**[!UICONTROL ファイル転送]**」アクティビティを追加して設定します。
1. 「**[!UICONTROL データ読み込み（ファイル）]**」アクティビティを追加し、ファイルのフォーマットを定義します。
1. 「**[!UICONTROL ファイルを前処理]**」オプションをオンにします。
1. 適用する前処理コマンドを選択します。
1. ファイルから取得したデータを管理するために必要なその他のアクティビティを追加します。
1. 保存して、ワークフローを実行します。

例として、次のユースケースを示します。

**関連トピック：**

* [データの読み込み（ファイル）アクティビティ](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/data-loading-file.html?lang=ja){target="_blank"}.
* [ファイルを圧縮または暗号化します](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/extraction-file.html?lang=ja){target="_blank"}。

## ユースケース：コントロールパネルで生成されたキーを使用して暗号化されたデータのインポート {#use-case-gpg-decrypt}

このユースケースでは、外部システムで暗号化されたデータを コントロールパネルで生成されたキーを使用してインポートするためのワークフローを作成します。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](#video)

このユースケースを実行する手順は次のとおりです。

1. コントロールパネルを使用して、キーペア（公開鍵と秘密鍵）を生成します。詳細な手順については、[コントロールパネルのドキュメント](https://experienceleague.adobe.com/docs/control-panel/using/instances-settings/gpg-keys-management.html?lang=ja#decrypting-data)を参照してください。

   * 公開鍵は外部システムと共有され、外部システムはこのキーを使用して Campaign に送信するデータを暗号化します。
   * 秘密鍵は、受信する暗号化されたデータを復号化するために Campaign Classic で使用されます。

   ![](assets/gpg_generate.png)

1. 外部システムでは、コントロールパネルからダウンロードした公開鍵を使用して、Campaign Classic にインポートするデータを暗号化します。

1. Campaign Classic で、暗号化されたデータをインポートするワークフローを作成し、コントロールパネル経由でインストールされた秘密鍵を使用して復号化します。これをおこなうには、次のようにワークフローを作成します。

   ![](assets/gpg_import_workflow.png)

   * **[!UICONTROL ファイル転送]**&#x200B;アクティビティ：ファイルを外部ソースから Campaign Classic に転送します。この例では、SFTP サーバーからファイルを転送します。
   * **[!UICONTROL データ読み込み（ファイル）]**&#x200B;アクティビティ：ファイルからデータベースにデータを読み込み、コントロールパネルで生成された秘密鍵を使用して復号化します。

1. **[!UICONTROL ファイル転送]**&#x200B;アクティビティを開き、暗号化された .gpg ファイルのインポート元の外部アカウントを指定します。

   ![](assets/gpg_key_transfer.png)

   アクティビティの設定方法に関するグローバルな概念について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/event-activities/file-transfer.html?lang=ja){target="_blank"}を参照してください。


1. **[!UICONTROL データ読み込み（ファイル）]**&#x200B;アクティビティを開き、必要に応じて設定します。アクティビティの設定方法に関するグローバルな概念について詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/action-activities/data-loading-file.html?lang=ja){target="_blank"}を参照してください。

   アクティビティに前処理ステージを追加して、受信データを復号化します。これを行うには、「**[!UICONTROL ファイルを前処理]**」オプションを選択してから、「**[!UICONTROL コマンド]**」ドロップダウンリストから「**[!UICONTROL 復号]**」を選択します。

   ![](assets/gpg_load.png)

   >[!NOTE]
   >
   >利用可能なコマンドを変更する必要がある場合は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に問い合わせて、preProcessCommand の設定を調整できます。
   >
   >ハイブリッドデプロイメントを使用している場合は、サーバー設定ファイル（serverConf.xml）から直接これらのコマンドを設定できます。[詳しくは、サーバー設定ファイルで前処理コマンドを設定する方法を参照してください](../../installation/using/the-server-configuration-file.md#preprocesscommand)。

1. 「**[!UICONTROL OK]**」をクリックして、アクティビティの設定を確定します。

1. これで、ワークフローを開始できます。ワークフローを実行したら、復号化が実行されたことと、ファイルのデータがインポートされたことをワークフローログで確認できます。

   ![](assets/gpg_run.png)

## チュートリアルビデオ {#video}

このビデオでは、GPG キーを使用してデータを復号化する方法を紹介します。

>[!VIDEO](https://video.tv.adobe.com/v/41360?captions=jpn&quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
