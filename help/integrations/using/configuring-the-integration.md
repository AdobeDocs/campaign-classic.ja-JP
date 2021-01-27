---
solution: Campaign Classic
product: campaign
title: Adobe Experience Manager 統合の設定
description: Campaign と AEM の統合を設定する方法を説明します
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 100%

---


# 統合の設定{#configuring-the-integration}

## Adobe Campaign での設定 {#configuring-in-adobe-campaign}

2 つのソリューションを同時に使用するには、相互接続を設定する必要があります。

次の手順に従って、Adobe Campaign での設定を開始します。

1. [Adobe Campaign での AEM 統合パッケージのインストール](#install-the-aem-integration-package-in-adobe-campaign)
1. [外部アカウントの設定](#configure-the-external-account)
1. [AEM リソースフィルターの設定](#configure-aem-resources-filtering)

パーソナライゼーションフィールドやパーソナライゼーションブロックの管理などの高度な設定については、Adobe Experience Manager の[ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/administering/using/campaignonpremise.html)を参照してください。

### Adobe Campaign での AEM 統合パッケージのインストール {#install-the-aem-integration-package-in-adobe-campaign}

最初に **[!UICONTROL AEM 統合]**&#x200B;パッケージをインストールする必要があります。

1. Adobe Campaign インスタンスから、上部のツールバーにある「**[!UICONTROL ツール]**」を選択します。
1. **[!UICONTROL ツール／高度なツール／パッケージをインポート...]**&#x200B;を選択します。

   ![](assets/aem_config_1.png)

1. 「**[!UICONTROL 標準パッケージをインストール]**」を選択します。
1. 「**[!UICONTROL AEM 統合]**」チェックボックスをオンにし、「**[!UICONTROL 次へ]**」ボタンをクリックします。

   ![](assets/aem_config_2.png)

1. 次のウィンドウで、「**[!UICONTROL 開始]**」ボタンをクリックして、パッケージのインストールを開始します。インストールが完了したら、ウィンドウを閉じます。

### AEM オペレーターのセキュリティゾーンの設定 {#configure-the-security-zone-for-aem-operator}

**[!UICONTROL AEM 統合]**&#x200B;パッケージは、Campaign に **[!UICONTROL aemserver]** オペレーターを設定します。このオペレーターは、Adobe Experience Manager サーバーを Adobe Campaign に接続するために使用されます。

Adobe Experience Manager 経由で Adobe Campaign に接続するには、このオペレーターのセキュリティゾーンを設定する必要があります。

>[!CAUTION]
>
>セキュリティ上の問題を回避するために、AEM 専用のセキュリティゾーンを作成することを強くお勧めします。詳しくは、[インストールガイド](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。

Campaign インスタンスがアドビによってホストされている場合は、アドビのサポートチームにお問い合わせください。Campaign をオンプレミスで使用している場合は、以下の手順に従います。

1. **serverConf.xml** 設定ファイルを開きます。
1. 選択したセキュリティゾーンの **allowUserPassword** 属性を **true** に設定します。

   これにより、Adobe Experience Manager がログイン／パスワード経由で Adobe Campaign に接続できるようになります。

### 外部アカウントの設定 {#configure-the-external-account}

**[!UICONTROL AEM 統合]**&#x200B;パッケージにより、Adobe Experience Cloud の外部アカウントが作成されました。次は、そのアカウントを Adobe Experience Manager インスタンスに接続するように設定する必要があります。

AEM 外部アカウントを設定するには、以下の手順に従います。

1. 「**[!UICONTROL エクスプローラー]**」ボタンをクリックします。

   ![](assets/aem_config_3.png)

1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;を選択します。
1. 「**[!UICONTROL 外部アカウント]**」の一覧から「**[!UICONTROL AEM インスタンス]**」を選択します。
1. AEM オーサーインスタンスの次のパラメーターを入力します。

   * **[!UICONTROL サーバー]**
   * **[!UICONTROL アカウント]**
   * **[!UICONTROL パスワード]**

   >[!NOTE]
   >
   >「**[!UICONTROL サーバー]**」のアドレスがスラッシュで終わっていないことを確認します。

   ![](assets/aem_config_4.png)

1. 「**[!UICONTROL 有効]**」ボックスをオンにします。
1. 「**[!UICONTROL 保存]**」ボタンをクリックします。

### AEM リソースフィルターの設定 {#configure-aem-resources-filtering}

**AEMResourceTypeFilter** オプションは、Adobe Campaign で使用できる Experience Manager リソースのタイプをフィルターするために使用します。これにより、Adobe Campaign は、Adobe Campaign のみで使用するように特別に設計された Experience Manager コンテンツを取得することができます。

**[!UICONTROL AEMResourceTypeFilter]** オプションが設定されているかどうかを確認するには：

1. 「**[!UICONTROL エクスプローラー]**」ボタンをクリックします。
1. **[!UICONTROL 管理／プラットフォーム／オプション]**&#x200B;を選択します。
1. 「**[!UICONTROL オプション]**」の一覧から「**[!UICONTROL AEMResourceTypeFilter]**」を選択します。
1. 「**[!UICONTROL 値 (テキスト)]**」フィールドでは、パスが次のようになっている必要があります。

   ```
   mcm/campaign/components/newsletter,mcm/campaign/components/campaign_newsletterpage,mcm/neolane/components/newsletter
   ```

   また、場合によっては次のようになります。

   ```
   mcm/campaign/components/newsletter
   ```

   ![](assets/aem_config_5.png)

## Adobe Experience Manager での設定 {#configuring-in-adobe-experience-manager}

次の手順に従って、Adobe Experience Manager での設定を開始します。

1. AEM オーサリングインスタンスから AEM パブリッシュインスタンスにレプリケートするように&#x200B;**レプリケーション**&#x200B;を設定します。

   レプリケーションの設定方法については、Adobe Experience Manager の[ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/deploying/using/replication.html)を参照してください。

1. オーサーインスタンスに統合 **FeaturePack** をインストールし、パブリッシュインスタンスにインストールをレプリケートします（AEM バージョン 5.6.1 および 6.0 のみ）。

   FeaturePack のインストール方法については、Adobe Experience Manager の[ドキュメント](https://helpx.adobe.com/jp/experience-manager/aem-previous-versions.html)を参照してください。

1. 専用の&#x200B;**クラウドサービス**&#x200B;を設定し、Adobe Experience Manager を Adobe Campaign に接続します。

   クラウドサービス経由で両方のソリューションを接続する方法については、Adobe Experience Manager の[ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/administering/using/campaignonpremise.html#ConfiguringAdobeExperienceManager)を参照してください。

1. **Externalizer サービス**&#x200B;を設定します。

   設定方法については、Adobe Experience Manager の[ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/sites/developing/using/externalizer.html)を参照してください。

