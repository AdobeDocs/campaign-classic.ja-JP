---
product: campaign
title: Adobe Campaignの用語集
description: Adobe Campaignの用語集
role: User, Data Architect
level: Beginner
hide: true
hidefromtoc: true
source-git-commit: 8aa45f4e9d41b7dc4faf89dad988703b63cea77c
workflow-type: tm+mt
source-wordcount: '6454'
ht-degree: 13%

---

# Adobe Campaign用語集{#ac-glossary}

Adobe Campaignの主な用語と概念の定義と関連ドキュメントへのリンクを以下に示します。 用語をクリックして定義を表示します。

## A ～ D{#sec-1}

+++**A/B テスト**

A/B テストは、ユーザーが 2～3 種類の E メールのバリエーションを定義できる機能です。どのバリアントが最適な結果を得られるかを判断するために、各バリアントが母集団サンプルに送信されます。 結果が明確になったら、勝者バリアントが残りの母集団に送信されます。

詳細情報： [A/B テスト](../../delivery/using/get-started-a-b-testing.md).
+++

+++**アクセス管理**

アクセス管理を使用すると、管理者は、Adobe Campaignのユーザーにアクセス権と権限を割り当てることができます。 権限には、ワークフローの実行、スキーマの定義、オーディエンスの管理など、Adobe Campaign機能の表示や使用の機能が含まれます。

詳細情報： [アクセス管理](access-management.md).
+++

+++**ACS コネクタ**

ACS コネクタ (Prime Offering) は、Adobe Campaign v7 とAdobe Campaign Standardを橋渡しします。 Campaign v7 の統合機能で、Campaign Standard にデータを自動的にレプリケートして、両方のアプリケーションの優れた機能を連携させます。Campaign v7 には、プライマリマーケティングデータベースを管理する高度なツールがあります。Campaign v7 からのデータレプリケーションにより、Campaign Standard の使いやすい環境でリッチデータを活用できます。

詳細情報： [ACS コネクタ](../../integrations/using/acs-connector-principles-and-data-cycle.md).
+++

+++**アクティビティ**

「アクティビティ」は、実行機能を定義するためにワークフローに追加されるパレット項目です。 アクティビティは、タスクを実行するコンテナです。 ワークフローでは、特定のアクティビティが複数のタスクを生成できます。特に、ループまたは繰り返し（定期的）アクションがある場合です。

詳細情報： [ワークフローアクティビティ](../../workflow/using/about-activities.md).
+++

+++**アクティブなプロファイル**

過去 12 ヶ月間にいずれかのチャネルを介してターゲット設定されたまたは通信を受けたプロファイルが、アクティブなプロファイルと見なされます。各 Campaign インスタンスには、契約に従って特定数のアクティブなプロファイルがプロビジョニングされ、課金用にその数がカウントされます。

詳細情報： [アクティブなプロファイル](about-profiles.md#active-profiles).
+++

+++**承認ワークフローアクティビティ**

*コンテキスト：キャンペーン分散型マーケティング*

「ローカルの承認」アクティビティは、メッセージが送信される前に配信の承認プロセスを設定するために使用されるワークフローアクティビティです。

詳しくは、 [ローカルの承認アクティビティ](../../workflow/using/local-approval.md).
+++

+++**オーディエンス**

オーディエンスとは、ルールと属性に基づいて、フィルター定義の条件を満たすプロファイルの結果セットです。

詳細情報： [オーディエンス](../../campaign/using/marketing-campaign-target.md).
+++

+++**監査記録**

監査記録を使用すると、Adobe Campaign のインスタンス内で発生するアクションとイベントの包括的なリストをリアルタイムで記録できます。データの履歴にアクセスして次のような質問に回答するためのセルフサービスが含まれています。ワークフローに対する影響、最後にワークフローを更新したユーザー、またはインスタンスでのユーザーの操作内容。

詳細情報： [監査証跡](../../production/using/audit-trail.md).
+++

+++**自動キャンペーン**

スケジュールに従って実行されるキャンペーン（誕生日または記念日を持つ受信者をターゲティングする場合など）。 また、前日購入したユーザーや、明日支払い期限があるユーザーなど、ルックアヘッドおよびルックバックロジックの実行に使用できます。

詳細情報： [キャンペーン](../../campaign/using/designing-marketing-campaigns.md).
+++

+++**バッチモード**

*コンテキスト：キャンペーンインタラクション*

キャンペーンインタラクションのコンテキストでは、バッチモードを使用すると、一連の連絡先に最適なオファー（複数可）をオファーエンジンで選択できます。 実施要件/優先順位付けルールは、すべての連絡先に適用されます。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**キャンペーン**

Campaign は、マーケティングキャンペーンを調整、定義、実行するためのインターフェイスです。 キャンペーンには、1 つ以上のワークフロー、配信、ドキュメント、その他の関連データポイントを、使いやすい単一のインターフェイスに含めることができます。

詳細情報： [キャンペーン](../../campaign/using/designing-marketing-campaigns.md).
+++

+++**切り替えプロセス**

*コンテキスト：キャンペーンインタラクション*

Campaign のインタラクションのコンテキストでは、変更プロセスは、特定の環境で有効化されるプロセスで、連絡先が明示的または暗黙的に特定されなかった場合に匿名環境に通話を転送します。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**チャネル**

チャネルとは、通信が送信される媒体です。 Adobe Campaignの組み込みチャネルは、E メール、SMS、ダイレクトメール、プッシュ通知、LINE およびTwitterです。 カスタムチャネルは、非標準のチャネル要件に対して実装できます。

詳細情報： [チャネル](../../delivery/using/communication-channels.md).
+++

+++**クライアントコンソール**

Campaign クライアントコンソールは、Campaign アプリケーションサーバーに接続できるリッチクライアントです。 クライアントコンソールの実行可能ファイル (.exe) アプリケーションは、Microsoft Windows オペレーティングシステムを搭載したコンピューターにインストールされます。 Campaign クライアントコンソールは、すべての機能と設定を一元化します。

詳細情報： [クライアントコンソール](../../platform/using/adobe-campaign-workspace.md).
+++

+++**コンテンツの承認**

コンテンツの承認とは、別のオペレーターまたはオペレーターのグループに、配信のコンテンツを送信する前に承認してもらうプロセスです。

詳細情報： [コンテンツの承認](../../campaign/using/marketing-campaign-approval.md).
+++

+++**コントロール母集団**

コントロール母集団を使用すると、キャンペーンのオーディエンスの一部を除外して、キャンペーンの影響を測定できます。 オペレーターは、メッセージを受信したターゲット母集団の行動と、ターゲット設定されていない連絡先の行動を比較できます。 オペレーターは、送信ログに基づいて、今後のキャンペーンでコントロール母集団をターゲットにすることもできます。

詳細情報： [コンテンツの承認](../../campaign/using/marketing-campaign-target.md#defining-a-control-group).
+++

+++**コントロールパネル**

このCampaign コントロールパネルを使用すると、各インスタンスの設定を管理したり使用状況を追跡したりできるので、Adobe Campaignの製品管理者としての作業の効率を向上できます。 直感的なインターフェイスにより、主要なアセットの使用状況を簡単に監視できるうえ、IP アドレスの許可リスト登録、SFTP ストレージの監視、鍵の管理などの管理タスクを実行できます。

詳細情報： [コンテンツの承認](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/key-features.html?lang=ja).
+++

+++**キューブ**

*コンテキスト：マーケティング分析*

キューブは、Adobe Campaignの直感的なデータ調査ツールで、動的レポートの作成と共有に役立ちます。

詳細情報： [キューブ](../../reporting/using/about-cubes.md).
+++

+++**カスタムリソース**

Adobe Campaignには事前定義済みのデータモデルが付属しています。このモデルでは、様々なパッケージのインストールを通じてデータタイプが定義されます。 オペレーターは、リソースを拡張してカスタムフィールドや、トランザクションテーブルや製品テーブルなどのカスタムテーブルを追加することで、提供されるデータモデルをエンリッチメントできます。

詳細情報： [カスタムリソース](../../configuration/using/about-schema-edition.md).
+++

+++**データモデル**

Campaign データモデルは、データタイプとその関係（リンク）を定義する一連のスキーマです。 データモデルは、実際のデータを含むデータベースと物理的に実装される抽象定義です。

詳細情報： [カスタムリソース](../../configuration/using/about-data-model.md).
+++

+++**データベースクリーンアップワークフロー**

データベースクリーンアップワークフローは、データベースの急激な増加を避けるために古いデータを削除します。 ワークフローは、ユーザーの操作なしで自動的にトリガーされます。

詳細情報： [データベースクリーンアップワークフロー](../../production/using/database-cleanup-workflow.md).
+++

+++**専用サーバー**

*コンテキスト：トランザクションメッセージ*

トランザクションメッセージを利用する専用の実行サーバー。 通常、1 台のサーバーで 1 時間に最大 50,000 件のエンジン呼び出しを処理できます。 Adobeが仮想化テクノロジーを利用して同等の効果を実現する可能性があるため、「専用サーバごと」の指定に物理サーバとの 1 対 1 の相関関係があるとは限りません。

詳細情報： [トランザクションメッセージ](../../message-center/using/about-transactional-messaging.md).
+++

+++**配信品質**

*コンテキスト：E メールの配信品質*

オペレーターがバウンスしたりスパムとしてマークされたりせずに受信者の受信ボックスに到達した場合のキャンペーンの成功を測定できる指標です。

詳細情報： [配信品質](../../delivery/using/about-deliverability.md).
+++

+++**配信**

配信とは、特定のチャネル（E メール、SMS、プッシュ通知など）でオーディエンスに送信される、特定のマーケティングコミュニケーション項目です。 マーケティング用語の「タッチ」とも呼ばれます。

詳細情報： [配信](../../delivery/using/communication-channels.md).
+++

+++**配信分析**

配信分析は、配信の準備です。 このプロセスは、コンテンツと受信者のプロファイルデータを組み合わせて、受信者が受け取るパーソナライズされた E メールを生成します。 配信分析ロジックでは、定義されたロジックに基づいて、受信者をターゲットから除外したり、配信を完全に停止したりできます。 このプロセスには、動的コンテンツロジックの評価と、個々の受信者プロファイルに固有のオファーの挿入も含まれます。

詳細情報： [配信分析](../../delivery/using/steps-validating-the-delivery.md#analyzing-the-delivery).
+++

+++**配信ログ**

配信ログには、メッセージの送信時に生成される情報が含まれます。 これらのログは、送信の詳細を示します。メッセージは、準備済み、無視、送信済みまたは失敗済みです。 配信レポートには、配信ダッシュボードから直接アクセスできます。

詳細情報： [配信ログ](../../delivery/using/delivery-dashboard.md#delivery-logs-and-history).
+++

+++**配信の基本**

*コンテキスト：E メールの配信品質*

Adobe Campaign Deliverability Fundamentals コンサルティングサービスは、Adobe Campaign配信を使用するお客様をサポートする、E メール配信品質のコンサルティングと評判の管理を提供します。

詳細情報： [配信品質](../../delivery/using/about-deliverability.md).
+++

+++**配信の概要**

*コンテキスト：ダイレクトメール*

配信の概要は、 これらは、会社が特定のキャンペーン用に作成したものです。これは、ダイレクトメール配信のコンテキストで使用されます。

詳細情報： [ダイレクトメール](../../delivery/using/about-direct-mail-channel.md).
+++

+++**デプロイウィザード**

デプロイウィザードでは、デフォルトの名前空間、データベースクリーンアップスケジュール、データ保持期間、その他の技術的設定など、Campaign インスタンスのパラメーターを定義します。

詳細情報： [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).
+++

+++**記述的分析**

記述的分析は、状況に応じたレポートツールで、ワークフローの作業用テーブル内のデータや、フォルダー内で選択されたデータを調べたり、選択した配信のターゲットや除外の詳細を調べたりできます。

詳細情報： [記述的分析](../../reporting/using/about-descriptive-analysis.md)
+++

+++**分散型マーケティング**

*コンテキスト：分散型マーケティング*

分散型マーケティングのアドオンオファーは、Campaign オペレーターに対して、セントラルエンティティ（本社、マーケティング部門など）間でキャンペーンを実装するための協調ワークスペースとして使用され、 ローカルエンティティ（販売店、地域代理店など）との共同作業によるキャンペーンを実装できます。この連携は、 **キャンペーンパッケージのリスト**：一元的に作成されたキャンペーンのテンプレートとインスタンスが、ローカルエンティティに提供されます。

詳細情報： [分散型マーケティング](../../distributed/using/about-distributed-marketing.md)
+++

+++**値の配分**

値の配分は、データベースに現在存在するスキーマ属性の値の配分を表示するツールです。 これにより、使用可能な値、その数と割合を判断し、クエリや式を作成する際の値の大文字と小文字の区別やスペルの問題を回避できます。

詳細情報： [分散型マーケティング](../../platform/using/defining-filter-conditions.md#selecting-data-to-extract)
+++

+++**ドメインデリゲーション**

サブドメイン設定を使用すると、Adobe Campaignで使用するドメインのサブセクション（技術的には「DNS ゾーン」）を設定できます。
ドメインデリゲーションを使用すると、Adobeは、E メールキャンペーンの配信、レンダリング、トラッキングに必要な DNS のあらゆる側面を制御および管理できます。

詳細情報： [ドメインのデリゲーション](https://experienceleague.adobe.com/docs/control-panel/using/subdomains-and-certificates/setting-up-new-subdomain.html?lang=ja)
+++

## E - H {#sec-2}

<!--
+++**E4X**

The version of Javascript that is used in Adobe Campaign Classic. Sometimes called ECMAScript, it is an extension of Javascript that allows the mixing of Javascript and XML primitives in the same code. Note that E4X is classified as a deprecated language. 
+++
-->

+++**実施要件ルール**

*コンテキスト：キャンペーンインタラクション*

実施要件ルールは、有効期間、ターゲットおよび重み付けに関して環境、カテゴリまたはオファーに適用される制約です。 オファーがターゲットとする連絡先に適合していることをオペレーターが確認できます。 オファー環境では、実施要件ルールには、オファーに適用されるプレゼンテーションルールと、ターゲットにする受信者が含まれます。 カテゴリの実施要件ルールを使用すると、オペレーターは、カテゴリの有効期間を制限し、アプリケーションテーマを定義し、ターゲットにする受信者を決定できます。 また、特定の期間に乗数の重み付けを定義することもできます。 これにより、オペレーターは他のカテゴリのオファーに対するルールを共有できるので、オファーの管理が簡単になります。 オファーでは、実施要件ルールを使用して、オペレーターはオファーの有効期限を制限し、ターゲットにする受信者を決定できます。

詳細情報： [実施要件ルール](../../interaction/using/interaction-and-offer-management.md).
+++

+++**適格なオファー**

*コンテキスト：キャンペーンインタラクション*

適格なオファーとは、上流で定義された制約に一致し、ターゲットに一貫して提供できるオファーです。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**BCC で E メールを送信**

「BCC で E メールを送信」機能では、対応する配信 E メールの正確なコピーを EML 形式で送信します。この E メールは専用の BCC E メールアドレスに保存され、E メールを処理して外部システムにアーカイブできます。

詳細情報： [BCC で E メールを送信](../../delivery/using/email-parameters.md#email-bcc).
+++

+++**E メールボリュームのコミット**

1 年間に予想される、注文に記載される E メールの数。 これは、次のような配信エラーが原因で送信されたが配信されなかった E メールを含む、年間合計 E メール量のコミットメントです。E メールアドレスエラー、ハードバウンス、ソフトバウンス、E メールクライアントの E メールフィルター、E メールブラックリストなどを含む、ただしこれらに限定されないメッセージの配信不能。
+++

+++**エンジン呼び出し**

エンジン呼び出しは、調査、Web アプリ、JSSP、API、モバイルアプリ登録などに関するデータの抽出に関して、サーバー側でリアルタイム処理を開始するサーバー呼び出しです。 エンジン呼び出しは、1 日に 5,000 個のエンジン呼び出しのパックでライセンスを受ける必要があります。
+++

+++**エンリッチメントアクティビティ**

「エンリッチメント」アクティビティは、ワークフロー内で処理される、生成された作業用テーブルデータをオペレーターがエンリッチメントできる高度なワークフローアクティビティです。 このアクティビティは、通常、ターゲティングアクティビティの後、またはファイルをインポートした後、およびターゲットデータを使用するアクティビティの前に使用されます。 エンリッチメントでは、インバウンドトランジションデータを変換し、拡張データを使用して出力トランジションを完了するようにアクティビティを設定できます。 オペレーターは、複数のデータセットのデータを組み合わせたり、一時的なリソースへのリンクを作成したりできます。

詳細情報： [エンリッチメントアクティビティ](../../workflow/using/enrichment.md).
+++

+++**列挙**

列挙とは、フィールドの有効な入力値を定義するスキーマまたは Platform レベルで定義されたデータ型です。 列挙は、ユーザーインターフェイスとクエリビルダーで候補リストとして表示されます。

詳細情報： [列挙](../../platform/using/managing-enumerations.md).
+++

+++**エクスプローラービュー**

エクスプローラービューは、Adobe Campaignのアーティファクトおよびデータを格納したフォルダーを階層的に表示します。 Adobe Campaignのフォルダーシステムは、通常のツリービューとは異なり、各フォルダーには配信、ワークフロー、オファーなどの特定のタイプのデータが格納されます。

詳細情報： [エクスプローラービュー](../../platform/using/adobe-campaign-explorer.md).
+++

+++**外部アカウント**

外部アカウントは、製品が他の環境やテクノロジーに接続するための入口と出口です。 外部アカウントは、製品が他のソースとの間でデータの送受信に使用する接続パラメーターを定義します。 一般的な外部アカウントのタイプは、SFTP サイトの接続、SMS の送信をサポートする通信、処理バウンス用のメールボックス、外部データベースへの接続です。

詳細情報： [外部アカウント](../../installation/using/external-accounts.md).
+++

+++**疲労管理**

*コンテキスト：キャンペーンの最適化*

疲労管理は、受信者の過剰勧誘を避けるために、メッセージの頻度と数量を制御するのに役立ちます。多くの場合、メッセージはタイポロジルールを使用して適用されます。

詳細情報： [疲労管理](../../campaign-opt/using/pressure-rules.md).
+++

+++**Federated Data Access（FDA）**

Federated Data Access は、クライアントデータモデルの拡張をサポートし、サードパーティのデータベースを含めます。 ターゲットテーブルの構造を自動的に検出し、SQL ソースのデータを使用します。Adobe Campaignデータの構造を変更しなくても、外部データにアクセスできます。

詳細情報： [Federated Data Access](../../installation/using/about-fda.md).
+++

+++**ファイル抽出の承認**

*コンテキスト：ダイレクトメール*

ファイル抽出の承認は、別のオペレーターまたはオペレーターグループに、抽出したファイルのコンテンツと設定を、ダイレクトメール配信などの外部ベンダーに送信する前に承認してもらうプロセスです。

詳細情報： [ファイル抽出の承認](../../delivery/using/validating.md).
+++

+++**フィルタリングディメンション**

フィルタリングディメンションは、クエリが目的の行をフィルタリングするために使用するデータまたは属性を含むスキーマです。 Adobe Campaignがデータベース結合をクロスし、回答者行を返せるように、「フィルタリングディメンションスキーマ」は、定義されたターゲティングディメンションに直接リンクされている必要があります。

詳細情報： [フィルタリングディメンション](../../workflow/using/building-a-workflow.md#targeting-and-filtering-dimensions).
+++

+++**フォルダー**

フォルダは、特定のデータ型のデータベースレコードを格納するエクスプローラビュー項目です。 例外は、整理要素として使用され、データ自体は含まれず、他のフォルダーのみを含む汎用フォルダータイプです。

詳細情報： [フォルダー](../../platform/using/adobe-campaign-explorer.md).
+++

+++**フォルダー表示**

フォルダビューは、特別なエクスプローラフォルダタイプで、選択したデータタイプのすべてのレコードを、そのデータタイプが属するフォルダに関係なく表示するために使用されます。 フォルダービューは、多くのフォルダーに分散されるパーティション化されたデータまたはデータを管理する管理ツールとして使用されます。

詳細情報： [フォルダー表示](../../platform/using/adobe-campaign-explorer.md).
+++

+++**フォーム**

Formsは、特定のスキーマタイプのインターフェイス表現を定義します。 Formsは、受信者、配信、キャンペーンなど、製品内のデータ要素を簡単に作成および編集するための手段です。 Adobe Campaignのすべてのインターフェイス要素は、Formsを使用して製品自体に作成されます。 フォームはオプションであり、すべてのスキーマにフォームがあるわけではありません。

詳細情報： [Forms](../../configuration/using/identifying-a-form.md).
+++

+++**生成される SQL クエリ**

オペレーターがスキーマを操作したときに基になるデータベースに対して生成される SQL コード。 スキーマは、データベースのテーブルと列を使用して実装されるデータ型を定義します。 （クエリなどで）スキーマ操作用に生成される SQL は、インストールされているデータベースのタイプに基づいています。 したがって、データベースを別のタイプにスワップしても、Campaign のクエリは変更されません。 Adobeは、この機能をデータベースに依存しないと呼びます。

詳細情報： [生成された SQL クエリ](../../platform/using/steps-to-create-a-query.md#step-6---preview-data).
+++

+++**ヒートマップ**

キャンペーンヒートマップは、24 時間のワークフロー実行情報を示すテーブルです。 期間内のワークフローの分布を時間別および 5 分間隔で表示します。 ヒートマップは、サーバー負荷を評価し、最もリソースを消費しているワークフローアクティビティを判断するために使用されます。

詳細情報： [ヒートマップ](../../workflow/using/heatmap.md).
+++

+++**ハイブリッドデプロイメント**

ハイブリッドデプロイメントは、オンデマンドサービスとオンプレミスソフトウェアを組み合わせてデプロイし、連携して機能するようにします。

詳細情報： [ハイブリッドデプロイメント](../../installation/using/hosting-models.md#hybrid).

+++

## I - L {#sec-3}

+++**識別モード**

*コンテキスト：キャンペーンインタラクション*

連絡先のステータスを指します。 明示的、暗黙的、匿名のいずれかを指定できます。

* **明示的**：チャネルインターフェイスにログインしたことにより連絡先が識別されている状態。
* **暗黙的**：Cookie（永続またはセッション）により連絡先が識別されている状態。このような連絡先は、匿名連絡先としても、識別された連絡先としても処理できます。
* **匿名**：連絡先が識別できない状態。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**画像サービング**

E メールに埋め込まれた画像を配信の受信者に提供する機能。 E メールシステムの「画像のダウンロード」機能に基づいて画像を挿入すると、Campaign のトラッキングログに「オープン」エントリが生成されます。

詳細情報： [画像サービング](../../delivery/using/defining-the-email-content.md#adding-images).
+++

+++**インバウンドインタラクション**

*コンテキスト：キャンペーンインタラクション*

インバウンドインタラクションは、Web、コールセンター、モバイルなどのチャネル内の連絡先のアクションによって生成された着信呼び出しに続くインタラクションです。 通常、このタイプのインタラクションは、単一モード（受信者ごと）で処理されます。

詳細情報： [インバウンドインタラクション](../../interaction/using/about-inbound-channels.md).
+++

+++**受信ボックスレンダリング**

受信ボックスレンダリングは、E メールのプレビューの生成で、様々な Web クライアント、Web メールおよびデバイスで受信者にメッセージが最適な方法で表示されるようにします。 Adobe Campaignは、Litmus を活用します。Litmus を使用すると、E メールコンテンツ作成者は、Gmail 受信トレイやApple Mail クライアントなど、70 を超える E メールレンダラーでメッセージコンテンツをプレビューできます。

詳細情報： [受信ボックスレンダリング](../../delivery/using/delivery-dashboard.md#delivery-rendering).
+++

+++**インスタンス設定**

インスタンス設定は、Adobe Campaignインスタンスの設定の詳細です。 これらの設定は、デプロイウィザード（ツール/詳細設定/デプロイウィザード）またはサーバー/インスタンスの設定ファイルで定義します。

詳細情報： [インスタンス設定](../../installation/using/about-initial-configuration.md).

+++

+++**ジョブ（インポートおよびエクスポート）**

ジョブは、製品との間でのデータのインポートとエクスポートを簡素化するウィザードシステムによって管理されます。 ジョブは、シンプルで一貫性のあるテンプレートシステムを使用し、スケジュールに従って実行するように定義できます。

詳細情報： [ジョブの読み込みと書き出し](../../platform/using/get-started-data-import-export.md).
+++

+++**リスト**

リストは静的データセットです。 リストは、他のソース (Audience Manager、Experience Platform、データベースなど ) から Campaign にインポートされ、インポートされたリストとしてインターフェイスに表示されるオーディエンスまたはセグメントです。

詳細情報： [リスト](../../platform/using/creating-and-managing-lists.md).
+++

+++**ローカルキャッシュ**

オペレーターのコンピューター上にローカルに保存される情報。 キャッシュされた情報は、サーバーへの必要なトラフィックを減らし、パフォーマンスを向上させるために、コンソールで使用されます。 （[ ファイル ] メニューの）ローカルキャッシュを定期的にクリアすると、保存された情報が更新され、パフォーマンスと安定性が向上します。

詳細情報： [ローカルキャッシュ](../../platform/using/faq-campaign-config.md#perform-soft-cache-clear).
+++

## M - P {#sec-4}

+++**マーケティングリソース管理 (MRM)**

*コンテキスト：マーケティングリソース管理 (MRM)*

この **マーケティングリソース管理 (MRM)** Adobe Campaignのモジュールでは、関連するタスク、予算およびマーケティングリソースの完全な管理とリアルタイムトラッキングにより、マーケティングアクションを協調モードで制御できます。 Adobe Campaignのオペレーターは、検証プロセスおよび適切なトラッキングツールを使用して、アクションを調整し、進行状況をすべての段階で承認できます。レポート、承認の追跡、通知、ディスカッションフォーラムなど

詳細情報： [MRM](../../mrm/using/about-marketing-resource-management.md).
+++

<!--
+++**Localization**

This template type is used to manage multilingual messages.  It is available for Email and SMS messages and useable in standalone mode, within a workflow or in a recurring delivery. In the multilingual feature templates, the language management is based on variants. Each variant represents one language.  This functionality is available only in Adobe Campaign Standard.  
+++
-->

+++**ネームド権限**

オペレーターグループのアクセス権と権限（役割）の定義に使用される詳細なデータベースアクセス権。 ネームド権限は、製品のインストール時、およびツールの特定の機能を定義する様々なパッケージをインポートする際に設定されます。 カスタムネームド権限は、クライアントのビジネス要件をサポートするために作成できます。

詳細情報： [ネームド権限](../../platform/using/access-management-named-rights.md).
+++

+++**名前空間**

データモデル内のAdobe Campaignのネイティブデータ型から顧客データ型を分離するパーティション。 また、スキーマやテンプレートを開発インスタンスから実稼動インスタンスに移動するなど、あるインスタンスから別のインスタンスへの定義の移行を容易にするためにも使用します。

詳細情報： [名前空間](../../configuration/using/about-schema-reference.md#identification-of-a-schema).
+++

+++**ナビゲーションバー**

インターフェイスの上部を通るナビゲーション要素。 ナビゲーションバーは、プラットフォームの様々なコア機能を再グループ化します。 ナビゲーションバーのリンクをクリックすると、この機能に関連する一連の機能が表示されます。 どのコア機能にアクセスできるかは、インストールしたパッケージおよびアドオンと、アクセス権によって異なります。ナビゲーションバーの目的は、画面の管理を簡素化し、生産性を高めることです。

詳細情報： [ナビゲーションバー](../../platform/using/adobe-campaign-workspace.md#browsing-pages).
+++

+++**ナビゲーションツリー**

Adobe Campaignのエクスプローラービューのメインナビゲーション。 ナビゲーションツリーは、ファイルブラウザー（Windows エクスプローラなど）のように機能します。 フォルダーには、サブフォルダーを含めることができます。 ノードを選択すると、そのノードに対応するビューが表示されます。表示されるビューは、選択した行を編集するためのスキーマと入力フォームに関連付けられたリストです。ナビゲーションツリーをカスタマイズし、フォルダーに対する権限を設定できます。

詳細情報： [ナビゲーションツリー](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarch).
+++

+++**目標**

*コンテキスト：マーケティングリソース管理 (MRM)*

キャンペーン、プログラムまたはプラン内で、オペレーターは目標のリストを記述できます。 目標は、到達すべき定量値です。キャンペーン、プログラムまたはプランの最後に MRM モジュールを使用して、オペレーターは目標と結果を専用レポートで比較できます。

詳細情報： [目標](../../mrm/using/creating-and-managing-tasks.md#expenses-and-revenues).
+++

+++**オファーカタログ**

*コンテキスト：キャンペーンインタラクション*

Adobe Campaignで定義され、インタラクション中に選択できるオファーのセット。 カタログは階層構造を持ち、1 つのカテゴリに対して 1 つのノードが作成されます。

詳細情報： [オファーカタログ](../../interaction/using/offer-catalog-overview.md).
+++

+++**オファー連絡先**

*コンテキスト：キャンペーンインタラクション*

インバウンドインタラクションからの連絡先。 エンジン呼び出しの処理中、連絡先はターゲティングディメンションに関連付けられます。 識別されていない匿名コンタクトは訪問者ターゲティングディメンションに関連付けられます。識別済みと匿名の 2 種類の連絡先があります。

* **識別された連絡先**：チャネル上で自主的に身元識別をおこなった連絡先。アウトバウンドインタラクションの場合、連絡先は自動的に識別されます。
* **匿名連絡先**：チャネルを通じて自主的に登録はしていないものの Cookie を通じて暗黙的に推測された連絡先。この用語はインバンドインタラクションに対してのみ使用されます。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**オファーデザイン環境**

*コンテキスト：キャンペーンインタラクション*

オファー **デザイン環境** は、オファーの作成、タイポロジルールの定義、オファーのターゲットにするスキーマの選択をおこなう環境です。 生成されたオファーの提案を保存するためのテーブルも、環境によって定義されます。 デフォルトでは、インタラクションアドオンには、 **デザイン** 環境と **ライブ** 環境がリンクされています。 これらの環境は、ビルトインの受信者テーブルをターゲットとするように事前に設定されています。

詳細情報： [デザイン環境](../../interaction/using/fundamental-principles.md).
+++

+++**オファーエンジンのアービトラージ**

*コンテキスト：キャンペーンインタラクション*

環境に表示されるオファー（適格なオファー）の選択 アービトラージの原則により、カテゴリおよびオファーで定義された条件に従って、オファーが優先順にランク付けされます。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**オファーエンジンのプルーニング**

*コンテキスト：キャンペーンインタラクション*

選択の対象でないオファーを削除するプロセス。 オファーエンジンのアービトラージ手順の前に実行されます。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**オファー環境**

*コンテキスト：キャンペーンインタラクション*

オファーカタログ、その使用可能なスペースおよび環境の事前定義済みフィルターを定義するルートフォルダー。 オペレーターは、ターゲティングディメンションごとに 1 つの環境を作成する必要があります。 オファー環境には次の 2 つのタイプがあります。デザインとライブ。

詳細情報： [環境](../../interaction/using/fundamental-principles.md).
+++

+++**オファーライブ環境**

*コンテキスト：キャンペーンインタラクション*

キャンペーンにリンクされた環境 **デザイン環境**. 実稼働環境には、**デザイン環境**&#x200B;でコンテンツと実施要件の承認を受けた読み取り専用のオファーが含まれています。Web サイトでの表示用に選択することも、アウトバウンドメッセージに挿入することもできます。

詳細情報： [ライブ環境](../../interaction/using/fundamental-principles.md).
+++

+++**オファーのプレビュー**

*コンテキスト：キャンペーンインタラクション*

フォルダー内で表示されるとおりのオファーのプレビュー。 これには、「オファーのプレビュー」タブまたは連絡先プロファイルからアクセスできます。

詳細情報： [オファーのプレビュー](../../interaction/using/creating-an-offer.md#previewing-the-offer).
+++

+++**オファープレゼンテーションルール**

*コンテキスト：キャンペーンインタラクション*

オファー環境で参照されるタイポロジルール。オペレーターは、受信者の提案履歴を考慮して特定のオファーを除外できます。

詳細情報： [オファープレゼンテーションルール](../../interaction/using/managing-offer-presentation.md#presentation-rules-overview).
+++

+++**オファーの提案**

*コンテキスト：キャンペーンインタラクション*

オファーの提案は、特定のオファースペース（Web サイト上のバナー、E メール、SMS コンテンツなど）で連絡先にオファーを提示するアクションから成るものです。 この結果は、オファー、受信者およびタイムスタンプを定義するオファー提案テーブルに保存され、受信者が受け取ったすべてのオファーの記録が提供されます。

詳細情報： [オファーの提案](../../interaction/using/creating-offer-spaces.md#offer-proposition-statuses).
+++

+++**オファー表示域**

*コンテキスト：キャンペーンインタラクション*

オファーの提案は、特定のオファースペース（Web サイト上のバナー、E メール、SMS コンテンツなど）で連絡先にオファーを提示するアクションから成るものです。 この結果は、オファー、受信者およびタイムスタンプを定義するオファー提案テーブルに保存され、受信者が受け取ったすべてのオファーの記録が提供されます。

詳細情報： [インタラクション](../../interaction/using/interaction-and-offer-management.md).
+++

+++**オファーのシミュレーション**

*コンテキスト：キャンペーンインタラクション*

オファーのシミュレーションを使用すると、オペレーターは、定義した範囲（配信日、ターゲットセグメント、オファー数、テーマなど）でのオファーの配分をテストできます。 実際にオファーを送信する前に。 オファーの優先度と実施要件ルールを調整して、オファーの効果を最大限に高めるために使用できます。

詳細情報： [シミュレーション](../../interaction/using/about-offers-simulation.md).
+++

+++**オファースペース**

*コンテキスト：キャンペーンインタラクション*

オファースペースは、オファーを公開する場所を定義するフォルダーです。 スペースを定義すると、使用するチャネルを指定し、オファーのコンテンツを作成し、提示されるオファーを指定できます。 オファースペースは、チャネルとオファーエンジンの間のインターフェイスです。

詳細情報： [シミュレーション](../../interaction/using/creating-offer-spaces.md).
+++

+++**オファーテーマ**

*コンテキスト：キャンペーンインタラクション*

オファーテーマは、カテゴリで定義されるキーワードで、オペレーターは、オファーが提示されたときにそのオファーをフィルタリングできます。 テーマを使用すると、カタログ構造からオファーを階層的でない方法で選択できます。

詳細情報： [オファーテーマ](../../interaction/using/integrating-an-offer-via-the-wizard.md).
+++

+++**オファーの重み付け**

*コンテキスト：キャンペーンインタラクション*

オファーの重み付けは、エンジンが最も関連性の高いオファーを選択できるように、オファーの関連度を正確に定義する数式に基づいています。 重み付けの定義は、オファーと乗数のカテゴリでおこないます。 重み付けの順位を下げる際には実施要件を満たすオファーが考慮されます。

詳細情報： [オファーの重み付け](../../interaction/using/creating-an-offer.md#offer-weight).
+++

+++**オペレーターグループ**

オペレーターグループを使用すると、Campaign オペレーターの役割を管理できます。 権利を付与するオペレーターのグループを定義し、オペレーターを 1 つ以上のグループに関連付けます。 これにより、権利を再利用することや、複数のオペレーターに一貫性の高いプロファイルを設定することができます。また、プロファイルの管理やメンテナンスをおこなううえでも便利な方法です。

詳細情報： [オペレーターグループ](../../platform/using/access-management-groups.md).
+++

+++**演算子**

オペレーターは、ログインしてアクションを実行する権限を持つ Adobe Campaign ユーザーです。オペレーターは、オペレーターグループに関連付けられ、これらのグループの権限と権限を継承します。 ネームド権限をオペレーターに直接関連付けることもできます。

詳細情報： [演算子](../../platform/using/access-management-operators.md).
+++

+++**オプション**

オプションは、Campaign インスタンスの設定を定義するために使用される Platform レベルの変数です。 オプションは、プラットフォームレベルで、期間（データベースクリーンアップワークフローなど）やその他のグローバル定義を定義できます。

詳細情報： [オプション](../../installation/using/configuring-campaign-options.md).
+++

+++**アウトバウンドインタラクション**

*コンテキスト：キャンペーンインタラクション*

アウトバウンドインタラクションは、（E メールやダイレクトメールの配信に使用される）連絡先リストからインタラクションエンジンへの呼び出しです。 各連絡先に同じルールとプロセスが適用されます。通常、このタイプのインタラクションはバッチモードで処理されます。

詳細情報： [アウトバウンドインタラクション](../../interaction/using/about-outbound-channels.md).
+++

+++**パッケージの書き出し/読み込み**

パッケージエクスポートは、オブジェクトの定義を含む XML ファイルの生成で構成される操作です。 パッケージは、機能と定義をインスタンス間で移行するために使用されます。 また、バックアップおよびソース管理システムに重要な製品定義を追加する場合にも使用します。

詳細情報： [パッケージの書き出し/読み込み](../../platform/using/working-with-data-packages.md).
+++

+++**パレット**

ワークフローパレットには、ワークフローに追加できる使用可能なアクティビティが表示されます。 このコンポーネントは、使用ごとに論理的にグループ化されたワークフローアクティビティを含むタブ形式で表示されます。 パレットで使用可能なアクティビティは、Campaign インスタンスにインストールされているアドオンと、ワークフローを表示しているコンテキストによって決まります。

詳細情報： [パレット](../../workflow/using/building-a-workflow.md#adding-and-linking-activities).
+++

+++**パフォーマンス監視**

[ 監視 ] タブにパフォーマンス監視情報が表示されます。 メモリと CPU 使用率、SMTP サーバーの統計、サーバープロセス、その他の関連情報など、基になるシステムの指標が表示されます。

詳細情報： [パフォーマンス監視](../../production/using/monitoring-processes.md).
+++

+++**パーソナライゼーションブロック**

Adobe Campaignには、配信に挿入できる、組み込みのパーソナライゼーションブロックが用意されています。 動的でパーソナライズされ、特定のレンダリングが含まれています。 例えば、ロゴ、挨拶メッセージまたはミラーページへのリンクを追加できます。デフォルトでは、複数のパーソナライゼーションブロックを使用できます。 また、配信のパーソナライゼーションを最適化するためのカスタムパーソナライゼーションブロックを定義することもできます。 実際のデータは、配信の分析フェーズで、生成された各メッセージに挿入されます。

詳細情報： [パーソナライゼーションブロック](../../delivery/using/personalization-blocks.md).
+++

+++**パーソナライゼーションフィールド**

パーソナライゼーションフィールドは、特定の受信者に対する配信をパーソナライズする際に使用される単一のデータフィールド参照です。 実際のデータ値は、配信分析フェーズで挿入されます。

詳細情報： [パーソナライゼーションフィールド](../../delivery/using/personalization-fields.md).
+++

+++**パーソナライゼーション変数**

パーソナライゼーション変数は、配信内のコードの一部で、受信者の情報に基づいて様々なテキストを様々な受信者に表示できます。 これらのフィールドは、パーソナライゼーションフィールドまたはブロックとして実装できます。

詳細情報： [パーソナライゼーション変数](../../delivery/using/about-personalization.md).
+++

+++**プラン**

プランとは、カレンダーベースでマーケティングアクティビティを整理するために使用されるフォルダータイプです。 エクスプローラビューのプランフォルダは、年、四半期、月など、時間に基づく単位を定義します。 プランフォルダはネストでき、他のプランフォルダ、プログラムフォルダ、キャンペーンを含むことができます。

詳細情報： [プラン](../../campaign/using/setting-up-marketing-campaigns.md).
+++

+++**定義済みフィルター**

定義済みフィルターは、再利用のために保存されたクエリです。 事前定義済みフィルターを使用すると、生産性が向上し（作成は 1 回のみなので）、一貫性を構築し（すべてのマーケターが使用できるので）、自分では作成できないコードやロジックを使用できるので、マーケターのスキルを低減できます。

詳細情報： [定義済みフィルター](../../platforrm/using/creating-filters.md).
+++

<!--
+++**Predictive Engagement Scoring**

Predictive engagement scoring predicts the probability of a recipient engaging with a message and the probability of opting out (unsubscribing) within the next seven days after the next email send. The probabilities are further divided into buckets according to the specific risk of disengagement, medium, or low. The model also provides the risk percentile rank for the customers to understand where the rank of a certain customer in relation to others. 

Learn more about [Predictive Engagement Scoring](../../platforrm/using/creating-filters.md).
+++
-->

+++**プライマリキー**

主キーは、データベーステーブル内の各レコードの一意の識別子です。 テーブルには少なくとも 1 つのキーが必要です。 原則として、キーはスキーマのメイン要素とインデックスの後に宣言されます。 プライマリキーを複合（複数のフィールドを含む）することはできません。

詳細情報： [プライマリキー](../../configuration/using/key.md).
+++

+++**プロファイル**

プロファイルとは、エンド顧客、見込み客、またはリードを表す情報のレコードです。 各プロファイルは、 nmsRecipient テーブル内のレコードまたは外部テーブルに対応し、特定のチャネルに関連する Cookie ID、顧客 ID、モバイル識別子、その他の情報が含まれます。

詳細情報： [プロファイル](../../platforrm/using/about-profiles.md).
+++

+++**プログラム**

プログラムとサブプログラムフォルダーは、ロイヤルティ、獲得、クロス販売など、ビジネス目標に関するマーケティングアクティビティを整理します。 また、会計期間やキャンペーン戦術（イベントやニュースレターなど）を表すこともできます。 各プログラムには、1 つのカレンダーにリンクされた複数のキャンペーンが含まれており、カレンダーが全体像を提供します。

詳細情報： [プログラム](../../campaign/using/setting-up-marketing-campaigns.md).
+++

+++**パブリックリソース**

パブリックリソースフォルダーは、Adobeキャンペーン内に、アプリケーションサーバーによってホストされる画像を保持します。 配信内の画像を E メールなどの配信に表示するには、アプリケーションサーバー（または Campaign が設定されている場合は画像ホスティングサーバー）に公開する必要があります。

詳細情報： [パブリックリソース](../../installation/using/deploying-an-instance.md#managing-public-resources).
+++

+++**プッシュ**

プッシュ通知は、モバイルアプリケーションが受信したメッセージです。 プッシュ通知は、モバイルアプリケーションにExperience PlatformSDK コードを含めることで、Adobe Campaignで機能するように設定されます。 「プッシュ」の場合、次の 2 つの配信チャネルを使用できます。iOSと Android。

詳細情報： [プッシュ](../../delivery/using/about-mobile-app-channel.md).
+++

## Q - T {#sec-5}

+++**受信者**

Adobe Campaignでは、受信者は、 を顧客に送信します。 データベースに格納された受信者データを使用して、ターゲットをフィルタリングし、パーソナライゼーションデータを追加できます。 通常、これは個人情報、連絡先情報、人口統計情報、トランザクション情報ですが、マーケティングや分析をサポートするあらゆる種類の情報が対象となります。

詳細情報： [受信者](../../configuration/using/about-data-model.md).
+++

+++**レンダリング関数**

*コンテキスト：キャンペーンインタラクション*

レンダリング関数は、オファースペースで定義されます。 これは、オファーで定義された属性に基づいてオファー表示域を構築するために使用します。 レンダリング関数のモードには、HTML、XML、テキストの 3 種類があります。

詳細情報： [レンダリング関数](../../interaction/using/creating-offer-spaces.md).
+++

+++**リターゲティングキャンペーン**

以前の配信または配信の受信者をリターゲティングするキャンペーン。
+++

+++**スキーマ拡張**

スキーマ拡張を使用すると、標準のスキーマを、ビジネスの使用例に最適にカスタマイズできます。 例えば、「Loyalty」フィールドを受信者テーブルに追加できます。

詳細情報： [スキーマ拡張](../../configuration/using/extending-a-schema.md).
+++

+++**スキーマ**

スキーマは、特定のデータ型を定義する XML ドキュメントです。 スキーマは、製品のデータベースのデータベーステーブルとして実装されます。  オペレーターが Campaign および製品でスキーマを操作すると、そのアクションが必要な SQL に変換され、データベースに対して実行されます。 これらの用語（スキーマ/テーブル）は、多くの場合、演算子と同じ意味で使用されますが、製品アーキテクチャの要素は異なります。

詳細情報： [スキーマ](../../configuration/using/about-schema-reference.md).
+++

+++**シードアドレス**

シードアドレスは、定義されたターゲット条件に合わない受信者を配信のターゲットにする場合に使用されます。これにより、配信スコープ外の受信者が他のターゲット受信者と同様に配信を受信することができます。

詳細情報： [シードアドレス](../../delivery/using/about-seed-addresses.md).
+++

<!--
+++**Send-time optimization**

To improve the open rate of your messages, you can manually define a sending time per recipient. Each profile will receive the message at the specified date and time, whenever possible. Defining a sending time can be done at the delivery level or using a workflow.

Learn more about [Send-time optimization](../../delivery/using/about-seed-addresses.md:).
+++
-->

+++**サービス**

Adobe Campaignでは、ニュースレターや製品の更新などの情報サービスを作成および管理し、これらのサービスの購読を管理できます。 複数のサービスを並行して定義できます。

詳細情報： [サービス](../../delivery/using/about-services-and-subscriptions.md).
+++

+++**SFTP 管理**

コントロールパネルでは、アクセス権のある Campaign インスタンスに接続しているすべての SFTP サーバーとやり取りできます。 Campaign コントロールパネルを使用すると、SFTP サーバーに対して、ストレージ容量の監視、IP アドレスの許可リストへの登録、SSH 公開鍵の管理などのアクションを実行できます。

詳細情報： [SFTP 管理](https://experienceleague.adobe.com/docs/control-panel/using/sftp-management/about-sftp-management.html?lang=en).
+++

+++**購読サービスアクティビティ**

このワークフローアクティビティでは、トランジションで指定された母集団の情報サービスに対する購読を作成または削除できます。

詳細情報： [購読サービスアクティビティ](../../workflow/using/subscription-services.md).
+++

+++**ターゲットの承認**

*コンテキスト：キャンペーン分散型マーケティング*

ターゲットの承認とは、別のオペレーターまたはオペレーターのグループに、（分析フェーズでターゲットが生成された後に）配信の最終ターゲットを配信が送信される前に承認してもらうプロセスです。

詳細情報： [ターゲットの承認](../../workflow/using/local-approval.md).
+++

+++**ターゲットデータ**

ターゲットデータとは、ワークフローの作業用テーブル（トランジション）に保存されるデータです。 このデータは、配信内で配信コンテンツのパーソナライゼーション用に使用したり、配信の動的要素のロジックを定義したりできます。

詳細情報： [ターゲットデータ](../../workflow/using/data-life-cycle.md#target-data).
+++

+++**ターゲットマップ**

これは、配信チャネルと特定のデータタイプとのマッピングです。 Adobe Campaignは、電子メールアドレスや電話番号には送信されず、データタイプに送信されます。 ターゲットマップ（配信マップとも呼ばれます）は、異なる配信チャネルをスキーマのデータフィールドにリンクする方法を定義します。 特定のフィールドまたは式を使用して、Campaign がデータタイプにどのように送信するかを定義します。

詳細情報： [ターゲットデータ](../../workflow/using/define-the-right-audience.md#target-mappings).
+++

+++**ターゲティングアクティビティ**

ターゲティング、母集団データの操作、フィルタリングアクティビティに固有のワークフローアクティビティです。 オペレーターは、セットを定義し、積集合、和集合、除外の各操作を使用して分割または組み合わせることで、1 つ以上のターゲットを作成できます。

詳細情報： [ターゲティングアクティビティ](../../workflow/using/about-targeting-activities.md).
+++

+++**ターゲティングディメンション**

クエリまたは他のワークフローアクティビティによって生成（返される）されるデータ型です。 Adobe Campaignは、取得に使用されたクエリに関係なく、回答者データベース行のプライマリキーのみを返すことに注意してください。

詳細情報： [ターゲティングディメンション](../../workflow/using/targeting-data.md).
+++

+++**タスクアクティビティ**

*コンテキスト：マーケティングリソース管理 (MRM)*

タスクワークフローアクティビティは、ワークフローのロジックに人間のアクションを組み込みます。 次の 2 つのシナリオを指定できます。1 つ目はタスクが完了した場合、もう 1 つはタスクが完了していない場合です（手動で未完了とマークされている場合、またはタスクの期限が切れる場合）。

一般的な使用例は、オフラインアクションをキャンペーンに組み込む場合、または承認などのカスタムアクションに組み込む場合です。

キャンペーンワークフローで、「タスク」アクティビティ



詳細情報： [タスクアクティビティ](../../workflow/using/task.md).
+++

<!--
+++**Task**

One iteration of the defined functionality of a workflow activity. Each execution of a task has a unique task identifier.   

Learn more about [Tasks](../../workflow/using/about-workflows.md).
+++
-->

+++**テンプレート**

テンプレートは、オブジェクトの作成に使用されるデザイン要素です。 オブジェクト設定と、オプションでオブジェクトのコンテンツが含まれます。 テンプレートシステムは、Adobe Campaignの配信、キャンペーン、ワークフロー、その他多くの要素を作成するために使用されます。 使用可能なファクトリテンプレートは、インストールされたパッケージによって定義されます。 その後、必要に応じて、キャンペーンオペレーターがテンプレートを複製し、カスタマイズできます。
+++

<!--
+++**Test profiles**

Allows targeting of additional recipients who do not match the defined targeting criteria. They are added to a message’s audience to detect any fraudulent use of your recipient database or to ensure delivery. Seen as the Seed type in the Campaign interface.

Learn more about [Test profiles](../../workflow/using/about-workflows.md).
+++
-->

<!--
+++**Total database storage**

The aggregate size of the production and non-production instance(s) database storage managed by Adobe. 

Learn more about [Total database storage](../../workflow/using/about-workflows.md).
+++
-->

+++**トラッキングログ**

配信が送信され、トラッキングがアクティブ化されると、トラッキングテクニカルワークフローはトラッキングデータを取得します。このデータは、配信の「トラッキング」タブに表示されます。E メールの開封数やクリック数、または受信者が受け取ったメッセージとのやり取りに関する情報を確認できます。

詳細情報： [トラッキングログ](../../delivery/using/accessing-the-tracking-logs.md).
+++

+++**トランザクションメッセージ**

トランザクショントリガーは、外部の情報システムから送信されるイベントから生成されるカスタムメッセージ通知を管理するために設計された Campaign モジュールです。 トランザクションメッセージは web サイトなどのプロバイダーがリアルタイムに送信する、個々に向けたユニークなコミュニケーションです。受信者が確認したい重要な情報が含まれているので、早い送信が特に期待されます。

詳細情報： [トランザクションメッセージ](../../message-center/using/about-transactional-messaging.md).
+++

+++**トリガーキャンペーン**

トリガーキャンペーンとは、ワークフローで API リクエストを受け取ったときに実行されるキャンペーンです。 API 呼び出しは、ワークフローの実行を開始するワークフロー内のシグナルアクティビティによって消費されます。

詳細情報： [トリガーキャンペーン](../../workflow/using/external-signal.md).
+++

<!--
+++**Triggers**

Signals that initiate execution of a workflow, delivery or other action. Typically an API call. 

Learn more about [Triggers](../../workflow/using/about-workflows.md).
+++
-->

+++**タイポロジルール**

*コンテキスト：キャンペーンの最適化*

タイポロジルールは、配信の分析フェーズの一環として実装されるビジネスルールです。 タイポロジルールとは、配信のコンテンツ（コントロールルール）や配信のターゲット（フィルタールール）、またはビジネス要件を適用する他のロジック（頻度ルール）を確認するものです。 ルールは、1 つ以上のタイポロジに含めることができる詳細な要素です。

詳細情報： [タイポロジ](../../campaign/using/about-campaign-typologies.md#typology-rules).
+++

+++**タイポロジ**

*コンテキスト：キャンペーンの最適化*

タイポロジとは、配信の分析段階に適用されるタイポロジルールのグループです。 キャンペーンタイポロジには、複数のタイポロジルールを含めることができますが、1 つの配信では 1 つのタイポロジしか参照できません。

詳細情報： [タイポロジ](../../campaign/using/about-campaign-typologies.md#typologies).
+++

## U - Z {#sec-6}

+++**単一モード**

*コンテキスト：Campaign インタラクション、トランザクションメッセージ*

単一モードでは、実行時にオファーエンジンによって 1 つの連絡先が処理されます。 通常、このモードはインバンドインタラクションとトランザクションメッセージで使用します。

詳細情報： [単一モード](../../interaction/using/about-inbound-channels.md).
+++

<!--
+++**Universes**

Application pages hosted by the Campaign instance. Used for approval forms, landing pages, opt-out forms, preference pages or to implement other business requirements.  

Learn more about [Universes](../../workflow/using/about-workflows.md).
+++
-->

+++**web アプリケーション**

Web アプリケーションは、Campaign インスタンスでホストされる動的でインタラクティブなアプリケーションページです。 データベースのデータと、接続したユーザーの権限に適合したコンテンツが含まれます。 例えば、エクストラネット上の編集フォームや、テーブル、グラフ、入力フォームなどを含むデータベースのデータを含む通知フォームを作成できます。 この機能を使用すると、ユーザーが情報を検索または入力できる Web ページをデザインおよび投稿できます。

詳細情報： [Web アプリケーション](../../web/using/about-web-applications.md).
+++

+++**ワークフロージャーナル**

ワークフロージャーナルは、ワークフローのステップバイステップの実行ログです。 ワークフローのすべての履歴または監査証跡が含まれます。 開発、トラブルシューティング、デバッグの目的で使用されます。

詳細情報： [ワークフロージャーナル](../../workflow/using/monitoring-workflow-execution.md).
+++

+++**ワークフロー**

ワークフローは、キャンペーン実行フローを視覚的に表現したものです。 アプリケーションサーバーの様々なモジュール間で、プロセスとタスク全体を調整できます。 この包括的なグラフィカル環境を使用すると、セグメント化、キャンペーン実行、ファイル処理、人の参加などを含むプロセスを設計できます。ワークフローエンジンは、これらのプロセスを実行およびトラッキングします。

詳細情報： [ワークフロー](../../workflow/using/about-workflows.md).
+++

+++**作業用テーブル**

作業用テーブルには、ワークフロートランジションによって実行されるすべての情報が含まれます。 各ワークフローは、複数のワークテーブルを使用します。
これらのテーブルで伝達されたデータは、パージされない限り、ワークフローのライフサイクル全体で高速化および使用できます。 不要なテーブルは、ワークフローが休止状態になるたびにパージされます。また、最大のワークフローの実行中にサーバーの過負荷を回避する目的でパージされることがあります。

詳細情報： [作業用テーブル](../../workflow/using/about-workflows.md).
+++