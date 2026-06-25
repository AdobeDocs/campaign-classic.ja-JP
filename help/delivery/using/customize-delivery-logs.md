---
product: campaign
title: 詳細設定 - 配信ログのカスタマイズ
description: Campaign Classic v7 で配信ログスキーマを拡張し、カスタムフィールドを追加する方法について説明します
feature: Monitoring
role: User, Developer
exl-id: 44ecc8c6-6584-43eb-96b4-7d8463053123
TQID: https://experienceleague.adobe.com/OXsHpEx96bDHmINu-WR7MDcwn68ZxHjQ1MsxWhbtyG0
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9id: b631758a-142d-425f-b9aa-f756d85cb979id: c858a28b-ea19-49b0-8d48-828717fad89c
subfeature_v2: id: e95a583b-fcfa-4524-8666-46a29c828119id: c8da4fdd-eb94-4751-a43c-f82733fb2d6eid: d5bbe3da-ba85-4242-817e-54f7c4b943e0id: f4da0e76-df77-451e-ad61-21afb7bd8810
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: ht
source-wordcount: 574
ht-degree: 100%

---

# 詳細設定：配信ログのカスタマイズ {#customize-delivery-logs}

>[!NOTE]
>
>配信リストへのアクセスと配信ダッシュボードの使用に関する包括的なガイダンスについて詳しくは、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-dashboard)を参照してください。 このコンテンツは、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用されます。
>
>このページでは、ハイブリッドおよびオンプレミスのデプロイメントでの **Campaign Classic v7 固有の高度なカスタマイズ**&#x200B;について説明します。

Campaign UI で配信を監視する方法について詳しくは、[Campaign v8 Campaign UI での配信の監視ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}を参照してください。

## 配信ログのカスタマイズ {#use-case}

**Campaign Classic v7 ハイブリッド／オンプレミスデプロイメント**&#x200B;の場合、スキーマを拡張して配信ログをカスタマイズできます。 この節では、送信者の IP アドレスを配信ログに追加する方法について説明します。

>[!NOTE]
>
>このカスタマイズには、オンプレミスデプロイメントで使用可能なスキーマ拡張機能が必要です。 Campaign v8 Managed Cloud Services ユーザーは、カスタム配信ログフィールドについてアドビカスタマーケアにお問い合わせください。
>
>この変更は、単一のインスタンスを使用する場合とミッドソーシングインスタンスを使用する場合とでは異なります。 変更をおこなう前に、メール送信インスタンスに接続していることを確認します。

### 手順 1：スキーマの拡張

配信ログに **publicID** を追加するには、まずスキーマを拡張する必要があります。 次の手順に従って進むことができます。

1. **[!UICONTROL 管理]**／**[!UICONTROL 設定]**／**[!UICONTROL データスキーマ]**／**[!UICONTROL 新規]**&#x200B;で、スキーマ拡張を作成します。

   スキーマ拡張について詳しくは、[このページ](../../configuration/using/extending-a-schema.md)を参照してください。

1. 受信者配信ログ（nms）を拡張し、カスタム名前空間を定義するには、**[!UICONTROL broadLogRcp]** を選択します。 この場合、「cus」になります。

   ![](assets/schema-parameters.png)

   >[!NOTE]
   >
   >インスタンスがミッドソーシングの場合は、broadLogMid スキーマを使用する必要があります。

1. 拡張に新しいフィールドを追加します。 このサンプルでは、

   ```
   <element img="nms:broadLog.png" label="Recipient delivery logs" labelSingular="Recipient delivery log" name="broadLogRcp"/>
   ```

   以下と置き換えます。

   ```
   <element img="nms:broadLog.png" label="Recipient delivery logs" labelSingular="Recipient delivery log" name="broadLogRcp">
   <attribute desc="Outbound IP identifier" label="IP identifier"
   name="publicId" type="long"/>
   </element>
   ```

   ![](assets/edit-schema.png)

### 手順 2：データベース構造の更新

変更が完了したら、データベース構造を更新して、論理的な説明と一致させる必要があります。

これをおこなうには、以下の手順に従います。

1. **[!UICONTROL ツール]**／**[!UICONTROL 詳細]**／**[!UICONTROL データベース構造の更新...]**&#x200B;メニューをクリックします。

   ![](assets/update-database-structure.png)

1. **[!UICONTROL テーブルの編集]**&#x200B;ウィンドウで、**[!UICONTROL NmsBroadLogRcp]** テーブル（ミッドソーシング環境の場合は **[!UICONTROL broadLogMid]** テーブル）が次のようにチェックされます。

   ![](assets/edit-tables.png)

   >[!IMPORTANT]
   >
   >**[!UICONTROL NmsBroadLoGRcp]** テーブル（ミッドソーシング環境の場合は **[!UICONTROL broadLogMid]** テーブル）を除き、他の変更がないことを必ず確認してください。 その場合は、他のテーブルのチェックを外します。

1. 「**[!UICONTROL 次へ]**」をクリックして確認します。 次の画面が表示されます。

   ![](assets/update-script.png)

1. 「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックして、データベース構造の更新を開始します。 インデックスの作成を開始しています。 この手順は、**[!UICONTROL NmsBroadLogRcp]** テーブルの行数に応じて長くなる場合があります。

   ![](assets/start-database-update.png)

>[!NOTE]
>
>データベースの物理構造の更新が正常に完了したら、変更を反映するために、接続を解除し、再接続する必要があります。

### 手順 3：変更の検証

すべてが正しく動作していることを確認するには、配信ログ画面を更新する必要があります。

これをおこなうには、配信ログにアクセスし、「IP 識別子」列を追加します。

![](assets/list-config.png)

>[!NOTE]
>
>Campaign Classic インターフェイスでリストを設定する方法については、[このページ](../../platform/using/adobe-campaign-workspace.md)を参照してください。

次に、変更後の「**[!UICONTROL 配信]**」タブの内容を示します。

![](assets/logs-with-ip.png)

## 関連トピック

* [Campaign UI での配信の監視](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-dashboard){target="_blank"}（Campaign v8 ドキュメント）
* [配信ステータス](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-statuses){target="_blank"}（Campaign v8 ドキュメント）
* [配信エラーについて](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"}（Campaign v8 ドキュメント）
* [強制隔離の管理](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"}（Campaign v8 ドキュメント）
* [スキーマの拡張](../../configuration/using/extending-a-schema.md)（v7 ハイブリッド／オンプレミス）

