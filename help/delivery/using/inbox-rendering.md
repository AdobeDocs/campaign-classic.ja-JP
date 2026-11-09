---
product: campaign
title: Campaign での受信ボックスレンダリング
description: メールのレンダリングを取り込み、専用レポートで使用可能にする方法を説明します。
badge-v8: label="Also applies to v8" type="Positive" tooltip="Also applies to Campaign v8"
feature: Inbox Rendering, Monitoring, Email Rendering
role: User
exl-id: a3294e70-ac96-4e51-865f-b969624528ce
TQID: 'https://experienceleague.adobe.com/d0fFXi4Ma-PwY8vsSBOmvbhRD4631kUoagNXlf4Rmek'
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: b631758a-142d-425f-b9aa-f756d85cb979
    internal-label: Campaign Email Designer
  - id: c858a28b-ea19-49b0-8d48-828717fad89c
    internal-label: Prepare and test messages
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
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
  - id: 2317b1ea-6db4-58c7-851f-717a69c0f5c0
    internal-label: Inbox Rendering
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
    internal-label: Monitoring guidelines
  - id: aef0b685-fc31-54d4-b831-a87fdb9d69de
    internal-label: Email Rendering
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 758d5159759b19f7ef32e8cc8f6237547599e727
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 82%
---
# インボックスレンダリング{#inbox-rendering}

Adobe Campaignは、[Litmus](https://litmus.com/email-testing) web ベースの電子メールテストソリューションを活用して、電子メールのレンダリングをキャプチャし、専用のレポートで利用できるようにします。

>[!NOTE]
>
>Campaign v7 から v8 への移行の一環として、Campaign Classic のドキュメントセットを効率化および再編成しました。 共通機能は、Campaign v8 ドキュメントセットでのみ使用できるようになりました。 受信トレイのレンダリングについて詳しくは、[Campaign v8 ドキュメント ](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/deliverability-management/inbox-rendering){target=_blank}を参照してください。
>
>[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/send/deliverability-management/inbox-rendering){target=_blank}

## 受信ボックスレンダリングの有効化 {#activating-inbox-rendering}

[!BADGE オンプレミスおよびハイブリッド]{type=Caution url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"}

ホストクライアントおよびハイブリッドクライアントの場合、受信ボックスレンダリングはアドビのテクニカルサポートおよびコンサルタントがインスタンスに設定します。 詳しくは、アドビのアカウント担当者にお問い合わせください。

オンプレミスインストールの場合は、次の手順に従って受信ボックスレンダリングを設定します。

1. **[!UICONTROL 受信ボックスレンダリング（IR）]**&#x200B;パッケージをインストールするには、**[!UICONTROL ツール]**／**[!UICONTROL 詳細設定]**／**[!UICONTROL パッケージをインポート]**&#x200B;メニューを使用します。 詳しくは、[Campaign Classic 標準パッケージのインストール](../../installation/using/installing-campaign-standard-packages.md)を参照してください。
1. HTTP タイプの外部アカウントは、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;ノードで設定します。 詳しくは、[外部アカウントの作成](../../installation/using/external-accounts.md#creating-an-external-account)を参照してください 。
1. 外部アカウントのパラメーターを次のように設定します。
   * **[!UICONTROL ラベル]**：配信品質サーバー情報
   * **[!UICONTROL 内部名]**： deliverabilityInstance
   * **[!UICONTROL タイプ]**： HTTP
   * **[!UICONTROL サーバー]**： https://deliverability-app.neolane.net/deliverability
   * **[!UICONTROL 暗号化]**：なし
   * 「**[!UICONTROL 有効]**」オプションをオンにします。

   ![](assets/s_tn_inbox_rendering_external-account.png)

1. **[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL オプション]**&#x200B;ノードに移動します。 「**[!UICONTROL DmRendering_cuid]**」オプションを検索します。サポートに連絡して、**[!UICONTROL 値 (テキスト)]** フィールドにコピーする必要のある、配信レポートの識別子を取得します。
1. **serverConf.xml** ファイルを編集して、Litmus サーバーへの呼び出しを許可します。 次の行を `<urlPermission>` セクションに追加します。

   ```
   <url dnsSuffix="deliverability-app.neolane.net" urlRegEx="https://.*"/>
   ```

1. 次のコマンドを使用して、設定を再読み込みします。

   ```
   nlserver config -reload
   ```

>[!NOTE]
>
>受信ボックスレンダリングを使用するには、コンソールからログアウトし、再度ログインする必要がある場合があります。
