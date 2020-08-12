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
translation-type: ht
source-git-commit: 0112d5bd052ad66169225073276d1da4f3c245d8
workflow-type: ht
source-wordcount: '438'
ht-degree: 100%

---


# パイプラインの監視 {#pipeline-monitoring}

[!DNL pipelined] ステータス Web サービスは、[!DNL pipelined] プロセスのステータスに関する情報を提供します。

ブラウザーを使用して手動でアクセスするか、監視アプリケーションを使用して自動的にアクセスすることができます。

情報は REST 形式です（以下で説明します）。

![](assets/triggers_8.png)

## 指標 {#indicators}

この節では、ステータス Web サービスの指標を示します。

監視対象として推奨される指標はハイライト表示されています。

* consumer：トリガーを取り込むクライアントの名前。パイプラインオプションで設定されます。
* http-request
   * last-alive-ms-ago：接続が確認されてからの経過時間（ミリ秒）。
   * last-failed-cnx-ms-ago：前回接続が確認できなかった時からの経過時間（ミリ秒）。
   * pipeline-host：パイプラインデータの取り込み元のホストの名前。
* pointer
   * current-offsets：子スレッドごとの、パイプラインへのポインターの値。
   * last-flush-ms-ago：トリガーが一括取得されてからの経過時間（ミリ秒）。
   * next-offsets-flush：終了時に次のバッチまで待機する時間。
   * processed-since-last-flush：前回のバッチで処理されたトリガーの数。
* routing
   * triggers：取得したトリガーのリスト。[!DNL pipelined] オプションで設定されます。
* stats
   * average-pointer-flush-time-ms:1 バッチのトリガーの平均処理時間。
   * average-trigger-processing-time-ms：トリガーデータの解析に費やされた平均時間。
   * bytes-read：プロセスの開始以降にキューから読み取られたバイト数。
   * current-messages：キューから取り出されて処理待ちになっている保留中メッセージの現在の数。**この指標はゼロに近くなるようにしてください**。
   * current-retries：処理に失敗し再試行を待機しているメッセージの現在の数。
   * peak-messages：プロセスの開始以降に処理されてきた保留メッセージの最大数。
   * pointer-flushes：開始以降に処理されたメッセージのバッチ数。
   * routing-JS-custom：カスタム JS で処理されたメッセージの数。
   * trigger-discarded: 処理エラーが原因で再試行が多すぎるために破棄されたメッセージの数。
   * trigger-processed：エラーなく処理されたメッセージの数。
   * trigger-received：キューから受信したメッセージの数。

これらの統計情報は、処理スレッドごとに表示されます。

* average-trigger-processing-time-ms：トリガーデータの解析に費やされた平均時間。
* is-JS-processor：スレッドがカスタム JS を使用する場合は値「1」。
* trigger-discarded: 処理エラーが原因で再試行が多すぎるために破棄されたメッセージの数。**この指標はゼロになるようにしてください**。
* trigger-failures：JS の処理エラーの数。**この指標はゼロになるようにしてください**。
* trigger-received：キューから受信したメッセージの数。

* settings：これらは設定ファイルで指定されます。
   * flush-pointer-msg-count:：バッチ内のメッセージ数。
   * flush-pointer-period-ms：2 回のバッチ間の間隔（ミリ秒）。
   * processing-threads-JS：カスタム JS を実行する処理スレッドの数。
   * retry-period-ms：処理エラーが発生した場合の 2 回の再試行間の時間。
   * retry-validity-duration-ms：処理が再試行されてからメッセージが破棄されるまでの時間。
   * パイプラインメッセージレポート

## パイプラインメッセージレポート {#pipeline-report}

このレポートには、過去 5 日間の 1 時間あたりのメッセージ数が表示されます。

![](assets/triggers_9.png)
