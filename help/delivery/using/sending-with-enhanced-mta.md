---
solution: Campaign Classic
product: campaign
title: Enhanced MTA を使用した Adobe Campaign Classic での送信
description: Adobe Campaign Enhanced MTA を使用した E メール送信の範囲と特異性について説明します。
audience: delivery
content-type: reference
topic-tags: sending-emails
translation-type: tm+mt
source-git-commit: d1b38acc5209a5c96ab7a35fe9640159141b110f
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 99%

---


# Enhanced MTA を使用した送信 {#sending-with-enhanced-mta}

**Adobe Campaign Enhanced MTA**（メール転送エージェント）は、アップグレードされた送信インフラストラクチャを提供し、配信品質、評判、スループット、レポート、バウンス処理、IP ランプアップ、接続設定管理を向上します。

Adobe Campaign Enhanced MTA は、スケーラビリティの向上、配信スループットの増加、より多くの E メールをより速く送信できるように実装されています。これは、インターネットサービスプロバイダーからのフィードバックに基づいて E メール送信設定をリアルタイムに変更する、新しいアダプティブ配信のテクニックを活用して達成されます。

>[!IMPORTANT]
>
>Adobe Campaign Enhanced MTA は、Campaign Classic のホスト型顧客またはハイブリッド型顧客のみ利用できます。Enhanced MTA を使用するために、Campaign Classic のオンプレミスインストールをアップグレードすることはできません。

2018 年 9 月以降に Campaign Classic インスタンスをプロビジョニングした場合は、Enhanced MTA を使用しています。その他の Campaign Classic の顧客の場合は、下記の[よくある質問](#enhanced-mta-faq)を参照してください。

Enhanced MTA の実装は、既存の Campaign 機能の一部に影響を与える場合があります。詳しくは、[Enhanced MTA の特異性](#enhanced-mta-impacts)を参照してください。

>[!NOTE]
>
>Adobe Campaign のエンドユーザーで、インスタンスが Enhanced MTA にアップグレード済みかどうかを確認する場合は、社内 Campaign 管理者にお問い合わせください。

## よくある質問 {#enhanced-mta-faq}

### 使用法とメリット

**Enhanced MTA とは何ですか？**

Adobe Campaign をアップグレードすると、SparkPost の商用 E メール MTA（**Momentum**）を実行する新しい MTA（メール転送エージェント）を使用できるようになります。

Momentum は、インボックスの最適な配信率を達成し維持するための高度なバウンス処理と自動配信品質最適化機能を含む、革新的で高パフォーマンスな MTA テクノロジーを提供します。<!--More than 37% of the world’s business email is sent using SparkPost’s MTA technology.-->

**メリットは何ですか？**

* Enhanced MTA を使用する Adobe Campaign クライアントは、<!--300%-->全体的なスループット速度が大幅に向上し、<!--90%+-->ソフトバウンスも大きく低下しています。
* Enhanced MTA は、最新の MTA テクノロジーを使用して、E メール配信の最適なスループット速度を提供します。
* 受け取ったフィードバックに即時に自動的に適応させることで、リアルタイムの配信データを使用した、より正確でインテリジェントな E メール配信も実現します。

**ネイティブの Adobe Campaign MTA と Enhanced MTA を同時に使用できますか？**

いいえ。インスタンスのアップグレード後は、E メール配信に Enhanced MTA のみ使用できます。

<!--
**Is there a fee associated with upgrading my instance to and subsequent use of the Enhanced MTA?**
No, there is no extra fee associated with the upgrade process to enable the use of the Enhanced MTA.

**When will the Enhanced MTA be available to me?**

* If you are new to Adobe Campaign Classic, you are already using the Enhanced MTA.

* For Adobe Campaign Classic existing customers, we’ve implemented a phased rollout that covers all hosted or partially hosted (hybrid) instances. If you’re not already using it, we’ll be contacting you in the near future with the dates and details for upgrading your Adobe Campaign Classic instances to the Enhanced MTA.
-->

### Enhanced MTA へのアップグレード

**Enhanced MTA にアップグレードするために必要なものは何ですか？**

2018 年 9 月以降に Campaign Classic インスタンスをプロビジョニングした場合は、Enhanced MTA を既に使用しているので、必要なアクションはありません。

その他すべてのホスト型または部分的にホストされている（ハイブリッド型）顧客の場合、Adobe Campaign チームから連絡が行き、移行の日付を調整し、移行に必要となる適切な手順の詳細を提供します。

>[!IMPORTANT]
>
>Enhanced MTA は、オンプレミスインストールでは使用できません。

**インスタンスを Enhanced MTA にアップグレードするプロセスとはどのようなものですか？**

ホストされるインスタンスのプロセス全体で、数分のダウンタイムが必要です。アドビは、アップグレード後 24 時間まで E メールのスループットと配信品質を監視し、E メール配信に与える影響を評価します。

問題が検出された場合、アドビは、インスタンスをネイティブ Adobe Campaign MTA にすばやく一時的に戻すことができます。

現在、Enhanced MTA は E メールチャネルにのみ影響します。プッシュ通知と SMS 配信は、引き続きネイティブ Campaign MTA を使用し、アップグレードの影響は受けません。

**Enhanced MTA にアップグレードした後、IP のウォーミングを再度おこなう必要がありますか？**

いいえ。アップグレードする際に新しい IP に切り替える必要がないので、ウォーミングがおこなわれた既存の E メール IP を引き続き使用できます。

**Enhanced MTA へのアップグレードは、現在進行中のキャンペーンや配信に影響を与えますか？**

インスタンスを Enhanced MTA にアップグレードする前に既に準備済みだった配信は、新しい MTA を正しく使用するために、準備をやり直す必要があります。

Adobe Campaign トランザクションメッセージ機能を使用する顧客の場合、E メールをトリガーする API 呼び出しは、アップグレードの非常に短いダウンタイム中にキューに入り、アップグレードの完了時に試行されます。

## Enhanced MTA の特異性 {#enhanced-mta-impacts}

### Enhanced MTA ヘッダー

最新の Campaign Classic インスタンスには、必要な Enhanced MTA ヘッダーをすべてのメッセージに追加するコードが含まれています。Adobe Campaign 19.1（ビルド 9032）以上を使用していて、このケースに当てはまらない場合は、（[serverConf.xml](../../installation/using/the-server-configuration-file.md#mta) ファイルの）マーケティングインスタンス設定に「useMomentum=true」パラメーターを追加する必要があります。

ただし、このコードを含まない古いインスタンスを使用している場合は、**[!UICONTROL Typology Rule for Enhanced MTAs]** という名前の新しいタイポロジルールを、Campaign インスタンス内のすべての既存タイポロジに追加する必要があります。
このルールは、Enhanced MTA へのアップグレードの一環としてインストールされた**[!UICONTROL タイポロジ]**&#x200B;パッケージによって追加されます。

>[!IMPORTANT]
>
>このタイポロジルールがタイポロジに表示される場合は、削除または変更をしないでください。E メール配信に悪い影響を与える可能性があります。

この&#x200B;**[!UICONTROL タイポロジ]**&#x200B;パッケージを Adobe Campaign マーケティングインスタンスにインストールする必要があります。

ハイブリッドクライアントの場合、Enhanced MTA へのアップグレードの一環として、Adobe Campaign チームからマーケティングインスタンスに&#x200B;**[!UICONTROL タイポロジ]**&#x200B;パッケージをインストールする方法に関する手順が提供されます。詳細な手順については、アカウント担当者にお問い合わせください。

>[!IMPORTANT]
>
>**[!UICONTROL タイポロジ]**&#x200B;パッケージのインストール方法に関する Adobe Campaign チームの指示に従う必要があります。従わない場合、E メールの送信に使用する IP に重大な問題が発生する場合があります。

タイポロジについて詳しくは、[この節](../../campaign/using/about-campaign-typologies.md)を参照してください。

### 新しい MX ルール

MX 管理配信のスループットルールは使用されなくなりました。Enhanced MTA には独自の MX ルールがあります。これにより、独自の E メールレピュテーション履歴および E メールを送信しているドメインから送信されるリアルタイムのフィードバックに基づいて、スループットをドメインごとにカスタマイズできます。

MX 設定について詳しくは、[この節](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

### バウンスの選定

Campaign **[!UICONTROL 配信ログの検証]**&#x200B;テーブルのバウンス選定は、**同期**&#x200B;配信の失敗エラーメッセージには使用されなくなりました。Enhanced MTA は、バウンスのタイプと選定を決定し、その情報を Campaign に返します。

>[!NOTE]
>
>Enhanced MTA は SMTP バウンスを選定し、その選定を Campaign バウンスの理由と選定にマッピングしたバウンスコードの形式で Campaign に返します。

バウンスの選定について詳しくは、[この節](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)を参照してください。

### 配信スループット

Campaign 配信スループットグラフでは、E メール受信者に対するスループットが表示されなくなります。グラフには Campaign から Enhanced MTA へのメッセージのリレーのスループット速度が表示されるようになりました。

配信スループットについて詳しくは、[この節](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。

### 有効期間

キャンペーン配信の有効期間設定は、Enhanced MTA で **3.5 日以下**&#x200B;に設定されている場合にのみ使用されます。Campaign で 3.5 日を超える値を定義した場合、その値は考慮されません。

例えば、Campaign で有効期間がデフォルト値の 5 日間に設定されている場合、ソフトバウンスメッセージは Enhanced MTA の再試行キューに入り、そのメッセージが Enhanced MTA に到達してから最大 3.5 日間再試行されます。この場合、Campaign に設定された値は使用されません。

メッセージが Enhanced MTA キューに置かれた日数が 3.5 日に達しても配信に失敗した場合は、タイムアウトになり、配信ログでのステータスは、**[!UICONTROL 送信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**&#x200B;に更新されます。

有効期間について詳しくは、[この節](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)を参照してください。

### DKIM 署名

DKIM（DomainKeys Identified Mail）E メール認証の署名は、Enhanced MTA によっておこなわれます。ネイティブの Campaign MTA による DKIM 署名は、Enhanced MTA アップグレードの一環として、ドメイン管理テーブル内で無効になります。DKIMの詳細については、『[Adobe配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html#authentication)』を参照してください。

### 配信成功レポート

E メール配信[ダッシュボード](../../delivery/using/delivery-dashboard.md)の&#x200B;**[!UICONTROL 概要]**&#x200B;表示では、**[!UICONTROL 成功]**&#x200B;のパーセンテージは 100%から開始し、配信[有効期間](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)を通してソフトバウンスとハードバウンスが Enhanced MTA から Campaign に返されるたびに、徐々に減少します。

実際、すべてのメッセージは、Campaign から Enhanced MTA へ正常に中継されるとすぐに、[送信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)に&#x200B;**[!UICONTROL 送信済み]**&#x200B;として表示されます。メッセージの[バウンス](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)が Enhanced MTA からキャンペーンに返されるまで、メッセージのステータスは変わりません。

Enhanced MTA からハードバウンスメッセージが返されると、ステータスが&#x200B;**[!UICONTROL 送信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わり、それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが減少します。

ソフトバウンスメッセージが Enhanced MTA から返されると、引き続き&#x200B;**[!UICONTROL 送信済み]**&#x200B;と表示され、**[!UICONTROL 成功]**&#x200B;の割合はまだ更新されません。ソフトバウンスメッセージは、配信の有効期間中ずっと[再試行](../../delivery/using/understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)されます。

* 有効期間の終了前に再試行が成功した場合、メッセージのステータスは&#x200B;**[!UICONTROL 送信済み]**&#x200B;のままで、**[!UICONTROL 成功]**&#x200B;のパーセンテージは変わりません。

* それ以外の場合は、ステータスが&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わり、それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが減少します。

そのため、有効期間の終了まで待って、最終的な&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージと、実際に&#x200B;**[!UICONTROL 送信済み]**&#x200B;および&#x200B;**[!UICONTROL 失敗]**&#x200B;となったメッセージの最終数を確認する必要があります。

<!--The fact that the Success percentage will go to 100% very quickly indicates that your instance has been upgraded to the Enhanced MTA.-->

### E メールフィードバックサービス（ベータ版） {#email-feedback-service}

E メールフィードバックサービス（EFS）機能を使用すると、フィードバックが Enhanced MTA（メッセージ転送エージェント）から直接取り込まれるので、各 E メールのステータスが正確にレポートされます。

>[!IMPORTANT]
>
>E メールフィードバックサービスは、現在ベータ版機能としてご利用いただけます。
>
>このベータプログラムへの参加を希望される場合は、[このフォーム](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4Rol2vQGupxItW9_BerXV6VUQTJPN1Q5WUI4OFNTWkYzQjg3WllUSDAxWi4u)に記入し、お問い合わせください。

配信の開始後、Campaign から Enhanced MTA にメッセージが正常に中継されると、**[!UICONTROL 成功]**&#x200B;のパーセンテージは変更されません。

<!--![](assets/efs-sending.png)-->

配信ログには、対象アドレスごとに&#x200B;**[!UICONTROL サービスプロバイダーで受信済み]**&#x200B;ステータスが表示されます。

<!--![](assets/efs-pending.png)-->

メッセージが対象プロファイルに実際に配信され、この情報が Enhanced MTA からリアルタイムでレポートされると、配信ログは、メッセージを受信した各アドレスの&#x200B;**[!UICONTROL 送信済み]**&#x200B;ステータスを示します。**[!UICONTROL 成功]**&#x200B;のパーセンテージは、成功した各配信に応じて増加します。

Enhanced MTA からハードバウンスメッセージが報告されると、ログのステータスが&#x200B;**[!UICONTROL サービスプロバイダーで受信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**<!-- and the **[!UICONTROL Bounces + errors]** percentage is increased accordingly-->に変更されます。

ソフトバウンスメッセージが Enhanced MTA から返されても、ログのステータスは変更されません（**[!UICONTROL サービスプロバイダーで受信済み]**）。[エラー理由](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)のみが更新されます<!-- and the **[!UICONTROL Bounces + errors]** percentage is increased accordingly-->。**[!UICONTROL 成功]**&#x200B;のパーセンテージは変更されません。その後、ソフトバウンスメッセージが配信[有効期間](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)中ずっと再試行されます。

* 有効期間の終了前に再試行が成功した場合、メッセージのステータスは&#x200B;**[!UICONTROL 送信済み]**&#x200B;に変わり、それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが増えます。

* それ以外の場合は、ステータスが&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わります。**[!UICONTROL 成功]**<!--and **[!UICONTROL Bounces + errors]** -->のパーセンテージは変更されません。

>[!NOTE]
>
>ハードバウンスとソフトバウンスについて詳しくは、[この節](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照してください。
>
>一時的な配信エラー後の再試行について詳しくは、[この節](../../delivery/using/understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)を参照してください。


次の表に、KPI の変更と、EFS 機能によって導入された送信ログのステータスを示します。

**E メールフィードバックサービスを使用する**

| 送信プロセスの手順 | KPI 概要 | 送信ログのステータス |
|--- |--- |--- |
| Campaign から Enhanced MTA にメッセージが正常に転送される | **[!UICONTROL 成功]**&#x200B;パーセンテージが表示されない（0%から開始） | サービスプロバイダーで受信済み |
| Enhanced MTA からハードバウンスメッセージが返される | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | 失敗 |
| ソフトバウンスメッセージが Enhanced MTA から返される | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | サービスプロバイダーで受信済み |
| ソフトバウンスメッセージの再試行が成功する | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが増加する | 送信済み |
| ソフトバウンスメッセージの再試行に失敗する | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | 失敗 |

**E メールフィードバックサービスを使用しない**

| 送信プロセスの手順 | KPI 概要 | 送信ログのステータス |
|--- |--- |--- |
| Campaign から Enhanced MTA にメッセージが正常に転送される | **[!UICONTROL 成功]**&#x200B;パーセンテージは 100%から開始 | 送信済み |
| Enhanced MTA からハードバウンスメッセージが返される | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;パーセンテージが減少する | 失敗 |
| ソフトバウンスメッセージが Enhanced MTA から返される | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | 送信済み |
| ソフトバウンスメッセージの再試行が成功する | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | 送信済み | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが増加する | 送信済み |
| ソフトバウンスメッセージの再試行に失敗する | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;パーセンテージが減少する | 失敗 |
