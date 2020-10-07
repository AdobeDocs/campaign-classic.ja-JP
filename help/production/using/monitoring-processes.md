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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# プロセスの監視{#monitoring-processes}

アプリケーションサーバーとリダイレクトサーバー(**追跡**)は、手動または自動で監視できます。

## 手動の監視 {#manual-monitoring}

Go to **[!UICONTROL Monitoring]** and click the **[!UICONTROL Overview]** link to display the Adobe Campaign process monitoring page.

![](assets/d_ncs_monitoring.png)

表示されるページでは、接続されたインスタンスの状態を表示できます。例：

* インスタンスの情報：バージョン，名前，データベースエンジン，インストール済みパッケージ，サーバーシステムインジケーター，
* 見つからないプロセスと実行情報(開始日、PIDなど)のリスト、
* ワークフローと配信の表示。

様々なキャンペーンプロセスを監視するその他の方法については、[このページ](../../production/using/monitoring-guidelines.md)で説明しています。

### ログ {#log-journal}

プロセスに関連するログジャーナルを表示できます。 これを行うには、プロセスをクリックし **ます(例：mta** )。次に、ログジャーナルを **[!UICONTROL 開くをクリックします]** 。

![](assets/d_ncs_monitoring2.png)

### システム指標 {#system-indicators}

システムインジケータのリストを使用すると、物理メモリや仮想メモリ、アクティブなプロセス、使用可能なディスク領域など、マシンに関する情報を表示できます。 インジケーターは、LinuxとWindowsのオペレーティングシステムで異なります。 「 **[!UICONTROL インスタンス監視]** 」ページに移動し、「 **[!UICONTROL 表示]** 」リンクをクリックして、インジケータのリストを開きます。

#### Windowsの場合 {#in-windows}

* **[!UICONTROL 保留中のイベントがキューに登録されました]** :「 **Message Center**」に固有のインジケーター。 詳しくは、[この節](../../message-center/using/monitoring-thresholds.md)を参照してください。
* **[!UICONTROL メモリ]** :物理メモリ(RAM)に関する情報。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :インストールされたメモリの合計量。

   **[!UICONTROL 利用可能]** :メモリの空き容量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   **[!UICONTROL 警告]** / **** 警告インジケーターが表示されたら、Adobe CampaignサーバーがインストールされているマシンにRAMを追加することで、この問題を解決できます。 また、専用のマシンにAdobe Campaignサーバーをインストールすることもできます。

* **[!UICONTROL スワップメモリ]** :ページングファイルと一致する仮想メモリに関する情報：ハードディスク上で、RAMのように使用される領域。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :メモリの合計容量。

   **[!UICONTROL 利用可能]** :メモリの空き容量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   [ **[!UICONTROL 警告]** ]インジケータと[ **[!UICONTROL 警告]** ]インジケータが表示されている場合は、Windowsの詳細設定で交換ファイルのサイズを増やすことで、この問題を解決できます。

* **[!UICONTROL ディスクXXX]** :マシンリーダーに関する情報です。

   **[!UICONTROL 現在の値]** :実際に使用されるディスク容量。

   **[!UICONTROL 最大値]** :合計ディスク容量。

   **[!UICONTROL 利用可能]** :空きディスク容量

   **[!UICONTROL 使用]** :使用ディスクの割合。

   **[!UICONTROL 警告]** :このインジケータは、使用可能なディスク領域が合計容量の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケータは、使用可能なディスク領域が合計容量の90%に達した場合に表示されます。

* **[!UICONTROL 古すぎるプロセス数]** :1日以上アクティブだったAdobe Campaignプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなプロセスの数。

   **[!UICONTROL 最大値]** :許可されたプロセスの最大数(1)。

   **[!UICONTROL 警告]** :このインジケーターは、プロセスの数が1に等しい場合に表示されます。

   ア **[!UICONTROL ラート]** ・インジケータが表示される場合は、該当するプロセスがSQLデータベース・エンジンによってロックされているか、無限ループで停止している可能性があります。 Adobe Campaignが提供する **ウォッチドッグ** ・プロセスは、毎日すべてのプロセスを自動的に開始し直し、この問題を解決できます。 ただし、関連するプロセスを自分で停止して、再開始を強制することもできます。

#### Linuxの場合 {#in-linux}

![](assets/production_system_indicators_linux_001.png)

* **[!UICONTROL 保留中のイベントがキューに登録されました]** :「 **Message Center**」に固有のインジケーター。 詳しくは、[この節](../../message-center/using/monitoring-thresholds.md)を参照してください。
* **[!UICONTROL 読み込み平均（1/5/15分）]** :負荷に関する情報、つまり、最後の1分、5分、15分間にわたってマシン上で実行されるプロセスによるプロセッサの使用率

   **[!UICONTROL 現在の値]** :装置の実際の負荷。

   **[!UICONTROL 最大値]** :マシン上のプロセスの最大使用負荷

   **[!UICONTROL 警告]** :このインジケーターは、最後の1分、5分、15分間に負荷が許可された最大値の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケーターは、読み込みが、最後の分、5分または15分の最大許可値の90%に達した場合に表示されます。

* **[!UICONTROL メモリ]** :物理メモリ(RAM)に関する情報。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :インストールされたメモリの合計量。

   **[!UICONTROL 利用可能]** :メモリの空き容量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   **[!UICONTROL 警告]** / **** 警告インジケーターが表示されたら、Adobe CampaignサーバーがインストールされているマシンにRAMを追加することで、この問題を解決できます。 また、専用のマシンにAdobe Campaignサーバーをインストールすることもできます。

* **[!UICONTROL スワップメモリ]** :ページングファイルと一致する仮想メモリに関する情報：ハードディスク上で、RAMのように使用される領域。

   **[!UICONTROL 現在の値]** :実際のメモリ消費量。

   **[!UICONTROL 最大値]** :メモリの合計容量。

   **[!UICONTROL 利用可能]** :メモリの空き容量。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケータは、メモリ消費量が合計量の90%に達した場合に表示されます。

   [ **[!UICONTROL 警告]** ]インジケータと[ **[!UICONTROL 警告]** ]インジケータが表示されている場合は、交換ファイルのサイズを増やすことでこの問題を解決できます。

* **[!UICONTROL コアファイル]** :adobe campaignプロセスのクラッシュ後に生成されるファイルに関する情報。 これらのファイルを使用して、クラッシュの原因を診断できます。

   **[!UICONTROL 現在の値]** :既存のファイルの数。

   **[!UICONTROL 最大値]** :許可されたファイルの最大数(1)。

   **[!UICONTROL 警告]** :このインジケータは、ファイル数が1に近づくと表示されます。

   **[!UICONTROL 警告]** :このインジケーターは、ファイル数が1に等しい場合に表示されます。

   クラッシュが原因でプロセスが見つからない場合、プロセスのリストに赤で表示され、Adobe Campaignが提供する **ウォッチドッグ** ・プロセスによって自動的に再起動されます。

* **[!UICONTROL 共有メモリセグメントの数]** :すべてのAdobe Campaignプロセスで共有されるメモリセグメントに関する情報。

   **[!UICONTROL 現在の値]** :現在使用中のメモリセグメントの数。

   **[!UICONTROL 最大値]** :許可されたメモリセグメントの最大数(2)。

   **[!UICONTROL 警告]** :このインジケーターは、メモリセグメントの数が1に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケーターは、メモリセグメントの数が2に達すると表示されます。

* **[!UICONTROL 古すぎるプロセス数]** :1日以上アクティブだったプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなプロセスの数。

   **[!UICONTROL 最大値]** :許可されたプロセスの最大数。

   **[!UICONTROL 警告]** :このインジケーターは、プロセスの数が許可されたしきい値の80%に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケーターは、プロセスの数が許可されたしきい値の90%に達した場合に表示されます。

* **[!UICONTROL ファイルハンドル]** :ファイル記述子に関する情報、つまりプロセスごとに開かれたファイルの数。

   **[!UICONTROL 現在の値]** :ファイル記述子の現在の数。

   **[!UICONTROL 最大値]** :オペレーティングシステムによって許可されたファイル記述子の最大数。

   **[!UICONTROL 警告]** :このインジケータは、許可されたファイル記述子の数が80%のしきい値に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケータは、許可されたファイル記述子の数が90%のしきい値に達した場合に表示されます。

* **[!UICONTROL プロセス]** :マシンプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなプロセスの数。

   **[!UICONTROL 最大値]** :許可されたプロセスの最大数。

   **[!UICONTROL アクティブなプロセス]** :アクティブなプロセスの数。

   **[!UICONTROL 非アクティブなプロセス]** :非アクティブなプロセスの数。

   **[!UICONTROL 警告]** :このインジケーターは、許可されたプロセスの数が80%のしきい値に達した場合に表示されます。

   **[!UICONTROL 警告]** :このインジケーターは、許可されたプロセスの数が90%のしきい値に達した場合に表示されます。

* **[!UICONTROL Zombie Processes]** :停止したが、プロセス識別子(PID)がまだあり、プロセステーブルに表示されたままのプロセスに関する情報。

   **[!UICONTROL 現在の値]** :現在アクティブなzombieプロセスの数。

   **[!UICONTROL 最大値]** :認証zombieプロセスの最大数(2)

   **[!UICONTROL 警告]** :このインジケータは、ゾンビプロセスの数が2に近づくと表示されます。

   **[!UICONTROL このインジケータは]** 、ゾンビ・プロセスの数が2に達した場合に表示されます。

#### カスタマイズされたインジケータ {#customized-indicators}

Adobe Campaignを使用すると、インジケーターをカスタマイズできます。 手順は次のとおりです。

1. .sh **ファイルを作成し** 、 **[!UICONTROL cust_indicators.shという名前を付けます]** 。
1. カスタマイズし追加たインジケーターをこのファイルに追加します。 例：

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

1. このファイルを **[!UICONTROL usr/local/neolane/nl6]** フォルダーに置きます。

このファイルはAdobe Campaignによって呼び出されます。

## SMTP Reports {#smtp-reports}

SMTP配信監視レポートは、Adobe Campaignプラットフォームに統合されています。 ユーザーは、コンソールからアクセスすることも、Webアクセスを使用することもできます。

これらのレポートには、SMTP配信の統計とSMTPエラーがドメイン別に表示されます。

これらにアクセスするには、演算子に管理者権限が必要です。

これらは、 **Monitoring** /&#39;SMTP Monitoring&#39;の下にグループ化されています。

![](assets/smtp_reports_access.png)

>[!CAUTION]
>
>* SMTP監視に関連する情報は、電子メールチャネルがアクティブ化されている場合にのみ利用できます。
>* SMTP送信統計 **[!UICONTROL 情報は]** 、インスタンスで統計サーバが起動した場合にのみ提供されます。

>



### SMTP 送信統計 {#smtp-sending-statistics}

SMTP送信統計 **[!UICONTROL レポートを使用すると、サーバーアクティビティを制御できます]** 。 これは、各マチルドの合成を表示します。

![](assets/smtp_stats_report.png)

このレポートの指標のリストがグラフの下に表示されます。

1. 送信されたメッセージの合計数。
1. 
   * 青い線：送信する準備ができたメッセージ、つまりSMTPを送信する前の最後のステージ（受信データと一致）。

   * 緑の線：メッセージは正常に送信されました（送信データと一致）。

   * 赤い線：Shaperによって破棄されたメッセージが **mta** （この回復で拒否されたデータと一致）に返されます。

   これらの値は、1時間あたりのメッセージ数で表されます。

1. Shaperの2つのキューを表します。

   * 青いカーブ：アクティブなメッセージのキュー。 これらのメッセージは、可能な限り早く送信されます。

   * カキ曲線：「deferred」キュー。 ジョブ数の制限またはターゲットへの接続が利用できないため、現在、これらのメッセージを返すことはできません。 再試行は5秒、10秒、20秒、40秒、2分ごとなど を返し **** ます。

1. 次のグラフは、破棄されたメッセージの詳細を示します（2番目のグラフの赤い曲線）。メッセージなしで破棄されたメッセージ(mauve)の割合と、送信に失敗した再試行(red)のメッセージの割合を示します。 これにより、統計サーバの制限（スロットリング）またはリモート・サーバの使用不可により、許可された期間内に処理されなかったメッセージの割合を表示できます。
1. SMTP 接続が既にオープンしているか、現在オープン中です。
1. mtachildの数の予測 **値**。

>[!NOTE]
>
>このレポートは、Email Traffic Shaperコンポーネントのステータスに関連しています。

### 各ドメインの SMTP エラー {#smtp-errors-per-domain}

このレポートでは、配信エラーを一定期間、ドメイン別に表示できます。

>[!NOTE]
>
>**minConnectionsToLog**、 **minErrorsToLog** 、 **minMessagesToLogの各** サーバーConf.xmlファイルのログ **** オプションでは、上記の接続統計を考慮に入れる、接続統計値が定義されます。

![](assets/smtp_error_report.png)

このレポートの指標のリストを表に示します。

* 「 **Domain** 」列には、メッセージの送信先のドメイン名（または、yahoo.frの場合はyahoo.comなどの実際のドメイン名）が含まれます。
* 「 **Cnx** 」列には、このドメインで開いているSMTP接続の数が表示されます。
* 「 **Sent** 」列は、このドメインに送信されるメッセージの数に対応します。
* 「 **Volume** 」列には、このドメインに送信しようとしたメッセージの量（概算値）が表示されます。
* 「 **エラー** 」列には、期間中のこのドメインのエラーのボリュームインジケーターが表示されます。
* 「 **最後の応答** 」列には、このドメインに対して最後に受信したSMTP応答メッセージが表示されます。
* 「 **日付** 」列には、このドメインで最後に受信したSMTP応答の日付が表示されます。

>[!NOTE]
>
>「 **Cnx**」、「 **Sent**」、「 **Volume** 」の各列に表示される値は、「 **** Period」フィールドで選択した期間を基準に計算されます。

ドメイン名をクリックして、エラーを表示します。

これらはPublicIdで分類されます。この識別子は、ルータの背後にある複数のAdobe Campaignmtaが共有するIPアドレスに対応します。 統計サーバは、この識別子を用いて、この起点とターゲットサーバとの間の配信および接続統計を記憶する。

![](assets/smtp_error_report_details.png)

「 **[!UICONTROL Owner of domain]** 」フィールドを使用すると、様々なドメイン名を同じラベル下にグループ化できます。 最初のレポート表示では、すべてのMXドメイン名がこの所有者に関連付けられます。

詳細を表示するには、PublicId識別子をクリックします。

![](assets/smtp_error_report_subdetails.png)

>[!NOTE]
>
>エラーの割合は2つのグラフで表されます。 1つ目は、黒の背景の上に横長のプログレスバーが表示されます。 2つ目の表は時系列です。 選択した期間は12の時間間隔に分割され、それぞれが垂直プログレスバーで表されます。 両方の表現で、エラーが検出されなかった場合、バーは黒です。 バーの色は、発生したエラーの割合（黄色、オレンジ、最後に赤）によって異なります。 カラーグレーは、重要なデータ量が見つからないことを意味します。 グラフにカーソルを置くと、エラーの正確な割合を表示できます。

>[!NOTE]
>
>SMTPエラーの詳細とAdobe Campaignでの管理については、 [この節を参照してください](../../installation/using/email-deliverability.md)。

## 請求レポート {#billing-report}

**[!UICONTROL 請求]** 技術ワークフローは、システムアクティビティレポートを「請求」演算子に電子メールで送信します。 毎月25日にデフォルトでトリガーされます。

技術的なワークフローは、次のノードのサブフォルダーにあります。 **管理** / **実稼働** / **テクニカルワークフロー**。

![](assets/billing.png)

ワークフローが月の25日に開始されると、請求担当者の受信トレイに次のレポートが表示されます。

![](assets/billing_2.png)

配信の追跡には、次の指標を使用できます。

* **[!UICONTROL 開始日]** :配信の開始日。 レポートの「開始日」より前に設定することもできます。
* **[!UICONTROL ラベル]** :配信のラベル。 100件未満のメッセージを送信する配信は小さすぎると見なされ、開始日別に集計されます。この場合、ラベルには集計数が表示されます(例： [集計数は3個の小配信])。
* **[!UICONTROL 総量]** :配信用に転送された合計バイト数。
* **[!UICONTROL 平均ボリューム]** :転送された平均バイト数。 これは、次の数式 **（合計ボリューム/メッセージ数）**( **[!UICONTROL 乗数]** 指標の計算基準)の結果です。
* **[!UICONTROL メッセージ]** :送信されたメッセージの数。 これには、正常に送信されたメッセージと、再試行（接続したサーバーからバウンスメッセージを受信した後）の両方が含まれます。
* **[!UICONTROL 乗数(x)]** :乗数の値は、メッセージの平均ボリュームから推定されます。
* **[!UICONTROL カウント]** :メッセージと乗算子の乗算の結果。

## 自動監視 {#automatic-monitoring}

Adobe Campaignオファーには、次に示す自動監視方法がいくつかあります。

### コマンドライン {#command-line}

コマンド

**nlserverモニタ**

Adobe Campaignモジュールとシステムに一連のインジケータをリストできます。

処理が容易なXML形式で出力が生成されます。

このコマンドは、 **-missing** パラメーターを指定して実行することもできます。このパラメーターは、設定ファイルで実行する必要があると指示された場合に、このインスタンスに見つからないプロセスをリストします。

```
nlserver monitor -missing
HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
mta@prod
stat@prod
wfserver@prod
```

### サーバーから発行された情報 {#information-published-by-the-server}

#### /r/test {#r-test}

リダイレク **トサーバーのテストには、`<application>`http(s)://** /r/testページが使用されます。 追跡に使用するフロントサーバーをテストする場合も、同じ方法を使用することをお勧めします。 このページは、読み込みディスパッチャーをテストする場合にも使用できます。

XML形式で次の行が表示されます。

```
<redir status='OK' date='YYYY-MM-DD HH:MM:SS.112Z' build='XXXX' host='<hostname>' localHost='<servername>'/>
```

**頻度**:このテストでは読み込みが使用されないので、非常に頻繁に実行されます（例：毎秒1回）。

#### /nl/jsp/ping.jsp {#nl-jsp-ping-jsp}

この **http(s):///nl/jsp/ping.jsp`<Application server url>`** ページの動作は、ネットワークの対応するページと同じです。apache/tomcat/web module/databaseを通じて完全なクエリをテストし、クライアントにアップロードします。 すべてが正常に動作している場合は、「OK」を返します。 データベース(mtaや調査など)にアクセスできるコンピューターでこのテストを実行することをお勧めします。

**使用状況**:リモートでログインするには、演算子のログインに関連付けられたセッショントークンを引数として渡す必要があります(Adobe Campaignスクリプトを使用した [自動監視のヒント](#automatic-monitoring-via-adobe-campaign-scripts))。

例：

![](assets/ncs_monitoring_ping.png)

オペレーター名とログインは、Adobe Campaignのクライアントコンソールで事前にデータベース権限を持つように設定する必要があります。

![](assets/ncs_operators_rights_01.png)

**頻度**:これは、帯域幅をほとんど使用しないテストです。 したがって、1分に1回以上は実行されないにもかかわらず、かなり頻繁に実行されます。

#### /nl/jsp/monitor.jsp {#nl-jsp-monitor-jsp}

これは、オペレーターがWebページを介してAdobe Campaignサーバーにアクセスできるかどうかを確認するテストです。クライアントコンソールのメニューからアクセスしたのと同じwebページ。 監視ツール（Tivoli、Nagiosなど）からこのページを呼び出すことができます。

![](assets/ncs_monitoring_web.png)

**使用状況**:インスタンスに接続できる演算子ログインに関連付けられたセッショントークンは、引数として使用する必要があります(Adobe Campaignスクリプトを使用した [自動監視のヒントを参照](#automatic-monitoring-via-adobe-campaign-scripts))。

オペレーターとそのログインは、Adobe Campaignのクライアントコンソールで、適切なデータベース権限と制限を持つように事前に設定する必要があります。

**頻度**:これは完全なサーバーテストであり、頻繁に実行する必要はありません（例えば、10分に1回実行できます）。

#### /nl/jsp/soaprouter.jsp {#nl-jsp-soaprouter-jsp}

この **jspは** 、Adobe CampaignアプリケーションAPIのエントリポイントを表します。 したがって、アプリケーションの詳細な監視を提供できます。 また、Adobe CampaignWebサービスの監視にも使用できます。 監視スクリプトで使用されますが、電源ユーザーのみが対象です。

### デプロイメントタイプに基づく監視 {#monitoring-based-on-deployment-types}

Adobe Campaignにより、様々なデプロイメント設定を有効にできます(詳しくは、 [この節を参照](../../installation/using/hosting-models.md))。 このセクションでは、インストールのタイプに応じて適用される様々な自動監視方法について説明します。

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
     <li><p> <span class="uicontrol">/r/test</span> and <span class="uicontrol">/nl/jsp/monitor.jsp</span> on theAdobe Campaignサーバ</p> </li> 
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

Adobe Campaignは、検出された異常値に関するレポートを電子メールで送信できるインスタンス監視ツール（インスタンス監視ツール）を提供できます。

![](assets/pro_netreport.png)

>[!CAUTION]
>
>このツールは、インスタンスの監視に使用できますが、Adobe Campaignではサポートされていません。 詳細については、キャンペーン管理者にお問い合わせください。

### 必須要素 {#required-elements}

自動監視には、次の事前インストールに関する注意が必要です。

* netreport.tgz **（Linuxのインストール）または** netreport.zip **** （Windowsのインストール）のファイルが存在する必要があります。
* 監視対象のマシンに監視をインストールしないことを強くお勧めします。
* JREまたはJDKを搭載したマシンにインストールする必要があります。
* Linuxでは、監視対象のマシンに **bc** パッケージが必要です。 詳しくは、[この節](../../installation/using/installing-packages-with-linux.md#distribution-based-on-rpm--packages)を参照してください。

### インストール手順 {#installation-procedure}

インストール手順は次のとおりです。

1. コンソールで、必要に応じて新しい演算子を作成します（「monitoring」ユーザーは既に存在します）が、権限は割り当てません。
1. アーカイブ抽出を実行します。
1. お **読みください** 。
1. netconf.xml **構成ファイルを更新します** 。
1. netreport.bat **(Windows)または** netreport.sh **** (Linux)ファイルを更新します。

### netconf.xmlファイルの設定 {#configuring-the-netconf-xml-file}

XML設定ファイルには、次の要素が含まれています。

* [&#39;Properties&#39;要素](#properties--element)
* [&#39;Instance&#39;要素](#instance--element)
* [&#39;Host&#39;要素](#host--element)
* [サブ要素](#sub-elements)

設定の例を次に示します。

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
>様々な設定を指定するには、 **netconf.xml** ファイルにサフィックスを追加します。 **netconf-dev.xml**、 **netconf-prod.xml**&#x200B;などがあります。 次に、netreport.bat **またはnetreport.sh** ファイルで、netreportの実行に使用する設定を指定します。 **$JAVA_HOME/bin/java netreport devを追加するか、** @%JAVA_HOME%port treport prodを例に追加し ******** ます。

>[!CAUTION]
>
>監視 **演算子が動作するためには** 、ネットポートが実行されるマシンが、 **sessionTokenOnly** モードのセキュリティゾーンに存在する必要があります。 この演算子に信頼できるIPマスクが指定されていない場合は、セキュリティゾーンも **allowEmptyPassword** モードとallowUserPassword **** モードになっている必要があります。

#### &#39;Properties&#39;要素 {#properties--element}

この要素は、電子メールの設定(例：

* **mailServer**:電子メールの送信に使用するSMTPサーバー(例：smtp.domain.net)。
* **mailFrom**:レポートの送信者の電子メールアドレス(例：monitoring@domain.net)。
* **recipientList**:監視受信者の電子メールアドレスのリスト。 アドレスはコンマで区切る必要があります（スペースは使用できません）。
* &#39;**night**&#39;モード（オプション）は、指定された期間の間に電子メールを送信しないようにするために使用します。 代わりに、データが統合され、夜のアクティビティに関する電子メールが終了時刻（デフォルトで7:00）の後に送信されます。
* buildRange **** サブ要素（オプション）を使用すると、最小と最大のビルド番号を指定できます。 ビルド番号がこの範囲に該当しないすべてのマシンに対してエラーが発生します

   ```
   <buildRange minimum="0000" maximum="9999"/>
   ```

* **`<sla>`** properties **** 要素に（オプションの）サブ要素を追加できます。 ネットワークポートが実行されるたびにログファイルが生成されます。 ファイルの名前には、設定名と日時が含まれます( **dev_06_12_13_16_47_05.tmp**&#x200B;など)。 このファイルには、次の情報が含まれています。インスタンス名、マシン名、重大度レベル、（0 ～ 3、最重要度から最重要度まで）、日付（タイムスタンプ形式）、クエリと応答の間の経過時間（ミリ秒）、使用されるサービス(http、ncs、ncsex、redir)。 この情報は、各サービスの最後にある集計記号と改行で区切られます。

>[!NOTE]
>
>要素の **persistHtmlFile** 属性の値が「true」の場合は、最新の監視ステータスをファイル **`<property>`** netreport.mdに記録するために使用されます ****。 このファイルは、インストールディレクトリに保存されます。

#### &#39;Instance&#39;要素 {#instance--element}

この要素を使用すると、複数のマシン（ホスト）を同じインスタンスに再グループ化できます。 インスタンス名は、監視用電子メールの最初の部分に表示されます。 インスタンスの名前をクリックすると、各マシンに関する詳細にアクセスできます。

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

この要素は、ホスト上の特定のサーバの監視を設定します。

* **name**:監視するマシンの名前。
* **alias** （オプション）:レポートに表示される監視対象マシンの名前。
* **sessionToken**:認証済みセッショントークンを介したログイン認証を提供します。

   セッショントークンを設定するには、Adobe Campaignコンソールで **monitoring** 演算子を選択します。 「 **アクセス権** 」タブで、このインスタンスを監視する権限を持つマシンのIPアドレスを指定します。 その後、監視 **IDを使用し、パスワードを指定する必要なく、これらのコンピューターから監視ページに接続できるようになります** 。

   ![](assets/ncs_operators_rights_02.png)

* **criticalLevel** （オプション）:表示されるエラーを重大度別に並べ替えることができます。 有効な値は、「0」（すべてのレベルが表示される）、「1」（高いエラーと重大なエラーのみが表示される）、「2」（重大なエラーのみが表示される）です。 この属性を指定しない場合、すべてのエラーレベルが表示されます。
* **filter** （オプション）:特定のワークフローエラー( **filter=&quot;wkf;wkf1&quot;など**)を除外できます。 ワークフローラベルはセミコロンで区切る必要があります。

#### サブ要素 {#sub-elements}

* **tcp**:サーバーが起動中かダウン中かを確認します。 ポート番号を入力してください。
* **http**:Webサーバーが存在するかどうかを確認します（アプリケーションサーバーが動作しているかどうか）。
* **ncs**:&#39;instance&#39;属性に入力されたインスタンスのプロセス（ワークフローエラー、メモリ使用量など）をチェックします。 「 **include** （必須）」属性を使用すると、デッドプロセス（「true」または「false」の値）を表示するオプションを選択できます。
* **redir**:でトラッキングをチェックします。

ほとんどの場合、 **ncs** と **** redirのサブ要素のみを保持できます。

いずれの場合でも、サブ要素で特定のノードを過負荷にすることができます(例えば、node **port=75** は、http、ncs、redir接続に使用するポートを過負荷にする)。

```
<ncs instance="clap40" url="/nl/jsp/soaprouter.jsp" includeDead="false" port="80"/>
```

ncs **、** redir **** 、およびhttp ******** サブ要素では、isSecure属性（オプション）を追加して、httpsプロトコル（「true」値または「false」値）を使用しないかどうかを選択できます。 この属性が指定されない場合、httpプロトコルが使用されます。

### netreport.batまたはnetreport.shファイルの設定 {#configuring-the-netreport-bat-or-netreport-sh--file}

設定するには、このファイルを編集し、JREまたはJDKがインストールされているディレクトリを指定します。

### 監視の開始 {#launching-monitoring}

監視を起動するには、スクリプトを使用して、 **netreport.bat** または **netreport.sh** ファイルを一定の間隔で実行します。 レポートは、最初の実行後、次にステータスの変更がイベントした場合にのみ送信されます。

### 監視のテスト {#testing-monitoring}

監視をテストするには、 **netreport.bat** または **netreport.sh** ファイルを実行します。

**netconf.xml** ファイルのrecipientList **** に指定された受信者に電子メールが送信されます。
