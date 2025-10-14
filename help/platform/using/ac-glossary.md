---
product: campaign
title: Adobe Campaign の用語集
description: Adobe Campaign の用語集
feature: Overview
role: User, Data Architect
level: Beginner
exl-id: 81f207a0-bb72-450b-abe4-0b229b6b1f3a
source-git-commit: ad6f3f2cf242d28de9e6da5cec100e096c5cbec2
workflow-type: tm+mt
source-wordcount: '6184'
ht-degree: 94%

---

# Adobe Campaign 用語集{#ac-glossary}

Adobe Campaign の主な用語と概念の定義と、関連ドキュメントへのリンクを以下に示します。用語をクリックすると、その定義が表示されます。

## A～D{#sec-1}

+++**A/B テスト**

A/B テストは、ユーザーが 2～3 種類のメールのバリエーションを定義できる機能です。どのバリアントが最適な結果を得られるかを判断するために、各バリアントが母集団サンプルに送信されます。結果が明確になったら、勝者バリアントが残りの母集団に送信されます。

詳細情報：[A/B テスト](../../delivery/using/get-started-a-b-testing.md)。
+++

+++**アクセス管理**

アクセス管理を使用すると、管理者は Adobe Campaign のユーザーにアクセスと権限を割り当てることができます。権限には、ワークフローの実行、スキーマの定義、オーディエンスの管理など、Adobe Campaign 機能の表示や使用の機能が含まれます。

詳細情報：[アクセス管理](access-management.md)。
+++

<!--
+++**ACS Connector**

ACS Connector (Prime Offering) bridges Adobe Campaign v7 and Adobe Campaign Standard. It is an integrated feature in Campaign v7 that automatically replicates data to Campaign Standard, uniting the best of both applications. Campaign v7 has advanced tools to manage the primary marketing database. The data replication from Campaign v7 allows Campaign Standard to leverage the rich data in a user-friendly environment. 

Learn more about [ACS Connector](../../integrations/using/acs-connector-principles-and-data-cycle.md).
+++
-->

+++**アクティビティ**

アクティビティは、実行機能を定義するためにワークフローに追加されるパレット項目です。アクティビティは、タスクを実行するコンテナです。ワークフローでは、指定されたアクティビティが、特にループまたは繰り返し（定期的）アクションがある場合に複数のタスクを生成できます。

ワークフローアクティビティについて詳しくは、[Campaign v8 ドキュメント ] （https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/activities）を参照してください
.html） {target="_blank"}.
+++

+++**アクティブなプロファイル**

過去 12 か月間にいずれかのチャネルを介してターゲット設定されたまたは通信を受けたプロファイルが、アクティブなプロファイルと見なされます。各 Campaign インスタンスには、契約に従って特定数のアクティブなプロファイルがプロビジョニングされ、課金用にその数がカウントされます。

詳細情報：[アクティブなプロファイル](../../platform/using/about-profiles.md#active-profiles)。
+++

+++**承認ワークフローアクティビティ**

*コンテキスト：Campaign 分散型マーケティング*

ローカルの承認アクティビティは、メッセージが送信される前に配信の承認プロセスを設定するために使用されるワークフローアクティビティです。

+++

+++**オーディエンス**

オーディエンスは、ルールと属性に基づいて、フィルター定義の条件を満たすプロファイルの結果セットです。

オーディエンスについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-target.html?lang=ja){target="_blank"} を参照してください。
+++

+++**監査記録**

監査記録を使用すると、Adobe Campaign のインスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムで記録できます。これには、データの履歴を確認することにより、ワークフローで発生した事象、ワークフローの最終更新者、インスタンス内でユーザーが行った操作などを知るのに役立つセルフサービス式の方法が含まれています。

詳細情報：[監査記録](../../production/using/audit-trail.md)。
+++

<!--
----DUPLICATE WITH THE "CAMPAIGN" ENTRY?---
+++**Automated campaigns**

Campaigns that run on a schedule, such as for targeting recipients who have a birthday or an anniversary. Can also be used to execute look-ahead and look-back logic, such as who purchased yesterday or who has a payment due tomorrow.

Learn more about [Campaigns](../../campaign/using/designing-marketing-campaigns.md).
+++
-->

+++**バッチモード**

*コンテキスト：Campaign インタラクション*

Campaign インタラクションのコンテキストでは、バッチモードを使用すると、一連の連絡先に最適なオファー（複数可）をオファーエンジンで選択できます。すべての連絡先グループに実施要件ルールと優先順位付けルールが適用されます。

詳細情報：[インタラクション](../../interaction/using/interaction-and-offer-management.md)。
+++

+++**キャンペーン**

Campaign は、マーケティングキャンペーンを調整、定義、実行するためのインターフェイスです。 Campaign には、1 つ以上のワークフロー、配信、ドキュメント、その他の関連データポイントを、使いやすい単一のインターフェイスに含めることができます。

キャンペーンについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/campaigns/campaigns.html?lang=ja){target=_blank} を参照してください。
+++

<!--
-----NOT USEFUL HERE?-----
+++**Changeover process**

*Context: Campaign Interaction*

In the context of Campaign Interaction, the changeover process is an activated process in an identified environment, responsible for directing the call to an anonymous environment if the contact has not been explicitly and/or implicitly identified.

Learn more about [Interaction](../../interaction/using/interaction-and-offer-management.md).
+++
-->

+++**チャネル**

チャネルは、通信を送信するための媒体です。Adobe Campaign のビルトインのチャネルは、メール、SMS、ダイレクトメール、プッシュ通知、LINE および X（旧 Twitter）です。カスタムチャネルは、非標準のチャネル要件に対して実装できます。

詳細情報：[チャネル](../../delivery/using/communication-channels.md)。
+++

+++**クライアントコンソール**

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。クライアントコンソールの実行可能ファイル（.exe）アプリケーションは、Microsoft Windows オペレーティングシステムを搭載したコンピューターにインストールされます。Campaign クライアントコンソールは、すべての機能と設定を一元化します。

詳細情報：[クライアントコンソール](../../platform/using/adobe-campaign-workspace.md)。
+++

+++**コンテンツの承認**

コンテンツの承認は、別のオペレーターまたはオペレーターのグループに、配信のコンテンツを送信前に承認させるプロセスです。

コンテンツの承認について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-approval.html?lang=ja){target="_blank"} を参照してください。

+++

+++**コントロール母集団**

コントロール母集団を使用すると、オーディエンスの一部を除外して、キャンペーンの影響を測定できます。オペレーターは、メッセージを受信したターゲット母集団の行動と、ターゲット設定されていない連絡先の行動を比較できます。送信ログに基づいて、オペレーターは今後のキャンペーンでコントロール母集団をターゲット設定することもできます。

コントロール母集団について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/marketing-campaign-target.html#add-a-control-group){target="_blank"} を参照してください。
+++

+++**コントロールパネル**

コントロールパネルを使用すると、Adobe Campaign の製品管理者が設定を管理し、各インスタンスの使用状況を追跡できるので、製品管理者の作業効率を向上させることができます。直感的なインターフェイスにより、主要なアセットの使用状況を簡単に監視できるうえ、IP アドレスの許可リスト登録、SFTP ストレージの監視、キー管理などの管理タスクも実行できます。

詳しくは、[コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html?lang=ja)を参照してください。
+++

+++**キューブ**

*コンテキスト：マーケティング分析*

キューブは、Adobe Campaign の直感的なデータ調査ツールで、動的レポートの作成と共有に役立ちます。

詳細情報：[キューブ](../../reporting/using/ac-cubes.md)。
+++

+++**カスタムリソース**

Adobe Campaign には事前定義済みのデータモデルが付属しており、様々なパッケージのインストールを通じてデータタイプが定義されます。オペレーターはリソースを拡張することで提供されるデータモデルをエンリッチメントし、トランザクションテーブルや製品テーブルなどのカスタムテーブルや、カスタムフィールドを追加できます。

詳細情報：[カスタムリソース](../../configuration/using/about-schema-edition.md)。
+++

+++**データモデル**

Campaign データモデルは、データタイプとその関係（リンク）を定義する一連のスキーマです。データモデルは、実際のデータを含むデータベースと物理的に実装される抽象定義です。

詳しくは、[データモデル](../../configuration/using/about-data-model.md)を参照してください。
+++

+++**データベースクリーンアップワークフロー**

データベースクリーンアップワークフローは、データベースの急激な拡大を避けるために古いデータを削除します。ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

詳細情報：[データベースクリーンアップワークフロー](../../production/using/database-cleanup-workflow.md)。
+++

<!--
----UNCLEAR----
+++**Dedicated server**

*Context: Transactional Messaging*

Dedicated execution server(s) to leverage Transactional Messaging. A server can typically process up to 50,000 Engine Calls per hour. The "Per-Dedicated Server" designation does not necessarily have a 1:1 correlation with a physical server as Adobe may utilize virtualization technologies to achieve the equivalent effect.

Learn more about [Transactional Messaging](../../message-center/using/about-transactional-messaging.md).
+++
-->

+++**配信品質**

*コンテキスト：電子メールの配信品質*

配信品質は、バウンスしたりスパムと見なされることなく受信者のインボックスに到達するキャンペーンの成否を測定する手法です。正確には、メール配信品質とは、メッセージが、期待される品質の内容と形式を持ち、個人のメールアドレスを通じて短時間で宛先に到達できるかどうかを判断する一連の特性のことを指します。

詳細情報：[配信品質](../../delivery/using/about-deliverability.md)。
+++

+++**配信**

配信とは、特定のチャネル（メール、SMS、プッシュ通知など）でオーディエンスに送信される、特定のマーケティングコミュニケーション項目です。マーケティング用語で「タッチ」とも呼ばれます。

詳細情報：[配信](../../delivery/using/communication-channels.md)。
+++

+++**配信分析**

配信分析は、配信の準備です。このプロセスでは、コンテンツと受信者のプロファイルデータを組み合わせて、受信者が受け取るパーソナライズされたメールを生成します。配信分析ロジックでは、定義されたロジックに基づいて、受信者をターゲットから除外したり、配信を完全に停止したりできます。このプロセスには、動的コンテンツロジックの評価と、個々の受信者プロファイルに固有のオファーの挿入も含まれます。

配信分析について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/validate/delivery-analysis.html){target="_blank"} を参照してください。
+++

+++**配信ログ**

配信ログには、メッセージの送信時に生成される情報が含まれます。これらのログで、どのメッセージが準備、無視、送信または失敗したか、送信の詳細が示されます。配信ダッシュボードから直接アクセスできます。

詳細情報：[配信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history)。
+++

<!--
----STRANGE IN DOCS?----
+++**Delivery fundamentals**

*Context: Email Deliverability*

Adobe Campaign Deliverability Fundamentals Consulting Service provides email deliverability consultation and reputation management to support customers using Adobe Campaign deliveries.

Learn more about [Deliverability](../../delivery/using/about-deliverability.md).
+++
-->

+++**配信の概要**

*コンテキスト：ダイレクトメール*

配信の概要は、企業が特定のキャンペーン用に作成した構造化された一連の要素（ドキュメント、店舗、プロモーション用クーポンなど）です。これは、ダイレクトメール配信のコンテキストで使用されます。

詳細情報：[ダイレクトメール](../../delivery/using/about-direct-mail-channel.md)。
+++

+++**デプロイメントウィザード**

デプロイメントウィザードでは、デフォルトの名前空間、データベースクリーンアップスケジュール、データ保持期間、その他の技術的な設定など、Campaign インスタンスのパラメーターを定義します。

詳しくは、[デプロイメントウィザード](../../installation/using/deploying-an-instance.md#deployment-assistant)を参照してください。
+++

+++**記述的分析**

記述的分析は、ワークフローのワークテーブル内のデータやフォルダー内で選択されたデータを調べたり、選択した配信のターゲットや除外の詳細を調べたりできる、コンテキスト依存レポートツールです。

詳細情報：[記述的分析](../../reporting/using/about-descriptive-analysis.md)
+++

+++**分散型マーケティング**

*コンテキスト：分散型マーケティング*

分散型マーケティングアドオンでは、Campaign オペレーターに、セントラルエンティティ（本社、マーケティング部門など）とローカルエンティティ（販売店、地域代理店など）の間でキャンペーンを実施する共同作業ワークスペースを提供します。この連携のベースとなるのは、**キャンペーンパッケージのリスト**&#x200B;と呼ばれる共有ワークスペースで、主にセントラルエンティティで作成されたキャンペーンのテンプレートやインスタンスが、ローカルエンティティに提供されます。

分散型マーケティングについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/distributed-marketing/about-distributed-marketing.html?lang=ja){target="_blank"} を参照してください。
+++

+++**値の配分**

値の配分は、現在データベースに存在するスキーマ属性の値の配分を表示するツールです。これにより、使用可能な値、およびその数と割合を判断し、クエリや式を作成する際の値の大文字と小文字の区別やスペルの問題を回避できます。

詳しくは、[値の配分](../../platform/using/about-queries-in-campaign.md)を参照してください。
+++

+++**ドメインデリゲーション**

サブドメイン設定を使用すると、Adobe Campaign で使用するためにドメインのサブセクション（技術的には「DNS ゾーン」）を設定できます。
ドメインのデリゲーションにより、アドビは、メールキャンペーンの配信、レンダリング、トラッキングに必要な DNS のあらゆる側面を制御および管理できます。

[ドメインのデリゲーション](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/setting-up-new-subdomain.html?lang=ja)についての詳細情報
+++

## E - H {#sec-2}

<!--
----DEPRECATED------>
+++**E4X**

E4X は、Adobe Campaign Classic で使用される JavaScript のバージョンです。ECMAScript とも呼ばれ、同じコード内で JavaScript と XML のプリミティブを組み合わせることができる、JavaScript の拡張機能です。なお、E4X は非推奨（廃止予定）の言語として分類されています。
+++


+++**実施要件ルール**

*コンテキスト：Campaign インタラクション*

実施要件ルールは、有効期間、ターゲットおよび重み付けに関して、環境、カテゴリまたはオファーに適用される制約です。実施要件ルールを使用すると、オペレーターは、ターゲットとなる連絡先に適したオファーを提示できるようになります。オファー環境の実施要件ルールには、オファーとターゲット受信者に適用されるプレゼンテーションルールが含まれます。カテゴリで実施要件ルールを使用すると、オペレーターはカテゴリの有効期限を設定したり、アプリケーションテーマを定義したり、ターゲット受信者を決定したりできます。また、特定の期間に乗数の重み付けを定義することもできます。これにより、オペレーターは他のカテゴリのオファーのルールを共有できるので、ルールの管理が簡単になります。オファーで実施要件ルールを使用すると、オペレーターはオファーの有効期限を設定したり、ターゲット受信者を決定したりできます。

実施要件ルールの詳細は[こちら](../../interaction/using/interaction-and-offer-management.md)。
+++

+++**実施要件を満たすオファー**

*コンテキスト：キャンペーンインタラクション*

実施要件を満たすオファーは、アップストリームで定義された制約を満たし、ターゲットに一貫して提示できるオファーです。

インタラクションの詳細は[こちら](../../interaction/using/interaction-and-offer-management.md)。
+++

+++**BCC でメールを送信**

「BCC でメールを送信」機能では、対応する配信メールの正確なコピーを EML 形式で送信します。このメールは専用の BCC メールアドレスに保存され、そこで処理されて外部システムに送信者別にアーカイブできます。

BCC でメールを送信について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/emails/email-bcc.html){target="_blank"} を参照してください。
+++

<!--
-----STRANGE FOR DOCS?----
+++**Email volume commitment**

The anticipated emails sent per year as set forth in the Sales Order. This is the total annual email volume commitment, including emails sent but not delivered due to delivery errors such as: non-delivery of a message including but not limited to email address errors, hard bounces, soft bounces, email filters of mail clients, and email blacklists. 
+++
-->

<!--
-----USEFUL FOR DOCS?----
+++**Engine call**

An engine call is a server call that starts real-time processing on server side for the extraction of data, such as data relating to surveys, WebApps, JSSP, APIs, mobile app registrations, etc. Engine calls must be licensed in packs of 5,000 Engine Calls per day.
+++
-->

+++**エンリッチメントアクティビティ**

エンリッチメントアクティビティは、ワークフロー内で処理される生成されたワークテーブルデータをオペレーターがエンリッチメントできる高度なワークフローアクティビティです。このアクティビティは、通常、ターゲティングアクティビティの後に使用されるか、ファイルをインポートした後かつターゲットデータを使用するアクティビティの前に使用されます。エンリッチメントでは、インバウンドトランジションデータを変換し、強化されたデータを使用して出力トランジションを完了するようにアクティビティを設定できます。オペレーターは、複数のデータセットのデータを組み合わせたり、一時的なリソースへのリンクを作成したりできます。

エンリッチメントアクティビティについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/enrichment.html?lang=ja){target="_blank"} を参照してください。
+++

+++**列挙**

列挙は、フィールドの有効な入力値を定義するデータタイプで、スキーマまたはプラットフォームレベルで定義されます。列挙は、ユーザーインターフェイスとクエリビルダーでピックリストとして表示されます。

**定義済みリストの操作**&#x200B;方法について詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/config/settings/enumerations){target=_blank}を参照してください。
+++

+++**エクスプローラービュー**

エクスプローラービューは、Adobe Campaign アーティファクトおよびデータを格納したフォルダーを階層的に表示したものです。 なお、Adobe Campaign のフォルダーシステムは、通常のツリービューとは異なり、各フォルダーには配信、ワークフロー、オファーなどの特定のタイプのデータが格納されます。


Campaign ユーザーインターフェイスについて詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank} を参照してください。

+++

+++**外部アカウント**

外部アカウントは、製品が他の環境やテクノロジーに接続するための入口と出口です。外部アカウントは、製品が他のソースとの間でデータの送受信に使用する接続パラメーターを定義します。一般的な外部アカウントタイプは、SFTP サイトの接続、SMS の送信をサポートする通信、バウンス処理のメールボックス、外部データベースへの接続です。

外部アカウントの詳細は[こちら](../../installation/using/external-accounts.md)。
+++

+++**疲労管理**

*コンテキスト：キャンペーンの最適化*

疲労管理は、メッセージの頻度と量を制御して受信者の過剰勧誘を避けるのに役立ち、多くの場合、タイポロジルールを使用して適用されます。

疲労管理について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/pressure-rules.html?lang=ja){target="_blank"} を参照してください。
+++

+++**Federated Data Access（FDA）**

Federated Data Access では、クライアントデータモデルを拡張してサードパーティのデータベースを含めることができます。ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。Adobe Campaign データの構造を変更せずに外部データにアクセスできます。

Federated Data Access の詳細は[こちら](../../installation/using/about-fda.md)。
+++

+++**ファイル抽出の承認**

*コンテキスト：ダイレクトメール*

ファイル抽出の承認は、ダイレクトメール配信などの外部ベンダーに送信する前に、別のオペレーターまたはオペレーターグループに、抽出したファイルの内容と設定を承認してもらうプロセスです。

ファイル抽出の承認について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/direct-mail.html#validating){target="_blank"} を参照してください。
+++

+++**フィルタリングディメンション**

フィルタリングディメンションは、クエリで目的の行のフィルタリングに使用されるデータまたは属性を含んだスキーマです。フィルタリングディメンションスキーマは、Adobe Campaign がクロスデータベース結合を実行して応答行を返せるように、定義済みのターゲティングディメンションに直接リンクされる必要があります。

フィルタリングディメンションについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/wf-type/targeting-workflows.html?lang=ja#targeting-and-filtering-dimensions){target="_blank"} を参照してください。
+++

+++**フォルダー**

フォルダーは、特定のデータタイプのデータベースレコードを格納するエクスプローラービュー項目です。ただし、編成要素として使用され、データそのものを含まず、他のフォルダーのみを含む汎用フォルダータイプは例外です。

Campaign ユーザーインターフェイスについて詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank} を参照してください。

+++

+++**フォルダービュー**

フォルダービューは、特殊なエクスプローラーフォルダータイプで、どのようなフォルダーに属しているかに関係なく、選択したデータタイプのすべてのレコードを表示するために使用されます。フォルダービューは、分割されたデータや多数のフォルダーに分散されるデータを管理する管理ツールとして使用されます。

Campaign ユーザーインターフェイスについて詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank} を参照してください。
+++

+++**フォーム**

フォームは、特定のスキーマタイプのインターフェイス表現を定義します。フォームは、受信者、配信、キャンペーンなど、製品内のデータ要素を簡単に作成および編集するための手段となります。Adobe Campaign のすべてのインターフェイス要素は、フォームを使用して製品そのものに作成されます。なお、フォームはオプションであり、すべてのスキーマにフォームがあるわけではありません。

フォームの詳細は[こちら](../../configuration/using/identifying-a-form.md)。
+++

<!--
-----USEFUL HERE?-----
+++**Generated SQL query**

The SQL code generated for the underlying database when an operator manipulates a schema. Schemas define the data types that are then implemented using database tables and columns. The SQL generated for schema manipulation (such as in a query) is based on the installed database type. Thus, the database can be swapped to a different type and the queries in Campaign remain unchanged. Adobe refers to this functionality as being database-agnostic.

Learn more about [Generated SQL queries](../../platform/using/steps-to-create-a-query.md#step-6---preview-data).
+++
-->

+++**ヒートマップ**

キャンペーンヒートマップは、24 時間のワークフロー実行情報を表示するテーブルです。その期間内のワークフローの分布を時間別および 5 分間隔で表示します。ヒートマップは、サーバー負荷の評価と、最もリソースを消費しているワークフローアクティビティの判定に使用されます。

[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/heatmap.html?lang=ja){target="_blank"} を参照してください。
+++

+++**ハイブリッドデプロイメント**

ハイブリッドデプロイメントは、オンデマンドサービスとオンプレミスソフトウェアを組み合わせて、一緒に機能するようにデプロイすることです。

ハイブリッドデプロイメントの詳細は[こちら](../../installation/using/hosting-models.md#hybrid)。

+++

## I～L {#sec-3}

<!-- added more details but maybe still not clear/useful here? -->
+++**識別モード**

*コンテキスト：キャンペーンインタラクション*

識別モードは、連絡先のステータスを指します。明示的、暗黙的、匿名のいずれかになります。

* **明示的**：チャネルインターフェイスにログインしたことにより連絡先が識別されている状態。
* **暗黙的**：Cookie（永続またはセッション）により連絡先が識別されている状態。このような連絡先は、匿名連絡先としても、識別された連絡先としても処理できます。
* **匿名**：連絡先が識別できない状態。

インタラクションの詳細は[こちら](../../interaction/using/interaction-and-offer-management.md)。
+++

<!--
----NOT USEFUL HERE?----
+++**Image serving**

The functionality that supplies the images embedded in emails to the delivery's recipients. The insertion of the images based on an emails system's "download images" functionality is what generates an "open" entry in Campaign's tracking logs.

Learn more about [Image serving](../../delivery/using/defining-the-email-content.md#adding-images).
+++
-->

+++**インバウンドインタラクション**

*コンテキスト：キャンペーンインタラクション*

インバウンドインタラクションは、web、コールセンター、モバイルなどのチャネル内の連絡先のアクションによって発生する着信呼び出しに続くインタラクションです。通常、このタイプのインタラクションは単一モードで処理（受信者ごとに処理）されます。

インバウンドインタラクションの詳細は[こちら](../../interaction/using/about-inbound-channels.md)。
+++

+++**インボックスレンダリング**

受信ボックスレンダリングはメールプレビューの生成のことで、様々な web クライアント、web メールおよびデバイスで受信者に最適な方法でメッセージが表示されるようにします。Adobe Campaign では Litmus を利用しているので、メールコンテンツ作成者は、Gmail 受信トレイや Apple Mail クライアントなど、70 を超えるメールレンダラーでメッセージコンテンツをプレビューできます。

受信ボックスレンダリングの詳細は[こちら](../../delivery/using/delivery-dashboard.md#delivery-rendering)。
+++

+++**インスタンス設定**

インスタンス設定は、Adobe Campaign インスタンスの設定の詳細です。これらの設定は、デプロイメントウィザード（ツール／詳細設定／デプロイメントウィザード）で定義するか、サーバーまたはインスタンスの設定ファイルで定義します。

詳しくは、[インスタンス設定](../../installation/using/about-initial-configuration.md)を参照してください。

+++

+++**ジョブ（インポートおよびエクスポート）**

ジョブは、製品との間でのデータのインポートとエクスポートを簡素化する、アシスタントシステムによって管理されます。ジョブは、簡潔さと一貫性を保つためにテンプレートシステムを使用しており、スケジュールに従って実行するように定義できます。

詳しくは、[ジョブのインポートとエクスポート](../../platform/using/get-started-data-import-export.md)を参照してください。
+++

+++**リスト**

リストは静的データセットです。リストは、他のソース（Audience Manager、Experience Platform、データベースなど）から Campaign にインポートされ、インポートされたリストとしてインターフェイスに表示されるオーディエンスまたはセグメントです。

リストの詳細は[こちら](../../platform/using/creating-and-managing-lists.md)。
+++

+++**ローカルキャッシュ**

ローカルキャッシュは、オペレーターのコンピューター上でローカルに保存される情報です。キャッシュされた情報は、サーバーへの必要なトラフィックを減らし、パフォーマンスを向上させるために、コンソールで使用されます。（ファイルメニューの）ローカルキャッシュを定期的にクリアすると、保存されている情報が更新され、パフォーマンスと安定性が向上します。

ローカルキャッシュの詳細は[こちら](../../platform/using/faq-campaign-config.md#perform-soft-cache-clear)。
+++

## M～P {#sec-4}

+++**マーケティングリソース管理（MRM）**

*コンテキスト：マーケティングリソース管理（MRM）*

Adobe Campaign の&#x200B;**マーケティングリソース管理（MRM）**&#x200B;モジュールを使用すると、関係するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調的に制御できます。Adobe Campaign オペレーターは、完全な検証プロセスおよび適切なトラッキングツール（レポート、承認のトラッキング、通知、ディスカッションフォーラムなど）を使用して、あらゆる段階でアクションを調整し、進行状況を承認できます。

MRM について詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/mrm/about-marketing-resource-management.html?lang=ja){target="_blank"} を参照してください。
+++

<!--
----ACS?----
+++**Localization**

This template type is used to manage multilingual messages.  It is available for Email and SMS messages and useable in standalone mode, within a workflow or in a recurring delivery. In the multilingual feature templates, the language management is based on variants. Each variant represents one language.  This functionality is available only in Adobe Campaign Standard.  
+++
-->

+++**ネームド権限**

オペレーターグループのアクセスと権限（役割）の定義に使用される、粒度の細かいデータベースアクセス権です。 ネームド権限の設定は、製品のインストール時や、ツールの特定の機能を定義する様々なパッケージのインポートで行われます。クライアントのビジネス要件をサポートするために、カスタムネームド権限を作成できます。

ネームド権限の詳細は[こちら](../../platform/using/access-management-named-rights.md)。
+++

+++**名前空間**

名前空間は、データモデル内の Adobe Campaign のネイティブデータタイプから顧客データタイプを分離するパーティションです。また、スキーマやテンプレートを開発インスタンスから実稼動インスタンスに移動するなど、あるインスタンスから別のインスタンスへの定義の移行を容易にするためにも使用します。

[名前空間](../../configuration/using/about-schema-reference.md#identification-of-a-schema)の詳細情報。
+++

<!--
----generic, not specific to campaign----
+++**Navigation bar**

The navigation bar is the navigation element running across the top of the interface. The navigation bar regroups the various core capabilities of the platform. Click a navigation bar link to display the set of functionalities related to this capability. The list of core capabilities you can access depends on the packages and add-ons you have installed and on your access rights. The purpose of the Navigation bar is to simplify screen management and increase productivity.

Learn more about [Navigation Bar](../../platform/using/adobe-campaign-workspace.md#browsing-pages).
+++
-->

+++**ナビゲーションツリー**

ナビゲーションツリーは、Adobe Campaign のエクスプローラービューのメインナビゲーションです。ナビゲーションツリーは、ファイルブラウザー（Windows エクスプローラなど）のように機能します。 フォルダーには、サブフォルダーを含めることができます。 ノードを選択すると、そのノードに対応するビューが表示されます。表示されるビューは、選択した行を編集するためのスキーマと入力フォームに関連付けられたリストです。ナビゲーションツリーをカスタマイズし、フォルダーに対する権限を設定できます。

Campaign ユーザーインターフェイスについて詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank} を参照してください。

+++

+++**目標**

*コンテキスト：マーケティングリソース管理（MRM）*

キャンペーン、プログラムまたはプラン内に、オペレーターは一連の目標を記述できます。目標は、到達すべき数値です。キャンペーン、プログラムまたはプランの終了時に MRM モジュールを使用して、オペレーターは目標と結果を専用レポートで比較できます。

目標について詳しくは、[Adobe Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/mrm/creating-and-managing-tasks.html#expenses-and-revenues){target=_blank} を参照してください。
+++

+++**オファーカタログ**

*コンテキスト：Campaign インタラクション*

オファーカタログは、Adobe Campaign で定義され、インタラクション中に選択できる一連のオファーです。カタログは階層構造を持ち、各ノードが 1 つのカテゴリに対応しています。

詳しくは、[オファーカタログ](../../interaction/using/offer-catalog-overview.md)を参照してください。
+++

+++**オファー連絡先**

*コンテキスト：Campaign インタラクション*

オファー連絡先は、インバウンドインタラクションからの連絡先です。連絡先は、エンジン呼び出し処理時にターゲティングディメンションに関連付けられます。識別されていない匿名の連絡先は訪問者ターゲティングディメンションに関連付けられます。連絡先には、識別済みと匿名の 2 種類あります。

* **識別された連絡先**：チャネル上で任意に識別された連絡先。アウトバウンドインタラクションの場合、連絡先は自動的に識別されます。
* **匿名連絡先**：チャネルを通じて任意に登録されてはいないものの Cookie を通じて暗黙的に識別された連絡先。この用語はインバンドインタラクションに対してのみ使用されます。

[インタラクション](../../interaction/using/interaction-and-offer-management.md)の詳細情報。
+++

+++**オファーデザイン環境**

*コンテキスト：Campaign インタラクション*

オファー&#x200B;**デザイン環境** は、オファーの作成、タイポロジルールの定義、オファーのターゲットにするスキーマの選択を行う環境です。 生成されたオファーの提案を保存するテーブルも、環境によって定義されます。デフォルトでは、インタラクションアドオンには、1 つの&#x200B;**デザイン**&#x200B;環境とそれにリンクされた 1 つの&#x200B;**ライブ**&#x200B;環境が用意されています。どちらの環境も、ビルトインの受信者テーブルをターゲットとするように事前に設定されています。

詳しくは、[オファーデザイン環境](../../interaction/using/fundamental-principles.md)を参照してください。
+++

+++**オファーエンジンのアービトラージ**

*コンテキスト：Campaign インタラクション*

オファーエンジンは、環境に表示されるオファー（適格なオファー）を選択します。アービトラージの原則により、各オファーはカテゴリおよびオファーで定義される基準に従って優先順にランク付けされます。

詳しくは、[インタラクション](../../interaction/using/interaction-and-offer-management.md)を参照してください。
+++

+++**オファーエンジンのプルーニング**

*コンテキスト：Campaign インタラクション*

オファーエンジンのプルーニングは、選択の対象でないオファーを削除するプロセスです。 オファーエンジンのアービトラージ手順の前に実行されます。

詳しくは、[インタラクション](../../interaction/using/interaction-and-offer-management.md)を参照してください。
+++

+++**オファー環境**

*コンテキスト：Campaign インタラクション*

オファー環境は、オファーカタログ、使用可能なスペースおよび環境の事前定義済みフィルターを定義するルートフォルダーです。オペレーターは、ターゲティングディメンションごとに 1 つの環境を作成する必要があります。 オファー環境には、デザインとライブの 2 つのタイプがあります。

詳しくは、[オファー環境](../../interaction/using/fundamental-principles.md)を参照してください。
+++

+++**オファーライブ環境**

*コンテキスト：Campaign インタラクション*

オファーライブ環境はキャンペーン&#x200B;**デザイン環境**&#x200B;にリンクされています。この環境には、**デザイン環境**&#x200B;でコンテンツと実施要件の承認を受けた読み取り専用のオファーが含まれています。Web サイトでの表示用に選択することも、アウトバウンドメッセージに挿入することもできます。

詳しくは、[オファーライブ環境](../../interaction/using/fundamental-principles.md)を参照してください。
+++

+++**オファープレゼンテーションルール**

*コンテキスト：Campaign インタラクション*

オファープレゼンテーションルールは、オファー環境で参照されるタイポロジルールであり、受信者の提案履歴を考慮して、オペレーターは特定のオファーを除外できます。

[オファープレゼンテーションルール](../../interaction/using/managing-offer-presentation.md#presentation-rules-overview)の詳細情報。
+++

+++**オファーのプレビュー**

*コンテキスト：Campaign インタラクション*

フォルダー内で表示されるオファーのプレビューです。オファープレビュータブまたは連絡先プロファイルからアクセスできます。

オファーのプレビューの詳細は[こちら](../../interaction/using/creating-an-offer.md#previewing-the-offer)。
+++

+++**オファーの提案**

*コンテキスト：キャンペーンインタラクション*

オファーの提案は、特定のオファースペース（web サイトのバナー、メール、SMS コンテンツなど）で連絡先にオファーを提示するアクションの結果です。 この結果は、オファー、受信者およびタイムスタンプを定義するオファー提案テーブルに格納され、受信者が受け取ったすべてのオファーの記録となります。

オファーの提案の詳細は[こちら](../../interaction/using/creating-offer-spaces.md#offer-proposition-statuses)。
+++

+++**オファー表示域**

*コンテキスト：キャンペーンインタラクション*

オファー表示域は、チャネルでオファーの表示に使用される情報です。オファー表示域は、オファーが表示されるスペースのレンダリング関数から作成でき、インターフェイス（HTML ブロックなど）に直接埋め込むこともできます。オファーはスペースに基づいて表示される場合があります。

インタラクションの詳細は[こちら](../../interaction/using/interaction-and-offer-management.md)。
+++

+++**オファーのシミュレーション**

*コンテキスト：キャンペーンインタラクション*

オファーシミュレーションを使用すると、オペレーターは、実際にオファーを送信する前に、定義した範囲（配信日、ターゲットセグメント、オファー数、テーマなど）でオファー配分をテストできます。これを使用すると、オファーの優先度と実施要件ルールを調整して、オファーの有効性を最大限に高めることができます。

オファーシミュレーションの詳細は[こちら](../../interaction/using/about-offers-simulation.md)。
+++

+++**オファースペース**

*コンテキスト：キャンペーンインタラクション*

オファースペースは、オファーの公開場所を定義するフォルダーです。スペースを定義すると、使用するチャネルの指定、オファーのコンテンツの作成、提示されるオファーの指定を行えます。 オファースペースは、チャネルとオファーエンジンの間のインターフェイスです。

詳しくは、[オファースペース](../../interaction/using/creating-offer-spaces.md)を参照してください。
+++

+++**オファーテーマ**

*コンテキスト：キャンペーンインタラクション*

オファーテーマは、カテゴリで定義されるキーワードです。オペレーターはカテゴリにより、オファーが提示されたときにそのオファーをフィルタリングできます。 テーマを使用すると、カタログ構造から階層的でない方法でオファーを選択できます。

オファーテーマの詳細は[こちら](../../interaction/using/integrating-an-offer-via-the-wizard.md)。
+++

+++**オファーの重み付け**

*コンテキスト：キャンペーンインタラクション*

オファーの重み付けは、最も関連性の高いオファーをエンジンが選択できるように、オファーの関連度を正確に定義する数式に基づいています。 重み付けはオファーで定義し、乗数はカテゴリで定義します。重み付けの順位を下げる際には実施要件を満たすオファーが考慮されます。

オファーの重み付けの詳細は[こちら](../../interaction/using/creating-an-offer.md#offer-weight)。
+++

+++**オペレーター**

オペレーターは、ログインしてアクションを実行する権限を持つ Adobe Campaign ユーザーです。オペレーターは、オペレーターグループに関連付けられ、これらのグループの権限を継承します。 また、ネームド権限をオペレーターに直接関連付けることもできます。

オペレーターの詳細は[こちら](../../platform/using/access-management-operators.md)。
+++

+++**オペレーターグループ**

オペレーターグループを使用すると、Campaign オペレーターの役割を管理できます。 権限の付与対象となるオペレーターグループを定義してから、オペレーターを 1 つ以上のグループに関連付けます。これにより、権限を再利用することや、オペレータープロファイル間の一貫性を高めることができます。また、プロファイルの管理やメンテナンスも楽になります。

オペレーターグループの詳細は[こちら](../../platform/using/access-management-groups.md)。
+++

+++**オプション**

オプションは、Campaign インスタンスの設定を定義するために使用されるプラットフォームレベルの変数です。オプションでは、期間（データベースクリーンアップワークフローなど）やその他のグローバル定義をプラットフォームレベルで定義できます。

オプションの詳細は[こちら](../../installation/using/configuring-campaign-options.md)。
+++

+++**アウトバウンドインタラクション**

*コンテキスト：キャンペーンインタラクション*

アウトバウンドインタラクションは、（メールやダイレクトメールの配信に使用される）連絡先リストからインタラクションエンジンへの呼び出しを意味します。各連絡先に同じルールとプロセスが適用されます。通常、このタイプのインタラクションはバッチモードで処理されます。

アウトバウンドインタラクションの詳細は[こちら](../../interaction/using/about-outbound-channels.md)。
+++

+++**パッケージのエクスポート／インポート**

パッケージエクスポートは、オブジェクトの定義を含んだ XML ファイルの生成で構成される操作です。パッケージは、インスタンス間で機能と定義を移行するために使用されます。また、バックアップシステムやソース管理システムに重要な製品定義を追加する場合にも使用します。

[パッケージのエクスポート／インポート](../../platform/using/working-with-data-packages.md)の詳細情報。
+++

+++**パレット**

ワークフローパレットには、ワークフローに追加できる使用可能なアクティビティが表示されます。このコンポーネントは、ワークフローアクティビティが用途別に論理的にグループ化され、タブ形式で表示されます。パレットで使用可能なアクティビティは、Campaign インスタンスにインストールされているアドオンおよびワークフローを表示するコンテキストによって決まります。

パレットについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/build-a-workflow.html#add-and-link-activities){target="_blank"} を参照してください。
+++

+++**パフォーマンス監視**

「監視」タブにパフォーマンス監視情報が表示されます。メモリと CPU 使用率、SMTP サーバーの統計、サーバープロセス、その他の関連情報など、基になるシステムの指標が表示されます。

詳しくは、[パフォーマンス監視](../../production/using/monitoring-processes.md)を参照してください。
+++

+++**パーソナライゼーションブロック**

Adobe Campaign は、配信に挿入できるビルトインのパーソナライゼーションブロックを提供しています。動的でパーソナライズされ、特定のレンダリングが含まれています。例えば、ロゴ、挨拶メッセージまたはミラーページへのリンクを追加できます。デフォルトでは、複数のパーソナライゼーションブロックを使用できます。また、カスタムパーソナライゼーションブロックを定義することで、配信のパーソナライゼーションを最適化できます。実際のデータは、配信の分析フェーズで、生成された各メッセージに挿入されます。

[パーソナライゼーションブロック](../../delivery/using/personalization-blocks.md)の詳細情報。
+++

+++**パーソナライゼーションフィールド**

パーソナライゼーションフィールドは、特定の受信者に対する配信をパーソナライズする際に使用される単一のデータフィールド参照です。実際のデータ値は、配信分析フェーズで挿入されます。

[パーソナライゼーションフィールド](../../delivery/using/personalization-fields.md)の詳細情報。
+++

+++**パーソナライゼーション変数**

パーソナライゼーション変数は、受信者の情報に基づいて様々なテキストを様々な受信者に表示できる、配信のコードの一部です。これらのフィールドは、パーソナライゼーションフィールドまたはブロックとして実装できます。

[パーソナライゼーション変数](../../delivery/using/about-personalization.md)の詳細情報。
+++

+++**プラン**

プランとは、カレンダー単位でマーケティングアクティビティを整理するために使用されるフォルダータイプです。エクスプローラービューのプランフォルダーは、年、四半期、月など、時間に基づく単位を定義します。プランフォルダーはネストでき、他のプランフォルダー、プログラムフォルダーまたはキャンペーンを含むことができます。

プランについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/set-up-campaigns.html?lang=ja){target=_blank} を参照してください。
+++

+++**定義済みフィルター**

定義済みフィルターは、再利用のために保存されたクエリです。定義済みフィルターを使用すると、生産性が向上し（作成は 1 回のみなので）、一貫性を構築し（すべてのマーケターが使用できるので）、マーケター自身では作成できないようなコードやロジックを使用できるため、マーケターに必要とされるスキルを低減できます。

フィルターについて詳しくは、[Campaign v8 （コンソール）ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/audience/create-filters){target=_blank} を参照してください。
+++

<!--
----DEPRECATED----
+++**Predictive Engagement Scoring**

Predictive engagement scoring predicts the probability of a recipient engaging with a message and the probability of opting out (unsubscribing) within the next seven days after the next email send. The probabilities are further divided into buckets according to the specific risk of disengagement, medium, or low. The model also provides the risk percentile rank for the customers to understand where the rank of a certain customer in relation to others. 

Learn more about [Predictive Engagement Scoring](../../platform/using/creating-filters.md).
+++
-->

+++**プライマリキー**

プライマリキーは、データベーステーブル内の各レコードの一意の ID です。テーブルには少なくとも 1 つのキーが必要です。原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。プライマリキーを複合する（複数のフィールドを含める）ことはできません。

[プライマリキー](../../configuration/using/schema/key.md)の詳細情報。
+++

+++**プロファイル**

プロファイルとは、エンド顧客、見込み客またはリードを表す情報のレコードです。各プロファイルは、Cookie ID、顧客 ID、モバイル識別情報または特定のチャネルに関連するその他の情報が含まれている nmsRecipient テーブルまたは外部テーブル内のレコードに対応します。

[プロファイル](../../platform/using/about-profiles.md)の詳細情報。
+++

+++**プログラム**

プログラムとサブプログラムフォルダーは、ロイヤルティ、獲得、クロスセルなど、ビジネス目標に関するマーケティングアクティビティを整理します。また、会計期間やキャンペーン戦術（イベントやニュースレターなど）を表すこともできます。各プログラムには、1 つのカレンダーにリンクされた複数のキャンペーンが含まれており、カレンダーで全体像を把握できます。

プログラムについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-orchestration/set-up-campaigns.html?lang=ja){target=_blank} を参照してください。
+++

+++**パブリックリソース**

Adobe Campaign のパブリックリソースフォルダーには、アプリケーションサーバーがホストする画像が格納されます。配信内の画像を電子メールなどの配信に表示するには、アプリケーションサーバー（または Campaign が設定されている場合は画像ホスティングサーバー）に公開する必要があります。

詳細情報：[パブリックリソース](../../installation/using/deploying-an-instance.md#managing-public-resources)。
+++

+++**プッシュ**

*コンテキスト：モバイルアプリチャネル*

プッシュ通知は、モバイルアプリケーションが受信するメッセージです。プッシュ通知は、モバイルアプリケーションに Experience Platform SDK コードを含めることで、Adobe Campaign で機能するように設定されます。プッシュの場合、iOS と Android の 2 つの配信チャネルを使用できます。

詳細情報：[プッシュ](../../delivery/using/about-mobile-app-channel.md)。
+++

## Q - T {#sec-5}

+++**受信者**

Adobe Campaign では、受信者は、顧客への配信（メール、SMS など）の送信先となるデフォルトプロファイルです。データベースに格納された受信者データを使用すると、ターゲットをフィルタリングし、パーソナライゼーションデータを追加できます。通常、これは個人情報、連絡先情報、デモグラフィック情報およびトランザクション情報ですが、マーケティングや分析をサポートするあらゆる種類の情報が対象となります。

詳細情報：[受信者](../../configuration/using/about-data-model.md)。
+++

+++**レンダリング関数**

*コンテキスト：Campaign インタラクション*

レンダリング関数は、オファースペースで定義されます。これは、オファーで定義された属性に基づいてオファー表示域を構築するために使用します。レンダリング関数のモードには、HTML、XML、テキストの 3 種類があります。

詳細情報：[レンダリング関数](../../interaction/using/creating-offer-spaces.md)。
+++

<!--
-----DID NOT FIND IN ACC DOCS, ACS?----
+++**Retargeting campaigns**

Campaigns that re-target the recipients of a previous delivery or deliveries.
+++
-->

+++**スキーマ**

スキーマは、データベーステーブルに関連付けられた XML ドキュメントです。データ構造を定義し、表の SQL 定義を記述します。オペレーターが Campaign および製品でスキーマを操作すると、必要な SQL にそのアクションが変換され、データベースに対して実行されます。

詳細情報：[スキーマ](../../configuration/using/about-schema-reference.md)。
+++

+++**スキーマ拡張**

スキーマ拡張を使用すると、標準のスキーマを、ビジネスのユースケースに最適にカスタマイズできます。例えば、受信者テーブルに「ロイヤルティ」フィールドを追加できます。

詳しくは、[スキーマ拡張](../../configuration/using/extending-a-schema.md)を参照してください。
+++

+++**シードアドレス**

シードアドレスは、定義されたターゲット条件に一致しない受信者を配信のターゲットにする場合に使用されます。これにより、配信スコープ外の受信者が他のターゲット受信者と同様に配信を受信することができます。受信者データベースの不正使用を検出したり、確実に配信したりすることを目的に、これらをメッセージのオーディエンスに追加します。

詳細情報：[シードアドレス](../../delivery/using/about-seed-addresses.md)。
+++

<!--
-------ACS?-----
+++**Send-time optimization**

To improve the open rate of your messages, you can manually define a sending time per recipient. Each profile will receive the message at the specified date and time, whenever possible. Defining a sending time can be done at the delivery level or using a workflow.

Learn more about [Send-time optimization](../../delivery/using/about-seed-addresses.md:).
+++
-->

+++**サービス**

Adobe Campaign では、ニュースレターや製品のアップデートなどの情報サービスを作成および管理したり、そのサービスの購読を管理したりできます。複数のサービスを並行して定義できます。

詳細情報：[サービス](../../delivery/using/about-services-and-subscriptions.md)。
+++

+++**SFTP 管理**

コントロールパネルでは、アクセス権のあるインスタンスに接続しているすべての SFTP サーバーとやり取りできます。 コントロールパネルを使用すると、SFTP サーバーに対して、ストレージ容量の監視、IP アドレスの許可リストへの登録、SSH 公開鍵の管理などのアクションを実行できます。

詳細情報：[SFTP 管理](https://experienceleague.adobe.com/docs/control-panel/using/sftp-management/about-sftp-management.html?lang=ja)。
+++

+++**購読サービスアクティビティ**

購読サービスワークフローのアクティビティでは、トランジションで指定された母集団の情報サービスに対する購読を作成または削除できます。

購読サービスアクティビティについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/subscription-services.html?lang=ja){target="_blank"} を参照してください。
+++

+++**ターゲットの承認**

*コンテキスト：Campaign 分散型マーケティング*

ターゲットの承認とは、別のオペレーターまたはオペレーターのグループに（分析フェーズでターゲットが生成された後に）、配信の最終ターゲットを配信が送信される前に承認してもらうプロセスです。

ターゲットの承認アクティビティについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/flow-control-activities/approval.html){target="_blank"} を参照してください。
+++

+++**データのターゲット**

ターゲットデータとは、ワークフローのワークテーブル（トランジション）に保存されるデータです。このデータは、配信内で配信コンテンツのパーソナライゼーション用に使用したり、配信の動的要素のロジックを定義したりできます。

ターゲットデータについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/use-workflow-data.html#target-data){target="_blank"} を参照してください。
+++

+++**ターゲットマッピング**

ターゲットマッピングとは、配信チャネルを特定のデータタイプにマッピングすることです。ターゲットマッピングは、様々な配信チャネルからスキーマのデータフィールドへのリンク方法を定義します。特定のフィールドまたは式を使用して、Campaign がデータタイプにどのように送信するかを定義します。

ターゲットマッピングについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/audience/add-profiles/target-mappings.html?lang=ja){target="_blank"} を参照してください。
+++

+++**ターゲティングアクティビティ**

ターゲティングアクティビティは、ターゲティング、母集団データの操作およびフィルタリングアクティビティに固有のワークフローアクティビティです。セットを定義するか、積集合、和集合、除外の各操作を使用して分割または結合することで、オペレーターが 1 つまたは複数のターゲットを作成できます。

ターゲティングアクティビティについて詳しくは、[Campaign v8 ドキュメント ] （https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/targeting-activities/targeting-activities）を参照してください
.html） {target="_blank"}.
+++

+++**ターゲティングディメンション**

ターゲティングディメンションとは、クエリまたは他のワークフローアクティビティによって生成される（返される）データタイプのことです。Adobe Campaign は、取得に使用されたクエリに関係なく、応答データベース行のプライマリキーのみを返すことに注意してください。

ターゲティングディメンションについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/introduction/wf-type/targeting-workflows.html){target="_blank"} を参照してください。
+++

+++**タスクアクティビティ**

*コンテキスト：マーケティングリソース管理（MRM）*

タスクワークフローアクティビティでは、ワークフローのロジックに人間が介入してアクションを実行します。指定できるのは 2 つのシナリオで、ひとつはタスクが完了した場合、もうひとつはタスクが完了していない場合です。一般的なユースケースは、オフラインアクションをキャンペーンに組み込む場合や、承認などのカスタムアクションを組み込む場合です。

Ask アクティビティについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/mrm/creating-and-managing-tasks.html?lang=ja){target="_blank"} を参照してください。
+++

<!--
-----NOT USEFUL, detail-----
+++**Task**

One iteration of the defined functionality of a workflow activity. Each execution of a task has a unique task identifier.   

Learn more about [Tasks](../../workflow/using/about-workflows.md).
+++
-->

+++**テンプレート**

テンプレートは、オブジェクトの作成に使用するデザイン要素です。オブジェクト設定が含まれているほか、オブジェクトのコンテンツが含まれている場合もあります。テンプレートシステムは、Adobe Campaign の配信、キャンペーン、ワークフロー、その他多くの要素を作成するために使用されます。使用可能なファクトリテンプレートは、インストールされたパッケージで定義されます。テンプレートはその後、必要に応じて Campaign オペレーターによって複製およびカスタマイズされます。
+++

<!--
-----ACS -> SEEDS IN ACC-----
+++**Test profiles**

Allows targeting of additional recipients who do not match the defined targeting criteria. They are added to a message's audience to detect any fraudulent use of your recipient database or to ensure delivery. Seen as the Seed type in the Campaign interface.

Learn more about [Test profiles](../../workflow/using/about-workflows.md).
+++
-->

<!--
-----NOT FOR DOCS?-----
+++**Total database storage**

The aggregate size of the production and non-production instance(s) database storage managed by Adobe. 

Learn more about [Total database storage](../../workflow/using/about-workflows.md).
+++
-->

+++**トラッキングログ**

配信が送信され、トラッキングがアクティブ化されると、トラッキングテクニカルワークフローはトラッキングデータを取得します。このデータは、配信の「トラッキング」タブに表示されます。メールの開封やクリックなど、受信者が受け取ったメッセージに対する操作の情報を確認できます。

トラッキングログの詳細は[こちら](../../delivery/using/accessing-the-tracking-logs.md)。
+++

+++**トランザクションメッセージング**

トランザクションメッセージングは、外部の情報システムで送信されたイベントから生成されるカスタムトリガー通知を管理するために設計された Campaign モジュールです。トランザクションメッセージは web サイトなどのプロバイダーがリアルタイムに送信する、個々に向けたユニークなコミュニケーションです。受信者が確認したい重要な情報が含まれているので、早い送信が特に期待されます。

トランザクションメッセージングの詳細は[こちら](../../message-center/using/about-transactional-messaging.md)。
+++

&lt;!------- ここで役に立ちます??----->
+++**トリガーキャンペーン**

トリガーキャンペーンとは、ワークフローで API リクエストを受け取ったときに実行されるキャンペーンです。 API 呼び出しは、ワークフローの実行を開始するワークフローでシグナルアクティビティによって消費されます。

トリガーキャンペーンについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/wf-activities/flow-control-activities/external-signal.html){target="_blank"} を参照してください。
+++

<!--
-----NOT USEFUL-----
+++**Triggers**

Signals that initiate execution of a workflow, delivery or other action. Typically an API call. 

Learn more about [Triggers](../../workflow/using/about-workflows.md).
+++
-->

+++**タイポロジ**

*コンテキスト：キャンペーンの最適化*

タイポロジとは、配信の分析フェーズに適用されるタイポロジルールのグループです。キャンペーンタイポロジには、複数のタイポロジルールを含めることができますが、1 つの配信では 1 つのタイポロジしか参照できません。

タイポロジについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/campaign-typologies.html?lang=ja){target="_blank"} を参照してください。
+++

+++**タイポロジルール**

*コンテキスト：キャンペーンの最適化*

タイポロジルールは、配信の分析フェーズの一環として実装されるビジネスルールです。 タイポロジルールとは、配信の内容（コントロールルール）や配信のターゲット（フィルタールール）、またはビジネス要件を実施するその他のロジック（頻度ルール）を確認するものです。ルールは、1 つ以上のタイポロジに含めることができる、粒度の細かい要素です。

タイポロジルールについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/campaign-optimization/campaign-typologies.html?lang=ja){target="_blank"} を参照してください。
+++

## U～Z {#sec-6}

+++**単一モード**

*コンテキスト：キャンペーンインタラクション、トランザクションメッセージング*

単一モードでは、実行時にオファーエンジンによって 1 つの連絡先だけが処理されます。 通常、このモードはインバウンドインタラクションとトランザクションメッセージで使用します。

単一モードの詳細は[こちら](../../interaction/using/about-inbound-channels.md)。
+++

+++**Web アプリケーション**

Web アプリケーションは、Campaign インスタンスでホストされる動的かつインタラクティブなアプリケーションページです。データベースのデータと、接続したユーザーの権限に応じたコンテンツが含まれます。 例えば、エクストラネット上の編集フォームや、テーブル、グラフ、入力フォームなどでデータベースのデータを組み込んだ通知フォームを作成できます。この機能を使用すると、ユーザーが情報を検索または入力できる web ページをデザインしてポストできます。

Web アプリケーションの詳細は[こちら](../../web/using/about-web-applications.md)。
+++

+++**ワークフロー**

ワークフローは、キャンペーン実行フローを視覚的に表現したものです。 アプリケーションサーバーの様々なモジュールにわたって、あらゆるプロセスとタスクのオーケストレーションを行えます。総合的なグラフィカル環境により、セグメント化、キャンペーン実行、ファイル処理、手作業での処理などのプロセスをデザインできます。これらのプロセスは、ワークフローエンジンが実行し、トラッキングします。

ワークフローの詳細は[こちら](../../workflow/using/about-workflows.md)。
+++

+++**ワークフロージャーナル**

ワークフロージャーナルは、ワークフローの段階的な実行ログです。 ワークフローのすべての履歴や監査記録が含まれています。開発、トラブルシューティングまたはデバッグの目的で使用されます。

ワークフロージャーナルについて詳しくは、[Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/automation/workflows/monitoring-workflows/monitor-workflow-execution.html?lang=ja){target="_blank"} を参照してください。
+++

+++**ワークテーブル**

ワークテーブルには、ワークフロートランジションで扱うすべての情報が含まれています。各ワークフローは、複数のワークテーブルを使用します。ワークテーブルには、起点となるアクティビティの結果が格納されており、その内容が、ワークフロー内の次の（接続されている）アクティビティに対する入力として使用されます。ワークテーブルの操作（拡張、カスタマイズ）は、Adobe Campaign オペレーターの主なスキルの 1 つです。

ワークテーブルの詳細は[こちら](../../workflow/using/about-workflows.md)。
+++
