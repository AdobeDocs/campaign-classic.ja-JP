---
product: campaign
title: Enhanced MTA を使用した Adobe Campaign Classic での送信
description: Adobe Campaign Enhanced MTA を使用したメール送信の範囲と特異性について説明します。
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Email
exl-id: 58cc23f4-9ab0-45c7-9aa2-b08487ec7e91
source-git-commit: dbbc5d9f354357e5ca13eaeffddf67865480070d
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 100%

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

Adobe Campaign をアップグレードして、SparkPost の商用メール MTA（**Momentum**）を実行する新しい MTA（メール転送エージェント）を使用できるようになりました。

Momentum は、インボックスの最適な配信率を達成し維持するための高度なバウンス処理と自動配信品質最適化機能を含む、革新的で高パフォーマンスな MTA テクノロジーを提供します。<!--More than 37% of the world's business email is sent using SparkPost's MTA technology.-->

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

* For Adobe Campaign Classic existing customers, we've implemented a phased rollout that covers all hosted or partially hosted (hybrid) instances. If you're not already using it, we'll be contacting you in the near future with the dates and details for upgrading your Adobe Campaign Classic instances to the Enhanced MTA.
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

Adobe Campaign トランザクションメッセージ機能を使用する顧客の場合、E メールをトリガーする API 呼び出しは、アップグレードの非常に短いダウンタイム中にキューに入り、アップグレードの完了時に試行されます。

## Enhanced MTA の特異性 {#enhanced-mta-impacts}

### 新しい MX ルール

MX 管理配信のスループットルールは使用されなくなりました。Enhanced MTA には独自の MX ルールがあり、独自のメールレピュテーション履歴およびメールの送信に使用するドメインからのリアルタイムのフィードバックに基づいて、スループットをドメインごとにカスタマイズできます。

MX 設定について詳しくは、[この節](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

### バウンスの選定

Campaign **[!UICONTROL 配信ログの検証]**&#x200B;テーブルのバウンス選定は、**同期**&#x200B;配信の失敗エラーメッセージには使用されなくなりました。Enhanced MTA は、バウンスのタイプと選定を決定し、その情報を Campaign に返します。

>[!NOTE]
>
>Enhanced MTA は SMTP バウンスを選定し、その選定を Campaign バウンスの理由と選定にマッピングしたバウンスコードの形式で Campaign に返します。

バウンスの選定について詳しくは、[この節](understanding-delivery-failures.md#bounce-mail-qualification)を参照してください。

### 配信スループット

Campaign 配信スループットグラフでは、E メール受信者に対するスループットが表示されなくなります。グラフには Campaign から Enhanced MTA へのメッセージのリレーのスループット速度が表示されるようになりました。

配信スループットについて詳しくは、[この節](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。

### 再試行

配信の再試行設定は、Campaign では使用されなくなりました。ソフトバウンスの再試行とその間隔は、メッセージの電子メールドメインから返されるバウンス応答のタイプと重大度に基づいて、Enhanced MTA が決定します。

再試行について詳しくは、[この節](steps-sending-the-delivery.md#configuring-retries)を参照してください。

### 有効期間

キャンペーン配信の有効期間設定は、Enhanced MTA で **3.5 日以下**&#x200B;に設定されている場合にのみ使用されます。Campaign で 3.5 日を超える値を定義した場合、その値は考慮されません。

例えば、Campaign で有効期間がデフォルト値の 5 日間に設定されている場合、ソフトバウンスメッセージは Enhanced MTA の再試行キューに入り、そのメッセージが Enhanced MTA に到達してから最大 3.5 日間再試行されます。この場合、Campaign に設定された値は使用されません。

メッセージが Enhanced MTA キューに置かれた日数が 3.5 日に達しても配信に失敗した場合は、タイムアウトになり、配信ログでのステータスは、**[!UICONTROL 送信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**&#x200B;に更新されます。

有効期間について詳しくは、[この節](steps-sending-the-delivery.md#defining-validity-period)を参照してください。

### DKIM 署名

DKIM（DomainKeys Identified Mail）E メール認証の署名は、Enhanced MTA によっておこなわれます。ネイティブの Campaign MTA による DKIM 署名は、Enhanced MTA アップグレードの一環として、ドメイン管理テーブル内で無効になります。DKIM の詳細については、[アドビの配信品質のベストプラクティスガイド](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#authentication)を参照してください。

### 配信成功レポート

E メール配信[ダッシュボード](delivery-dashboard.md)の&#x200B;**[!UICONTROL 概要]**&#x200B;表示では、**[!UICONTROL 成功]**&#x200B;のパーセンテージは 100%から開始し、配信[有効期間](steps-sending-the-delivery.md#defining-validity-period)を通してソフトバウンスとハードバウンスが Enhanced MTA から Campaign に返されるたびに、徐々に減少します。

実際、すべてのメッセージは、Campaign から Enhanced MTA へ正常に中継されるとすぐに、[送信ログ](delivery-dashboard.md#delivery-logs-and-history)に&#x200B;**[!UICONTROL 送信済み]**&#x200B;として表示されます。メッセージの[バウンス](understanding-delivery-failures.md#delivery-failure-types-and-reasons)が Enhanced MTA からキャンペーンに返されるまで、メッセージのステータスは変わりません。

Enhanced MTA からハードバウンスメッセージが返されると、ステータスが&#x200B;**[!UICONTROL 送信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わり、それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが減少します。

ソフトバウンスメッセージが Enhanced MTA から返されると、引き続き&#x200B;**[!UICONTROL 送信済み]**&#x200B;と表示され、**[!UICONTROL 成功]**&#x200B;の割合はまだ更新されません。ソフトバウンスメッセージは、配信の有効期間中ずっと[再試行](understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)されます。

* 有効期間の終了前に再試行が成功した場合、メッセージのステータスは&#x200B;**[!UICONTROL 送信済み]**&#x200B;のままで、**[!UICONTROL 成功]**&#x200B;のパーセンテージは変わりません。

* それ以外の場合は、ステータスが&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わり、それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが減少します。

そのため、有効期間の終了まで待って、最終的な&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージと、実際に&#x200B;**[!UICONTROL 送信済み]**&#x200B;および&#x200B;**[!UICONTROL 失敗]**&#x200B;となったメッセージの最終数を確認する必要があります。

次の表に、送信プロセスの様々な手順と、対応する KPI および送信ログのステータスを示します。

| 送信プロセスの手順 | KPI 概要 | 送信ログのステータス |
|--- |--- |--- |
| Campaign から Enhanced MTA にメッセージが正常に転送される | **[!UICONTROL 成功]**&#x200B;パーセンテージは 100%から開始 | 送信済み |
| Enhanced MTA からハードバウンスメッセージが返される | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが減少する | 失敗 |
| ソフトバウンスメッセージが Enhanced MTA から返される | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | 送信済み |
| ソフトバウンスメッセージの再試行が成功する | **[!UICONTROL 成功]**&#x200B;のパーセンテージに変更はない | 送信済み | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが増加する | 送信済み |
| ソフトバウンスメッセージの再試行に失敗する | それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;のパーセンテージが減少する | 失敗 |

