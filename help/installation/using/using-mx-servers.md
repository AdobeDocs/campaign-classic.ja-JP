---
product: campaign
title: Campaign での MX サーバーの使用
description: MX サーバーとAdobe Campaign Classicの連携方法を学ぶ
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
hidefromtoc: true
exl-id: 47f50bf5-4d5b-4c07-af71-de4390177cf5
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 3%

---

# Campaign での MX サーバーの使用 {#using-mx-servers}



MX サーバーがAdobe Campaign Classicでどのように機能するかを説明します。

## MX サーバー {#mx-servers}

### MX サーバーとは

メール エクスチェンジャーレコード （MX レコード）は、ドメイン ネーム システム （DNS）のリソース レコードの一種で、ドメインの代わりにメール メッセージを受け入れる責任があるメール サーバーを指定します。

### MX サーバーはどのように機能しますか？

メールを送信すると、ソフトウェア・サーバは受信者ドメイン・サーバとの接続を確立します。 2 つのサーバー間の通信は SMTP 言語を使用しており、1 つのドメインに複数の MX サーバーを含めることができます。 このドメインへの接続は、優先順位が最も高い（最も小さい数字）から開始され、その他のサーバーは「バックアップ」サーバーと呼ばれます。 接続プロトコルを考慮する必要があります。

### MX サーバーはAdobe Campaignでどのように機能しますか？

接続プロトコルでは、スパミングやサーバーの独占を防ぐためのルールを尊重する必要があります。 最も重要なものは次のとおりです。

* **許可される最大接続数**：この数が考慮されると、IP はブロックリストに表示されず、追加の接続が原因でメールが拒否されません。
* **メッセージの最大数**：接続中に、送信が許可されるメッセージ数を定義する必要があります。 この数が定義されていない場合、サーバーはできるだけ多く送信します。 その結果、スパマーとして識別され、ISP によってブロックリストに追加されます。
* **1 時間あたりのメッセージ数**：電子レピュテーションに合わせるために、Adobe Campaignは、IP が 1 時間あたりに送信できるメールの数を制御します。 このシステムは、電子メールの拒否やブロックリストからユーザーを保護します。

## インバウンスメール

### インバウンスメールとは

これは、サーバー通信中にエラーを処理するためにAdobe Campaignが使用するプロセスです。

### インバウンスメールはどのように機能しますか？

エラーアドレスは、ISP から送り返されたバウンスを処理します。 このプロセスは、様々な SMTP エラーコードを分析し、RegEx 標準に従って適切なアクションを適用します。

例えば、あるメールアドレスに、ISP から送信されたフィードバック「550 ユーザーが不明」があるとします。 このエラーコードは、Adobe Campaign エラーアドレス（returnpath アドレス）によって処理されます。 次に、このエラーを正規表現の標準と比較すると、適切なルールが適用されます。 メールは（タイプに一致する *ハードバウンス* と（理由に一致する） *ユーザー不明* と見なされ、最初のループの後に強制隔離されてシステムにプッシュされます。

### Adobe Campaignでの管理方法

Adobe Campaignは、エラータイプと理由の一致を使用してこのプロセスを管理します。

* **[!UICONTROL 不明なユーザー]**：構文上は正しいが存在しないアドレス。 このエラーはハードバウンスに分類され、最初のエラー内で強制隔離にプッシュされます。
* **[!UICONTROL メールボックス容量超過]**：メールボックスが最大容量に達しました。 このエラーは、ユーザーがこのメールボックスをもう使用していないことを示している場合もあります。 このエラーはソフトバウンスに分類され、3 番目のエラー内に強制隔離にプッシュされ、30 日後に強制隔離から削除されます。
* **[!UICONTROL 非アクティブユーザー]**：過去 6 か月間にユーザーが非アクティブになったので、メールボックスが ISP によって非アクティブ化されました。 このエラーはソフトバウンスに分類され、3 番目のエラー内で強制隔離にプッシュされます。
* **[!UICONTROL 無効なドメイン]**: メールアドレスにドメインが存在しません。 このエラーはソフトバウンスに分類され、3 番目のエラー内で強制隔離にプッシュされます。
* **[!UICONTROL 拒否]**:ISP は、ユーザーへのメールの配信を拒否しました。 このエラーは、メールアドレスではなく IP またはドメインの評判にリンクされているので、ソフトバウンスとして分類され、強制隔離にはプッシュされません。

>[!NOTE]
>
>配信エラーのタイプと理由について詳しくは、この [ 節 ](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons) を参照してください。

## 配信品質インスタンス {#deliveratbility-env}

MX ルールとインバウンスルールの日別更新は、これらのルールの配信品質インスタンス所有者に接続されたクライアントインスタンス内の特定のワークフローによって管理されます。

この毎日の更新は、透明性プロセスを通じてインスタンスを最新の状態に保つことを希望するすべてのクライアントに対して実行されます。

MX ルールには 6 つの異なるレベルのスループットがあり、主にランプアッププロセス中に使用されます。

![](assets/mx-rules-throughput.png)

カスタムモードは、独自の MX ルールを設定する高度なクライアント向けです。 カスタムモードが有効になっていると、同期がオフになるので、クライアントは配信品質インスタンスによって更新されません。

## バウンスの例

* **不明なユーザー** （ハードバウンス）: 550 5.1.1 ...不明なユーザー {mx003}
* **メールボックス容量超過** （ソフトバウンス）: 550 5.2.2 ユーザークォータ超過
* **非アクティブなメールボックス** （ソフトバウンス）: 550 5.7.1：受信者アドレスが拒否されました：非アクティブなメールボックスで、6 か月以上ポッピングされていない
* **ドメインが無効です** （ソフトバウンス） : 「ourdan.com」の DNS クエリに失敗しました
* **拒否** （ソフトバウンス） : インバウンド E メールのバウンス （ルール「Feedback_loop_Hotmail」がこのバウンスに一致しました）
* **未到達** （ソフトバウンス）:421 4.16.55 [TS01] x.x.x からのメッセージは、ユーザーからの過剰な苦情が原因で一時的に延期されました

**関連トピック：**
* [MX 設定](../../installation/using/email-deliverability.md#mx-configuration)
* [技術的なメール設定](../../installation/using/email-deliverability.md)
* [配信エラーについて](../../delivery/using/understanding-delivery-failures.md)
* [Campaign Classic - テクニカルRecommendations](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/additional-resources/campaign/acc-technical-recommendations.html?lang=ja)
