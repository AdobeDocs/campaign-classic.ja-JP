---
title: プロセスの監視
seo-title: プロセスの監視
description: プロセスの監視
seo-description: null
page-status-flag: never-activated
uuid: 9dc1461f-5e95-454d-8df5-19baab85f184
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: 968d0ee3-5efc-46d8-b408-b9cce3e730c4
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 954018e1016fc924064bd795066f80704499f6a7

---


# プロセスの監視{#monitoring-processes}

アプリケーションサーバーとリダイレクトサーバー(ト&#x200B;**ラッキング**)は、手動または自動で監視できます。

## 手動監視 {#manual-monitoring}

に移動し、リ **[!UICONTROL Monitoring]** ンクをクリック **[!UICONTROL Overview]** して、Adobe Campaignプロセスの監視ページを表示します。

![](assets/d_ncs_monitoring.png)

表示されるページでは、接続されたインスタンスの状態を表示できます。例：

* インスタンスの情報：バージョン，名前，データベースエンジン，インストール済みパッケージ，サーバーシステムインジケーター，
* 見つからないプロセスと実行情報（開始日、PIDなど）のリスト、
* ワークフローと配信のビュー。

様々なキャンペーンプロセスを監視するその他の方法については、このページ [を参照しま](https://helpx.adobe.com/campaign/kb/acc-maintenance.html)す。

### ログ {#log-journal}

プロセスに関連するログジャーナルを表示することが可能です。 これを行うには、プロセスをクリックし、例え **ば** 「mta」をクリックして、をクリックしま **[!UICONTROL Open the log journal]** す。

![](assets/d_ncs_monitoring2.png)

### システム指標 {#system-indicators}

システムインジケータのリストを使用すると、物理メモリや仮想メモリ、アクティブなプロセス、使用可能なディスク領域など、マシンに関する情報を表示できます。 インジケータは、LinuxとWindowsのオペレーティングシステムで異なります。 ページに移動し、 **[!UICONTROL Instance Monitoring]** リンクをクリックし **[!UICONTROL Display]** てインジケーターのリストを開きます

#### Windowsの場合 {#in-windows}

* **[!UICONTROL Pending events queued]** :message Centerに固有のイ **ンジケータ**。 詳しくは、[この節](../../message-center/using/monitoring-thresholds.md)を参照してください。
* **[!UICONTROL Memory]** :物理メモリ(RAM)に関する情報。

   **[!UICONTROL Current value]** :実際のメモリ消費量。

   **[!UICONTROL Max Value]** :インストールされたメモリの合計容量。

   **[!UICONTROL Available]** :使用可能なメモリ量。

   **[!UICONTROL Warning]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   とのインジケ **[!UICONTROL Warning]** ータ **[!UICONTROL Alert]** ーが表示されたら、Adobe CampaignサーバーがインストールされているマシンにRAMを追加することで、この問題を解決できます。 また、専用のマシンにAdobe Campaignサーバーをインストールすることもできます。

* **[!UICONTROL Swap Memory]** :ページングファイルに一致する仮想メモリに関連する情報：ハードディスク上で、RAMのように使用される領域。

   **[!UICONTROL Current value]** :実際のメモリ消費量。

   **[!UICONTROL Max Value]** :合計メモリ量。

   **[!UICONTROL Available]** :使用可能なメモリ量。

   **[!UICONTROL Warning]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   インジケータ **[!UICONTROL Warning]** とが表 **[!UICONTROL Alert]** 示されている場合は、Windowsの詳細設定で交換ファイルのサイズを大きくすることで、この問題を解決できます。

* **[!UICONTROL Disk XXX]** :マシンリーダーに関する情報です。

   **[!UICONTROL Current value]** :実際に使用されるディスク容量。

   **[!UICONTROL Max Value]** :合計ディスク容量。

   **[!UICONTROL Available]** :空きディスク容量

   **[!UICONTROL Used]** :使用ディスクの割合。

   **[!UICONTROL Warning]** :このインジケータは、使用可能なディスク領域が合計容量の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケータは、使用可能なディスク領域が合計容量の90%に達した場合に表示されます。

* **[!UICONTROL Number of processes too old]** :1日以上アクティブだったAdobe Campaignプロセスに関する情報です。

   **[!UICONTROL Current value]** :現在アクティブなプロセスの数。

   **[!UICONTROL Max Value]** :許可されたプロセスの最大数(1)。

   **[!UICONTROL Alert]** :このインジケーターは、プロセスの数が1に等しい場合に表示されます。

   インジケータ **[!UICONTROL Alert]** が表示されるときは、該当するプロセスがSQLデータベースエンジンによってロックされているか、無限ループで停止している可能性があります。 Adobe Campaignが **提供するウォッチドッグプロセスは** 、毎日すべてのプロセスを自動的に再開し、この問題を解決できます。 ただし、関連するプロセスを自分で停止して、再起動を強制することもできます。

#### Linuxの場合 {#in-linux}

![](assets/production_system_indicators_linux_001.png)

* **[!UICONTROL Pending events queued]** :message Centerに固有のイ **ンジケータ**。 詳しくは、[この節](../../message-center/using/monitoring-thresholds.md)を参照してください。
* **[!UICONTROL Load average (1/5/15 minutes)]** :負荷に関する情報、すなわち、マシン上で最後の1分、5分、15分間に実行されているプロセスによるプロセッサの使用率

   **[!UICONTROL Current value]** :装置の実際の負荷。

   **[!UICONTROL Max value]** :マシン上のプロセスの最大使用負荷

   **[!UICONTROL Warning]** :このインジケーターは、最後の1分、5分または15分間に、負荷が許可された最大値の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケーターは、負荷が最後の1分、5分または15分の最大許可値の90%に達した場合に表示されます。

* **[!UICONTROL Memory]** :物理メモリ(RAM)に関する情報。

   **[!UICONTROL Current value]** :実際のメモリ消費量。

   **[!UICONTROL Max Value]** :インストールされたメモリの合計容量。

   **[!UICONTROL Available]** :使用可能なメモリ量。

   **[!UICONTROL Warning]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   とのインジケ **[!UICONTROL Warning]** ータ **[!UICONTROL Alert]** ーが表示されたら、Adobe CampaignサーバーがインストールされているマシンにRAMを追加することで、この問題を解決できます。 また、専用のマシンにAdobe Campaignサーバーをインストールすることもできます。

* **[!UICONTROL Swap Memory]** :ページングファイルに一致する仮想メモリに関連する情報：ハードディスク上で、RAMのように使用される領域。

   **[!UICONTROL Current value]** :実際のメモリ消費量。

   **[!UICONTROL Max Value]** :合計メモリ量。

   **[!UICONTROL Available]** :使用可能なメモリ量。

   **[!UICONTROL Warning]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   とのインジケ **[!UICONTROL Warning]** ータ **[!UICONTROL Alert]** ーが表示されたら、交換ファイルのサイズを増やすことでこの問題を解決できます。

* **[!UICONTROL Core Files]** :adobe Campaignプロセスのクラッシュ後に生成されるファイルに関する情報です。 これらのファイルを使用して、クラッシュの原因を診断できます。

   **[!UICONTROL Current Value]** :既存のファイルの数。

   **[!UICONTROL Max Value]** :許可されたファイルの最大数(1)。

   **[!UICONTROL Warning]** :このインジケータは、ファイル数が1に近づくと表示されます。

   **[!UICONTROL Alert]** :このインジケーターは、ファイル数が1に等しい場合に表示されます。

   クラッシュによってプロセスが見つからない場合は、プロセスのリストに赤色で表示され、Adobe Campaignが提供するウォッチドッグ **プ** ロセスによって自動的に再開されます。

* **[!UICONTROL Number of shared memory segments]** :すべてのAdobe Campaignプロセスで共有されるメモリセグメントに関する情報です。

   **[!UICONTROL Current value]** :現在使用中のメモリセグメントの数。

   **[!UICONTROL Max Value]** :許可されたメモリセグメントの最大数(2)。

   **[!UICONTROL Warning]** :このインジケーターは、メモリセグメント数が1に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケーターは、メモリセグメント数が2に達した場合に表示されます。

* **[!UICONTROL Number of processes too old]** :1日以上アクティブなプロセスに関する情報。

   **[!UICONTROL Current value]** :現在アクティブなプロセスの数。

   **[!UICONTROL Max Value]** :許可されたプロセスの最大数。

   **[!UICONTROL Warning]** :このインジケーターは、プロセスの数が許可されたしきい値の80%に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケーターは、プロセスの数が許可されたしきい値の90%に達した場合に表示されます。

* **[!UICONTROL File Handles]** :ファイル記述子に関する情報、つまり、プロセスごとに開かれたファイルの数。

   **[!UICONTROL Current value]** :ファイル記述子の現在の数。

   **[!UICONTROL Max Value]** :オペレーティングシステムによって許可されたファイル記述子の最大数。

   **[!UICONTROL Warning]** :このインジケータは、許可されたファイル記述子の数が80%のしきい値に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケータは、許可されたファイル記述子の数が90%のしきい値に達した場合に表示されます。

* **[!UICONTROL Processes]** :マシンプロセスに関する情報。

   **[!UICONTROL Current value]** :現在アクティブなプロセスの数。

   **[!UICONTROL Max Value]** :許可されたプロセスの最大数。

   **[!UICONTROL Active Processes]** :アクティブなプロセスの数。

   **[!UICONTROL Inactive Processes]** :非アクティブなプロセスの数。

   **[!UICONTROL Warning]** :このインジケーターは、許可されたプロセスの数が80%のしきい値に達した場合に表示されます。

   **[!UICONTROL Alert]** :このインジケーターは、許可されたプロセスの数が90%のしきい値に達した場合に表示されます。

* **[!UICONTROL Zombie Processes]** :停止したが、プロセス識別子(PID)を持ち、プロセステーブルに表示されたままのプロセスに関する情報。

   **[!UICONTROL Current value]** :現在アクティブなゾンビプロセスの数。

   **[!UICONTROL Max Value]** :認証ゾンビプロセスの最大数(2)

   **[!UICONTROL Warning]** :このインジケータは、ゾンビプロセスの数が2に近づくと表示されます。

   **[!UICONTROL Alert]** このインジケータは、ゾンビプロセスの数が2に達したときに表示されます。

#### カスタマイズされた指標 {#customized-indicators}

Adobe Campaignでは、インジケーターをカスタマイズできます。 手順は次のとおりです。

1. .shファイル **を作成し** 、名前を付けま **[!UICONTROL cust_indicators.sh]** す。
1. カスタマイズしたインジケーターをこのファイルに追加します。 次に例を示します。

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

1. ファイルをフォルダーに配置 **[!UICONTROL usr/local/neolane/nl6]** します。

このファイルはAdobe Campaignによって呼び出されます。

## SMTP Reports {#smtp-reports}

SMTP配信監視レポートは、Adobe Campaignプラットフォームに統合されています。 コンソールからアクセスすることも、Webアクセスを使用してアクセスすることもできます。

これらのレポートには、SMTP配信統計とSMTPエラーがドメイン別に表示されます。

これらのユーザーにアクセスするには、オペレーターに管理権限が必要です。

これらは、「 **Monitoring** 」>「SMTP Monitoring」の下にグループ化されます。

![](assets/smtp_reports_access.png)

>[!CAUTION]
>
>* SMTP監視に関する情報は、電子メールチャネルがアクティブ化されている場合にのみ利用できます。
>* は、統計 **[!UICONTROL SMTP sending statistics]** サーバがインスタンス上で起動されている場合にのみ提供されます。
>



### SMTP 送信統計 {#smtp-sending-statistics}

このレポー **[!UICONTROL SMTP sending statistics]** トを使用して、サーバーのアクティビティを制御できます。 これは、各マチルドの合成を表示します。

![](assets/smtp_stats_report.png)

このレポートの指標のリストがグラフの下に表示されます。

1. 送信されたメッセージの合計数。
1. 
   * 青の線：送信する準備が整ったメッセージ、つまりSMTPを送信する前の最後のステージ（受信データと一致）。

   * 緑の線：メッセージは正常に送信されました（送信データと一致）。

   * 赤線：Shaperによって破棄されたメッセージがmtaに返 **され** （この回復で拒否されたデータと一致）。
   これらの値は、1時間あたりのメッセージ数で表されます。

1. Shaperの2つのキューを表します。

   * 青のカーブ：アクティブなメッセージのキュー。 これらのメッセージはできるだけ早く送信されます。

   * カキ曲線：「延期」キュー。 ジョブ数が制限されているか、ターゲットへの接続が利用できないため、このメッセージはしばらく返されません。 再試行は、5秒、10秒、20秒、40秒、2分ごとなどに行われます。 を返しま **す** 。

1. 次のグラフは、破棄されたメッセージの詳細を示します（2番目のグラフの赤い曲線）。再試行なしで破棄されたメッセージ(mauve)と、送信に失敗したメッセージ(red)の割合が表示されます。 これにより、統計サーバの制限（ジョブ数の制限）またはリモートサーバの利用不能により、許可された期間内に処理されなかったメッセージの割合を表示できます。
1. SMTP 接続が既にオープンしているか、現在オープン中です。
1. mtachildの推定数 **です**。

>[!NOTE]
>
>このレポートは、電子メールトラフィックシェーパコンポーネントのステータスに関連しています。

### 各ドメインの SMTP エラー {#smtp-errors-per-domain}

このレポートでは、配信エラーを一定期間、ドメイン別に分類して表示できます。

>[!NOTE]
>
>**** serverConf.xmlファイルの **minConnectionsToLog、** minErrorsToLog **、****** minMessagesToLogの各オプションでは、接続統計値を上記の値に設定し、上記の値を考慮します。

![](assets/smtp_error_report.png)

このレポートのインジケーターのリストを次の表に示します。

* 「 **Domain** 」列には、メッセージの送信先のドメインの名前（例えば、yahoo.comの場合は実際のドメイン名、yahoo.com）が含まれます。
* 「 **Cnx** 」列には、このドメインで開いているSMTP接続の数、
* 「送 **信済み** 」列は、このドメインに送信されるメッセージの数に対応し、
* 「 **Volume** 」列には、このドメインに送信しようとしたメッセージの量（概算値）、
* 「エ **ラー** 」列には、期間中のこのドメインのエラーのボリュームインジケーターが表示されます。
* 「 **Last response** 」列には、このドメインに対して受信した最後のSMTP応答メッセージ、
* 「日 **付** 」列には、このドメインに対して最後に受信したSMTP応答の日付が表示されます。

>[!NOTE]
>
>「 **Cnx**」、「 **Sent**」、「 **Volume** 」の各列に表示される値は、フィールドで選択した期間を基準に計算さ **[!UICONTROL Period]** れます。

エラーを表示するには、ドメイン名をクリックします。

PublicId別に分類されます。この識別子は、ルーターの背後にある複数のAdobe Campaignで共有されるIPアドレスに対応します。 統計サーバは、この識別子を用いて、この始点と対象サーバとの間の接続と配信の統計を記憶する。

![](assets/smtp_error_report_details.png)

このフィ **[!UICONTROL Owner of domain]** ールドを使用すると、様々なドメイン名を同じラベルにグループ化できます。 最初のレポートビューでは、すべてのMXドメイン名がこの所有者に関連付けられます。

詳細を表示するには、PublicId識別子をクリックします。

![](assets/smtp_error_report_subdetails.png)

>[!NOTE]
>
>エラーの割合は2つのグラフで表されます。 1つ目は、黒の背景の水平プログレスバーです。 第2図は年代順。 選択した期間は12の時間間隔に分割され、それぞれが垂直プログレスバーで表されます。 両方の表現で、エラーが検出されなかった場合、バーは黒です。 バーの色は、発生したエラーの割合（黄色、オレンジ、最後に赤）によって異なります。 カラーグレーは、重要なデータ量が見つからないことを意味します。 グラフ上にカーソルを置くと、エラーの正確な割合を表示できます。

>[!NOTE]
>
>SMTPエラーとAdobe Campaignでの管理について詳しくは、この節を参照し [てください](../../installation/using/email-deliverability.md)。

## 請求レポート {#billing-report}

The **[!UICONTROL Billing]** technical workflow sends the system activity report to the &#39;billing&#39; operator by email. デフォルトでは、毎月25日にトリガーされます。

技術ワークフローは、次のノードのサブフォルダーにあります。管理 **/** 実稼働 **/技** 術ワークフロー ****。

![](assets/billing.png)

ワークフローが月の25日に開始されると、請求先担当者の受信トレイに次のレポートが表示されます。

![](assets/billing_2.png)

配信を追跡するには、次の指標を使用できます。

* **[!UICONTROL Start date]** :配信の開始日。 レポートの「開始日」より前に設定することもできます。
* **[!UICONTROL Label]** :配信のラベル。 送信するメッセージが100件未満の配信は、小さすぎると見なされ、開始日別に集計されます。この場合、ラベルには集計数が表示されます(例： [Aggregation of 3 small delivery])。
* **[!UICONTROL Total volume]** :配信用に転送された合計バイト数。
* **[!UICONTROL Avg volume]** :転送された平均バイト数。 これは、指標の計算基準である次 **の数式（合計ボリューム/メッセージ）**&#x200B;の結果 **[!UICONTROL Multiplier]** です。
* **[!UICONTROL Messages]** :送信されたメッセージの数。 これには、正常に送信されたメッセージと再試行されたメッセージの両方が含まれます（接続したサーバーからバウンスメッセージを受信した後）。
* **[!UICONTROL Multiplier (x)]** :乗数の値は、メッセージの平均ボリュームから推定されます。
* **[!UICONTROL Count]** :メッセージと乗数の乗算の結果。

## 自動監視 {#automatic-monitoring}

Adobe Campaignには、以下に示す自動監視方法がいくつか用意されています。

### コマンドライン {#command-line}

コマンド

**nlserverモニタ**

Adobe Campaignモジュールとシステムに関する一連の指標を一覧表示できます。

簡単に処理できるXML形式で出力が生成されます。

このコマンドは **-missing** パラメーターを使用して実行することもできます。このパラメーターは、設定ファイルで実行する必要があると指定された場合に、このインスタンスに存在しないプロセスをリストします。

```
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
mta@prod
stat@prod
wfserver@prod
```

### サーバーが発行した情報 {#information-published-by-the-server}

#### /r/test {#r-test}

リダ **イレクトサーバーのテストには、`<application>`http(s)://** /r/testページが使用されます。 追跡に使用するフロントサーバーをテストする場合も、同じ方法を使用することをお勧めします。 このページは、読み込みディスパッチャーのテストにも使用できます。

XML形式で次のような行が表示されます。

```
<redir status='OK' date='YYYY-MM-DD HH:MM:SS.112Z' build='XXXX' host='<hostname>' localHost='<servername>'/>
```

**頻度**:このテストは負荷を使用しないので、非常に頻繁に実行できます（例：毎秒1回）。

#### /nl/jsp/ping.jsp {#nl-jsp-ping-jsp}

この **http(s)://`<Application server url>`/nl/jsp/ping.jsp** ページは、ネットワークに対応するページと同じように動作します。apache/tomcat/web module/databaseを通じて完全なクエリーをテストし、クライアントにアップロードします。 すべてが正常に動作している場合は、「OK」を返します。 データベース（mtaや調査など）にアクセスできるマシン上でこのテストを実行することをお勧めします。

**使用状況**:リモートでログインするには、演算子のログインに関連付けられたセッショントークンを引数として渡す必要があります(Adobe Campaignスクリプトを使用した自動監視 [のヒントを参照](#automatic-monitoring-via-adobe-campaign-scripts))。

次に例を示します。

![](assets/ncs_monitoring_ping.png)

オペレーター名とログインは、Adobe Campaignクライアントコンソールで事前にデータベース権限を持つように設定する必要があります。

![](assets/ncs_operators_rights_01.png)

**頻度**:これは、帯域幅をほとんど使用しないテストです。 したがって、1分に1回しか実行できないにもかかわらず、かなり頻繁に実行できます。

#### /nl/jsp/monitor.jsp {#nl-jsp-monitor-jsp}

これは、オペレーターがWebページを介してAdobe Campaignサーバーにアクセスできるかどうかを確認するテストです。クライアントコンソールメニューからアクセスしたのと同じWebページ。 このページは、監視ツール（Tivoli、Nagiosなど）から呼び出すことができます。

![](assets/ncs_monitoring_web.png)

**使用状況**:インスタンスに接続できる演算子ログインに関連付けられたセッショントークンは、引数として使用する必要があります(Adobe Campaignスクリプトを使用した自動監視 [のヒントを参照](#automatic-monitoring-via-adobe-campaign-scripts))。

オペレーターとそのログインは、Adobe Campaignクライアントコンソールで、適切なデータベース権限と制限を持つように事前に設定する必要があります。

**頻度**:これは完全なサーバーテストであり、頻繁に実行する必要はありません（例えば、10分に1回実行できます）。

#### /nl/jsp/soaprouter.jsp {#nl-jsp-soaprouter-jsp}

この **jspは** 、Adobe CampaignアプリケーションAPIのエントリポイントを表します。 したがって、アプリケーションの詳細な監視を提供できます。 また、Adobe Campaign webサービスの監視にも使用できます。 監視スクリプトで使用されますが、電源ユーザーのみが対象です。

### 展開の種類に基づく監視 {#monitoring-based-on-deployment-types}

Adobe Campaignを使用すると、様々なデプロイメント設定を有効にできます(詳しくは、この節 [を参照](../../installation/using/hosting-models.md))。 このセクションでは、インストールのタイプに応じて適用される様々な自動監視手法について説明します。

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
     <li><p> <span class="uicontrol">/nl/jsp/monitor.jsp Campaignサーバーでの</span> /r/test <span class="uicontrol"></span> and </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> 標準 </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/r/test</span> and <span class="uicontrol">/nl/jsp/ping.jsp</span> on the front servers</p> </li> 
     <li><p> <span class="uicontrol">/nl/jsp/monitor.jsp</span> on the application server</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> エンタープライズ </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/r/test</span> and <span class="uicontrol">/nl/jsp/ping.jsp</span> on the front servers</p> </li> 
     <li><p> <span class="uicontrol">/r/test</span> and <span class="uicontrol">/nl/jsp/monitor.jsp</span> on the application server</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td> ミッドソーシング </td> 
   <td> 
    <ul> 
     <li><p> <span class="uicontrol">/nl/jsp/monitor.jsp</span> on the application server</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Adobe Campaignスクリプトによる自動監視 {#automatic-monitoring-via-adobe-campaign-scripts}

Adobe Campaignは、検出された異常値に関するレポートを電子メールで送信できるインスタンス監視ツール（インターポート）を提供します。

![](assets/pro_netreport.png)

>[!CAUTION]
>
>このツールはインスタンスの監視に使用できますが、Adobe Campaignではサポートされていません。 詳しくは、キャンペーン管理者にお問い合わせください。

### 必須要素 {#required-elements}

自動監視には、次の事前インストールに関する注意が必要です。

* **netreport.tgz **（Linuxのインストール）またはnetreport.zip **** （Windowsのインストール）ファイルが必要です。
* 監視対象のマシンに監視機能をインストールしないことを強くお勧めします。
* JREまたはJDKを使用するマシンにインストールする必要があります。
* linuxでは、監視対象のマシンに **bc** packageが必要です。 詳しくは、[この節](../../installation/using/installing-packages-with-linux.md#distribution-based-on-rpm--packages)を参照してください。

### インストール手順 {#installation-procedure}

インストール手順は次のとおりです。

1. コンソールで、必要に応じて新しい演算子を作成します（「monitoring」ユーザーが既に存在します）が、権限は割り当てません。
1. アーカイブの抽出を実行します。
1. お読みくだ **さい** 。
1. netconf.xml設 **定ファイルを更新し** ます。
1. netreport.bat **** (Windows)または**netreport.sh **(Linux)ファイルを更新します。

### netconf.xmlファイルの設定 {#configuring-the-netconf-xml-file}

XML設定ファイルには、次の要素が含まれます。

* [&#39;Properties&#39;要素](#properties--element)
* [&#39;Instance&#39;要素](#instance--element)
* [&#39;Host&#39;要素](#host--element)
* [サブ要素](#sub-elements)

設定例を次に示します。

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
>様々な設定を指定するには、 **netconf-dev.xml** 、 **netconf-prod.xml******&#x200B;など、netconf.dev.xmlファイルにサフィックスを追加します。 次に、 **$JAVA_HOME/bin/** java netreport devを追加して、 **netreport.batまたは** netreport.sh **ファイル内のnetreportの実行に使用する設定を指定します。例えば、** $JAVA_HOME/bin/java netreport devを、 **** @%JAVA_HOME%binportバインport prodサンプル用に追加します。

>[!CAUTION]
>
>監視演算子 **が動作するには** 、ネットワークを実行するマシンが、sessionTokenOnlyモードのセキュリティゾーンに存在する必要が **あります** 。 この演算子に対して信頼できるIPマスクが指定されていない場合、セキュリティゾーンも **allowEmptyPassword** モードとallowUserPasswordモードになってい **る必要があります** 。

#### &#39;Properties&#39;要素 {#properties--element}

この要素は、電子メールの設定(例：

* **mailServer**:電子メールの送信に使用するSMTPサーバー(例：smtp.domain.net)。
* **mailFrom**:レポートの送信者の電子メールアドレス(例：monitoring@domain.net)。
* **recipientList**:監視する受信者の電子メールアドレスのリスト。 アドレスはコンマで区切る必要があります（スペースは使用できません）。
* 「**night**」モード（オプション）は、指定した期間の間に電子メールを送信しないようにするために使用します。 代わりに、データが統合され、夜のアクティビティに関する電子メールが終了時間（デフォルトで7:00）の後に送信されます。
* buildRangeサブ **要素** （オプション）を使用すると、最小および最大のビルド番号を指定できます。 ビルド番号がこの範囲に含まれないすべてのマシンに対してエラーが発生します

   ```
   <buildRange minimum="0000" maximum="9999"/>
   ```

* properties要素に(オプシ **`<sla>`** ョンの)サブ要素を追加で **きます** 。 ネットワークポートが実行されるたびに、ログファイルが生成されます。 ファイルの名前には、設定名と日時が含まれます(例： **dev_06_12_13_16_47_05.tmp**)。 ファイルには次の情報が含まれます。インスタンス名、マシン名、重大度レベル（0 ～ 3、最も重要でないものから）、日付（タイムスタンプ形式）、クエリーと応答の間の経過時間（ミリ秒）、使用されるサービス(http、ncs、ncexx、redir)。 この情報は、各サービスの終わりに、集計マークと改行で区切られます。

>[!NOTE]
>
>要素 **のpersistHtmlFile** 属性の値が「true」の場合、 **`<property>`** netreport.mdファイルに最新の監視ステータスが記録され **ます**。 このファイルはインストールディレクトリに保存されます。

#### &#39;Instance&#39;要素 {#instance--element}

この要素を使用すると、複数のマシン（ホスト）を同じインスタンスに再グループ化できます。 インスタンス名は、監視用電子メールの最初の部分に表示されます。 インスタンスの名前をクリックして、各マシンに関する詳細にアクセスできます。

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

* **name**:電子メールの最初の部分に表示されるインスタンス名。
* **recipientList** （オプション）:特定のインスタンスに関する監視レポートを電子メールで送信できます。

#### &#39;Host&#39;要素 {#host--element}

この要素は、ホスト上の特定のサーバーの監視を設定します。

* **name**:監視するマシンの名前。
* **alias** （オプション）:レポートに表示される監視対象マシンの名前。
* **sessionToken**:認証済みセッショントークンを介したログイン認証を提供します。

   セッショントークンを設定するには、Adobe Campaignコ **ンソールで** 、監視演算子を選択します。 「アクセ **ス権」タブで** 、このインスタンスを監視する権限を持つコンピューターのIPアドレスを指定します。 その後、監視IDを使用して監視ページに接続でき、パスワードを指定す **る必要は** ありません。

   ![](assets/ncs_operators_rights_02.png)

* **criticalLevel** （オプション）:エラーを重大度別に並べ替えることができます。 使用可能な値は、「0」（すべてのレベルが表示される）、「1」（高いエラーと重大なエラーのみが表示される）、「2」（重大なエラーのみが表示される）です。 この属性を指定しない場合、すべてのエラーレベルが表示されます。
* **filter** （オプション）:特定のワークフローエラー( **filter=&quot;wkf;wkf1&quot;など)を除外できます**。 ワークフローラベルはセミコロンで区切る必要があります。

#### サブ要素 {#sub-elements}

* **tcp**:サーバーが起動中かダウン中かを確認します。 ポート番号を入力してください。
* **http**:webサーバーが存在するかどうかを確認します（アプリケーションサーバーが動作しているかどうか）。
* **ncs**:は、「インスタンス」属性に入力されたインスタンス上のプロセス（ワークフローエラー、メモリ使用量など）を確認します。 include **** （必須）属性は、デッドプロセス（「true」または「false」値）を表示するオプションを提供します。
* **redir**:トラッキングをチェックします。

ほとんどの場合、 **ncs** と **** redirサブ要素のみを保持できます。

いずれの場合でも、サブ要素で特定のノードを過負荷にすることができます(例えば、 **node port=75** はhttp、ncs、redir接続に使用するポートを過負荷にする)。

```
<ncs instance="clap40" url="/nl/jsp/soaprouter.jsp" includeDead="false" port="80"/>
```

**ncs**、 **redir** 、およびhttpサブ要素で、isSecure ******** sub属性（オプション）を追加して、httpsプロトコルを使用しない（「true」または「false」の値）かどうかを選択できます。 この属性を指定しない場合、httpプロトコルが使用されます。

### netreport.batまたはnetreport.shファイルの設定 {#configuring-the-netreport-bat-or-netreport-sh--file}

設定するには、このファイルを編集し、JREまたはJDKがインストールされているディレクトリを指定します。

### 監視の開始 {#launching-monitoring}

監視を開始するには、スクリプ **トを使用して** 、netreport.batまたは **** netreport.shファイルを一定の間隔で実行します。 レポートは、最初の実行の後、ステータスが変更された場合にのみ送信されます。

### 監視のテスト {#testing-monitoring}

監視をテストするには、 **netreport.bat** または **netreport.shファイルを実行します** 。

電子メールが、 **netconf.xmlファイルのrecipientList** に指定された受信者に **送信されます** 。
