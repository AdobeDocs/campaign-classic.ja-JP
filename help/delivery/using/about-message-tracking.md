---
product: campaign
title: トラッキングの基本を学ぶ
description: Adobe Campaign のトラッキングに関する一般的なガイドラインを学ぶ
feature: Monitoring, Email
role: User
exl-id: 43779505-9917-4e99-af25-b00a9d29a645
source-git-commit: ba53107ce06c0484070cbe0943ba439d33d5f710
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 64%

---

# メッセージトラッキングの基本を学ぶ {#get-started-tracking}

>[!IMPORTANT]
>
>Campaign v7 とCampaign Classic v8 の両方に適用される **一般的なトラッキングガイダンス** については、[Campaign v8 メッセージトラッキングドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/tracking){target="_blank"} を参照してください。
>
>* [&#x200B; トラッキングするリンクの設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/tracked-links){target="_blank"}
>* [URL トラッキングオプションの設定](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/url-tracking){target="_blank"}
>* [&#x200B; パーソナライズされたリンクの追跡 &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/personalized-links){target="_blank"}
>* [&#x200B; トラッキングログへのアクセス &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/tracking-logs){target="_blank"}
>* [トラッキングのテスト](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/testing-tracking){target="_blank"}
>* [&#x200B; トラッキングレポート &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/reporting/delivery-reports#tracking-indicators){target="_blank"}
>
>**このページでは、主にハイブリッドデプロイメントとオンプレミスデプロイメントのCampaign Classic v7 固有のトラッキング機能のみ** について説明します。

## トラッキング機能

### トラッキング設定 {#configure-tracking}

Campaign Classic v7 **ハイブリッド/オンプレミスデプロイメント** の場合は、使用前にインスタンスレベルでトラッキングを設定する必要があります。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services の場合、トラッキング設定はAdobeによって実行されます。

**動作の仕組み**

トラッキングを使用する前に、まずインスタンスに対して設定する必要があります。設定は、Adobe Campaign アプリケーションサーバーと web サーバーで実行する必要があります。

Campaign には、次の 2 種類のトラッキングがあります。

* **Web トラッキング**：このモードでは、web サイトページへの訪問を追跡できます
* **メッセージトラッキング**：このモードでは、メッセージ配信と受信者の行動をトラッキングできます

インストール時にトラッキングモードが選択されます。 オンプレミスインストールの場合、トラッキング設定はインスタンスレベルで定義する必要があります。 [詳細情報](../../installation/using/deploying-an-instance.md#operating-principle)

**トラッキングサーバー**

トラッキングを設定するには、インスタンスを宣言し、トラッキングサーバーに登録する必要があります。トラッキングサーバーは、受信者がクリックした URL に関する情報を記録および取得するために使用されます。

オンプレミスインストールの場合、トラッキングサーバーは通常、Adobe Campaign web アプリケーションを実行している web サーバーです。 トラッキングサーバー URL は、インスタンス設定で定義する必要があります。 [詳細情報](../../installation/using/deploying-an-instance.md#tracking-server)

**トラッキングの保存**

トラッキングを設定し、URL を入力したら、トラッキングサーバーを登録する必要があります。登録により、Adobe Campaignはトラッキング情報を保存し、トラッキングされたアクティビティに関するレポートと統計を提供できます。

オンプレミスインストールの場合、トラッキング情報はデータベースに保存され、テクニカルワークフローを通じて取得されます。 **トラッキング** テクニカルワークフローは、リダイレクトサーバーから収集したトラッキングデータを処理および保存します。 [詳細情報](../../installation/using/deploying-an-instance.md#saving-tracking)

### Web アプリケーショントラッキング {#web-application-tracking}

<img src="assets/do-not-localize/icon-web-app.svg" width="60px">

>[!NOTE]
>
>**Web アプリケーションのトラッキングはCampaign Classic v7 に固有で** Campaign v8 では使用できません。

**web アプリケーションのトラッキング**

また、トラッキングタグを含む web アプリケーションページの訪問をトラッキングおよび測定できます。この機能は、フォームやランディングページなど、あらゆる種類の Web アプリケーションで使用できます。[詳細情報](../../web/using/tracking-a-web-application.md)

**web アプリケーショントラッキングのオプトアウト**

web アプリケーショントラッキングのオプトアウトを使用すると、行動トラッキングをオプトアウトしたエンドユーザーの web 行動のトラッキングを停止できます。web アプリケーションやランディングページにバナーを表示して、ユーザーがオプトアウトできるようにする機能を追加できます。[詳細情報](../../web/using/web-application-tracking-opt-out.md)

## トラッキングのトラブルシューティング {#tracking-troubleshooting}

<img src="assets/do-not-localize/icon-troubleshooting.svg" width="60px">

次のトラブルシューティングのヒントは、**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** に当てはまります。 一部の情報は、Campaign v8 オンプレミスデプロイメントにも当てはまる場合があります。 Campaign v8 Managed Cloud Services の場合は、Adobe担当者にお問い合わせください。

Campaign v8 の基本的なトラッキングのトラブルシューティング手順については、[Campaign v8 のトラッキングのトラブルシューティング &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/analytics/tracking/tracking-logs#troubleshooting){target="_blank"} ドキュメントを参照してください。

### 基本チェック {#basic-checks}

**trackinglogd プロセスが実行中であることを確認します**

このプロセスは、IIS/web サーバーの共有メモリから読み取り、リダイレクトログを書き込みます。

インスタンスで「監視」タブを選択すると、ホームページからアクセスできます。 また、インスタンスで次のコマンドを実行することもできます。`<user>@<instance>:~$ nlserver pdump`

trackinglogd プロセスがリストに表示されない場合は、インスタンスで次のコマンドを使用して起動します。`<user>@<instance>:~$ nlserver start trackinglogd`

**最近、トラッキング テクニカルワークフローが実行されていることを確認する**

トラッキングのテクニカルワークフローは、管理／製品／テクニカルワークフローのフォルダーで確認できます。

### 詳細なトラブルシューティング {#advanced-troubleshooting}

+++トラッキングワークフローが失敗する

>[!NOTE]
>
>Windows でのみ使用できます

破損したトラッキングログファイル .../nl6/var/&lt;インスタンス名>/redir/log/0x0000 ログにより、トラッキングワークフローが停止する可能性があります。破損した行を容易に検出して削除し、トラッキングワークフローを再開するには、次のコマンドを使用します。

**どのファイルが破損した行かわかっている**

このコマンドでは、0x00000000000A0000.log ファイル内にある破損した行が見つかります。他のファイルにある破損した行を見つけるには、同じ処理を各ファイルに適用する必要があります。

```
$ cd {install directory}/var/{instance name}/redir/log
$ cat 0x00000000000A0000.log | sed -nE '/^[[:alnum:]]{2}x[[:alnum:]]*\t[0-9T:\.-]*\t[0-9a-fA-F]*\t[0-9a-fA-F]*\t[0-9a-fA-F]*\t[[:alnum:]]*\t[[:alnum:]-]*\t[[:print:]]*\t[[:print:]]*\t[[:print:]]*\t([0-9a-fA-F\.:]*|[0-9a-fA-F\.:]*\t[[:print:]]*|[0-9a-fA-F\.:]*,[[:print:]]*)$/!p'
```

その後、トラッキングワークフローを停止し、破損した行を削除して、ワークフローを再度開始できます。

**どのファイルが破損した行かわからない**

1. 次のコマンドラインを使用して、すべてのトラッキングファイルを確認します。

   ```
   $ cd {install directory}/var/{instance name}/redir/log
   $ cat *.log | sed -nE '/^[[:alnum:]]{2}x[[:alnum:]]*\t[0-9T:\.-]*\t[0-9a-fA-F]*\t[0-9a-fA-F]*\t[0-9a-fA-F]*\t[[:alnum:]]*\t[[:alnum:]-]*\t[[:print:]]*\t[[:print:]]*\t[[:print:]]*\t([0-9a-fA-F\.:]*|[0-9a-fA-F\.:]*\t[[:print:]]*|[0-9a-fA-F\.:]*,[[:print:]]*)$/!p'
   ```

1. このコマンドは、破損した行をすべてリストアップします。例：

   ```
   50x000000000FD7EC86 2017-06-24T21:00:50.96 1f506d71 1aeab4b6 1af77020 0 e5155671-4ab7-4ce4-a763-3b82dda6d881 h
   Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.95 Safari/537.36 52.46.20.64
   ```

   >[!NOTE]
   >
   >読みやすいように、ユーザーエージェントの前にキャリッジリターン（CR）が追加されました。ただし、効果的なレンダリングはされません。

1. grep コマンドを実行して、対応するファイルを探します。

   ```
   $ grep -Rn <Log Id>
   # for example:
   $ grep -Rn 50x000000000FD7EC86
   ```

1. ファイル名と行番号を使用して、障害のあるログを見つけます。例：

   ```
   ./0x000000000FD7E000.log:3207:50x000000000FD7EC86 2017-06-24T21:00:50.96 1f506d71 1aeab4b6 1af77020 0 e5155671-4ab7-4ce4-a763-3b82dda6d881 h
   Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/55.0.2883.95 Safari/537.36 52.46.20.64
   ```

   >[!NOTE]
   >
   >読みやすいように、ユーザーエージェントの前にキャリッジリターン（CR）が追加されました。ただし、効果的なレンダリングはされません。

その後、トラッキングワークフローを停止し、破損した行を削除して、ワークフローを再度開始できます。

+++

+++トラッキングリンクが断続的に失敗する

トラッキングリンクにアクセスしようとすると、次のメッセージが表示されます。

`Requested URL '/r/ id=h787bc0,281a4d8,281a4da&p1=1' cannot be found`

1. &lt;redirection_server>/r/test URL にアクセスし、ビルド番号と localhost がリクエストによって返されたかどうかを確認します。

1. serverConf.xml ファイルで、トラッキングサーバー用の spareServer の設定を確認します。この設定はリダイレクトモードにする必要があります。

   ```
   <redirection>
      <spareServer _operation="update" enabledIf="$(hostname)!='test-rt1'" id="1"
      url="http://test-rt1:8080"/>
      <spareServer _operation="insert" enabledIf="$(hostname)!='test-rt4'" id="4"
      url="http://test-rt4:8080"/>
      <spareServer _operation="insert" enabledIf="$(hostname)!='test-rt3'" id="3"
      url="http://test-rt3:8080"/>
      <spareServer _operation="insert" enabledIf="$(hostname)!=test-rt2'" id="2"
      url="http://test-rt2:8080"/>
   </redirection>
   ```

1. &lt;deliveryID>.xml ファイルがマシン上の .../nl6/var/&lt;インスタンス名>/redir/url/&lt;YYYY> ディレクトリ（YYYY は配信の年）に存在するかどうかを手動で確認します。

1. &lt;trackingUrlId> が &lt;deliveryID>.xml ファイル内に見つかるかどうかを手動で確認します。

1. 関連する deliveryID 配信内に broadlogID が存在するかどうかを手動で確認します。

1. .../nl6/var/&lt;インスタンス名>/redir/url/year ディレクトリにある &lt;deliveryID>.xml ファイルのパーミッションを確認します。

   リクエストされたリンクをリダイレクトするために Apache がトラッキング URL を読み取れるように、少なくともパーミッションは 644 が必要です。

+++

+++NmsTracking_Pointer オプションの更新

NmsTracking_Pointer オプションを更新する場合は、次の手順に従います。

1. トラッキングワークフローを停止します。

1. trackinglogd サービスを停止します。

1. NmsTracking_Pointer オプションを必要な値に更新します。

1. trackinglogd サービスを再度開始します。

1. トラッキングワークフローを再度開始します。

+++

+++トラッキングが一部の Web メールで機能しない

クリックトラッキングの数式をカスタマイズして、カスタムの Adobe Analytics トラッキングの数式を指定できます。

このようなカスタマイズは、不要な改行文字を追加しないように、注意しておこなう必要があります。JavaScript 式の外にある改行文字はすべて、最終的な式に含まれます。

この種の追加の改行文字がトラッキング URL に含まれている場合、一部の webMail（AOL、GMail など）で問題が発生します。

**1 つ目の例：**

* 正しくない構文

  ```
  <%@ include option='NmsTracking_ClickFormula' %><% // Parameters expected by Adobe Analytics
  var pattern = new RegExp("(nl611\.test15|google\.com)", 'i')
  if( $(urlstring).match(pattern) && delivery.FCP == false )
  {
  %>
  &cid=<%= message.delivery.internalName %>&bid=<%= message.id.toString().toLowerCase() %><% } %>
  ```

* 正しい構文

  ```
  <%@ include option='NmsTracking_ClickFormula' %><% // Parameters expected by Adobe Analytics
  var pattern = new RegExp("(nl611\.test15|google\.com)", 'i')
  if( $(urlstring).match(pattern) && delivery.FCP == false )
  {
  %>&cid=<%= message.delivery.internalName %>&bid=<%= message.id.toString().toLowerCase() %><% } %>
  ```

余分な改行がどこにあるかを理解するには、JavaScript 式を固定文字列 STRING に置き換えることができます。

```
// Incorrect
STRING1
&cid=STRING2&bid=STRING3

// Correct
STRING1&cid=STRING2&bid=STRING3
```

**2 つ目の例：**

* 正しくない構文

  ```
  <%@ include option='NmsTracking_ClickFormula' %>
  <% // Parameters expected by Adobe Analytics
  var pattern = new RegExp("(vistaprint|entryUrl)", 'i')
  if( $(urlstring).match(pattern) && delivery.FCP == false )
  {%>&cid=<%= message.delivery.internalName%>&bid=<%= message.id.toString().toLowerCase()%>&SHPID=<%= message.recipient.factShopper.shopper_id %><% }
  
  %>
  ```

* 正しい構文

  ```
  <%@ include option='NmsTracking_ClickFormula' %><% // Parameters expected by Adobe Analytics
  var pattern = new RegExp("(vistaprint|entryUrl)", 'i')
  if( $(urlstring).match(pattern) && delivery.FCP == false )
  {%>&cid=<%= message.delivery.internalName%>&bid=<%= message.id.toString().toLowerCase()%>&SHPID=<%= message.recipient.factShopper.shopper_id %><% }
  
  %>
  ```

余分な改行がどこにあるかを理解するには、JavaScript 式を固定文字列 STRING に置き換えることができます。

```
// Incorrect
STRING1&cid=STRING2&bid=STRING3&SHPID=STRING4

// Correct
STRING1&cid=STRING2&bid=STRING3&SHPID=STRING4
```

+++

+++トラッキングログの取得が遅すぎる

インスタンスが直接トラッキングログを取得せず、遠く離れた Adobe Campaign Classic サーバーからログを取得する場合、そのログは remoteTracking スキーマで定義されている GetTrackingLogs SOAP 呼び出しを通じて取得されます。

serverConf.xml ファイルのオプションを使用すると、logCountPerRequest メソッドを使用して一度に取得されるログの数を設定できます。

logCountPerRequest のデフォルト値は 1000 です。場合によっては、値が小さすぎることがあります。指定できる値は 0～10000 の範囲です。

+++

+++トラッキングログを受信者にリンクできない

Adobe Campaign Classic では、ターゲットマッピングは、受信者スキーマに対する broadLog/trackingLog スキーマという点で一意であると見なされます。

![](assets/tracking-troubleshooting.png)

トラッキングワークフローでは、データとターゲティング ID を紐付けできないので、同じ trackingLog スキーマで複数のターゲティングスキーマを使用することはできません。

nms:recipient に標準で用意されているターゲットマッピングを使用しない場合は、次の方法をお勧めします。

* カスタムターゲティングディメンションを使用する場合は、nms:broadlog をテンプレート（nms:broadLogRcp、nms:broadLogSvc など）として使用してカスタム broadLog/trackingLog スキーマを作成する必要があります。

* OOB trackingLogRcp/broadLogRcp を使用する場合、ターゲティングディメンションは nms にする必要があり :recipient フィルタリングディメンションはカスタムスキーマにすることができます。

+++
