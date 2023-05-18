---
product: campaign
title: Experience Manager ニュースレターの作成
description: Experience Manager ニュースレターの作成
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
audience: integrations
content-type: reference
exl-id: 9fa3ce08-3007-4c65-9841-bad339428b7c
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: ht
source-wordcount: '349'
ht-degree: 100%

---

# Experience Manager ニュースレターの作成{#creating-an-experience-manager-newsletter}



この統合を利用して、例えば、Adobe Experience Manager で作成したニュースレターを Adobe Campaign でメールキャンペーンの一部として使用できます。

**Adobe Experience Manager から：**

1. AEM オーサーインスタンスから、ページの左上にある **Adobe Experience** ロゴをクリックし、「**[!UICONTROL サイト]**」を選択します。

   ![](assets/aem_uc_1.png)

1. **[!UICONTROL キャンペーン／ブランド名（ここでは We.Retail）／メイン領域／電子メールキャンペーン]**&#x200B;を選択します。
1. ページの右上にある「**[!UICONTROL 作成]**」ボタンをクリックし、「**[!UICONTROL ページ]**」を選択します。

   ![](assets/aem_uc_2.png)

1. 「**[!UICONTROL Adobe Campaign 電子メール (AC 6.1)]**」テンプレートを選択し、ニュースレターに名前を付けます。
1. ページが作成されたら、**[!UICONTROL ページ情報]**&#x200B;メニューにアクセスし、「**[!UICONTROL プロパティを開く]**」をクリックします。

   ![](assets/aem_uc_3.png)

1. 「**[!UICONTROL クラウドサービス]**」タブで、「**[!UICONTROL クラウドサービスの設定]**」として「**[!UICONTROL Adobe Campaign]**」を、2 番目のドロップダウンで Adobe Campaign インスタンスを選択します。

   ![](assets/aem_uc_4.png)

1. Adobe Campaign のパーソナライゼーションフィールドなどのコンポーネントを追加して E メールコンテンツを編集します。
1. E メールが準備できたら、**[!UICONTROL ページ情報]**&#x200B;メニューにアクセスし、「**[!UICONTROL ワークフローを開始]**」をクリックします。

   ![](assets/aem_uc_5.png)

1. 最初のドロップダウンから、ワークフローモデルとして「**[!UICONTROL Adobe Campaign に公開]**」を選択し、「**[!UICONTROL ワークフローを開始]**」をクリックします。

   ![](assets/aem_uc_6.png)

1. 次に、前の手順と同じように、**[!UICONTROL Campaign 用に承認]**&#x200B;ワークフローを開始します。
1. ページの上部に免責事項が表示されます。「**[!UICONTROL 完了]**」をクリックしてレビューを確認し、「**[!UICONTROL OK]**」をクリックします。

   ![](assets/aem_uc_7.png)

1. もう一度「**[!UICONTROL 完了]**」をクリックし、「**[!UICONTROL 次のステップ]**」ドロップダウンで「**[!UICONTROL ニュースレターの承認]**」を選択します。

   ![](assets/aem_uc_8.png)

これでニュースレターが準備でき、Adobe Campaign で同期されました。

**Adobe Campaign から：**

1. 「**[!UICONTROL キャンペーン]**」タブで、「**[!UICONTROL 配信]**」、「**[!UICONTROL 作成]**」の順にクリックします。

   ![](assets/aem_uc_9.png)

1. 「**[!UICONTROL 配信テンプレート]**」ドロップダウンで、「**[!UICONTROL AEM コンテンツで E メール配信 (mailAEMContent)]**」テンプレートを選択します。

   ![](assets/aem_uc_10.png)

1. 配信に&#x200B;**[!UICONTROL ラベル]**&#x200B;を追加し、「**[!UICONTROL 続行]**」をクリックします。
1. 「**[!UICONTROL 同期]**」ボタンをクリックします。

   このボタンがインターフェイスに表示されていない場合は、「**[!UICONTROL プロパティ]**」ボタンをクリックし、「**[!UICONTROL 詳細設定]**」タブを選択します。「**[!UICONTROL コンテンツ編集モード]**」フィールドを「**[!UICONTROL AEM]**」に、「**[!UICONTROL AEM アカウント]**」フィールドを AEM インスタンスに設定する必要があります。

   ![](assets/aem_uc_11.png)

1. 以前に Adobe Experience Manager で作成した配信を選択し、「**[!UICONTROL OK]**」をクリックします。
1. AEM 配信に変更を加えたら、すぐに「**[!UICONTROL コンテンツを更新]**」ボタンをクリックします。

   ![](assets/aem_uc_12.png)

これで E メールをオーディエンスに送信する準備が整いました。
