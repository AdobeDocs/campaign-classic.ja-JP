---
title: オファーの承認と有効化
seo-title: オファーの承認と有効化
description: オファーの承認と有効化
seo-description: null
page-status-flag: never-activated
uuid: 1be96bb4-ef17-4b4d-b872-05e1c6b1412d
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: managing-an-offer-catalog
discoiquuid: 7b1c58a0-6fd6-4c9d-b1c4-f3dffda42523
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 215e4d1ca78938b38b53cae0357612deebf7727b

---


# オファーの承認と有効化{#approving-and-activating-an-offer}

オファーコンテンツが完成したら、オファーを承認して、ライブ環境への複製と配信が実行されるようにする必要があります。承認は、オファーのコンテンツおよび実施要件に関しておこなわれます。

オファーダッシュボード上のバナーには、そのオファーについて承認サイクルを実行する必要があるかどうかが示されます。

![](assets/offer_validate_001.png)

## オファーコンテンツの承認 {#approving-offer-content}

オファーコンテンツを承認することは、ライブ環境で利用可能にする表示域を選択することを意味します。

オファーのコンテンツは、スペースごとに表示域を 1 つ持っています。各オファースペースには、独自の構造とレンダリング関数があるので、オファー表示域にも違いがあります。

利用可能な特定のスペースに対してオファーコンテンツを承認し、他のスペースに対しては却下することもできます。

>[!CAUTION]
>
>オファーのコンテンツおよび実施要件が承認されると、パブリッシュワークフロー（オファー通知）が自動的に実行されてオファーがライブ環境に移行し、すべての有効化されたスペース上で利用できるようになります。

オファーコンテンツを承認するには、次の手順に従います。

1. ボタンをクリック **[!UICONTROL Approval]** し、ポップアップで **[!UICONTROL Approve content]** 選択します。

   ![](assets/offer_validate_002.png)

1. Using the drop-down list, select the representations you want to keep editing or those you want to publish to the live environment, then click **[!UICONTROL Content approval]**.

   ![](assets/offer_validate_003.png)

   オファーコンテンツが承認されると、オファーダッシュボードの表の情報が更新されます。

   ![](assets/offer_validate_004.png)

   >[!NOTE]
   >
   >The **[!UICONTROL Content approved]** mention does not mean that all the offer representations have been enabled and approved. すべてのオファーが有効になり承認されているかどうかに関わらず、コンテンツの承認プロセスが達成されたことを示しています。

## オファーの実施要件の承認 {#approving-offer-eligibility}

オファーの実施要件を承認することは、オファーに設定された、または親カテゴリに作成されたルールから継承された、オファーの重み付けと実施要件ルールを承認または却下することを意味します。

>[!CAUTION]
>
>オファーのコンテンツおよび実施要件が承認されると、パブリッシュワークフロー（オファー通知）が自動的に実行されてオファーがライブ環境に移行し、すべての有効化されたスペース上で利用できるようになります。

* ルールの完全なリストは、をクリックすると表示できま **[!UICONTROL Schedule and eligibility rules]**&#x200B;す。

   ![](assets/offer_validate_005.png)

* 適格性ルールを変更するには、をクリックし、 **[!UICONTROL Reject]**&#x200B;をクリックしま **[!UICONTROL Eligibility approval]**&#x200B;す。

   ![](assets/offer_validate_007.png)

   オファーダッシュボード上の様々なステータスが更新されます。

   ![](assets/offer_validate_006.png)

* To accept the offer eligibility, click **[!UICONTROL Approve eligibility]**.

   ![](assets/offer_validate_008.png)

   Approve eligibility, add a comment if necessary, then click **[!UICONTROL Eligibility approval]**.

   ![](assets/offer_validate_009.png)

   オファーダッシュボード上の様々なステータスが更新されます。

   ![](assets/offer_validate_010.png)

## 承認トラッキング {#approval-tracking}

オファーダッシュボードでは、承認をトラッキングできます。をクリック **[!UICONTROL Hide/display logs]** してアクセスします。

![](assets/offer_validate_012.png)

>[!NOTE]
>
>Tracking is also available in the **[!UICONTROL Audit]** tab of the offer, with details of reviewers&#39; comments.

## 承認の再開 {#restart-the-approval}

承認が開始された後で、承認を再開できます。それには、次の手順に従います。

1. オファーダ **[!UICONTROL Content approved]** ッシュボードのをクリックします。
1. 表示される **[!UICONTROL Edit]** ウィンドウで、再起動する承認を選択し、をクリックしま **[!UICONTROL Re-initialize approval to submit it again]**&#x200B;す。
1. Confirm by clicking **[!UICONTROL Ok]**.

![](assets/offer_validate_013.png)

## オファーのパブリッシュ {#publishing-the-offer}

コンテンツと実施要件が両方とも承認されると、承認サイクルが完了した各オファーに対して自動実行されるワークフローによって、オファーがパブリッシュされます。The **[!UICONTROL Offer notification]** workflow also runs every hour in order to synchronize (if necessary) the spaces and categories contained in the offer catalog from the design environment to the live environment.

デザイン環境で利用可能なオファーのダッシュボードには、ライブ環境の対応するオファーの名前など、パブリッシュに関する情報が含まれます。

![](assets/offer_golive_001.png)

ライブ環境で利用可能なオファーを表示するには、オファーのラベルをクリックします。ライブオファーには、すべての関連情報を含むダッシュボードがあります。

![](assets/offer_golive_002.png)

## オファーの無効化 {#disabling-an-offer}

承認済みのオファーは無効化できます。

To do this, go to the dashboard for an online offer or an offer waiting to go online, then click **[!UICONTROL Disable offer]**.

You can also directly disable a category by going to the **[!UICONTROL Eligibility]** tab and checking the **[!UICONTROL Enabled]** box.

>[!NOTE]
>
>デザイン環境でオファーを削除すると、そのオファーは、リンクされたオンライン環境で自動的に無効化されます。提案の保持期間が過ぎると、無効化されているオファーはオンライン環境から削除されます。

![](assets/offer_preview_deactivate.png)

