---
title: 配信品質の重要なポイント
description: 配信品質を改善するための重要な点
page-status-flag: never-activated
uuid: 2681042b-3018-42ae-b252-2367b56616bd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: 6a394eeb-fbe1-4712-bb13-db5d7965fb73
translation-type: tm+mt
source-git-commit: cb2fb5a338220c54aba96b510a7371e520c2189e
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 98%

---


# 配信品質の重要なポイント{#deliverability-key-points}

Adobe Campaign の E メールの配信品質を最適化するために、次に示すベストプラクティスを使用することをお勧めします。配信品質の問題は、通常、インターネットサービスプロバイダーおよびメールサーバー管理者が実行するスパムに対する保護の指標に関係しています。

**E メール配信品質**&#x200B;とは、期待される品質のコンテンツとフォーマットを持つメッセージが、個人の E メールアドレスを通じて短時間で宛先に到達する能力を判断する一連の特性のことを指します。

これらの特性は、4 つの主要カテゴリに分類されます。
* データ品質
* メッセージおよびコンテンツ
* 送信インフラストラクチャ
* レピュテーション

これらにより、成功する E メール配信品質プログラムの基礎が形成されます。

**配信品質の割合**&#x200B;は、受信者に適切に配信された送信 E メールの数です。

配信品質の割合は、様々な要素に依存しますが、特に以下に依存します。
* インスタンスの適切な設定
* IP アドレスのレピュテーション
* ターゲットアドレスの品質
* 低い苦情率およびハードバウンス率
* メッセージのコンテンツ
* メッセージ認証（SPF、DKIM、DMARC）
* 送信者のレピュテーション

次に、良好な配信品質を実現するための重要なチェックポイントを示します。

## ネットワーク設定の確認 {#network-configuration}

スパム送信者は、実際の ID を隠蔽し、結果としてサーバーの識別を困難にします。大量の E メールを送信する場合は、サーバーの ID を隠そうとしない適切なネットワーク設定が不可欠です。

## 有効なアドレスへの送信 {#valid-addresses}

スパム送信者は、多くの場合、よくある姓と名のリストに基づくアドレスジェネレーターを使用します。また、メールサーバーから返信される技術的な通知をほとんど処理しません。無効なアドレス率が高いと、多くの場合はスパムと解釈されます。ダブルオプトインメカニズムおよび技術的なバウンスメッセージの効果的な処理により、これを回避することができます。

## 苦情数とバウンス率の低減 {#reduce-complaint-rates}

ISP は、通常、受け取ったメッセージをスパムとしてレポートする優れた手段を持っています。これにより、信頼性を欠くソースの特定が可能です。オプトアウトリクエストを直ちにおこない、所定のリストを定期的に使用し、ダブルオプトインシステムで同意を検証し、フィードバックループを実装することで、苦情率を減らすことができます。

## ハニーポットアドレスへの送信 {#honeypot-addresses}

ISP やその他の組織（[プロジェクトハニーポット](https://www.projecthoneypot.org/) Web サイトを参照）は、実際の個人としては存在しない、単にスパム送信者を欺くために作成されたメールボックスを使用します。このいわゆる「ハニーポット」アドレスは、スパムボットによって収集され、不正な送信者を捕らえるために Web で公開されます。ダブルオプトインメカニズムを使用することで、この種のアドレスがリストに追加されないようにします。サードパーティのリストを使用する場合、そのリストが信頼できる方法で管理されているか確認する必要があります。

## メッセージコンテンツの適応 {#message-content}

可能性は高くはありませんが、特定のメッセージのコンテンツがフィルターでスパムとして検出される場合があります。ある種の単語の使用、件名およびメッセージ内での感嘆符の使用は、スパムの明らかな兆候として読み取られます。スパム送信者は、アンチスパムフィルターによってテキストが自動的に分析されるのを防ぐために、テキストを画像で置き換えることも知られています。これに対応するために、画像の比率の高いメッセージ（HTML 形式）や添付された画像はブロックされます。

## レピュテーションに対する取り組み {#reputation}

スパム送信者は、長期的にレピュテーションを維持するためにプログラムされた配信をおこないます。スパム送信者は、ISP などによって課せられたベストプラクティスに対応するためにマーケティングプランの変更が必要な場合があり、レピュテーションのピーク後（ランプアップ）、通常の配信を設定します。

## ベストプラクティス{#best-practices}

Adobe Campaign での配信品質に関するベストプラクティスについて説明します。トピック間を移動してガイダンスを確認するには、次のリンクを使用してください。

<table>
<tr>
  <td>
    <a href="starting-new-platform.md">
      <img alt="開始" src="assets/do-not-localize/start.svg" width="60px"/>
    </a>
    <div>
      <a href="starting-new-platform.md">
    <strong>開始</strong>
    </a>
    </div>
    <p>
    <em>新しいプラットフォームの開始</em>
    <p>
  </td>
   <td>
    <a href="control-message-content.md">
      <img alt="設計" src="assets/do-not-localize/design.svg" width="60px"/>
    </a>
    <div>
      <a href="control-message-content.md">
    <strong>設計</strong>
    </a>
    </div>
    <p>
    <em>メッセージコンテンツの制御</em>
    <p>
  </td>
  <td>
    <a href="improve-reputation.md">
      <img alt="設計" src="assets/do-not-localize/check.svg" width="60px"/>
    </a>
    <div>
      <a href="improve-reputation.md">
    <strong>送信</strong>
    </a>
    </div>
    <p>
    <em>レピュテーションの向上</em>
    <p>
  </td>
</tr>
<tr>
  <td>
    <a href="technical-recommendations.md">
      <img alt="最適化" src="assets/do-not-localize/optimize.svg" width="60px"/>
    </a>
    <div>
      <a href="technical-recommendations.md">
    <strong>最適化</strong>
    </a>
    </div>
    <p>
    <em>技術的な推奨事項</em>
    <p>
  </td>
   <td>
    <a href="monitoring-deliverability.md">
      <img alt="確認" src="assets/do-not-localize/monitor.svg" width="60px"/>
    </a>
    <div>
      <a href="monitoring-deliverability.md">
    <strong>監視</strong>
    </a>
    </div>
    <p>
    <em>監視ツール</em>
    <p>
  </td>
  <td>
    <a href="deliverability-faq.md">
      <img alt="最適化" src="assets/do-not-localize/troubleshoot.svg" width="60px"/>
    </a>
    <div>
      <a href="deliverability-faq.md">
    <strong>トラブルシューティング</strong>
    </a>
    </div>
    <p>
    <em>問題の解決</em>
    <p>
  </td>
</tr>
</table>
