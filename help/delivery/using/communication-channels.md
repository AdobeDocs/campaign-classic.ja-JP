---
title: 通信チャネル
seo-title: 通信チャネル
description: 通信チャネル
seo-description: null
page-status-flag: never-activated
uuid: 42975431-64c9-4ecb-98ed-b1f9b13c157e
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: about-deliveries-and-channels
discoiquuid: 2e2d1134-9b83-4ada-b74f-c3842a0cf044
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: c1f7ff6a281c2830ac23ad995b750dc09ade5e92
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 96%

---


# 通信チャネル{#communication-channels}

Adobe Campaign では、E メール、SMS、LINE メッセージ、プッシュ通知およびダイレクトメールを含むクロスチャネルキャンペーンを送信し、各種の専用[レポート](../../reporting/using/delivery-reports.md)を使用してそれらの有効性を評価できます。これらのメッセージは、デザインし、配信を介して送信します。また、受信者ごとにパーソナライズすることができます。

コア機能には、ターゲティング、メッセージの定義とパーソナライゼーション、通信の実行、関連する運用可能なレポートなどがあります。機能への主なアクセスポイントは、配信ウィザードです。ここから、Adobe Campaign で提供されるいくつかの機能にアクセスします。

>[!NOTE]
>
>Adobe Campaign は、配信品質を監視し、E メール送信を最適化するための一連のツールを備えています。詳しくは、[配信品質の概要](https://docs.adobe.com/content/help/ja-JP/campaign-classic/using/sending-messages/deliverability-management/about-deliverability.html)および[配信品質の管理](../../delivery/using/about-deliverability.md)を参照してください。

配信の送信は、ワークフローのプロセスの中で配信を準備または送信することによって自動化できます。ワークフロー内の配信タイプのアクティビティについて詳しくは、[この節](../../workflow/using/about-action-activities.md)を参照してください。

Adobe Campaign は次の配信チャネルを提供します。

1. **E メールチャネル**：E メール配信によって、ターゲット母集団にパーソナライズされた E メールを送信できます。[E メールチャネルについて](../../delivery/using/about-email-channel.md)を参照してください。
1. **ダイレクトメールチャネル**：ダイレクトメール配信によって、ターゲット母集団に関するデータを含む抽出ファイルを生成できます。[ダイレクトメールチャネルについて](../../delivery/using/about-direct-mail-channel.md)を参照してください。
1. **モバイルチャネル**：モバイルチャネル経由の配信によって、ターゲット母集団にパーソナライズされた SMS または LINE メッセージを送信できます。[SMS チャネル](../../delivery/using/sms-channel.md)を参照してください。
1. **モバイルアプリケーションチャネル**：モバイルアプリ配信では通知を iOS システムおよび Android システムに送信できます。[モバイルアプリチャネル](../../delivery/using/about-mobile-app-channel.md)の章を参照してください。

   その他のチャネルについて詳しくは、[このページ](../../delivery/using/communication-channels.md#other-channels)を参照してください。

   >[!NOTE]
   >
   >複数のチャネルを使用できるかどうかは、パッケージによって異なります。使用許諾契約書を確認してください。

配信は、**オンライン**（E メール、いずれかのモバイルチャネルおよびプッシュ通知）および&#x200B;**オフライン**（ダイレクトメールチャネル）で実行できます。

チャネルに応じて、配信モードは次のようになります。

* Adobe Campaign 経由の直接一括配信（E メールチャネルのデフォルトモード）。
* 配信ウィザードで生成された出力ファイルを受け取る専門オペレーター経由の外部配信（ダイレクトメールチャネルのデフォルトモード）。

外部アカウントは、**[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;ノードで設定できます。この設定は、エキスパートユーザーのみが実行するようにしてください。

## E メール配信 {#email-deliveries}

[E メールチャネル](../../delivery/using/about-email-channel.md)は、Adobe Campaign のコアチャネルの 1 つで、パーソナライズされた E メールをスケジュールし、特定のターゲットに送信できます。

異なるタイプの E メールを送信できます。

* 単一送信 E メール：定義したターゲットに 1 回送信できる E メール。これらは、通常、1 回だけ準備されて送信される特定のコンテンツ（ニュースレター、プロモーション E メールなど）をプロモーションするために使用します。
* 繰り返し E メール：キャンペーンで、同じ E メールを定期的に送信し、各送信とそのレポートを定期的に集計します。同じ E メールが送信されますが、通常は、送信日の適格なターゲットに基づいて、異なるターゲットに送信されます。一般的な例に誕生日の E メールがあります。詳しくは、[繰り返し配信](../../workflow/using/recurring-delivery.md)を参照してください。
* トランザクション E メール：顧客の行動に基づいてトリガーされる単一の E メール。[トランザクションメッセージ](../../message-center/using/about-transactional-messaging.md)を参照してください。

配信の使用と推奨事項については、Campaign の[配信のベストプラクティス](https://docs.campaign.adobe.com/doc/AC/getting_started/JA/deliveryBestPractices.html)を参照してください。

配信のタイプについて詳しくは、[この節](../../delivery/using/types-of-deliveries.md)を参照してください。

## モバイル配信 {#mobile-deliveries}

Adobe Campaign では、モバイルデバイスに [SMS](../../delivery/using/sms-channel.md) および [LINE](../../delivery/using/line-channel.md) メッセージを配信できます。

SMS メッセージの場合、テキスト形式のメッセージのみを作成、変更およびパーソナライズできます。SMS メッセージは、送信前にプレビューすることもできます。

LINE メッセージの場合は、テキストまたは画像とリンクを送信できます。

SMS または LINE メッセージを携帯電話に配信するには、以下が必要です。

* **[!UICONTROL モバイル（SMS）]**&#x200B;チャネルまたは **[!UICONTROL LINE]** チャネルに設定された外部アカウント。
* この外部アカウントに適切にリンクされた SMS または LINE 配信テンプレート。

## プッシュ通知{#push-notifications}

Adobe Campaign では、専用アプリを通じて iOS および Android モバイルデバイスにパーソナライズおよびセグメント化された[プッシュ通知](../../delivery/using/about-mobile-app-channel.md)を送信できます。設定および統合手順を実行すると、iOS および Android 配信を作成および送信できます。画像またはビデオを含むリッチな通知をデザインすることもできます。

## ダイレクトメール{#direct-mail}

[ダイレクトメール](../../delivery/using/about-direct-mail-channel.md)は、ダイレクトメールプロバイダーから求められるファイルのパーソナライズおよび生成を可能にするオフラインチャネルです。ダイレクトメールにより、カスタマージャーニーにオンラインチャネルとオフラインチャネルを混在させることができます。

オンラインチャネルでは、メッセージ（E メール、SMS、モバイルアプリ配信など）を作成し、Adobe Campaign から直接オーディエンスにメッセージを送信できます。オフラインチャネルの場合は異なります。ダイレクトメール配信を準備すると、Adobe Campaign により、すべてのターゲットプロファイルと選択した連絡先情報（例えば、郵便の宛先）を含むファイルが生成されます。その後、このファイルを実際の発送処理をおこなうダイレクトメールプロバイダーに送信できます。

## その他のチャネル {#other-channels}

Adobe Campaign には、エージェンシーや電話の配信テンプレートが用意されており、外部配信の作成に使用できます。これらのチャネルを使用する場合、出力ファイルを処理するための専用の方法を設定することになります。設定の手順は、[ダイレクトメールチャネル](../../delivery/using/about-direct-mail-channel.md)の場合と同様です。

さらに、「その他」タイプの配信は、プロセスを実行しない特定の専門的なテンプレートを使用します。これによって、Adobe Campaign プラットフォーム以外で実行されたマーケティングアクションを管理できます。

このチャネルには特定のメカニズムはありません。これは汎用チャネルで、Adobe Campaign で使用できる他のコミュニケーションチャネルと同様に、独自の外部アカウントルーティングオプション、配信テンプレートタイプ、キャンペーンワークフローアクティビティがあります。

このチャネルは、説明的な目的のためにのみ設計されています。例えば、Adobe Campaign以外のツールで実行されたキャンペーンのターゲットのトレースを保持する配信を定義する場合などです。
