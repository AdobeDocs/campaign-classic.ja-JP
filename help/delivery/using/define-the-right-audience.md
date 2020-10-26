---
title: 適切なオーディエンスの定義
seo-title: 適切なオーディエンスの定義
page-status-flag: never-activated
uuid: a540efc7-105d-4c7f-a2ee-ade4d22b3445
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliveries-best-practices
discoiquuid: 0cbc4e92-482f-4dac-a1fb-b738e7127938
translation-type: ht
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: ht
source-wordcount: '478'
ht-degree: 100%

---


# 適切なオーディエンスの定義 {#define-the-right-audience}

ターゲット母集団が鍵です。リストを慎重に作成し、一般的な E メールクライアントやモバイルデバイスで E メールをテストし、E メールリストが最新のものであるか（不明なアドレスや古いアドレスが含まれていないこと）を確認します。また、もれのない検証サイクルを確立するために、配達確認を送信することもできます。

ターゲット母集団について詳しくは、[この節](../../delivery/using/steps-defining-the-target-population.md)を参照してください。

## 適切なオーディエンスのターゲティング {#target-the-right-audience}

コンテンツを用意できたら、メッセージの受信者を慎重に定義する必要があります。

配信を適切におこなうには、適切な受信者に最も関連性の高いパーソナライズされたコンテンツを送信する必要があります。Adobe Campaign では、精度の高いターゲットを作成できます。つまり、年齢、場所、購入履歴、以前の配信でリンクをクリックしたかどうかなどの条件に基づいて、受信者を選択できます。また、ターゲットの的確性を確認するために、テストプロファイル、コントロール母集団、シードアドレスを定義することもできます。

## ターゲットマッピング {#target-mappings}

Campaign Classic では、配信テンプレートはデフォルトで&#x200B;**受信者**&#x200B;をターゲットに設定します。Adobe Campaign では、必要に応じて、これ以外のターゲットマッピングも配信に使用できます。

例えば、ソーシャルネットワークからプロファイルを収集された訪問者や、情報サービスを購読している訪問者に配信できます。

これらのマッピングについては、[この節](../../delivery/using/selecting-a-target-mapping.md)を参照してください。

また、カスタマイズしたターゲットマッピングを作成して使用することもできます。詳しくは、[この節](../../configuration/using/target-mapping.md)を参照してください。

## 外部受信者 {#external-recipients}

データベースに保存されている受信者ではなく、外部ファイルに保存されている受信者に配信できます。詳しくは、[この節](../../delivery/using/steps-defining-the-target-population.md#selecting-external-recipients)を参照してください。

## 購読者への送信{#send-to-subscribers}

ニュースレターの購読者にメッセージを送信するには、対応する情報サービスの購読者を直接ターゲットにできます。詳しくは、[この節](../../delivery/using/managing-subscriptions.md#delivering-to-the-subscribers-of-a-service)を参照してください。


## テスト受信者とシードアドレス {#test-recipients-seed-addresses}

配信をテストするには、メインターゲットに送信する前に配達確認を使用します。

配達確認の受信者には適切な人を選択してください。配達確認の受信者は、メッセージのフォームとコンテンツを検証する必要があります。配達確認受信者を定義する手順については、[この節](../../delivery/using/steps-defining-the-target-population.md#selecting-the-proof-target)を参照してください。

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにして、メインターゲットに送信する前に配信テストをおこなう場合に使用します。詳しくは、[この節](../../delivery/using/about-seed-addresses.md)を参照してください。

## 重複したアドレス {#deduplicate-addresses}

重複した E メールアドレスがあると、ターゲットに影響する可能性があるので、E メールアドレスの重複を回避することが重要です。

* ターゲットが分割されている場合は、同じメッセージを複数回送信できます。

* 受信者がメッセージを受信後に購読解除しても、重複したプロファイルはその後もメッセージを受信します。

アドレスの重複は、送信レピュテーションを保護し、適切な強制隔離管理をおこなうためのものです。

詳しくは、[この使用例](../../workflow/using/deduplication.md#example--identify-the-duplicates-before-a-delivery)を参照してください。

## E メールアドレスのインデックス化 {#index-addresses}

このアプリケーションで使用する SQL クエリのパフォーマンスを最適化するには、データスキーマのメイン要素からインデックスを宣言します。

E メールアドレスにインデックスを追加する手順については、[この節](../../configuration/using/database-mapping.md#indexed-fields)を参照してください。
