---
product: campaign
title: 配信エラーと強制隔離の管理
description: Campaign Classic v7 で配信エラーを把握し強制隔離を管理する方法を説明します
feature: Monitoring, Deliverability
role: User
exl-id: 86c7169a-2c71-4c43-8a1a-f39871b29856
source-git-commit: 2ebae2b84741bf26dd44c872702dbf3b0ebfc453
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 35%

---

# 配信エラーと強制隔離の管理 {#delivery-failures-quarantine}

>[!NOTE]
>
>配信の失敗と強制隔離管理に関する包括的なガイダンスについては、Campaign v8 ドキュメントを参照してください。 このコンテンツは、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用されます。
>
>* [&#x200B; 配信失敗について &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} – 失敗のタイプ、エラー理由、同期/非同期エラー、再試行管理、トラブルシューティングについて説明します
>* [&#x200B; 強制隔離管理 &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} – 強制隔離とブロックリストに加える、ソフトエラーしきい値、強制隔離レポート、アドレス削除について説明します
>
>このページは、ハイブリッドデプロイメントとオンプレミスデプロイメントでのバウンスメールおよび強制隔離の管理について **0&rbrace;Campaign Classic v7 固有の設定 &rbrace; を説明します。**

## 配信エラーについて

配信エラーの一般的な概念、エラータイプおよびトラブルシューティングガイダンスについては、[Campaign v8 配信エラーについてのドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} を参照してください。

## バウンスメールの設定 {#bounce-mail-config}

バウンスメールの処理を管理するための **Campaign Classic v7 ハイブリッド/オンプレミスデプロイメントでは** 次の設定オプションを使用できます。

### バウンスメールボックスの設定 {#bounce-mailbox-configuration}

オンプレミスインストールの場合、バウンスメールボックスの設定について詳しくは [&#x200B; この節 &#x200B;](../../installation/using/deploying-an-instance.md#managing-bounced-emails) を参照してください。

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

バウンスメールの選定について詳しくは、[&#x200B; この節 &#x200B;](#bounce-mail-qualification-management) を参照してください。

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

* **[!UICONTROL タイプ]**：送信動作を決定するために使用されるエラータイプ（ハード、ソフト、無視）。 エラータイプの定義については、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} を参照してください。

MX 管理について詳しくは、[この節](../../installation/using/email-deliverability.md#about-mx-rules)を参照してください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、MX ルールとメールフロー管理は、管理インフラストラクチャの一部としてAdobeによって管理されます。 特定の使用例に合わせて MX 設定を調整する必要がある場合は、Adobe カスタマーケアにお問い合わせください。

## 強制隔離の管理 {#quarantine-management}

包括的な強制隔離管理ガイダンスについては、[Campaign v8 強制隔離管理ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} を参照してください。

## 強制隔離の設定 {#quarantine-config}

強制隔離の動作をカスタマイズするための設定オプションは、**Campaign Classic v7 ハイブリッド/オンプレミスデプロイメント** で次のとおりです。

### ソフトエラーしきい値の設定 {#soft-error-threshold}

従来の Campaign MTA を使用したオンプレミスインストールの場合、エラーの数と、アドレスが強制隔離される前の 2 つのエラー間の期間を変更できます。

これらの設定を行うには：

1. **[!UICONTROL ツール]**/**[!UICONTROL 詳細]**/**[!UICONTROL デプロイメントウィザード]** からデプロイメントウィザードにアクセスします
2. **[!UICONTROL メールチャネル]**/**[!UICONTROL 詳細設定パラメーター]** に移動します。
3. 次の設定をおこないます。
   * **エラー数**：アドレスが強制隔離される前のソフトエラーの最大数（デフォルト：5）
   * **2 つの重要なエラーの間の期間**：エラーをカウントする期間（秒単位）（デフォルト：86,400 秒= 1 日）

エラーカウンターがしきい値に達すると、アドレスが強制隔離されます。 最後の重大なエラーが 10 日以上前に発生した場合、エラーカウンターは再初期化されます。

詳しくは、[&#x200B; 配信送信 &#x200B;](communication-channels.md)/**再試行を設定** の **このページ** を参照してください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、再試行設定とエラーのしきい値は、IP パフォーマンスとドメインのレピュテーションに基づいてAdobeで管理されます。 設定は不要です。

### データベースクリーンアップのワークフロー {#database-cleanup-workflow}

オンプレミスインストールの場合、**[!UICONTROL データベースクリーンアップ]** テクニカルワークフローは、特定の条件に一致する強制隔離アドレスを自動的に削除します。

このワークフローには、**[!UICONTROL 管理]**/**[!UICONTROL プロダクション]**/**[!UICONTROL テクニカルワークフロー]**/**[!UICONTROL データベースクリーンアップ]** からアクセスします。

ワークフローは、次の場合に強制隔離からアドレスを削除します。

* 配信成功後に **[!UICONTROL エラーあり]** ステータスになったアドレス
* 最後のソフトバウンスが 10 日以上前に発生した場合の **[!UICONTROL エラーあり]** ステータスのアドレス
* 30 日後に「メールボックス容量超過 **&#x200B;**&#x200B;エラーが発生した **[!UICONTROL エラーあり]** ステータスのアドレス

強制隔離リストのハイジーンを維持するために、このワークフローが定期的に実行されていること（推奨：毎日）を確認します。

データベースのクリーンアップについて詳しくは、[&#x200B; この節 &#x200B;](../../production/using/database-cleanup-workflow.md) を参照してください。

>[!NOTE]
>
>Campaign v8 Managed Cloud Services ユーザーの場合、データベースクリーンアップワークフローはAdobeで監視および管理されます。

### プッシュ通知の強制隔離の詳細 {#push-quarantine-specifics}

Campaign Classic v7 の場合、プッシュ通知の強制隔離は、チャネル固有の動作で、一般的な強制隔離メカニズムに従います。

**iOS** および **Android** のプッシュ通知の場合、強制隔離メカニズムはメールアドレスではなくデバイストークンを使用します。 モバイルアプリケーションがアンインストールまたは再インストールされると、関連するトークンが強制隔離されます。

プッシュ通知の強制隔離シナリオ（iOSおよびAndroidのエラータイプ、再試行動作など）について詳しくは、[&#x200B; 配信エラーについて &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} のドキュメントを参照してください。このドキュメントには、包括的なプッシュ通知エラータイプの表が含まれています。

### SMS の強制隔離の詳細 {#sms-quarantine-specifics}

Campaign Classic v7 の場合、SMS の強制隔離は、メールアドレスではなく電話番号に関連するチャネル固有の動作で、一般的な強制隔離メカニズムに従います。

SMS の強制隔離メカニズムは、使用するコネクタによって異なります。

* **標準 SMPP コネクタ**:**[!UICONTROL 管理/キャンペーン管理/配信不能件数の管理/配信ログの選定]** で定義されたエラー選定ルールが、SMS 配信に適用されます。

* **拡張された汎用 SMPP コネクタ**: エラー管理は、正規表現（正規表現）を使用して異なる方法で処理され、SMSC プロバイダーによって返されたステータスレポート（SR）メッセージを解析します。

SMS 強制隔離のシナリオとエラータイプについて詳しくは、包括的な SMS エラータイプ テーブルを含む [&#x200B; 配信エラーについて &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} ドキュメントを参照してください。

## 関連トピック

* [&#x200B; 配信エラーについて &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; 強制隔離の管理 &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; 配信ステータス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-statuses){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; データベースクリーンアップワークフロー &#x200B;](../../production/using/database-cleanup-workflow.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; 配信再試行の設定 &#x200B;](communication-channels.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; バウンス認定条件の更新 &#x200B;](update-bounce-qualification.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; メール配信品質の設定 &#x200B;](../../installation/using/email-deliverability.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; インスタンスのデプロイ &#x200B;](../../installation/using/deploying-an-instance.md#managing-bounced-emails) （v7 ハイブリッド/オンプレミス）

