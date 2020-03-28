---
title: オーディエンスのインポートおよびエクスポート
seo-title: オーディエンスのインポートおよびエクスポート
description: オーディエンスのインポートおよびエクスポート
seo-description: null
page-status-flag: never-activated
uuid: af03ce68-8a58-4909-83e9-23c385820284
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: audience-sharing
discoiquuid: f26cc65a-76be-4b7a-bde3-d0cbe3eedaaf
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# オーディエンスのインポートおよびエクスポート{#importing-and-exporting-audiences}

## オーディエンスのインポート {#importing-an-audience}

受信者リストを使用して、Audience Manager または People コアサービスから Adobe Campaign にオーディエンスとセグメントをインポートできます。

1. Adobe Campaign のエクスプローラーで、**[!UICONTROL プロファイルとターゲット]**／**[!UICONTROL リスト]**&#x200B;ノードに移動します。
1. アクションバーで、 **[!UICONTROL 新規]**／**[!UICONTROL 共有オーディエンスを作成]**&#x200B;を選択します。

   ![](assets/aam_import_audience.png)

1. 表示されるウィンドウで、「**[!UICONTROL 共有オーディエンスを選択]**」をクリックして、他の Adobe Experience Cloud ソリューションから使用可能な共有オーディエンスおよびセグメントに移動します。
1. オーディエンスを選択し、確定します。オーディエンスの情報は自動的に追加されます。

   共有オーディエンスをインポートするには、Admin Console で&#x200B;**[!UICONTROL オーディエンスライブラリ]**&#x200B;製品を割り当てられた、Audience Manager の管理者である必要があります。詳しくは、[Admin Console のドキュメント](https://helpx.adobe.com/jp/enterprise/managing/user-guide.html)を参照してください。

   ![](assets/aam_import_audience_3.png)

1. 「**[!UICONTROL AMC データソース]**」フィールドから AMC データソースを選択し、予測されるデータタイプを定義します。

   ![](assets/aam_import_audience_2.png)

1. オーディエンスを保存します。

オーディエンスはテクニカルワークフローを使用してインポートされます。インポートされたリストには、AMC データソースを使用して紐付けできる要素が含まれています。Adobe Campaign が認識しない要素はインポートされません。

インポートプロセスで、People コアサービスまたは Audience Manager からセグメントを直接インポートする場合は、同期に 24～36 時間かかります。同期が終了すると、Adobe Campaign で新しいオーディエンスを検索したり、使用したりできます。

>[!NOTE]
>
>Adobe Analytics から Adobe Campaign にオーディエンスをインポートする場合は、最初に People コアサービスまたは Audience Manager でそれらのオーディエンスを共有する必要があります。このプロセスには 12～24 時間を要し、Campaign との同期にはさらに 24～36 時間が必要です。
>
>場合により、オーディエンスの共有プロセスは最大 60 時間に及ぶことがあります。People コアサービスと Audience Manager での Adobe Analytics オーディエンスの共有について詳しくは、この[ドキュメント](https://marketing.adobe.com/resources/help/ja_JP/mcloud/t_publish_audience_segment.html)を参照してください。

オーディエンスデータは、同期されるたびに完全に置き換えられます。インポートできるのはセグメントのみです。キーと値のペア、特徴、ルールなどの詳細データはサポートされません。

## オーディエンスのエクスポート {#exporting-an-audience}

ワークフローを使用して、Adobe Campaign から Audience Manager または People コアサービスにオーディエンスをエクスポートできます。ワークフローの作成と使用に関するプロセスについて詳しくは、[このドキュメント](../../workflow/using/building-a-workflow.md)を参照してください。エクスポートされたオーディエンスは、People コアサービスにセグメントとして保存されます。

1. 新しいターゲティングワークフローを作成します。
1. 使用可能な異なるアクティビティを使い、一連の受信者をターゲティングします。
1. ターゲティングした後、**[!UICONTROL 共有オーディエンスを更新]**&#x200B;アクティビティをドラッグ＆ドロップして開きます。

   ![](assets/aam_export_example.png)

1. 「**[!UICONTROL 共有オーディエンスを選択]**」オプションを使用して、エクスポートするオーディエンスを定義します。表示されるウィンドウで、既存オーディエンスを選択したり、新規オーディエンスを作成したりできます。

   既存オーディエンスを選択した場合、新規レコードだけがオーディエンスに追加されます。

   受信者リストを新規オーディエンスにエクスポートするには、「**[!UICONTROL セグメント名]**」フィールドを入力し、新しく作成されたオーディエンスを選択する前に「**[!UICONTROL 作成]**」をクリックします。

   ウィンドウの右上にあるチェックマークをクリックし、次に「**[!UICONTROL OK]**」ボタンをクリックして操作を終了します。

1. 予測されるデータタイプを指定するには、「**[!UICONTROL AMC データソース]**」を選択します。スキーマは自動的に決定されます。

   ![](assets/aam_export_audience_activity.png)

1. オーディエンスを保存します。

オーディエンスがエクスポートされます。オーディエンス保存アクティビティには、アウトバンドトランジションが 2 種類あります。主なトランジションは、エクスポートに成功した受信者を含みます。追加トランジションは、訪問者 ID または宣言済み ID でマッピングできなかった受信者を含みます。

Adobe Campaign と People コアサービス間の同期には、24～36 時間かかります。同期が終了すると、People コアサービスで新しいオーディエンスを検索できるようになり、そのオーディエンスを他の Adobe Experience Cloud ソリューションで再利用することができます。Adobe People コアサービスで Adobe Campaign の共有オーディエンスを使用する方法について詳しくは、この[ドキュメント](https://marketing.adobe.com/resources/help/ja_JP/mcloud/t_audience_create.html)を参照してください。

>[!NOTE]
>
>紐付けするには、レコードに Adobe Experience Cloud ID（「訪問者 ID」または「宣言済み ID」）が必要です。Adobe Experience Cloud ID がないレコードは、オーディエンスのエクスポートおよびインポート中に無視されます。

