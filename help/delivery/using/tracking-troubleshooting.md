---
solution: Campaign Classic
product: campaign
title: トラッキングのトラブルシューティング
description: この節では、Adobe Campaign Classic でのトラッキングの設定と実装に関するよくある質問について説明します。
audience: delivery
content-type: reference
topic-tags: tracking-messages
translation-type: ht
source-git-commit: efa36dc08ce4dd59805bb9eba63a4249e14609d7
workflow-type: ht
source-wordcount: '759'
ht-degree: 100%

---


# トラッキングのトラブルシューティング {#tracking-troubleshooting}

この節では、Adobe Campaign Classic でのトラッキングの設定と実装に関するよくある質問について説明します。

## トラッキングワークフローが失敗する {#tracking-workflow-failing}

トラッキングワークフローが失敗します。トラッキングファイル内の破損した行を検出するにはどうすれば良いですか？

>[!NOTE]
>
>Windows でのみ使用できます

破損したトラッキングログファイル .../nl6/var/&lt;instance_name>/redir/log/0x0000 ログにより、トラッキングワークフローが停止する可能性があります。破損した行を容易に検出して削除し、トラッキングワークフローを再開するには、次のコマンドを使用します。

### どのファイルに破損した行があるかわかっている場合：

このコマンドでは、0x00000000000A0000.log ファイル内にある破損した行が見つかります。他のファイルにある破損した行を見つけるには、同じ処理を各ファイルに適用する必要があります。

```
$ cd {install directory}/var/{instance name}/redir/log
$ cat 0x00000000000A0000.log | sed -nE '/^[[:alnum:]]{2}x[[:alnum:]]*\t[0-9T:\.-]*\t[0-9a-fA-F]*\t[0-9a-fA-F]*\t[0-9a-fA-F]*\t[[:alnum:]]*\t[[:alnum:]-]*\t[[:print:]]*\t[[:print:]]*\t[[:print:]]*\t([0-9a-fA-F\.:]*|[0-9a-fA-F\.:]*\t[[:print:]]*|[0-9a-fA-F\.:]*,[[:print:]]*)$/!p'
```

その後、トラッキングワークフローを停止し、破損した行を削除して、ワークフローを再度開始できます。

### 破損した行がどのファイルにあるかわからない場合：

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

## トラッキングリンクが断続的に失敗する {#tracking-links-fail-intermittently}

トラッキングリンクにアクセスしようとすると、次のメッセージが表示されます。

`Requested URL '/r/ id=h787bc0,281a4d8,281a4da&amp;p1=1' cannot be found`

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

1. &lt;deliveryID>.xml ファイルがマシン上の .../nl6/var/&lt;instance_name>/redir/url/&lt;YYYY> ディレクトリ（YYYY は配信の年）に存在するかどうかを手動で確認します。

1. &lt;trackingUrlId> が &lt;deliveryID>.xml ファイル内に見つかるかどうかを手動で確認します。

1. 関連する deliveryID 配信内に broadlogID が存在するかどうかを手動で確認します。

1. .../nl6/var/&lt;instance_name>/redir/url/year ディレクトリにある &lt;deliveryID>.xml ファイルのパーミッションを確認します。

   リクエストされたリンクをリダイレクトするために Apache がトラッキング URL を読み取れるように、少なくともパーミッションは 644 が必要です。

## NmsTracking_Pointer オプションの更新 {#updating-option}

NmsTracking_Pointer オプションを更新する場合は、次の手順に従います。

1. トラッキングワークフローを停止します。

1. trackinglogd サービスを停止します。

1. NmsTracking_Pointer オプションを必要な値に更新します。

1. trackinglogd サービスを再度開始します。

1. トラッキングワークフローを再度開始します。

## トラッキングが一部の webMail で動作しない {#webmail}

クリックトラッキングの数式をカスタマイズして、カスタムの Adobe Analytics トラッキングの数式を指定できます。

このようなカスタマイズは、不要な改行文字を追加しないように、注意しておこなう必要があります。JavaScript 式以外に存在する改行文字はすべて、最終式に含まれます。

この種の追加の改行文字がトラッキング URL に含まれている場合、一部の webMail（AOL、GMail など）で問題が発生します。

**1 つ目の例：**

* 正しくない構文

   ```
   <%@ include option='NmsTracking_ClickFormula' %><% // Parameters expected by Adobe-Genesis
   var pattern = new RegExp("(nl611\.test15|google\.com)", 'i')
   if( $(urlstring).match(pattern) && delivery.FCP == false )
   {
   %>
   &cid=<%= message.delivery.internalName %>&bid=<%= message.id.toString().toLowerCase() %><% } %>
   ```

* 正しい構文

   ```
   <%@ include option='NmsTracking_ClickFormula' %><% // Parameters expected by Adobe-Genesis
   var pattern = new RegExp("(nl611\.test15|google\.com)", 'i')
   if( $(urlstring).match(pattern) && delivery.FCP == false )
   {
   %>&cid=<%= message.delivery.internalName %>&bid=<%= message.id.toString().toLowerCase() %><% } %>
   ```

余分な改行がどこにあるかを理解するために、Javascript 式を固定文字列 STRING で置き換えることができます。

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
   <% // Parameters expected by Adobe-Genesis
   var pattern = new RegExp("(vistaprint|entryUrl)", 'i')
   if( $(urlstring).match(pattern) && delivery.FCP == false )
   {%>&cid=<%= message.delivery.internalName%>&bid=<%= message.id.toString().toLowerCase()%>&SHPID=<%= message.recipient.factShopper.shopper_id %><% }
   
   %>
   ```

* 正しい構文

   ```
   <%@ include option='NmsTracking_ClickFormula' %><% // Parameters expected by Adobe-Genesis
   var pattern = new RegExp("(vistaprint|entryUrl)", 'i')
   if( $(urlstring).match(pattern) && delivery.FCP == false )
   {%>&cid=<%= message.delivery.internalName%>&bid=<%= message.id.toString().toLowerCase()%>&SHPID=<%= message.recipient.factShopper.shopper_id %><% }
   
   %>
   ```

余分な改行がどこにあるかを理解するために、Javascript 式を固定文字列 STRING で置き換えることができます。

```
// Incorrect
STRING1&cid=STRING2&bid=STRING3&SHPID=STRING4

// Correct
STRING1&cid=STRING2&bid=STRING3&SHPID=STRING4
```

## トラッキングログの取得が遅すぎる {#slow-retrieval}

インスタンスが直接トラッキングログを取得せず、遠く離れた Adobe Campaign Classic サーバーからログを取得する場合、そのログは remoteTracking スキーマで定義されている GetTrackingLogs SOAP 呼び出しを通じて取得されます。

serverConf.xml ファイルのオプションを使用すると、logCountPerRequest メソッドを使用して一度に取得されるログの数を設定できます。

logCountPerRequest のデフォルト値は 1000 です。場合によっては、値が小さすぎることがあります。指定できる値は 0～10000 の範囲です。

## トラッキングログを受信者にリンクできない {#link-recipients}

Adobe Campaign Classic では、ターゲットマッピングは、受信者スキーマに対する broadLog/trackingLog スキーマという点で一意であると見なされます。

![](assets/tracking-troubleshooting.png)

トラッキングワークフローでは、データとターゲティング ID を調整できないので、同じ trackingLog スキーマで複数のターゲティングスキーマを使用することはできません。

nms:recipient で標準のターゲットマッピングを使用しない場合は、次の方法を使用することをお勧めします。

* カスタムのターゲティングディメンションを使用する場合、nms:broadlog をテンプレートとして使用するカスタム broadLog/trackingLog スキーマを作成する必要があります（例：nms:broadLogRcp、nms:broadLogSvc など）。

* OOB trackingLogRcp/broadLogRcp を使用する場合、ターゲティングディメンションは nms:recipient である必要があります。フィルタリングディメンションは、カスタムスキーマでも構いません。
