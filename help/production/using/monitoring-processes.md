---
product: campaign
title: プロセスの監視
description: Campaign プロセスの監視方法の詳細
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 1f5d8c7e-6f9b-46cd-a9b4-a3b48afb1794
source-git-commit: bd9f035db1cbad883e1f27fe901e34dfbc9c1229
workflow-type: tm+mt
source-wordcount: '3779'
ht-degree: 2%

---

# プロセスの監視{#monitoring-processes}

![](../../assets/v7-only.svg)

アプリケーションサーバーとリダイレクションサーバー（**トラッキング**）は、手動または自動で監視できます。

## 手動監視 {#manual-monitoring}

**[!UICONTROL 監視]** に移動し、「**[!UICONTROL 概要]**」リンクをクリックして、Adobe Campaignのプロセス監視ページを表示します。

![](assets/d_ncs_monitoring.png)

表示されるページで、接続されたインスタンスの状態を確認できます。例：

* インスタンスに関する情報：バージョン、名前、データベースエンジン、インストール済みパッケージ、サーバーシステムインジケーター、
* 見つからないプロセスと実行情報（開始日、PID など）のリスト
* ワークフローと配信のビュー。

様々なキャンペーンプロセスを監視するその他の方法については、[このページ](../../production/using/monitoring-guidelines.md)で説明しています。

### ログ {#log-journal}

プロセスに関連するログジャーナルを表示できます。 これをおこなうには、例えば **mta** というプロセスをクリックし、「**[!UICONTROL ログジャーナル]** を開く」をクリックします。

![](assets/d_ncs_monitoring2.png)

### システム指標 {#system-indicators}

システムインジケータのリストを使用すると、物理メモリや仮想メモリ、アクティブなプロセス、使用可能なディスク領域など、マシンに関する情報を表示できます。 インジケータは、Linux と Windows のオペレーティングシステムで異なります。 **[!UICONTROL インスタンスの監視]** ページに移動し、**[!UICONTROL 表示]** リンクをクリックして指標のリストを開きます

#### Windows {#in-windows}

* **[!UICONTROL 保留中のイベントがキューに入れられました]** :インジケーター ( **Message Center に特有 )**&#x200B;詳しくは、[この節](../../message-center/using/additional-configurations.md#monitoring-thresholds)を参照してください。

* **[!UICONTROL メモリ]** :物理メモリ (RAM) に関する情報。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :インストールされたメモリの合計容量。

   **[!UICONTROL 利用可能]** :使用可能なメモリの量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費が総量の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、メモリ消費が全量の 90%に達した場合に表示されます。

   **[!UICONTROL 警告]** および **[!UICONTROL アラート]** インジケーターが表示されたら、Adobe Campaignサーバーがインストールされているマシンに RAM を追加することで、問題を解決できます。 また、専用マシンにAdobe Campaignサーバーをインストールすることもできます。

* **[!UICONTROL スワップメモリ]** :ページングファイルに一致する仮想メモリに関する情報：Windows が RAM のように使用するハードディスク上の領域。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :メモリの合計容量。

   **[!UICONTROL 利用可能]** :使用可能なメモリの量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費が総量の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、メモリ消費が全量の 90%に達した場合に表示されます。

   **[!UICONTROL 警告]** および **[!UICONTROL 警告]** インジケーターが表示されたら、Windows の詳細設定で交換ファイルのサイズを大きくすることで、この問題を解決できます。

* **[!UICONTROL ディスク XXX]** :マシンリーダーに関する情報。

   **[!UICONTROL 現在の値]** :実際に使用されたディスク容量。

   **[!UICONTROL 最大値]** :ディスクの総容量。

   **[!UICONTROL 利用可能]** :空きディスク容量

   **[!UICONTROL 使用]** :使用ディスクの割合。

   **[!UICONTROL 警告]** :このインジケータは、使用可能なディスク領域が総容量の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、使用可能なディスク領域が総容量の 90%に達した場合に表示されます。

* **[!UICONTROL 古すぎるプロセスの数]** :1 日以上アクティブであったAdobe Campaignプロセスに関する情報です。

   **[!UICONTROL 現在の値]** :現在アクティブなプロセスの数。

   **[!UICONTROL 最大値]** :許可されたプロセスの最大数 (1)。

   **[!UICONTROL アラート]** :このインジケータは、プロセスの数が 1 の場合に表示されます。

   **[!UICONTROL Alert]** インジケータが表示された場合、該当するプロセスが SQL データベースエンジンによってロックされているか、無限ループに陥っている可能性があります。 Adobe Campaignが提供する **ウォッチドッグ** プロセスは、毎日すべてのプロセスを自動的に再起動し、この問題を解決できます。 ただし、関係するプロセスを自分で停止して、強制的に再起動することもできます。

#### Linux {#in-linux}

![](assets/production_system_indicators_linux_001.png)

* **[!UICONTROL 保留中のイベントがキューに入れられました]** :インジケーター ( **Message Center に特有 )**&#x200B;詳しくは、[この節](../../message-center/using/additional-configurations.md#monitoring-thresholds)を参照してください。

* **[!UICONTROL 負荷平均 (1/5/15分 )]** :負荷に関する情報、すなわち、最後の 1 分、5 分、15 分間にマシン上で実行されたプロセスによるプロセッサの使用率

   **[!UICONTROL 現在の値]** :装置の実際の負荷。

   **[!UICONTROL 最大値]** :マシン上のプロセスの最大使用負荷

   **[!UICONTROL 警告]** :この指標は、最後の 1 分、5 分または 15 分で、負荷が最大許可値の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケーターは、最後の分、5 分または 15 分の最大許可値の 90%に負荷が到達した場合に表示されます。

* **[!UICONTROL メモリ]** :物理メモリ (RAM) に関する情報。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :インストールされたメモリの合計容量。

   **[!UICONTROL 利用可能]** :使用可能なメモリの量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費が総量の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、メモリ消費が全量の 90%に達した場合に表示されます。

   **[!UICONTROL 警告]** および **[!UICONTROL アラート]** インジケーターが表示されたら、Adobe Campaignサーバーがインストールされているマシンに RAM を追加することで、問題を解決できます。 また、専用マシンにAdobe Campaignサーバーをインストールすることもできます。

* **[!UICONTROL スワップメモリ]** :ページングファイルに一致する仮想メモリに関する情報：Windows が RAM のように使用するハードディスク上の領域。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :メモリの合計容量。

   **[!UICONTROL 利用可能]** :使用可能なメモリの量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費が総量の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、メモリ消費が全量の 90%に達した場合に表示されます。

   **[!UICONTROL 警告]** および **[!UICONTROL 警告]** インジケーターが表示されたら、交換ファイルのサイズを大きくすることで、この問題を解決できます。

* **[!UICONTROL コアファイル]** :Adobe Campaignプロセスのクラッシュ後に生成されるファイルに関する情報です。これらのファイルを使用して、クラッシュの原因を診断できます。

   **[!UICONTROL 現在の値]** :既存のファイルの数。

   **[!UICONTROL 最大値]** :許可されたファイルの最大数 (1)。

   **[!UICONTROL 警告]** :このインジケータは、ファイル数が 1 に近づくと表示されます。

   **[!UICONTROL アラート]** :このインジケータは、ファイル数が 1 の場合に表示されます。

   クラッシュが原因でプロセスが見つからない場合は、プロセスのリストに赤で表示され、Adobe Campaignが提供する **ウォッチドッグ** プロセスによって自動的に再起動されます。

* **[!UICONTROL 共有メモリセグメントの数]** :すべてのAdobe Campaignプロセスで共有されるメモリセグメントに関する情報。

   **[!UICONTROL 現在の値]** :現在使用中のメモリセグメントの数。

   **[!UICONTROL 最大値]** :許可されるメモリセグメントの最大数 (2)。

   **[!UICONTROL 警告]** :このインジケータは、メモリセグメントの数が 1 に達すると表示されます。

   **[!UICONTROL アラート]** :このインジケータは、メモリセグメントの数が 2 に達した場合に表示されます。

* **[!UICONTROL 古すぎるプロセスの数]** :1 日以上アクティブなプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなプロセスの数。

   **[!UICONTROL 最大値]** :許可されたプロセスの最大数。

   **[!UICONTROL 警告]** :このインジケータは、プロセス数が許可されたしきい値の 80%に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、プロセス数が許可されたしきい値の 90%に達した場合に表示されます。

* **[!UICONTROL ファイルハンドル]** :ファイル記述子に関する情報（プロセスごとに開かれたファイルの数）。

   **[!UICONTROL 現在の値]** :ファイル記述子の現在の数。

   **[!UICONTROL 最大値]** :オペレーティングシステムによって許可されるファイル記述子の最大数。

   **[!UICONTROL 警告]** :このインジケータは、許可されたファイル記述子の数が 80%しきい値に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、許可されたファイル記述子の数が 90%しきい値に達した場合に表示されます。

* **[!UICONTROL プロセス]** :マシンプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなプロセスの数。

   **[!UICONTROL 最大値]** :許可されたプロセスの最大数。

   **[!UICONTROL アクティブなプロセス]** :アクティブなプロセスの数。

   **[!UICONTROL 非アクティブなプロセス]** :非アクティブなプロセスの数。

   **[!UICONTROL 警告]** :このインジケータは、許可されたプロセスの数が 80%しきい値に達した場合に表示されます。

   **[!UICONTROL アラート]** :このインジケータは、許可されたプロセスの数が 90%しきい値に達した場合に表示されます。

* **[!UICONTROL ゾンビプロセス]** :停止したが、まだプロセス識別子 (PID) を持ち、プロセステーブルに表示され続けているプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなゾンビプロセスの数。

   **[!UICONTROL 最大値]** :認証ゾンビプロセスの最大数 (2)

   **[!UICONTROL 警告]** :このインジケータは、ゾンビプロセスの数が 2 に近づくと表示されます。

   **** このインジケータは、ゾンビプロセスの数が 2 に達したときに表示されます。

#### カスタマイズされた指標 {#customized-indicators}

Adobe Campaignでは、指標をカスタマイズできます。 手順は次のとおりです。

1. **.sh** ファイルを作成し、 **[!UICONTROL cust_indicators.sh]** という名前を付けます。
1. カスタマイズした指標をこのファイルに追加します。 例：

   ```
   #!/bin/bash 
   echo "<indicator name='Zombie Processes'>  
   <current label='Current Value' value='0' display=''/>  
   <warning value='2'/>  <alert value='2'/>  
   <max label='Max Value' value='2'/>
   </indicator>"
   ```

   または

   ```
   #!/bin/bash 
   echo "<indicator name='Availability'>  
   <current label='Last update of data' display='2012-09-03 10:00'/>  
   <current label='Availability last month' display='100.00%'/>  
   <current label='Availability this month' display='100.00%'/> 
   <current label='Recent downtime periods' display='2012-07-04 11:10:00 - 11:19:59'/>
   </indicator>"
   ```

1. ファイルを **[!UICONTROL usr/local/neolane/nl6]** フォルダーに配置します。

このファイルはAdobe Campaignによって呼び出されます。

## SMTP レポート {#smtp-reports}

SMTP 配信監視レポートは、Adobe Campaignプラットフォームに統合されています。 アクセスするには、コンソールまたは Web アクセスを使用します。

これらのレポートには、ドメインごとに SMTP 配信統計と SMTP エラーが表示されます。

これらにアクセスするには、オペレーターに管理者権限が必要です。

これらは **Monitoring** > &#39;SMTP Monitoring&#39;の下にグループ化されています。

![](assets/smtp_reports_access.png)

>[!IMPORTANT]
>
>* SMTP 監視に関する情報は、E メールチャネルがアクティブ化されている場合にのみ使用できます。
>* **[!UICONTROL SMTP 送信統計]** は、統計サーバーがインスタンスで起動された場合にのみ提供されます。

>


### SMTP 送信統計 {#smtp-sending-statistics}

**[!UICONTROL SMTP sending statistics]** レポートを使用して、サーバーのアクティビティを制御できます。 各 mtachilds の合成が表示されます。

![](assets/smtp_stats_report.png)

このレポートの指標のリストがグラフの下に表示されます。

1. 送信されたメッセージの合計数。
1. 
   * 青い線：Shaper に到着したメッセージ（SMTP を送信する前の最後のステージ）を送信する準備が整いました（受信データと一致します）。

   * 緑の線：メッセージが正常に送信されました（送信データと一致）。

   * 赤い線：Shaper によって破棄されたメッセージが **mta** に返されます（この回復で拒否されたデータと一致します）。

   これらの値は、1 時間あたりのメッセージ数で表されます。

1. Shaper の 2 つのキューを表します。

   * 青い曲線：アクティブなメッセージのキュー。 これらのメッセージは、できるだけ早く送信されます。

   * カキ曲線：&#39;deferred&#39;キュー ジョブ数の制限や、ターゲットへの接続が利用できないため、現時点ではこのメッセージを返せません。 再試行は、5 秒、10 秒、20 秒、40 秒、2 分ごとにおこなわれます。 を返します。****

1. このグラフは、破棄されたメッセージの詳細を示します（2 番目のグラフの赤い曲線）。再試行なしで破棄されたメッセージ（マウス）と、送信に失敗したメッセージ（赤）の割合を示します。 これにより、統計サーバの制限（スロットリング）またはリモート・サーバの使用不可に起因して、許可された期間内に処理されなかったメッセージの割合を表示できます。
1. SMTP 接続が既にオープンしているか、現在オープン中です。
1. **mtachild** の数の推定値。

>[!NOTE]
>
>このレポートは、E メールトラフィックシェイパーコンポーネントのステータスに関連しています。

### 各ドメインの SMTP エラー {#smtp-errors-per-domain}

このレポートでは、設定された期間にわたって、ドメイン別に分類された配信エラーを表示できます。

>[!NOTE]
>
>**serverConf.xml** ファイルの **minConnectionsToLog**、**minErrorsToLog** および **minMessagesToLog** オプションは、接続統計を考慮する上記のしきい値を定義します。

![](assets/smtp_error_report.png)

このレポートの指標のリストを次の表に示します。

* **ドメイン** 列には、メッセージが送信されるドメインの名前（または yahoo.fr の実際のドメイン名、yahoo.com など）が含まれます。
* **Cnx** 列には、このドメインで開いている SMTP 接続の数が表示されます。
* **Sent** 列は、このドメインに送信されたメッセージの数に対応します。
* **Volume** 列には、このドメインに送信しようとしたメッセージの量（概算値）が表示されます。
* **エラー** 列には、このドメインで発生したエラーのボリュームインジケーターが期間中に表示されます。
* **最後の応答** 列には、このドメインに対して最後に受信した SMTP 応答メッセージが表示されます。
* **Date** 列には、このドメインで最後に受信した SMTP 応答の日付が表示されます。

>[!NOTE]
>
>**Cnx**、**送信済み**、**ボリューム** の各列に表示される値は、「**[!UICONTROL 期間]**」フィールドで選択した期間に基づいて計算されます。

ドメイン名をクリックして、エラーを表示します。

公開 ID 別に分類されます。この識別子は、ルータの背後にある複数のAdobe Campaign mta が共有する IP アドレスに対応します。 統計サーバは、この識別子を用いて、この開始点とターゲットサーバとの間の接続および配信統計を記憶する。

![](assets/smtp_error_report_details.png)

「**[!UICONTROL ドメインの所有者]**」フィールドを使用すると、様々なドメイン名を同じラベルでグループ化できます。 最初のレポート表示では、すべての MX ドメイン名がこの所有者に関連付けられます。

詳細を表示するには、PublicId 識別子をクリックします。

![](assets/smtp_error_report_subdetails.png)

>[!NOTE]
>
>エラーの割合は、2 つのグラフで表されます。 1 つ目は、黒い背景の横のプログレスバーです。 2 番目の図は時系列です。 選択した期間は 12 個の時間間隔に分けられ、それぞれが垂直方向の進行状況バーで表されます。 両方の表現で、エラーが検出されなかった場合、バーは黒です。 バーの色は、発生したエラーの割合（黄、オレンジ、最後に赤）によって異なります。 カラーグレーは、重要なデータ量が見つからないことを意味します。 グラフにカーソルを置くと、エラーの正確な割合を表示できます。

>[!NOTE]
>
>SMTP エラーとAdobe Campaignでの管理について詳しくは、[ この節 ](../../installation/using/email-deliverability.md) を参照してください。

## 請求レポート {#billing-report}

**[!UICONTROL 請求]** テクニカルワークフローは、システムアクティビティレポートを「請求」オペレーターに電子メールで送信します。 デフォルトで、マーケティングインスタンスで毎月 25 日にトリガーされます。

テクニカルワークフローは、次のノードのサブフォルダーにあります。**管理** > **プロダクション** > **テクニカルワークフロー**

![](assets/billing.png)

ワークフローが毎月 25 日に開始されると、請求オペレーターのインボックスに次のレポートが表示されます。

![](assets/billing_2.png)

次の指標を使用して配信をトラッキングできます。

* **[!UICONTROL 開始日]** :配信の開始日。レポートの「開始日」より前に設定することもできます。
* **[!UICONTROL ラベル]** :配信のラベル。送信するメッセージが 100 件未満の配信は小さすぎると見なされ、開始日別に集計されます。この場合、ラベルには集計数が表示されます ( 例：[3 つの小さな配信の集計 ]。
* **[!UICONTROL 総ボリューム]** :配信用に転送された合計バイト数。
* **[!UICONTROL 平均ボリューム]** :転送されたバイトの平均ボリューム。これは、**[!UICONTROL 乗数]** 指標の計算基礎となる数式 **（合計ボリューム/メッセージ数）** の結果です。
* **[!UICONTROL メッセージ]** :送信されたメッセージの数。これには、正常に送信されたメッセージと、（接続されたサーバーからバウンスメッセージを受信した後の）再試行の両方が含まれます。
* **[!UICONTROL 乗数 (x)]** :乗数の値は、メッセージの平均ボリュームから推定されます。
* **[!UICONTROL カウント]** :メッセージと乗数の乗算の結果。

## 自動監視 {#automatic-monitoring}

Adobe Campaignには、以下に示す自動監視方法がいくつか用意されています。

### コマンドライン {#command-line}

コマンド

**nlserver モニター**

Adobe Campaignモジュールおよびシステムに関する一連の指標をリストできます。

処理が容易な XML 形式で出力が生成されます。

このコマンドは、**-missing** パラメーターを使用して実行することもできます。このパラメーターは、設定ファイルが実行する必要があると判断した場合に、このインスタンスに存在しないプロセスをリストします。

```
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
mta@prod
stat@prod
wfserver@prod
```

### サーバーによって公開された情報 {#information-published-by-the-server}

#### /r/test {#r-test}

**http(s)://`<application>`/r/test** ページは、リダイレクションサーバーのテストに使用されます。 この同じ方法を使用して、追跡に使用するフロントルサーバーをテストすることをお勧めします。 このページは、読み込みディスパッチャーをテストする場合にも使用できます。

次のような行が XML 形式で表示されます。

```
<redir status='OK' date='YYYY-MM-DD HH:MM:SS.112Z' build='XXXX' host='<hostname>' localHost='<servername>'/>
```

**頻度**:このテストは負荷を使用しないので、非常に頻繁に（例えば、1 秒に 1 回）実行できます。

#### /nl/jsp/ping.jsp {#nl-jsp-ping-jsp}

この **http(s)://`<Application server url>`/nl/jsp/ping.jsp** ページは、対応するネットワークと同じように動作します。apache/tomcat/web module/database を通じて完全なクエリをテストし、クライアントにアップロードします。 すべてが正常に動作している場合は、「OK」が返されます。 このテストは、データベース（mta や調査など）にアクセスできるマシンで実行することをお勧めします。

**使用方法**:リモートでログインするには、オペレーターのログインに関連付けられたセッショントークンを引数として渡す必要があります (  [Adobe Campaignスクリプトを使用した自動監視](#automatic-monitoring-via-adobe-campaign-scripts)のヒントを参照 )。

例：

![](assets/ncs_monitoring_ping.png)

オペレーター名とログインは、事前にAdobe Campaignクライアントコンソールでデータベース権限を持つように設定しておく必要があります。

![](assets/ncs_operators_rights_01.png)

**頻度**:これは、帯域幅をほとんど使用しないテストです。したがって、1 分に 1 回以上実行することはできませんが、かなり頻繁に実行できます。

#### /nl/jsp/monitor.jsp {#nl-jsp-monitor-jsp}

これは、オペレーターが Web ページを介してAdobe Campaignサーバーにアクセスできるかどうかを確認するテストです。クライアントコンソールのメニューからアクセスしたのと同じ web ページ このページは監視ツール（Tivoli、Nagios など）から呼び出すことができます。

![](assets/ncs_monitoring_web.png)

**使用方法**:インスタンスに接続できるオペレーターログインに関連付けられたセッショントークンは、引数として使用する必要があります (  [Adobe Campaignスクリプトを使用した自動監視](#automatic-monitoring-via-adobe-campaign-scripts)のヒントを参照 )。

オペレーターとそのログインは、以前にAdobe Campaignクライアントコンソールで設定しておく必要があります。この設定には、適切なデータベース権限と制限が必要です。

**頻度**:これは完全なサーバーテストであり、頻繁に実行する必要はありません（例えば 10 分に 1 回実行できます）。

#### /nl/jsp/soaprouter.jsp {#nl-jsp-soaprouter-jsp}

この **jsp** は、Adobe Campaignアプリケーション API のエントリポイントを表します。 したがって、アプリケーションの詳細な監視を提供できます。 また、Adobe Campaign Web サービスの監視にも使用できます。 監視スクリプトで使用されますが、電源ユーザー専用です。

### デプロイメントタイプに基づく監視 {#monitoring-based-on-deployment-types}

Adobe Campaignは様々なデプロイメント設定を有効にします（詳しくは、[ この節 ](../../installation/using/hosting-models.md) を参照）。 この節では、インストールのタイプに応じて適用する様々な自動監視手法について説明します。

<table> 
 <thead> 
  <tr> 
   <th> デプロイメントタイプ </th> 
   <th> 監視 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> スタンドアロン </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/r/</span> testand  <span class="uicontrol">/nl/jsp/monitor.</span> jspon Adobe Campaignサーバ</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 標準 </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/r/</span> testand  <span class="uicontrol">/nl/jsp/ping.</span> jspon フロントサーバー</p> </li> 
     <li><p> <span class="uicontrol">/nl/jsp/monitor.</span> jspon アプリケーションサーバー</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> エンタープライズ </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/r/</span> testand  <span class="uicontrol">/nl/jsp/ping.</span> jspon フロントサーバー</p> </li> 
     <li><p> <span class="uicontrol">/r/</span> testand  <span class="uicontrol">/nl/jsp/monitor.</span> jspon アプリケーションサーバー</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシング </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/nl/jsp/monitor.</span> jspon アプリケーションサーバー</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Campaignスクリプトを使用した自動監視 {#automatic-monitoring-via-adobe-campaign-scripts}

Adobe Campaignは、検出された異常値に関するレポートを E メールで送信できるインスタンス監視ツール（インスタンス監視ツール）を提供できます。

![](assets/pro_netreport.png)

>[!IMPORTANT]
>
>このツールは、インスタンスの監視に使用できますが、Adobe Campaignではサポートされていません。 詳しくは、Campaign 管理者にお問い合わせください。

### 必須要素 {#required-elements}

自動監視を行うには、次の事前インストールの注意事項が必要です。

* **netreport.tgz** （Linux のインストール）または **netreport.zip** （Windows のインストール）ファイルが必要です。
* 監視対象のマシンに監視をインストールしないことを強くお勧めします。
* JRE または JDK を使用しているマシンにインストールする必要があります。
* Linux では、監視対象のマシンに **bc** パッケージが必要です。 詳しくは、[この節](../../installation/using/installing-packages-with-linux.md#distribution-based-on-rpm--packages)を参照してください。

### インストール手順 {#installation-procedure}

インストール手順は次のとおりです。

1. コンソールで、必要に応じて新しいオペレーターを作成します（「監視」ユーザーは既に存在します）が、権限は割り当てません。
1. アーカイブ抽出を実行します。
1. **readme** ファイルを読みます。
1. **netconf.xml** 設定ファイルを更新します。
1. **netreport.bat**(Windows) または **netreport.sh**(Linux) ファイルを更新します。

### netconf.xml ファイルの設定 {#configuring-the-netconf-xml-file}

XML 設定ファイルには、次の要素が含まれています。

* [「Properties」要素](#properties--element)
* [「Instance」要素](#instance--element)
* [「ホスト」要素](#host--element)
* [サブ要素](#sub-elements)

次に設定例を示します。

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<netconf>
  <properties mailServer="mail.adobe.net" mailFrom="mail@adobe.com" recipientList="recipient@adobe.com">
    <nightMode start="00:00 am" end="07:00 am"/>
    <buildRange minimum="7829" maximum="8180"/>
    <buildRange minimum="8300" maximum="8400"/>
    <sla/>
  </properties>

  <instance name="dev" recipientList="mail@mail.com,mail2@mail.com">
                <host name="devrd.domain.com" alias="devrd" sessiontoken="monitoring" criticalLevel="1" filter="wkf;new">
                                <ncs instance="devrd" url="/nl/jsp/soaprouter.jsp" includeDead="false" isSecure="false"/>
                                <redir url="/r/test"/>
                                <http url="/nl/jsp/ping.jsp"/>
                </host>
                <host name="devtrk.domain.com" alias="devtrk" sessiontoken="monitoring" criticalLevel="0" filter="wkf;new">
                                <ncs instance="devrd" url="/nl/jsp/soaprouter.jsp" includeDead="true" isSecure="false"/>
                </host>
  </instance>
  <host name="dev-test" alias="dev-test" sessiontoken="monitoring" criticalLevel="2">
                <ncs instance="dev" url="/nl/jsp/soaprouter.jsp" includeDead="false"/>
  </host>
</netconf>
```

>[!NOTE]
>
>**netconf.xml** ファイルにサフィックスを追加して、様々な設定を指定できます。例えば、**netconf-dev.xml**、**netconf-prod.xml** などです。 次に、**$JAVA_HOME/bin/java netreport dev** または **@%JAVA_HOME%binnetreport&lt;a7/a7 を追加して、** netreport.bat **または** netreport.sh **ファイルで netreport の実行に使用する設定を指定します。/> 例：**

>[!IMPORTANT]
>
>**モニタリング** オペレーターが動作するには、ネットポートを実行するマシンが **sessionTokenOnly** モードのセキュリティゾーンに属している必要があります。 このオペレーターに信頼できる IP マスクが指定されていない場合は、セキュリティゾーンも **allowEmptyPassword** モードと **allowUserPassword** モードにする必要があります。

#### 「Properties」要素 {#properties--element}

この要素は、E メールの設定 (

* **mailServer**:E メールの送信に使用する SMTP サーバー ( 例：smtp.domain.net など ) に置き換えます。
* **mailFrom**:レポート送信者の電子メールアドレス ( 例：monitoring@domain.net) です。
* **recipientList**:受信者を監視する電子メールアドレスのリスト。アドレスはコンマで区切る必要があります（スペースは使用できません）。
* 「**night**」モード（オプション）は、指定した期間の間に E メールが送信されるのを防ぐために使用します。 代わりに、データが統合され、夜間のアクティビティに関する E メールが終了時間（デフォルトでは 7:00）の後に送信されます。
* **buildRange** サブ要素（オプション）を使用して、ビルドの最小数と最大数を指定できます。 ビルド番号がこの範囲に含まれないすべてのマシンに対してエラーが発生します

   ```
   <buildRange minimum="0000" maximum="9999"/>
   ```

* **`<sla>`**（オプション）サブ要素を **properties** 要素に追加できます。 インポートが実行されるたびに、ログファイルが生成されます。 ファイルの名前には、設定名と日時 ( 例：**dev_06_12_13_16_47_05.tmp**) が含まれます。 このファイルには次の情報が含まれます。インスタンス名、マシン名、重大度レベル、（0 ～ 3、最も重要でない状態から）、日付（タイムスタンプ形式）、クエリと応答の間の経過時間（ミリ秒）、使用されるサービス (http、ncs、ncsex、redir)。 この情報は、各サービスの最後に、タブマークと改行で区切られます。

>[!NOTE]
>
>**`<property>`** 要素の値が「true」の **persistHtmlFile** 属性を使用して、最新の監視ステータスをファイル **netreport.md** に記録します。 このファイルはインストールディレクトリに保存されます。

#### 「Instance」要素 {#instance--element}

この要素を使用すると、複数のマシン（ホスト）を同じインスタンスに再グループ化できます。 インスタンス名は、監視 E メールの最初の部分に表示されます。 インスタンスの名前をクリックして、各マシンに関する詳細にアクセスできます。

```
instance name="instanceName" recipientList="mail@mail.com,mail2@mail.com">
                <host name="devcamp.domain.com" ...>
                       ...
                </host>
                <host name="devtrack.domain.com" ...>
                       ...
                </host>
</instance
```

* **名前**:E メールの最初の部分に表示されるインスタンス名。
* **recipientList** （オプション）:では、特定のインスタンスに関する監視レポートを E メールで送信できます。

#### 「ホスト」要素 {#host--element}

この要素は、ホスト上の特定のサーバーの監視を設定します。

* **名前**:監視対象のマシンの名前。
* **エイリアス** （オプション）:レポートに表示される監視対象マシンの名前。
* **sessionToken**:は、認証済みセッショントークンを介したログイン認証を提供します。

   セッショントークンを設定するには、Adobe Campaignコンソールで **monitoring** 演算子を選択します。 「**アクセス権**」タブで、このインスタンスを監視する権限を持つマシンの IP アドレスを指定します。 その後、**モニタリング** 識別子を使用して、パスワードを指定する必要なく、これらのマシンからモニタリングページに接続できます。

   ![](assets/ncs_operators_rights_02.png)

* **criticalLevel** （オプション）:では、エラーを重大度のレベルで並べ替えることができます。指定できる値は、「0」（表示されるすべてのレベル）、「1」（高いエラーと重大なエラーのみ）、「2」（重大なエラーのみ表示される）です。 この属性を指定しない場合は、すべてのエラーレベルが表示されます。
* **filter** （オプション）:を使用すると、 **filter=&quot;wkf;wkf1&quot;**&#x200B;など、特定のワークフローエラーを除外できます。ワークフローラベルはセミコロンで区切る必要があります。

#### サブ要素 {#sub-elements}

* **tcp**:サーバーが起動しているかどうかを確認します。ポート番号を入力してください。
* **http**:Web サーバーが存在するかどうかを確認します（アプリケーションサーバーが動作している）。
* **ncs**:「インスタンス」属性に入力されたインスタンスのプロセス（ワークフローエラー、メモリ使用量など）を確認します。**included** （必須）属性は、デッドプロセス（&#39;true&#39;または&#39;false&#39;値）を表示するオプションを提供します。
* **redir**:トラッキングを確認します。

ほとんどの場合、**ncs** と **redir** サブ要素のみを保持できます。

いずれの場合でも、サブ要素で特定のノードがオーバーロードできます（例えば、ノード **port=75** は、http、ncs、redir 接続に使用するポートをオーバーロードします）。

```
<ncs instance="clap40" url="/nl/jsp/soaprouter.jsp" includeDead="false" port="80"/>
```

**ncs**、**redir** および **http** サブ要素で、**isSecure** 属性（オプション）を追加して、https プロトコルを使用するかどうかを選択できます（「true」または「false」値）。 この属性を指定しない場合は、http プロトコルが使用されます。

### netreport.bat または netreport.sh ファイルの設定 {#configuring-the-netreport-bat-or-netreport-sh--file}

設定するには、このファイルを編集し、JRE または JDK がインストールされているディレクトリを指定します。

### 監視の開始 {#launching-monitoring}

監視を開始するには、スクリプトを使用して、**netreport.bat** または **netreport.sh** ファイルを一定の間隔で実行します。 レポートは、最初の実行後に送信され、次にステータスが変更された場合にのみ送信されます。

### 監視のテスト {#testing-monitoring}

監視をテストするには、**netreport.bat** または **netreport.sh** ファイルを実行します。

**netconf.xml** ファイルの **recipientList** で指定された受信者に電子メールが送信されます。
