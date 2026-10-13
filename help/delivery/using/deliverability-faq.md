---
product: campaign
title: Adobe Campaign Classic で配信品質を管理する際の重要なポイント
description: Adobe Campaign で配信品質を管理する際に確認すべき重要なポイントを学ぶ
feature: Deliverability, Troubleshooting
role: User
exl-id: f94897c1-b44c-4100-ac50-a89b13fa6f2f
TQID: 'https://experienceleague.adobe.com/ZRai7Bd-IRaWUQQmkuUYwXhNXp2BI-B4k-4cGq1k6uk'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
  - id: b631758a-142d-425f-b9aa-f756d85cb979
    internal-label: Campaign Email Designer
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
    internal-label: Prepare and test messages
  - id: 63876777-85c3-57e1-a2da-81f02956c63c
    internal-label: Deliverability
  - id: a4671286-a59f-47e3-b97b-90627a1977d5
    internal-label: Communication channels
subfeature_v2:
  - id: e95a583b-fcfa-4524-8666-46a29c828119
    internal-label: Email messaging
  - id: c8da4fdd-eb94-4751-a43c-f82733fb2d6e
    internal-label: Email design
  - id: d5bbe3da-ba85-4242-817e-54f7c4b943e0
    internal-label: A/B testing
  - id: f4da0e76-df77-451e-ad61-21afb7bd8810
    internal-label: Manage deliverability
  - id: a39dbcf0-89cb-4765-9bcb-cf9dfbe2875f
    internal-label: Troubleshooting
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: d7e5f68c0d2e0b94fd5cfdf2981bed29f33d9f62
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 95%
---
# 配信品質のトラブルシューティング{#deliverability-faq}

配信品質で問題が発生した場合は、 以下のソリューションを参照してください。

Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 強制隔離について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/quarantines){target=_blank}を参照して、強制隔離のブロックリストとアドレスの削除方法を確認してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/quarantines){target=_blank}

## MX ルールエラー {#mx-rule-error}

**エラーメッセージ「割り当てに達しました」とはどのような意味ですか。**

このメッセージは、特定の MX が割り当て制限に達し、このプロバイダーに別のメールを送信できるようになるまで待つ必要があることを示します。

Adobe Campaign には、1 時間に送信できるメールの数に関する設定があります。 インスタンスに定義されている数は、実際に送信されるメールの数ではなく ISP で実行される接続の数に関するものなので、この設定は慎重に使用する必要があります。

つまり、接続では、正常にメールを送信できなくても MX ルールを使用できます。 この場合、レピュテーションの低い IP アドレスまたはドメインの設定では、メールを送信するまでに数回接続を試みる必要があります。 接続を試みるたびに、「時間あたりのメッセージ数」の割り当てが消費されます。 その結果、マーケティングキャンペーンのパフォーマンスに重大な影響が出ることになります。

そのため、「割り当てに達しました」とは、設定の問題だけでなく、レピュテーションに関連している可能性があります。 [SMTP ログ](../../production/using/monitoring-processes.md#smtp-errors-per-domain)に記載されているエラーメッセージを分析することが重要です。

MX 設定について詳しくは、[この節](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

## ISP に対する同じエラーメッセージ {#same-error-for-an-isp}

**特定の ISP でいつも同じエラーメッセージが表示されるのはなぜですか。**

ある ISP でいつも同じエラーメッセージが表示される場合、メールまたは IP が ISP で誤って検出されている可能性があります。 次のレコメンデーションを実行します。
* 受け取っているエラーの多くが、存在しないメールアドレス（**不明なユーザー**&#x200B;エラー）に関連するものかどうかを確認します。
* 入力したドメイン名のエラーを検出するために、購読フォームを更新します（例：gmaul.com または yaho.com）。
* メッセージがスパムであることを宣言していることを示すエラーの場合、または、メッセージが常にブロックされていることを示すエラーの場合、過去 12 ヶ月間にメッセージを開封またはクリックしていない受信者をターゲットから除外してみます。

それでも問題が解決されない場合は、商用サービス、配信品質サービスまたは[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## WebブロックリストからのIPの削除 {#remove-from-denylist}

* **IP のいずれかがブロックリストに登録されているかどうかを確認するにはどうすればよいですか。 IP をブロックリストから削除する方法を教えてください。**

  IP アドレスがブロックリストに登録されているかどうかは、以下のような様々な Web サイトを使用して検証できます。
  * [MX Toolbox](https://mxtoolbox.com/)
  * [What is my IP address](https://whatismyipaddress.com)

  通常、IP アドレスチェックの結果は、ブロックリストの詳細と IP アドレスを拒否した Web サイトの名前を含むリストで返されます。

  対応するリンクをクリックすると、Web サイトの詳細にアクセスできます。 次に、IP アドレスがブロックリストに登録された Web サイトのリストから Web サイトを削除するようリクエストできます。

  >[!NOTE]
  >
  >リストからの削除のプロセスは、Web サイトによって異なります。 サイトによって、アカウントの作成が必要な場合や、IP アドレスを指定するだけの場合があります。
