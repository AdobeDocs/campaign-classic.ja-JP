---
title: 統合の設定
seo-title: 統合の設定
description: 統合の設定
seo-description: null
page-status-flag: never-activated
uuid: e2db7bdb-8630-497c-aacf-242734cc0a72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 1c20795d-748c-4f5d-b526-579b36666e8f
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0112d5bd052ad66169225073276d1da4f3c245d8
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 2%

---


# パイプラインの監視 {#pipeline-monitoring}

ステータス [!DNL pipelined] Webサービスは、プロセスのステータスに関する情報を提供し [!DNL pipelined] ます。

ブラウザーを使用して手動でアクセスするか、監視アプリケーションを使用して自動的にアクセスすることができます。

REST形式です。以下に説明します。

![](assets/triggers_8.png)

## 指標 {#indicators}

このセクションでは、ステータスWebサービスのインジケーターをリストします。

モニターに推奨されるインジケーターは強調表示されます。

* 消費者： トリガーを取り込むクライアントの名前。 パイプラインオプションで設定されます。
* http-request
   * last-alive-ms-ago: 接続チェックが行われてからの経過時間（ミリ秒）。
   * last-failed-cnx-ms-ago: 前回の接続チェック失敗からの経過時間（ミリ秒）。
   * pipeline-host: パイプラインデータの取り込み元のホストの名前。
* pointer
   * current-offsets: 子スレッドごとの、パイプラインへのポインタの値。
   * last-flush-ms-ago: 一括のトリガーが取得されてからの経過時間（ミリ秒）。
   * next-offsets-flush: 終了時に次のバッチまで待機する時間。
   * processed-since-last-flush: 最後のバッチで処理されたトリガーの数。
* ルーティング
   * トリガー： 取得したトリガーのリスト。 オプションで設定され [!DNL pipelined] ます。
* stats
   * average-pointer-flush-time-ms: 1バッチのトリガーの平均処理時間。
   * average-trigger-processing-time-ms: トリガーデータの解析に費やされた平均時間です。
   * bytes-read: プロセスの開始以降にキューから読み取られたバイト数。
   * current-messages: キューから取り出され、処理待ちの保留中メッセージの現在の数。 **このインジケーターはゼロに近い必要があります**。
   * current-再試行: 処理に失敗し、再試行を待機しているメッセージの現在の数です。
   * ピークメッセージ： プロセスの開始後に処理されている保留メッセージの最大数。
   * ポインタのフラッシュ： 開始以降に処理されたメッセージのバッチ数。
   * ルーティング-JS — カスタム： カスタムJSによって処理されたメッセージの数。
   * trigger-discarded: 処理エラーが原因で再試行が多すぎると破棄されたメッセージの数です。
   * trigger-processed: エラーなく処理されたメッセージの数。
   * trigger-received: キューから受信したメッセージの数。

これらの統計は、処理スレッドごとに表示されます。

* average-trigger-processing-time-ms: トリガーデータの解析に費やされた平均時間です。
* is-JS-processor: 値&quot;1&quot;を返します。
* trigger-discarded: 処理エラーが原因で再試行が多すぎると破棄されたメッセージの数です。 **このインジケーターはゼロにする必要があります**。
* trigger-failures: JSの処理エラーの数。 **このインジケーターはゼロにする必要があります**。
* trigger-received: キューから受信したメッセージの数。

* 設定： これらはconfigファイル内に設定されます。
   * flush-pointer-msg-count: バッチ内のメッセージ数。
   * flush-pointer-period-ms: 2つのバッチの間隔（ミリ秒）。
   * processing-threads-JS: カスタムJSを実行する処理スレッドの数。
   * retry-period-ms: 処理エラーが発生した場合の2つの再試行間の時間。
   * retry-validity-duration-ms: 時間処理から、メッセージが破棄されるまでの時間が再試行されます。
   * パイプラインメッセージレポート

## パイプラインメッセージレポート {#pipeline-report}

このレポートには、過去5日間の1時間あたりのメッセージ数が表示されます。

![](assets/triggers_9.png)
