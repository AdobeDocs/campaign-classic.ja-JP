---
solution: Campaign Classic
product: campaign
title: データのインポートとエクスポートの基礎知識
description: Campaign Classic でのデータのインポートとエクスポートについて詳しく説明します。
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
translation-type: ht
source-git-commit: 37cc6cd8b71ec82cd4e6a910d6664a51ed5c091e
workflow-type: ht
source-wordcount: '325'
ht-degree: 100%

---


# データのインポートとエクスポートの基礎知識 {#get-started-data-import-export}

Adobe Campaign Classic は、データのインポートとエクスポートを可能にするデータ管理機能を備えています。 これらの操作は、ワークフローまたは一般的なインポートおよびエクスポートのいずれかを使用して実行できます。

>[!IMPORTANT]
>
>この機能を使用する際は、Adobe Campaign の契約条件が定める SFTP ストレージ、データベースストレージ、アクティブプロファイルの制限に注意してください。

## ワークフロー {#workflows}

<img src="assets/do-not-localize/icon_workflows.svg" width="60px">

**ワークフロー**&#x200B;は、インポートプロセスを自動化する便利な方法です。データをローカルファイルからインポートするか、SFTP からインポートするかに関係なく、データ管理手順を標準化することができます。

ワークフローを使用すると、例えば複数の情報システム間のデータ交換を自動化するために、インポートとエクスポートの操作をスケジュールに従って自動的に繰り返すことができます。

詳しくは、[こちらの節](../../platform/using/import-export-workflows.md)を参照してください。

## 一般的なインポートおよびエクスポート {#generic-import-export}

<img src="assets/do-not-localize/icon_templates.svg" width="60px">

また、Campaign Classic には、不定期のインポート／エクスポートジョブを作成できる&#x200B;**一般的なインポートおよびエクスポート**&#x200B;が用意されています。

インポートとエクスポートは、インポートおよびエクスポートジョブを起動および監視するように設定および使用できる専用のテンプレートで設定されます。

一般的なインポートおよびエクスポートの詳細については、[こちらの節](../../platform/using/about-generic-imports-exports.md)を参照してください。

>[!IMPORTANT]
>一般的なインポートおよびエクスポートは、不定期の操作にのみ使用します。データの一貫性を確保し効率を向上させるには、ワークフローを使用してインポートおよびエクスポート操作を実行することをお勧めします。

## データの暗号化と圧縮 {#data-encryption-compression}

<img src="assets/do-not-localize/icon_encrypt.svg" width="60px">

Campaign Classic では、圧縮ファイルまたは暗号化ファイルのインポートやエクスポートが可能です。

これらの操作は、活用するデータに前処理段階を適用することで、ワークフロー内で実行されます。

詳しくは、以下の節を参照してください。

* [ファイルの解凍または復号化](../../platform/using/unzip-decrypt.md)
* [ファイルの圧縮または暗号化](../../platform/using/zip-encrypt.md)

## ベストプラクティスとトラブルシューティング {#best-practices-troubleshooting}

<img src="assets/do-not-localize/icon_bestpractices.svg" width="60px">

インポートおよびエクスポート操作を実行する際は、いくつかの[ベストプラクティス](../../platform/using/import-export-best-practices.md)に従って、データベース内のデータの一貫性を確保し、更新またはエクスポート時の一般的なエラーの発生を防いでください。

さらに、SFTP サーバーの使用に関する推奨事項と一般的な問題については、[こちらの節](../../platform/using/sftp-server-usage.md)を参照してください。
