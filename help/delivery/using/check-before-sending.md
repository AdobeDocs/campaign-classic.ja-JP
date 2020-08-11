---
title: 送信前に確認
seo-title: 送信前に確認
page-status-flag: never-activated
uuid: a540efc7-105d-4c7f-a2ee-ade4d22b3445
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliveries-best-practices
discoiquuid: 0cbc4e92-482f-4dac-a1fb-b738e7127938
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5e6ecd636ee0b2199808c03b2fd898a194f0c1ea
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 80%

---


# 送信前にすべてのチェックを実行する {#perform-all-checks}

メッセージを用意できたら、そのコンテンツがすべてのデバイス上で正しく表示されることを確認します。また、パーソナライゼーションの誤りや壊れたリンクなどのエラーがないことも確認します。

メッセージを送信する前に、配信パラメーターと配信設定に矛盾がないことも確認します。

## 検証が重要な理由 {#validation-is-key}

配信を送信する前に、配信を本当に届けたい受信者にメッセージが届くかどうかを確認する必要があります。そのためには、メッセージのコンテンツと配信パラメーターを検証します。

この手順により、メインターゲットに配信する前に、エラーを検出して修正できます。

配信を検証する手順は、この節 [で説明します](../../delivery/using/steps-validating-the-delivery.md)。

## 受信ボックスレンダリング {#inbox-and-email-rendering}

受信ボックスレンダリングを使用すると、主な E メールクライアントでメッセージをプレビューし、コンテンツとレピュテーションをスキャンし、受信者がどのようにメッセージを読むかを確認できます。

**ヒント**:

* 送信されたメッセージは、Web メールやメッセージサービス、モバイルなど、メッセージを受信する様々なコンテキストで表示できます。

* 受信ボックスレンダリング機能は、E メールキャンペーンで E メールが主要な ISP（インターネットサービスプロバイダー）および Web メールサービスのフィルターを無事通過できるかどうかを確認するために非常に重要です。このようなツールは、テスト用受信ボックスのネットワークに E メールのプリフライトコピーを送信します。これにより、メッセージがこれらのサービスでどのように表示（レンダリング）されるかを確認できます。このツールには、迅速な識別および修正に役立つレポートとコード修正オプションも含まれており、配信品質を向上させることができます。

Learn more [in this section](../../delivery/using/inbox-rendering.md).

## 配達確認メッセージ {#proof-messages}

配達確認を送信すると、オプトアウトリンクやミラーページ、その他のリンクの確認、メッセージの検証、画像の表示の確認、エラーの検出などをおこなうことができます。また、様々なデバイス上でデザインとレンダリングを確認することもできます。

Learn more [in this section](../../delivery/using/steps-validating-the-delivery.md#sending-a-proof).

## 配信の A/B テストの設定 {#a-b-testing-deliveries}

E メール配信で使用するコンテンツがいくつかある場合は、A/B テストを使用して、ターゲット母集団に与える影響が最も大きいコンテンツを見つけることができます。

**ヒント**:

* 一部の受信者に異なるバージョンを送信する

* 成功率が最も高い成功率のものを選択し、それを残りのターゲットに送信します。

Learn more [in this section](../../workflow/using/a-b-testing.md).

## メッセージを確実に配信する {#make-sure-your-message-is-delivered}

最後の手順です。メッセージが実際に関連性の高い受信者に配信されるように Adobe Campaign Classic の機能を最大限に活用します。

### 検証プロセスの実行

Adobe Campaign のオペレーターやグループが関与する包括的な検証プロセスを定義して、ターゲットとメッセージコンテンツの両方を検証できます。これにより、キャンペーンの様々なプロセスを完全に監視および制御できます。ターゲット設定、コンテンツ、予算、抽出、配達確認の送信を行います。 ユーザーは、それぞれの権限に応じた通知を受け取ります。また、配達確認を受信したり、メッセージを検証または却下することもできます。Learn more [in this section](../../campaign/using/marketing-campaign-approval.md#approval-process).

### ウェーブの使用

ウェーブを使用すると、送信するボリュームを徐々に増やせます。これにより、メッセージがスパムとしてマークされたり、1日あたりのメッセージ数を制限したい場合を回避できます。 ウェーブを使用すると、一度に大量のメッセージを送信するのではなく、配信をいくつかのバッチに分割できます。Learn more [in this section](../../delivery/using/steps-sending-the-delivery.md#sending-using-multiple-waves).

### メッセージの優先順位

配信の優先順位レベルを設定すると、配信の送信順を指定できます。それには、次の手順に従います。

1. 配信プロパティを編集し、「**[!UICONTROL 配信]**」タブを選択します。

1. 「**[!UICONTROL 非常に低い]**」から「**[!UICONTROL 非常に高い]**」までのスケール上で、この配信の優先順位レベルを定義します。

>[!NOTE]
>
>配信内からメッセージを送信する順序を定義することはできません。

### IPアフィニティの設定

アウトバウンド SMTP トラフィックの制御を強化するには、各アフィニティに使用できる IP アドレスを定義してアフィニティを管理します。この設定により、コンピューターや出力アドレスに配信される E メールの数を制限できます。例えば、1 つの国またはサブドメインにつき 1 つのアフィニティを使用できます。さらに、1 つの国につき 1 つのタイポロジを作成し、各アフィニティを各国の対応するタイポロジに関連付けることができます。

次の操作をおこなうことができます。

* serverConf.xml 設定ファイルに IP アフィニティを定義します。[詳細情報](../../installation/using/configuring-campaign-server.md#managing-outbound-smtp-traffic-with-affinities)

* IPAffinity 要素ごとに、使用可能な IP アドレスを宣言します。[詳細情報](../../installation/using/email-deliverability.md#list-of-ip-addresses-to-use)

* In the [typology](../../campaign/using/about-campaign-typologies.md) of your choice, use the **[!UICONTROL Managing affinities with IP addresses]** field to link deliveries to the delivery server (MTA) which manages the said affinity. [詳細情報](../../campaign/using/applying-rules.md#control-outgoing-smtp-traffic)。

* E メールを送信したら、配信の送信元 IP アドレスをヘッダーで確認します。ヘッダー情報は E メール管理者から入手できます。

>[!NOTE]
>
>これらの手順のほとんどは外部ユーザーのみ実行できます。

### タイポロジの使用

タイポロジルールを使用すると、特定の条件に基づいてターゲットの一部を除外できます。このテストにより、企業のコミュニケーションポリシーに準拠しつつ、顧客のニーズと期待に応える最適なメッセージを送信できます。例えば、ニュースレターの対象から未成年の受信者を除外できます。詳し [くは、この例を参照してください](../../campaign/using/filtering-rules.md)。

### ファイルを添付しない

現在も添付ファイルを媒介としたマルウェアの拡散は後を絶ちません。一括送信の場合は特に注意が必要です。ドキュメントを添付するのではなく、ドキュメントへのセキュアなリンクを渡します。これにより、セキュリティレベルを引き上げて意図しない再配布を防ぐことができます。また、受信側の E メールゲートウェイでサイズ超過やセキュリティ上の理由によりメッセージが拒否される可能性を大幅に減らすこともできます。
