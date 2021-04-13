---
solution: Campaign Classic
product: campaign
title: キャンペーンからAdobe Experience Platformへのデータのエクスポート
description: Campaign ClassicからAdobe Experience Platformにデータをエクスポートする方法を説明します。
audience: integrations
content-type: reference
translation-type: tm+mt
source-git-commit: 1c07c3b10a6d38ca67c20746a51301d71aec0015
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# キャンペーンからAdobe Experience Platformへのデータのエクスポート{#sources}

Campaign ClassicデータをAdobeリアルタイムCustomer Data Platform (RTCDP)にエクスポートするには、まず、Campaign Classicでワークフローを構築して、共有するデータをS3またはAzure BLOBストレージの場所にエクスポートする必要があります。

ワークフローが構成され、ストレージの場所にデータが送信されたら、S3またはAzure BLOBストレージの場所をAdobeエクスペリエンスプラットフォームの&#x200B;**Source**&#x200B;として接続する必要があります。

>[!NOTE]
>
>キャンペーン生成データのみ（送信、開く、クリック数など）をエクスポートすることをお勧めします。 Adobe Experience Platformに サードパーティのソース（CRMなど）から取り込まれたデータは、Adobe Experience Platformに直接読み込む必要があります。

## Campaign Classicでの書き出しワークフローの作成

Campaign ClassicからS3またはAzure Blobストレージの場所にデータをエクスポートするには、エクスポートするデータをターゲットするワークフローを構築し、ストレージの場所に送信する必要があります。

これを行うには、以下を追加して設定します。

* ターゲットデータをCSVファイルに抽出する&#x200B;**[!UICONTROL データ抽出（ファイル）]**&#x200B;アクティビティ。 このアクティビティの設定方法について詳しくは、[この](../../workflow/using/extraction--file-.md)セクションを参照してください。

   ![](assets/rtcdp-extract-file.png)

* CSVファイルをストレージの場所に転送する&#x200B;**[!UICONTROL ファイル転送]**&#x200B;アクティビティ。 このアクティビティの設定方法について詳しくは、[この](../../workflow/using/file-transfer.md)セクションを参照してください。

   ![](assets/rtcdp-file-transfer.png)

例えば、以下のワークフローでは、ログを定期的にCSVファイルに抽出し、そのファイルをストレージーの場所に転送します。

![](assets/aep-export.png)

## ストレージの場所をソースとして接続する

S3またはAzure BLOBストレージの場所をAdobeエクスペリエンスプラットフォームの&#x200B;**ソース**&#x200B;として接続する主な手順を以下に示します。 これらの各手順に関する詳細は、[ソースコネクタドキュメント](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html)を参照してください。

1. Adobe Experience Platform **[!UICONTROL ソース]**&#x200B;メニューで、ストレージの場所への接続を作成します。

   * [AmazonS3ソース接続の作成](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/cloud-storage/s3.html)
   * [Azure BLOBコネクタ](https://experienceleague.adobe.com/docs/experience-platform/sources/connectors/cloud-storage/blob.html)

   >[!NOTE]
   >
   >ストレージの場所は、AmazonS3、パスワード付きSFTP、SSHキー付きSFTP、またはAzure Blob接続です。 Adobe Campaignにデータを送信する推奨される方法は、AmazonS3またはAzure Blobを使用する方法です：

   ![](assets/rtcdp-connector.png)

1. クラウドストレージのバッチ接続のデータフローを設定します。 データフローとは、ストレージの場所からAdobe Experience Platformデータセットにデータを取得し、取り込むスケジュール設定されたタスクです。 この手順では、データ選択、CSVフィールドのXDMスキーマへのマッピングなど、ストレージの場所からのデータインジェストを設定できます。

   詳細な情報は、[このページ](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/cloud-storage.html)にあります。

   ![](assets/rtcdp-map-xdm.png)

1. ソースの設定が完了すると、Adobe Experience Platformは指定したストレージーの場所からファイルをインポートします。

   この操作は、必要に応じてスケジュールできます。 インスタンスに既に存在する負荷に応じて、1日に最大6回エクスポートを実行することをお勧めします。
