---
solution: Campaign Classic
product: campaign
title: 拡張MTAを使用したAdobe Campaign Classicでの送信
description: Adobe Campaign拡張MTAを使用した電子メール送信の範囲と特性について説明します。
audience: delivery
content-type: reference
topic-tags: sending-emails
translation-type: tm+mt
source-git-commit: 07ed17a093cb6fb2d7aae376325a127c61b1dcc2
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 3%

---


# 拡張MTAでの送信{#sending-with-enhanced-mta}

**Adobe Campaign拡張MTA** (Mail Transfer Agent)は、アップグレードされた送信インフラストラクチャを提供し、配信性、評価、スループット、レポート、バウンス処理、IPランプのアップ、接続設定管理を改善します。

拡張性の向上、配信のスループットの向上、より多くの電子メールをより速く送信できるように実装されています。 これは、インターネットサービスプロバイダーからのフィードバックに基づいて電子メール送信設定をリアルタイムに変更する、新しいアダプティブ配信のテクニックを活用して達成できます。

>[!IMPORTANT]
>
>Adobe Campaign拡張MTAは、Campaign Classicがホストするお客様またはハイブリッドのお客様のみ利用できます。 拡張MTAを使用するために、Campaign Classicのオンプレミスインストールをアップグレードすることはできません。

2018年9月以降にCampaign Classicインスタンスをプロビジョニングした場合は、拡張MTAを使用します。 その他のCampaign Classicのお客様の場合は、下記の[よくある質問](#enhanced-mta-faq)を参照してください。

拡張MTAの実装は、既存のキャンペーン機能の一部に影響を与える場合があります。 詳しくは、[拡張MTAの特殊性](#enhanced-mta-impacts)を参照してください。

## よくある質問 {#enhanced-mta-faq}

### 使用状況とメリット

**拡張MTAとは**

SparkPostの商用電子メールMTA **Moment**&#x200B;を実行する新しいMTA (Mail Transfer Agent)を使用するように、Adobe Campaignをアップグレードできるようになりました。

Momementは、インボックスの最適な配信率を達成し維持するための高度なバウンス処理と自動配信品質最適化機能を含む、革新的で高パフォーマンスなMTAテクノロジーを表しています。<!--More than 37% of the world’s business email is sent using SparkPost’s MTA technology.-->

**メリットは何ですか。**

* 拡張MTAを使用するAdobe Campaignクライアントは、<!--300%-->全体的なスループット速度が大幅に向上し、<!--90%+-->ソフトバウンスが大幅に低下しています。
* 拡張MTAは、最新のMTAテクノロジを使用して、電子メール配信の最適なスループット速度を提供します。
* 受け取ったフィードバックに即時に自動的に適応させることで、リアルタイムの配信データを使用した、より正確でインテリジェントな電子メール配信も実現します。

**ネイティブのAdobe CampaignMTAと拡張MTAを同時に使用できますか。**

いいえ。インスタンスのアップグレード後は、電子メール配信に拡張MTAのみを使用できます。

<!--
**Is there a fee associated with upgrading my instance to and subsequent use of the Enhanced MTA?**
No, there is no extra fee associated with the upgrade process to enable the use of the Enhanced MTA.

**When will the Enhanced MTA be available to me?**

* If you are new to Adobe Campaign Classic, you are already using the Enhanced MTA.

* For Adobe Campaign Classic existing customers, we’ve implemented a phased rollout that covers all hosted or partially hosted (hybrid) instances. If you’re not already using it, we’ll be contacting you in the near future with the dates and details for upgrading your Adobe Campaign Classic instances to the Enhanced MTA.
-->

### 拡張MTAへのアップグレード

**拡張MTAにアップグレードするために必要なもの**

2018年9月以降にCampaign Classicインスタンスをプロビジョニングした場合は、拡張MTAを既に使用しているので、操作は必要ありません。

その他すべてのホストまたは部分的にホストされる（ハイブリッド）お客様の場合、Adobe Campaignチームは移行の日付を調整するために声を上げ、移行に必要な適切な手順の詳細を提供します。

>[!IMPORTANT]
>
>拡張MTAは、オンプレミスインストールでは使用できません。

**インスタンスを拡張MTAにアップグレードするプロセスについて教えてください。**

ホストされるインスタンスのプロセス全体で、数分のダウンタイムが必要です。 Adobeは、アップグレード後24時間までEメールのスループットと配信品質を監視し、Eメール配信に与える影響を評価します。

問題が検出された場合、Adobeは、すばやく一時的にインスタンスをネイティブAdobe CampaignMTAに戻すことができます。

現在、拡張MTAは電子メールチャネルにのみ影響します。 プッシュ通知とSMS配信は、引き続きネイティブキャンペーンMTAを使用し、アップグレードの影響を受けません。

**拡張MTAにアップグレードした後、IPのウォーミングを再度行う必要がありますか。**

いいえ。アップグレードする際に新しいIPに切り替える必要がないので、既存の、温められた電子メールIPを引き続き使用できます。

**拡張MTAへのアップグレードは、現在進行中のキャンペーンや配信に影響を与えますか。**

拡張MTAを使用するようにインスタンスをアップグレードする前に準備された配信は、新しいMTAを正しく使用するために再準備する必要があります。

Adobe Campaignトランザクションメッセージング機能を使用するお客様の場合、トリガーへのAPI呼び出しと電子メールは、アップグレードの非常に短いダウンタイム中にキューに入れられ、アップグレードの完了時に試行されます。

## MTAの特殊性の強化{#enhanced-mta-impacts}

### MTAヘッダの強化

最新のCampaign Classicインスタンスには、必要な拡張MTAヘッダーをすべてのメッセージに追加するコードが含まれています。 Adobe Campaign19.1（ビルド9032）以上を使用していて、そうでない場合は、（[serverConf.xml](../../installation/using/the-server-configuration-file.md#mta)ファイル内で）マーケティングインスタンス設定に「useMoment=true」パラメーターを追加する必要があります。

ただし、このコードを含まない古いインスタンスを使用する場合は、拡張MTA用の&#x200B;**[!UICONTROL タイポロジルール]**という新しいタイポロジルールを、キャンペーンインスタンス内の既存のすべてのタイポロジに追加する必要があります。
このルールは、拡張MTAへのアップグレードの一環としてインストールされた**[!UICONTROL タイポロジ]**&#x200B;パッケージによって追加されます。

>[!IMPORTANT]
>
>このタイポロジルールがタイポロジに表示される場合は、削除または変更をしないでください。 そうしないと、電子メール配信に悪影響が及ぶ可能性があります。

この&#x200B;**[!UICONTROL タイポロジ]**&#x200B;パッケージをAdobe Campaignマーケティングインスタンスにインストールする必要があります。

ハイブリッドクライアントの場合、拡張MTAへのアップグレードの一環として、Adobe Campaignチームからマーケティングインスタンスに&#x200B;**[!UICONTROL Typology]**&#x200B;パッケージをインストールする方法に関する手順が提供されます。 詳細な手順については、アカウント担当者にお問い合わせください。

>[!IMPORTANT]
>
>**[!UICONTROL Typology]**&#x200B;パッケージのインストール方法に関するAdobe Campaignチームの指示に従う必要があります。 そうしないと、電子メールの送信に使用するIPに重大な問題が発生する場合があります。

類型について詳しくは、[このセクション](../../campaign/using/about-campaign-typologies.md)を参照してください。

### 新しいMXルール

MX管理配信のスループットルールは使用されなくなりました。 拡張MTAには独自のMXルールがあり、このMXルールを使用して、独自の履歴電子メールの評価に基づいて、また電子メールを送信するドメインからのリアルタイムフィードバックに基づいて、ドメイン別にスループットをカスタマイズできます。

MX 設定について詳しくは、[この節](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

### バウンスの資格

キャンペーン&#x200B;**[!UICONTROL 配信ログ資格]**&#x200B;テーブルのバウンスの資格は、**同期**&#x200B;配信エラーメッセージには使用されなくなりました。 Enhanced MTA は、バウンスのタイプと選定を決定し、その情報を Campaign に返します。

>[!NOTE]
>
>拡張MTAはSMTPバウンスの資格を得、その資格をキャンペーンバウンスの理由と資格にマッピングされたバウンスコードの形式でキャンペーンに返します。

バウンスの資格について詳しくは、[このセクション](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)を参照してください。

### 拡張MTAでの送信ステータス

電子メール配信[ダッシュボード](../../delivery/using/delivery-dashboard.md)の&#x200B;**[!UICONTROL 概要]**&#x200B;表示では、**[!UICONTROL 成功]**&#x200B;の開始は100%で終わり、配信[有効期間](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)を通じて徐々に減少し、ソフトバウンスとハードバウンスは拡張MTAから返されます。キャンペーン

実際、すべてのメッセージは、キャンペーンから拡張MTAへ正常に中継されると、[送信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)に&#x200B;**[!UICONTROL 送信済み]**&#x200B;として表示されます。 メッセージの[バウンス](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)が拡張MTAからキャンペーンに返されるまで、これらのメッセージはそのステータスのままです。

強化されたMTAからハードバウンスメッセージが報告されると、そのステータスが&#x200B;**[!UICONTROL 送信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わり、**[!UICONTROL 成功]**&#x200B;の割合がそれに応じて減少します。

ソフトバウンスメッセージが拡張MTAから返されると、**[!UICONTROL 送信済み]**&#x200B;と表示され、**[!UICONTROL 成功]**&#x200B;の割合はまだ更新されていません。 ソフトバウンスメッセージは、配信の有効期間全体で[再試行](../../delivery/using/understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)されます。

* 有効期間の終了前に再試行が成功した場合、メッセージのステータスは&#x200B;**[!UICONTROL 送信済み]**&#x200B;のままとなり、**[!UICONTROL 成功]**&#x200B;の割合は変わりません。

* それ以外の場合は、ステータスが&#x200B;**[!UICONTROL 失敗]**&#x200B;に変わり、それに応じて&#x200B;**[!UICONTROL 成功]**&#x200B;の割合が減少します。

その結果、有効期間の終わりまで待って、最終的な&#x200B;**[!UICONTROL 成功]**&#x200B;の割合と、実際に&#x200B;**[!UICONTROL 送信された]**&#x200B;および&#x200B;**[!UICONTROL 失敗した]**&#x200B;のメッセージの最終数を確認する必要があります。

<!--The fact that the Success percentage will go to 100% very quickly indicates that your instance has been upgraded to the Enhanced MTA.-->

### 配信スループット

キャンペーン配信のスループットグラフには、電子メール受信者に対してスループットが表示されなくなります。 このグラフは、キャンペーンから拡張MTAへのメッセージのリレーのスループット速度を示します。

配信のスループットの詳細については、[このセクション](../../reporting/using/global-reports.md#delivery-throughput)を参照してください。

### 有効期間

キャンペーン配信の有効期間設定は、拡張MTAで&#x200B;**3.5日以下**&#x200B;に設定されている場合にのみ使用されます。 キャンペーンが3.5日を超える値を定義した場合は、考慮されません。

例えば、有効期間がデフォルト値の5日間のキャンペーンに設定されている場合、ソフトバウンスメッセージは拡張MTAの再試行キューに入り、そのメッセージが拡張MTAに到達してから最大3.5日間再試行されます。 この場合、キャンペーンに設定された値は使用されません。

メッセージが3.5日間拡張MTAキューに入り、配信に失敗すると、タイムアウトになり、配信ログ内の&#x200B;**[!UICONTROL 送信済み]**&#x200B;から&#x200B;**[!UICONTROL 失敗]**&#x200B;にステータスが更新されます。

有効期間について詳しくは、[この節](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)を参照してください。

### DKIM署名

DKIM(DomainKeys Identified Mail)電子メール認証の署名は、拡張MTAによって行われます。 ネイティブの Campaign MTA による DKIM 署名は、Enhanced MTA アップグレードの一環としてドメイン管理テーブル内で無効になります。DKIMの詳細については、[このセクション](../../delivery/using/technical-recommendations.md#dkim)を参照してください。