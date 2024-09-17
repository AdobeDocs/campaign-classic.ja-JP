---
product: campaign
title: 新しい配信サーバーへの更新
description: 新しい Campaign 配信サーバーに更新する方法を説明します
feature: Technote, Deliverability
hide: true
hidefromtoc: true
exl-id: bc62ddb9-beff-4861-91ab-dcd0fa1ed199
source-git-commit: 8d15a5666b5768bc0f17a4391061c4fcb9f76811
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 98%

---

# 新しい配信サーバーへの更新 {#acc-deliverability}

[v7.2.2 リリース](../../rn/using/latest-release.md#release-7-2-2)以降、Adobe Campaign は、可用性が高くセキュリティコンプライアンスの問題にも対処できる新しい配信品質サーバーを利用しています。Campaign Classic は、新しい配信サーバーとの間で、配信品質ルール、broadLog および抑制アドレスを同期するようになりました。古い配信品質サーバーは 2022年8月31日に廃止されます。

Campaign Classic のお客様は、**2022年8月31日までに**&#x200B;新しい配信品質サーバーを実装する必要があります。

>[!NOTE]
>
>これらの変更に関する詳細な質問については、[FAQ](#faq) を参照するか、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){_blank}にお問い合わせください。
>

## 変更点{#acc-deliverability-changes}

アドビは、セキュリティコンプライアンス上の理由により、古いデータセンターを廃止しています。Adobe Campaign Classic のクライアントは、Amazon Web Service（AWS）でホストされる新しい配信サービスに移行する必要があります。

この新しいサーバーは、高い可用性（99.9）を保証し、安全で認証済みのエンドポイントを提供して、キャンペーンサーバーが必要なデータを取得できるようにします。新しい配信サーバーは、リクエストごとにデータベースに接続するのではなく、可能な限りリクエストに対応するためにデータをキャッシュします。このメカニズムにより、応答時間が改善されます。

## 影響の有無{#acc-deliverability-impacts}

すべてのお客様に影響があるので、新しい配信品質サーバーのメリットを得るには [Campaign v7.2.2](../../rn/using/latest-release.md#release-7-2-2)（またはそれ以上）にアップグレードして、環境を実装する必要があります。

## 更新方法{#acc-deliverability-update}

**ホスト環境のお客様**&#x200B;の場合、アドビはお客様と協力してインスタンスを新しいバージョンにアップグレードし、Adobe Developer Console でプロジェクトを作成します。

**オンプレミス／ハイブリッド環境のお客様**&#x200B;の場合、新しい配信品質サーバーのメリットを得るには、 [Campaign v7.2.2](../../rn/using/latest-release.md#release-7-2-2)（またはそれ以上）にアップグレードする必要があります。すべてのインスタンスがアップグレードされると、アドビ配信品質サーバーに[新しい統合を実装し](#implementation-steps)、シームレスな移行を確実に実現できるようになります。

## 実装手順 {#implementation-steps}

>[!WARNING]
>
>これらの手順は、ハイブリッド実装とオンプレミス実装でのみ実行してください。

新しい配信サーバーの統合の一環として、Campaign は、Identity Management Service（IMS）ベースの認証を経由して Adobe Shared Services と通信する必要があります。推奨される方法は、Adobe Developer ベースのゲートウェイトークン（テクニカルアカウントトークンまたは Adobe I/O JWT とも呼ばれます）を使用することです。

>[!AVAILABILITY]
>
> サービスアカウント（JWT）資格情報はアドビによって廃止され、アドビのソリューションおよびアプリとの Campaign 統合では、OAuth サーバー間の資格情報に依存する必要があります。</br>
>
> * Campaign とのインバウンド統合を実装している場合は、[このドキュメント](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#_blank)の詳細な説明に従ってテクニカルアカウントを移行する必要があります。既存の [ サービスアカウント（JWT）資格情報 ](oauth-technical-account.md) は、2025 年 1 月 27 日（PT）まで引き続き機能します。</br>
>
> * Campaign と Analytics 統合や Experience Cloud トリガー統合などのアウトバウンド統合を実装している場合は、2025年1月27日（PT）まで引き続き機能します。ただし、この日付までに、Campaign 環境を v7.4.1 にアップグレードし、テクニカルアカウントを OAuth に移行する必要があります。

### 前提条件{#prerequisites}

実装を開始する前に、インスタンスの設定を確認します。

1. Campaign クライアントコンソールを開き、管理者として Adobe Campaign にログオンします。
1. **管理／プラットフォーム／オプション**&#x200B;を参照します。
1. `DmRendering_cuid` オプションの値が入力されていることを確認します。

   * オプションの値が入力されている場合は、実装を開始できます。
   * 値が入力されていない場合は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){_blank} に連絡して CUID を取得してください。

   このオプションは、すべての Campaign インスタンス (MKT、MID、RT、EXEC) に正しい値で入力する必要があります。ハイブリッド環境のお客様は、アドビに連絡して、MID、RT、EXEC の各インスタンスでオプションを設定してもらいます。

また、オンプレミス環境の顧客は Campaign の&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;が組織で使用できることを確認する必要があります。手順は次のとおりです。

1. 管理者として、[Adobe Admin Console](https://adminconsole.adobe.com/){_blank} に接続します。
1. 「**製品とサービス**」セクションにアクセスし、**Adobe Campaign** が一覧表示されていることを確認します。
**Adobe Campaign** が表示されない場合、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html){_blank} に連絡し、Adobe Campaign を追加します。
1. **Adobe Campaign** をクリックし、組織を選択します。
   **注意**：複数の組織がある場合は、正しい組織を選択していることを確認します。組織について詳しくは、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/faq.html?lang=ja#ims-org-id){_blank}を参照してください。

1. **[!UICONTROL 製品プロファイル]**&#x200B;が存在するか確認します。存在しない場合は作成します。この&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;には権限は必要ありません。 


>[!CAUTION]
>
>オンプレミス環境のお客様がファイアウォールを自ら実装する場合は、この URL `https://deliverability-service.adobe.io` を許可リストに追加する必要があります。 [詳細情報](../../installation/using/url-permissions.md)。


### 手順 1：Adobe Developer プロジェクトを作成／更新 {#adobe-io-project}

Adobe Analytics コネクタの設定に進むには、Adobe Developer Console にアクセスして、OAuth サーバー間プロジェクトを作成します。

詳しくは、[こちらのページ](../../integrations/using/oauth-technical-account.md#oauth-service)を参照してください。

### 手順 2：Adobe Campaign へのプロジェクト資格情報の追加 {#add-credentials-campaign}

[こちらのページ](../../integrations/using/oauth-technical-account.md#add-credentials)で説明されている手順に従って、OAuth プロジェクト資格情報を Adobe Campaign に追加します。

### 手順 3：設定を検証

統合が成功したことを確認するには、以下の手順に従います。

1. クライアントコンソールを開き、Adobe Campaign にログオンします。
1. **管理／プロダクション／テクニカルワークフロー**&#x200B;を参照します。
1. **配信品質の更新** (deliverabilityUpdate) ワークフローを再起動します。すべての Campaign インスタンス（MKT、MID、RT、EXEC）でこの手順を実行する必要があります。ハイブリッド環境のお客様は、アドビに連絡して、MID、RT、EXEC の各インスタンスでワークフローを再開してもらいます。
1. ログを確認：ワークフローは、エラーなく実行する必要があります。

>[!CAUTION]
>
>更新後、 **受信ボックスレンダリング用のシードネットワークを更新（updateRenderingSeeds）**&#x200B;ワークフローは適用されなくなり、失敗するため、ワークフローを停止する必要があります。

## よくある質問 {#faq}

### 更新のタイムライン

新しい配信品質サーバーへの移行は、これらの強化された機能の追加とセキュリティの強化を可能にし、ホスト環境のお客様 (Campaign Managed Services) 向けに 2022年7月に開始されます。 すべてのホスト環境のお客様は、8月末までに更新されます。

オンプレミス環境およびハイブリッド環境のお客様は、同じ期間中に移行する必要があります。

### 環境をアップグレードしない場合はどうなりますか？

8月31日までにアップグレードされなかった Campaign インスタンスは、Campaign 配信品質サーバーに接続できなくなります。結果として、**配信品質の更新** (deliverabilityUpdate) ワークフローは失敗し、配信品質に影響を与えます。

環境をアップグレードしない場合、メール設定の同期は停止されます（MX 管理ルール、インバウンドメールルール、ドメイン管理ルール、バウンスの選定ルール）。これは、配信品質の長期化に影響を与える可能性があります。これらのルールに大きな変更が加えられた場合は、この時点から手動で適用する必要があります。

MKT インスタンスの場合は、[グローバル抑制リスト](../../campaign-opt/using/filtering-rules.md#default-deliverability-exclusion-rules)のみが影響を受けます。
