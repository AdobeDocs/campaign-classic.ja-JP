---
product: campaign
title: 配信の失敗について
description: 配信失敗を理解する方法を学ぶ
feature: Monitoring, Deliverability
role: User
exl-id: 86c7169a-2c71-4c43-8a1a-f39871b29856
source-git-commit: eac670cd4e7371ca386cee5f1735dc201bf5410a
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 52%

---

# 配信の失敗について{#understanding-delivery-failures}

>[!NOTE]
>
>配信エラーについてに関する包括的なガイダンスは、[Campaign v8 配信エラーについて ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures) ページに記載されています。 このコンテンツは、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用され、以下をカバーしています。
>
>* 配信エラーのタイプと理由（ハード、ソフト、無視）
>* 同期エラーと非同期エラー
>* バウンスメールの選定
>* メール、プッシュ通知、SMS のエラータイプ
>* 再試行の管理と有効期間
>* 一般的な配信エラーのトラブルシューティング
>
>このページは、ハイブリッドデプロイメントおよびオンプレミスデプロイメントでのバウンスメール管理の **0}Campaign Classic v7 固有の設定 } について説明します。**

配信エラーの一般的な概念、エラータイプおよびトラブルシューティングガイダンスについては、[Campaign v8 配信エラーについてのドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} を参照してください。

## バウンスメールの設定 {#v7-bounce-mail-config}

バウンスメールの処理を管理するための **Campaign Classic v7 ハイブリッド/オンプレミスデプロイメントでは** 次の設定オプションを使用できます。

### バウンスメールボックスの設定 {#bounce-mailbox-configuration}

オンプレミスインストールの場合、バウンスメールボックスの設定について詳しくは [ この節 ](../../installation/using/deploying-an-instance.md#managing-bounced-emails) を参照してください。

非同期エラーメッセージは、バウンスメールボックスを通じてAdobe Campaign プラットフォームによって収集され、inMail プロセスによって選定されて、メール管理ルールのリストを充実させます。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、バウンスメールボックスの設定は、Adobeによって実行および管理されます。 設定は不要です。

### バウンスメールの認定管理 {#bounce-mail-qualification-management}

従来の Campaign MTA を使用したオンプレミスインストールおよびホスト／ハイブリッドインストールの場合、メールの配信に失敗すると、Adobe Campaign 配信サーバーは、メッセージングサーバーまたはリモート DNS サーバーからエラーメッセージを受け取ります。エラーのリストは、リモートサーバーが返したメッセージに含まれる文字列で構成されます。エラータイプと理由が各エラーメッセージに割り当てられます。

このリストは、**[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／配信ログ選定]**&#x200B;ノードから表示できます。このリストには、配信エラーを評価するために Adobe Campaign が使用するすべてのルールが含まれています。このリストは、完成されたものではなく、Adobe Campaign によって定期的に更新されます。ユーザーが管理することもできます。

![](assets/tech_quarant_rules_qualif.png)

このエラータイプが最初に発生したときにリモートサーバーから返されたメッセージは、**[!UICONTROL 配信ログ選定]**&#x200B;テーブルの&#x200B;**[!UICONTROL 最初のテキスト]**&#x200B;列に表示されます。この列が表示されない場合は、リストの右下にある「**[!UICONTROL リストを設定]**」ボタンをクリックし、この列を選択します。

![](assets/tech_quarant_rules_qualif_text.png)

Adobe Campaign は、このメッセージをフィルター処理して変数コンテンツ（ID、日付、メールアドレス、電話番号など）を削除し、フィルター処理した結果を&#x200B;**[!UICONTROL テキスト]**&#x200B;列に表示します。変数は、**`#xxx#`** で置き換えられます（ただし、アドレスは **`*`** で置き換えられます）。

このプロセスで同じタイプのすべてのエラーをまとめることにより、同じようなエラーの複数のエントリが配信ログ選定テーブルに含まれないようにすることができます。

>[!NOTE]
>
>「**[!UICONTROL 発生数]**」フィールドには、リスト内のメッセージの発生回数が表示されます。上限は 100,000 回です。このフィールドは、リセットする場合など、必要に応じて編集できます。

バウンスメールは、次の選定ステータスを持つことができます。

* **[!UICONTROL 選定]**：バウンスメールを選定できませんでした。 選定を配信品質チームに割り当てて、効率的なプラットフォーム配信品質を保証する必要があります。選定されていないバウンスメールは、メール管理ルールのリストのエンリッチメントには使用されません。
* **[!UICONTROL 保持]**：バウンスメールは検証されました。**配信品質の更新**&#x200B;ワークフローは、このバウンスメールを既存の E メール管理ルールとの比較およびリストのエンリッチメントに使用します。
* **[!UICONTROL 無視]**：バウンスメールは Campaign MTA によって無視され、このバウンスによって受信者のアドレスが隔離されることはありません。 **配信品質の更新**&#x200B;ワークフローでは使用されず、クライアントインスタンスに送信されません。

![](assets/deliverability_qualif_status.png)

>[!NOTE]
>
>ISP を利用できなくなった場合、Campaign を通じて送信されたメールは、誤ってバウンスとしてマークされます。 これを修正するには、バウンス選定条件を更新する必要があります。詳しくは、[このページ](update-bounce-qualification.md)を参照してください。

### メール管理ルールの設定 {#email-management-rules}

メールルールには、**[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／メールルールセット]**&#x200B;ノードからアクセスします。メール管理ルールがウィンドウの下部に表示されます。

![](assets/tech_quarant_rules.png)

>[!NOTE]
>
>プラットフォームのデフォルトのパラメーターは、デプロイウィザードで設定します。詳しくは、[この節](../../installation/using/deploying-an-instance.md)を参照してください。

デフォルトのルールには次のものがあります。

>[!IMPORTANT]
>
>* パラメーターが変更されている場合は、配信サーバー（MTA）を再起動する必要があります。
>* 管理ルールを変更または作成できるのは、エキスパートユーザーのみです。

#### 受信メール {#inbound-email}

これらのルールには、リモートサーバーから返される文字列と、エラーを検証できる文字列が含まれています（**ハード**、**ソフト**、または **無視**）。

メールが失敗すると、リモートサーバーがプラットフォームのパラメーターで指定されたアドレスにバウンスメールを返します。Adobe Campaignは、各バウンスメッセージのコンテンツをルールリストの文字列と比較して、3 つのエラータイプのいずれかを割り当てます。

>[!NOTE]
>
>ユーザーは独自のルールを作成できます。パッケージをインポートしたり、**配信品質の更新**&#x200B;ワークフローでデータを更新すると、ユーザーが作成したルールが上書きされます。

バウンスメールの選定について詳しくは、[ この節 ](#bounce-mail-qualification-management) を参照してください。

#### ドメイン管理 {#domain-management}

オンプレミスインストールの場合、MTA は単一の **ドメイン管理** ルールをすべてのドメインに適用します。

<!--![](assets/tech_quarant_domain_rules_02.png)-->

* 特定の識別標準や、**送信者 ID**、**DomainKeys**、**DKIM**、**S/MIME** などドメイン名をチェックするための暗号鍵を有効化するかどうかを選択できます。
* **SMTP リレー** パラメーターを使用すると、特定のドメインのリレーサーバーの IP アドレスとポートを設定できます。 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#smtp-relay)を参照してください。

メッセージが送信者アドレスに **[!UICONTROL 次の人物の代理]** と表示される場合は、**Sender ID** を使用してメールに署名しないでください。これは、Microsoftが以前から採用している独自のメール認証標準です。 「**[!UICONTROL 送信者 ID]**」オプションが有効な場合は、対応するボックスのチェックマークを外し、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に連絡します。配信品質に影響はありません。

#### MX 管理 {#mx-management}

オンプレミスインストールの場合、MX 管理ルールを使用して、特定のドメインに対する送信メールのフローを規制します。

<!--![](assets/tech_quarant_domain_rules_01.png)-->

これらのルールは、デプロイメントウィザードで使用でき、カスタマイズできます。

* **[!UICONTROL MX 管理]**：このルールは、ドメインの送信メールのフローを制御するために使用されます。 必要に応じて、バウンスメッセージとブロック送信のサンプルを収集します。

* **[!UICONTROL 期間]**：メッセージがスロットルまたはブロックされる期間です。

* **[!UICONTROL 制限]**：期間ごとに許可されるメッセージの最大数。

* **[!UICONTROL タイプ]**：送信動作を決定するために使用されるエラータイプ（ハード、ソフト、無視）。 エラータイプの定義については、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} を参照してください。

MX 管理について詳しくは、[この節](../../installation/using/email-deliverability.md#about-mx-rules)を参照してください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、MX ルールとメールフロー管理は、管理インフラストラクチャの一部としてAdobeによって管理されます。 特定の使用例に合わせて MX 設定を調整する必要がある場合は、Adobe カスタマーケアにお問い合わせください。

## 関連トピック

* [ 配信エラーについて ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} （Campaign v8 ドキュメント）
* [ 配信ステータス ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-statuses){target="_blank"} （Campaign v8 ドキュメント）
* [ 強制隔離の管理 ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} （Campaign v8 ドキュメント）
* [ 強制隔離の設定 ](understanding-quarantine-management.md) （v7 ハイブリッド/オンプレミス）
* [ バウンス認定条件の更新 ](update-bounce-qualification.md) （v7 ハイブリッド/オンプレミス）
* [ メール配信品質の設定 ](../../installation/using/email-deliverability.md) （v7 ハイブリッド/オンプレミス）
* [ インスタンスのデプロイ ](../../installation/using/deploying-an-instance.md#managing-bounced-emails) （v7 ハイブリッド/オンプレミス）
