---
product: campaign
title: 強制隔離管理について
description: 強制隔離管理について
feature: Monitoring, Deliverability
role: User
exl-id: cfd8f5c9-f368-4a31-a1e2-1d77ceae5ced
source-git-commit: eac670cd4e7371ca386cee5f1735dc201bf5410a
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 2%

---

# 強制隔離管理について{#understanding-quarantine-management}

>[!NOTE]
>
>強制隔離管理に関する包括的なガイダンスは、[Campaign v8 強制隔離管理 &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines) ページに記載されています。 このコンテンツは、Campaign Classic v7 と Campaign v8 の両方のユーザーに適用され、以下をカバーしています。
>
>* 強制隔離とブロックリストの概念
>* アドレスが強制隔離に送信される理由（ハードエラーまたはソフトエラー）
>* ソフトエラー管理とエラーカウンターのしきい値
>* 強制隔離アドレスへのアクセスと識別方法
>* 強制隔離からアドレスを削除する方法（自動、手動、一括）
>* 強制隔離管理レポート
>
>このページでは、ハイブリッドデプロイメントおよびオンプレミスデプロイメントでの強制隔離の管理について **0&rbrace;Campaign Classic v7 固有の設定 &rbrace; を説明します。**

包括的な強制隔離管理ガイダンスについては、[Campaign v8 強制隔離管理ドキュメント &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} を参照してください。

## 強制隔離の設定 {#v7-quarantine-config}

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

* [&#x200B; 強制隔離の管理 &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/quarantines){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; 配信エラーについて &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/monitor/delivery-failures){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; 配信のベストプラクティス &#x200B;](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/start/delivery-best-practices){target="_blank"} （Campaign v8 ドキュメント）
* [&#x200B; データベースクリーンアップワークフロー &#x200B;](../../production/using/database-cleanup-workflow.md) （v7 ハイブリッド/オンプレミス）
* [&#x200B; 配信再試行の設定 &#x200B;](communication-channels.md) （v7 ハイブリッド/オンプレミス）
