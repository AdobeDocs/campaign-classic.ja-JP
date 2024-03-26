---
product: campaign
title: Campaign での MX サーバーの使用
description: MX サーバーとAdobe Campaign Classicの連携の仕組み
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
hidefromtoc: true
exl-id: 47f50bf5-4d5b-4c07-af71-de4390177cf5
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 3%

---

# Campaign での MX サーバーの使用 {#using-mx-servers}



MX サーバーがAdobe Campaign Classicと連携する仕組みを説明します。

## MX サーバー {#mx-servers}

### MX サーバーとは

メール交換レコード（MX レコード）は、ドメインの代わりに E メールメッセージを受け入れる役割を持つメールサーバーを指定する、Domain Name System(DNS) 内のリソースレコードの一種です。

### MX サーバーの仕組み

電子メールを送信すると、ソフトウェアサーバーは受信者ドメインサーバーとの接続を確立します。 2 つのサーバー間の通信では SMTP 言語が使用され、1 つのドメインに複数の MX サーバーを含めることができます。 このドメインへの接続は、最も優先度の高い（最小の図）から開始され、その他のサーバは「バックアップ」サーバと呼ばれます。 接続プロトコルを考慮する必要があります。

### MX サーバーがAdobe Campaignでどのように動作しますか？

接続プロトコルでは、サーバーのスパム化と独占を防ぐために、ルールを尊重する必要があります。 最も重要なのは次のとおりです。

* **許可される最大接続数**：この数が考慮される場合、IP は上になブロックリストに加えるく、追加の接続が原因で E メールが拒否されません。
* **メッセージの最大数**：接続中に、送信を許可するメッセージの数を定義する必要があります。 この数を定義しない場合、サーバーはできるだけ多くの数を送信します。 その結果、スパム送信者として識別され、ISP によってブロックリストに加えるに追加されます。
* **1 時間あたりのメッセージ数**:e レピュテーションと照合するために、Adobe Campaignは IP で 1 時間に送信できる電子メールの数を制御します。 このシステムは、メールの拒否や拒否からお客様を保護しブロックリストに加えるます。

## E メールのインバウンス

### インバウンス E メールとは

サーバー通信中のエラーを処理するために、Adobe Campaignが使用するプロセスです。

### インバウンス E メールの仕組み

エラーアドレスは、ISP から返されたバウンスを処理します。 このプロセスは、様々な SMTP エラーコードを分析し、RegEx 標準に従って適切なアクションを適用します。

例えば、ある電子メールアドレスでは、ISP から送信されたフィードバック「550 User Unknown」が返されます。 このエラーコードは、Adobe Campaignエラーアドレス（returnpath アドレス）で処理されます。 次に、このエラーは RegEx 標準と比較され、適切なルールが適用されます。 この E メールは *ハードバウンス* （タイプに一致）、 *不明なユーザー* （理由に一致）、最初のループの後でシステムに強制隔離されました。

### Adobe Campaignはどのように管理しているのですか？

Adobe Campaignは、エラータイプと理由の照合を使用して、このプロセスを管理します。

* **[!UICONTROL 不明なユーザー]**：構文的に正しいが存在しないアドレス。 このエラーは、ハードバウンスとして分類され、最初のエラー内に強制隔離されます。
* **[!UICONTROL メールボックス容量超過]**：最大容量に達したメールボックス。 このエラーは、ユーザーがこのメールボックスをこれ以上使用していないことを示す場合もあります。 このエラーはソフトバウンスとして分類され、3 番目のエラー内に強制隔離され、30 日後に強制隔離から削除されます。
* **[!UICONTROL 非アクティブなユーザー]**：過去 6 か月間ユーザーが非アクティブであったので、メールボックスは ISP によって非アクティブにされています。 このエラーはソフトバウンスとして分類され、3 番目のエラー内に強制隔離されます。
* **[!UICONTROL 無効なドメイン]**:E メールアドレスにドメインが存在しません。 このエラーはソフトバウンスとして分類され、3 番目のエラー内に強制隔離されます。
* **[!UICONTROL 拒否]**:ISP は、ユーザーへの E メールの配信を拒否しました。 このエラーはソフトバウンスとして分類され、エラーは E メールアドレスではなく IP またはドメインのレピュテーションにリンクされるので、強制隔離されません。

>[!NOTE]
>
>配信エラーのタイプと理由について詳しくは、こちらを参照してください。 [セクション](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons).

## 配信品質インスタンス {#deliveratbility-env}

MX ルールとインバウンスルールの日々の更新は、これらのルールの配信品質インスタンス所有者に接続されているクライアントインスタンスの特定のワークフローによって管理されます。

この毎日の更新は、透明性のプロセスを通じてインスタンスを最新の状態に保ちたいすべてのクライアントで実行されます。

MX ルールには 6 つの異なるレベルのスループットがあり、主にランプアッププロセスで使用されます。

![](assets/mx-rules-throughput.png)

カスタムモードは、独自の MX ルールを設定する高度なクライアント向けです。 カスタムモードが有効になっている場合、同期がオフになるので、クライアントは配信品質インスタンスで更新されません。

## バウンスの例

* **不明なユーザー** （ハードバウンス）: 550 5.1.1 ...不明なユーザーです {mx003}
* **メールボックス容量超過** （ソフトバウンス）:550 5.2.2 ユーザーの割り当てを超えました
* **非アクティブなメールボックス** （ソフトバウンス）:550 5.7.1 ：受信者のアドレスが却下されました：非アクティブなメールボックス（6 ヶ月以上入力されていません）
* **ドメインが無効です** （ソフトバウンス）: DNS クエリが「ourdan.com」で失敗しました
* **拒否** （ソフトバウンス）：インバウンドメールのバウンス（ルール「Feedback_loop_Hotmail」がこのバウンスに一致しました）
* **未到達** （ソフトバウンス）:421 4.16.55 [TS01] x.x.x.x からのメッセージは、ユーザーの過剰な苦情により一時的に延期されました

**関連トピック：**
* [MX 設定](../../installation/using/email-deliverability.md#mx-configuration)
* [技術的な E メール設定](../../installation/using/email-deliverability.md)
* [配信エラーについて](../../delivery/using/understanding-delivery-failures.md)
* [Campaign Classic — テクニカルRecommendations](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/acc-technical-recommendations.html)
