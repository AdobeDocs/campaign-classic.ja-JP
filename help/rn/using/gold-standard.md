---
title: Gold Standard リリース
description: Gold Standard リリース
page-status-flag: never-activated
uuid: 269d590c-5a6d-40b9-a879-02f5033863fc
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rns
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 5df34f55-135a-4ea8-afc2-f9427ce5ae7b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: eccf0e9899426c2517748c7a72611ff098291cd2
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 100%

---


# Gold Standard リリース{#gold-standard}

Gold Standard のユーザーは、安定した最新バージョンを使用することで、自動的に Gold Standard のアップグレードのメリットが得られるため、操作は必要ありません。

オンプレミスおよびハイブリッドの顧客も、Gold Standard リリースのメリットを受けられます。

これは、長期サポートリリースです。古いビルドから移行する場合は、最初にこのバージョンにアップグレードすることをお勧めします。

このページには、Gold Standard のリリースがリストされています。

Gold Standard のアップグレードの詳細については、この[記事](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html)を参照してください。

## ![](assets/do-not-localize/green_2.png) Gold Standard 10 リリース{#gs-10}

_2020 年 7 月 7 日_

ビルド（9032@efd8a94）には、以下の修正が含まれています。

署名機能が無効な場合にトラッキングが機能しない問題を修正しました。（NEO-26411）

>[!CAUTION]
>
>クライアントコンソールをこのリリースに含まれるものにアップグレードすることをお勧めします。この[ページ](../../installation/using/installing-the-client-console.md)を参照してください。

## ![](assets/do-not-localize/red_2.png) Gold Standard 9 リリース{#gs-9}

_2020 年 6 月 22 日_

ビルド（9032@800be2e）には、以下の修正が含まれています。

* iOS HTTP2 コネクタが強化されました（サードパーティのアップデートおよびエラー管理）。（NEO-25904、NEO-25903、NEO-25799）

以下はトラッキングリンクのセキュリティメカニズムに関する修正です（[セキュリティとプライバシーのチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照）。

* 「通知クリック数」のトラッキングが機能しない問題を修正しました（iOS および Android のプッシュ通知）。（NEO-25965）
* 一部のレガシーバージョンの Outlook を使用する場合に、トラッキング URL を開いたりクリックしたりできない問題を修正しました。（NEO-25688）
* パーソナライゼーションパラメーター（シャープ記号の付いたアンカータグ）のフラグメントを使用した URL のトラッキングが機能しなかった問題を修正しました。（NEO-25774）
* フィッシング詐欺対策サービスの問題を修正しました。（NEO-25283）
* 特定のカスタムトラッキング式を使用する場合のトラッキングの問題を修正しました。（NEO-25277）


## ![](assets/do-not-localize/red_2.png) Gold Standard 8 リリース{#gs-8}

_2020 年 4 月 29 日_

ビルド（9032@3a9dc9c）には、以下の修正が含まれています。

* E メール内のリンクの追跡に関するセキュリティを改善。これは、あらゆる顧客に対してデフォルトで有効です。さらに、強化されたセキュリティ機能が利用できます。この機能はカスタマーケアにご連絡いただくと有効にできます。これを非ホスト型顧客が有効にするための手順と機能の詳細については、[セキュリティおよびプライバシーチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照してください。

>[!CAUTION]
>
>トラッキングリンクを使用したプッシュ通知、またはアンカータグを使用した配信で問題が発生した場合は、トラッキングリンク用の新しい署名メカニズムを無効にすることをお勧めします。手順について詳しくは、この[ページ](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照してください。

* LINE 配信に画像が表示されない可能性がある問題を修正しました。（NEO-23207）
* SFTP キーに基づく認証が Debian 9 で動作しない&#x200B;**ファイル転送**&#x200B;アクティビティの問題を修正しました。（NEO-23183）
* 高い頻度で送信されたときにプッシュ通知に影響を与える可能性がある問題を修正しました。（NEO-20516）
* Web サーバーのクラッシュを引き起こす可能性があるオファー応答管理の問題を修正しました。（NEO-19482）
* LibreOffice 管理で、レポートをエクスポートできなかったエラーを修正しました。（NEO-20982）
* 調査アクティビティを使用して多数のワークフローをアップグレードする場合にエラーが発生する問題を修正しました。
* .odt ファイルを含む E メールプレビューでエラーが発生しないように、LibreOffice の管理を改善しました。
* Apache 接続の管理を改善し、Web サービスでの待ち時間を回避しました。
* **バージョン情報**&#x200B;メニューでのバージョンタグ（7 桁）の表示を改善しました。
* リスト管理でオファーが公開されない問題を修正しました。
* クリーンアップワークフローがクラッシュする原因となる問題を修正しました。
* クリーンアップワークフローログの軽度の問題を修正しました。

## ![](assets/do-not-localize/orange_2.png) Gold Standard 6 リリース{#gs-6}

_2020 年 3 月 9 日_

ビルド（9032@19f73c5）には、以下の修正が含まれています。

* FTP over SSL を使用する外部アカウントの問題を修正しました。（NEO-20498）

## ![](assets/do-not-localize/orange_2.png) Gold Standard 5 リリース{#gs-5}

_2019 年 12 月 17 日_

ビルド（9032@d6b8062）には、以下の修正が含まれています。

* モバイル（SMS、MMS）、プッシュ（iOS、Android）およびソーシャルネットワーク（Facebook、Twitter）の各通信チャネルでのトラッキングの問題を修正しました。（NEO-19595）

## ![](assets/do-not-localize/orange_2.png) Gold Standard 4 リリース{#gs-4}

_2019 年 12 月 11 日_

ビルド（9032@bc4a935）には、以下の修正が含まれています。

* MSSQL データベースでメッセージを送信する際のパフォーマンスの問題を修正しました。（NEO-17558）

## ![](assets/do-not-localize/orange_2.png) Gold Standard 3 リリース{#gs-3}

_2019 年 11 月 20 日_

ビルド（9032@3468c7b）には、以下の修正が含まれています。

* IMS 認証を使用したログインの問題を修正しました。（NEO-17312）
* 複数の配信に関する累積レポートを表示する際の問題を修正しました。（NEO-18165）
* Web サーバーがブロックまたはクラッシュする可能性がある問題を修正しました。

## ![](assets/do-not-localize/red_2.png) Gold Standard 2 リリース{#gs-2}

_2019 年 9 月 19 日_

ビルド（9032@cee805c）には、以下の修正が含まれています。

* Salesforce 用 CRM コネクタを使用する際の問題を修正しました。（NEO-17712）
* トランザクションメッセージの送信時にパフォーマンスの問題を引き起こす可能性があるインデックスの問題を修正しました。

## ![](assets/do-not-localize/red_2.png) リリース 19.1.4 - ビルド 9032{#release-19-1-4-build-9032}

_2019 年 8 月 13 日_

初期の 19.1.4 ビルドには以下の修正が含まれています。

* スケジューラーアクティビティで、ウィザード設定時に望ましくないエラーメッセージが生成される問題を修正しました。NEO-11662 から、更新を元に戻します。（NEO-17097）
* テストアクティビティが 2 回実行された際にワークフローが停止する、NEO-12727 が原因の回帰を修正しました。（NEO-16835）
* 無効な、または期限切れのセッショントークンが API 呼び出しで使用されると、間違った HTTP コード（HTTP 403 Forbidden ではなく HTTP 200 OK）が返される問題を修正しました。（NEO-16826）
* DKIM キーが E メールに埋め込まれなくなった結果、配信品質が低下していた問題を修正しました。（NEO-16804）
* スケジューリングワークフローの様々な問題を修正しました。ワークフローは、スケジューラー設定を考慮することなく、1 日 1 回実行されるようにスケジュールされていました。（NEO-16619、NEO-16426）
