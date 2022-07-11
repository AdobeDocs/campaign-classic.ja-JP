---
product: campaign
title: 新しい配信サーバーに移行
description: Campaign 配信サーバーの実装方法を学ぶ
hide: true
hidefromtoc: true
exl-id: bc62ddb9-beff-4861-91ab-dcd0fa1ed199
source-git-commit: a007e4d5dd73f01657f1642be6f0b1a92f39e9bf
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 87%

---

# Campaign 配信サーバー {#acc-deliverability}

Campaign Classic v7 21.1 リリースより、Adobe Campaign は、高可用性をもたらし、セキュリティコンプライアンスの問題に対処する新しい配信サーバーを提案します。Campaign Classic は、新しい配信サーバーとの間で、配信品質ルール、broadLog および抑制アドレスを同期するようになりました。

Campaign Classic のお客様は、新しい配信サーバーを実装する必要があります

>[!NOTE]
>
>これらの変更点に関するご質問については、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

## 変更点{#acc-deliverability-changes}

アドビは、セキュリティコンプライアンス上の理由により、古いデータセンターを廃止しています。Adobe Campaign Classic のクライアントは、Amazon Web Service（AWS）でホストされる新しい配信サービスに移行する必要があります。

この新しいサーバーは、高い可用性（99.9）を保証し、安全で認証済みのエンドポイントを提供して、キャンペーンサーバーが必要なデータを取得できるようにします。新しい配信サーバーは、リクエストごとにデータベースに接続するのではなく、可能な限りリクエストに対応するためにデータをキャッシュします。このメカニズムにより、応答時間が改善されます。


## 影響の有無{#acc-deliverability-impacts}

古い Adobe Campaign 配信サーバーを使用していて、環境が Campaign 21.1.1 よりも低いビルドで実装されている場合は、影響を受けます。Campaign 21.1（またはそれ以上）にアップグレードする必要があります。

バージョンを確認する方法については、](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)この節[を参照してください。

## 更新方法{#acc-deliverability-update}

As a **ホスト顧客**&#x200B;の場合、Adobeはお客様と連携して、インスタンスを新しいバージョンにアップグレードし、Adobe Developer Console でプロジェクトを作成します。

As a **オンプレミス/ハイブリッド顧客**&#x200B;新しい配信品質サーバーのメリットを活用するには、新しいバージョンの 1 つにアップグレードする必要があります。 すべてのインスタンスがアップグレードされると、アドビ配信サーバーに[新しい統合を実装し](#implementation-steps)、シームレスな移行を確実に行うことができるようになります。

## 実装手順（ハイブリッドおよびオンプレミスのお客様） {#implementation-steps}

>[!WARNING]
>
>これらの手順は、ハイブリッド実装とオンプレミス実装でのみ実行してください。
>
>ホスト環境での実装については、[アドビカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。

### 前提条件{#prerequisites}

新しい配信サーバーの統合の一環として、Campaign は、Identity Management Service（IMS）ベースの認証を経由して Adobe Shared Services と通信する必要があります。推奨される方法は、Adobe Developer ベースのゲートウェイトークン（テクニカルアカウントトークンまたは Adobe I/O JWT とも呼ばれます ) を使用することです。

### 手順 1：Adobe Developer プロジェクトを作成／更新 {#adobe-io-project}



1. [Adobe Developer Console](https://developer.adobe.com/console/home) にアクセスし、組織の開発者アクセス権を使用してログインします。

   >[!NOTE]
   >
   > 正しい組織ポータルにログインしていることを確認します。

1. 選択 **[!UICONTROL 新規プロジェクトを作成]**.
   ![](assets/New-Project.png)


   >[!CAUTION]
   >
   >別の統合 (Analytics コネクタ、Adobeトリガーなど ) で既にAdobeI/O JWT 認証機能を使用している場合は、 **キャンペーン API** をそのプロジェクトに追加します。
1. 選択 **[!UICONTROL API を追加]**.
   ![](assets/Add-API.png)
1. **[!UICONTROL API を追加]**&#x200B;ウィンドウで、「**[!UICONTROL Adobe Campaign]**」を選択します。
   ![](assets/AC-API.png)
<!--1. Choose **[!UICONTROL Service Account (JWT)]** as the authentication type.-->
1. クライアント ID が空の場合は、「**[!UICONTROL キーペアを生成]**」を選択して、公開鍵と秘密鍵のペアを作成します。
   ![](assets/Generate-a-key-pair.png)

   キーは、デフォルトの有効期限 365 日で自動的にダウンロードされます。 有効期限が切れたら、新しいキーペアを作成し、設定ファイルで統合を更新する必要があります。 オプション 2 を使用すると、有効期限の長い&#x200B;**[!UICONTROL 公開鍵]**を手動で作成してアップロードすることを選択できます。
   ![](assets/New-key-pair.png)

   >[!CAUTION]
   >
   >次のファイルを保存します。 `config.zip` ファイルをダウンロードする必要があります。

1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 既存の&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;を選択するか、必要に応じて新しいプロファイルを作成します。 この&#x200B;**[!UICONTROL 製品プロファイル]**&#x200B;には権限は必要ありません。 **[!UICONTROL 製品プロファイル]**&#x200B;について詳しくは、[このページ](https://helpx.adobe.com/jp/enterprise/using/manage-developers.html)を参照してください。
   ![](assets/Product-Profile-API.png)

   次に、「**[!UICONTROL 設定済み API を保存]**」をクリックします。

1. プロジェクトから、 **[!UICONTROL Adobe Campaign]** 次の情報を **[!UICONTROL サービスアカウント (JWT)]**

   ![](assets/Config-API.png)

   * **[!UICONTROL クライアント ID]**
   * **[!UICONTROL クライアント秘密鍵]**
   * **[!UICONTROL テクニカルアカウント ID]**
   * **[!UICONTROL 組織 ID]**

>[!CAUTION]
>
>Adobe Developer 証明書は 12 か月後に期限が切れます。毎年新しいキーペアを生成する必要があります。

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

1. 変更を反映させるには、サーバーを停止し、再起動する必要があります。 また、 `config -reload` コマンドを使用します。

### 手順 3：設定を確認

設定が完了したら、インスタンスの設定を確認できます。 以下の手順に従います。

1. クライアントコンソールを開き、管理者としてAdobe Campaign にログオンします。
1. **管理／プラットフォーム／オプション**&#x200B;を参照します。
1. `DmRendering_cuid` オプションの値が入力されていることを確認します。 すべての Campaign インスタンス（MKT、MID、RT、EXEC）で入力する必要があります。値が入力されていない場合は、[アドビカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) に連絡して CUID を取得してください。

### 手順 4：新しい配信サーバーを有効にする

これで、新しい配信サーバーを有効にできます。次の手順を実行します。

1. クライアントコンソールを開き、管理者としてAdobe Campaign にログオンします。
1. **管理／プラットフォーム／オプション**&#x200B;を選択します。
1. `NewDeliverabilityServer_FeatureFlag` オプションにアクセスし、値を `1` に設定します。この設定は、すべての Campaign インスタンス（MKT、MID、RT、EXEC）で実行する必要があります。

### 手順 5：設定を検証

統合が成功したことを確認するには、以下の手順に従います。


1. クライアントコンソールを開き、Adobe Campaign にログオンします。
1. **管理／プロダクション／テクニカルワークフロー**&#x200B;を参照します。
1. **配信品質を更新**（deliverabilityUpdate）ワークフローを再起動します。 これは、すべての Campaign インスタンス（MKT、MID、RT、EXEC）で実行する必要があります。
1. ログを確認：ワークフローは、エラーなく実行する必要があります。

詳しくは、[アドビカスタマーケア](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせください。
