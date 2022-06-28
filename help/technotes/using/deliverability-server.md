---
product: campaign
title: 新しい配信サーバーに移行
description: Campaign 配信サーバーの実装方法を説明します
hide: true
hidefromtoc: true
source-git-commit: cd2fa2450f6e8389e9c47c412da8943a5c8bb7f3
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 38%

---

# キャンペーン配信サーバー {#acc-deliverability}

Campaign Classicv7 21.1 リリースより、Adobe Campaignは、高可用性をもたらし、セキュリティコンプライアンスの問題に対処する新しい配信品質サーバーを提案します。 Campaign Classicは、新しい配信品質サーバーとの間で、配信品質ルール、broadlog および抑制アドレスを同期するようになりました。

Campaign Classicのお客様は、新しい配信品質サーバーを実装する必要があります

>[!NOTE]
>
>これらの変更点に関するご質問については、[FAQ](#faq-aa) を参照してください。 詳しくは、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## 変更点{#acc-deliverability-changes}

Adobeは、セキュリティコンプライアンス上の理由により、古いデータセンターを廃止しています。 Adobe Campaign Classicのクライアントは、Amazon Web Service(AWS) でホストされる新しい配信品質サービスに移行する必要があります。

この新しいサーバーは、高い可用性 (99.9) を保証し、安全で認証済みのエンドポイントを提供し&#x200B;て、キャンペーンサーバーが必要なデータを取得できるようにします。新しい配信品質サーバーは、リクエストごとにデータベースに接続するのではなく、可能な限りリクエストに対応するためにデータをキャッシュします。 このメカニズムにより、応答時間が短縮されま&#x200B;す。


## 影響の有無{#acc-deliverability-impacts}

古いAdobe Campaign配信品質サーバーを使用していて、環境が Campaign 21.1.1 よりも低いビルドで実装された場合は、影響を受けます。 Campaign 21.1（またはそれ以上）にアップグレードする必要があります。

バージョンを確認する方法については、](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)この節[を参照してください。

## 更新方法{#acc-deliverability-update}

ホステッド環境のお客様の場合、アドビはお客様と協力してインスタンスを新しいバージョンにアップグレードします。

オンプレミス/ハイブリッド型の顧客は、新しい配信品質サーバーのメリットを活用するには、新しいバージョンの 1 つにアップグレードする必要があります。
すべてのインスタンスをアップグレードすると、次の操作が可能になります。 [新しい統合の実装](#implementation-steps) をAdobe配信サーバーに追加し、シームレスな移行を確保します。

## 実装手順（ハイブリッドおよびオンプレミスのお客様） {#implementation-steps}

>[!IMPORTANT]
>
>これらの手順は、ハイブリッド実装とオンプレミス実装のみで実行する必要があります。
>
>ホストされている実装の場合は、にお問い合わせください。 [Adobeカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html).

### 前提条件{#prerequisites}

新しい配信品質サーバーの統合の一環として、Campaign は、Identity Managementサービス (IMS) ベースの認証を通じてAdobeの Shared Services と通信する必要があります。 推奨される方法は、Adobe Developerベースのゲートウェイトークン ( テクニカルアカウントトークンまたはAdobeI/O JWT とも呼ばれます ) を使用することです。

### 手順 1:Adobe Developerプロジェクトを作成/更新 {#adobe-io-project}

1. アクセス [Adobe Developer Console](https://developer.adobe.com/console/home) 組織の開発者アクセス権でログインします。

   >[!NOTE]
   >
   > 正しい組織ポータルにログインしていることを確認します。

1. 「**[!UICONTROL + プロジェクトに追加]**」を選択して、「**[!UICONTROL API]**」を選択します。
1. 内 **[!UICONTROL API を追加]** ウィンドウ：選択 **[!UICONTROL Adobe Campaign]**.
1. 認証のタイプとして「**[!UICONTROL Service Account (JWT)]**」を選択します。
1. クライアント ID が空の場合は、「**[!UICONTROL キーペアを生成]**」を選択して、公開鍵と秘密鍵のペアを作成します。

   キーは、デフォルトの有効期限 365 日で自動的にダウンロードされます。 有効期限が切れたら、新しいキーペアを作成し、設定ファイルで統合を更新する必要があります。 オプション 2 を使用すると、有効期限の長い&#x200B;**[!UICONTROL 公開鍵]**&#x200B;を手動で作成してアップロードすることを選択できます。

   >[!CAUTION]
   >
   >再度ダウンロードすることができないので、ダウンロードプロンプトが表示されたら、config.zip ファイルを保存してください。

1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 既存の&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を選択するか、必要に応じて新しいプロファイルを作成します。 この&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;には権限は必要ありません。 詳しくは、 [!DNL Analytics] **[!UICONTROL 製品プロファイル]**（を参照） [このページ](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html).

   次に、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

1. プロジェクトから、 **[!UICONTROL Adobe Campaign]** 次の情報を **[!UICONTROL サービスアカウント (JWT)]**:

   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

>[!CAUTION]
>
>Adobe Developer証明書は、12 ヶ月後に期限が切れます。 毎年新しいキーペアを生成する必要があります。

### 手順 2：Adobe Campaign へのプロジェクト資格情報の追加 {#add-credentials-campaign}

秘密鍵は、Base64 UTF-8 形式でエンコードする必要があります。

それには、次の手順に従います。

1. 上記の手順で生成された秘密鍵を使用します。
1. `base64 ./private.key > private.key.base64` というコマンドを使用して秘密鍵をエンコードします。これにより、base64 コンテンツが新しいファイル `private.key.base64` に保存されます。

   >[!NOTE]
   >
   >秘密鍵をコピーして貼り付けるときに、余分な行が自動的に追加される場合があります。 これは、秘密鍵をエンコードする前に忘れずに削除してください。

1. ファイル `private.key.base64` からコンテンツをコピーします。
1. Adobe Campaign インスタンスがインストールされている各コンテナに SSH 経由でログインし、`neolane` ユーザーとして次のコマンドを実行して Adobe Campaign にプロジェクト資格情報を追加します。これにより、**[!UICONTROL テクニカルアカウント]**&#x200B;資格情報がインスタンス設定ファイルに挿入されます。

   ```
   nlserver config -instance:<instance name> -setimsjwtauth:Organization_Id/Client_Id/Technical_Account_ID/<Client_Secret>/<Base64_encoded_Private_Key>
   ```

1. 変更を反映させるには、サーバーを停止してから再起動する必要があります。 また、 `config -reload` コマンドを使用します。

### 手順 3:設定を確認

設定が完了したら、インスタンスの設定を確認できます。 以下の手順に従います。

1. クライアントコンソールを開き、管理者としてAdobe Campaignにログオンします。
1. 参照先 **管理/プラットフォーム/オプション**.
1. 次を確認します。 `DmRendering_cuid` オプションの値が入力されます。 すべての Campaign インスタンス (MKT、MID、RT、EXEC) で入力する必要があります。 値が入力されていない場合は、値を入力する必要があります。 値が入力されていない場合は、に連絡してください。 [Adobeカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) をクリックして CUID を取得します。

### 手順 4:新しい配信サーバーを有効にする

これで、新しい配信品質サーバーを有効にできます。 次の手順を実行します。

1. クライアントコンソールを開き、管理者としてAdobe Campaignにログオンします。
1. 参照先 **管理/プラットフォーム/オプション**.
1. 次にアクセス： `NewDeliverabilityServer_FeatureFlag` オプションを選択し、値を `1`. この設定は、すべての Campaign インスタンス (MKT、MID、RT、EXEC) で実行する必要があります。


### 手順 5:設定の検証

統合が成功したことを確認するには、次の手順に従います。


1. クライアントコンソールを開き、Adobe Campaignにログオンします。
1. 参照先 **管理/プロダクション/テクニカルワークフロー**.
1. を再起動します。 **配信品質の更新** (deliverabilityUpdate) ワークフロー。 これは、すべての Campaign インスタンス (MKT、MID、RT、EXEC) で実行する必要があります。
1. ログを確認する：ワークフローは、エラーなしで実行する必要があります。

## FAQ{#faq-aa}

Q:回答：

Q:回答：



詳しくは、[アドビカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。
