---
solution: Campaign Classic
product: campaign
title: データのインポートとエクスポートの開始
description: Campaign Classicでのデータのインポートとエクスポートについての詳細。
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
translation-type: tm+mt
source-git-commit: 37cc6cd8b71ec82cd4e6a910d6664a51ed5c091e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 8%

---


# データのインポートとエクスポートの開始{#get-started-data-import-export}

Adobe Campaign Classicは、データの読み込みと書き出しを可能にするデータ管理機能を提供しています。 これらの操作は、ワークフローまたは汎用のインポートおよびエクスポートのいずれかを使用して実行できます。

>[!IMPORTANT]
>
>この機能を使用する際は、Adobe Campaign契約に従って、SFTPストレージ、データベースストレージ、およびアクティブなプロファイルの制限に留意してください。

## ワークフロー {#workflows}

<img src="assets/do-not-localize/icon_workflows.svg" width="60px">

**** ワークフローは、読み込みプロセスを自動化する便利な方法です。ローカルファイルまたはSFTPのどちらからデータをインポートする場合でも、データ管理手順を標準化できます。

ワークフローを使用すると、スケジュールに従ってインポート/エクスポート操作を自動的に繰り返し実行できます。例えば、複数の情報システム間でのデータ交換を自動化できます。

詳しくは、[こちらの節](../../platform/using/import-export-workflows.md)を参照してください。

## 一般的なインポートおよびエクスポート {#generic-import-export}

<img src="assets/do-not-localize/icon_templates.svg" width="60px">

また、Campaign Classicは、**一般的なインポートとエクスポート**&#x200B;を提供し、これにより、一時的なインポートまたはエクスポートジョブを作成できます。

インポートとエクスポートは専用のテンプレートで設定され、インポートとエクスポートのジョブを起動および監視するように設定および使用できます。

一般的なインポートとエクスポートの詳細については、[このセクション](../../platform/using/about-generic-imports-exports.md)を参照してください。

>[!IMPORTANT]
>一般的なインポートおよびエクスポートは、一部の操作にのみ使用します。 データの一貫性を確保し、効率を向上させるには、ワークフローを使用してインポートおよびエクスポート操作を実行することをお勧めします。

## データの暗号化と圧縮{#data-encryption-compression}

<img src="assets/do-not-localize/icon_encrypt.svg" width="60px">

Campaign Classicを使用すると、圧縮ファイルまたは暗号化ファイルを読み込んだり、圧縮ファイルまたは暗号化ファイルを書き出したりできます。

これらの操作は、活用するデータに前処理段階を適用することで、ワークフロー内で実行されます。

詳しくは、以下の節を参照してください。

* [ファイルの解凍または復号化](../../platform/using/unzip-decrypt.md)
* [ファイルの圧縮または暗号化](../../platform/using/zip-encrypt.md)

## ベストプラクティスとトラブルシューティング{#best-practices-troubleshooting}

<img src="assets/do-not-localize/icon_bestpractices.svg" width="60px">

インポートおよびエクスポート操作を実行する際は、[ベストプラクティス](../../platform/using/import-export-best-practices.md)のいくつかに従って、データベース内のデータの一貫性を確保し、更新またはエクスポート中のエラーの発生を防ぎます。

さらに、SFTPサーバーの使用に関する推奨事項と一般的な問題については、[このセクション](../../platform/using/sftp-server-usage.md)を参照してください。
