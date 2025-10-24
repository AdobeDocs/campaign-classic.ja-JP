---
product: campaign
title: その他の設定
description: Adobe Campaign Classic でトランザクションメッセージ用の追加設定を行う方法を説明します
feature: Transactional Messaging, Message Center
audience: message-center
content-type: reference
topic-tags: instance-configuration
exl-id: 4d25d740-db57-4d18-8cae-2dd49c4a786e
source-git-commit: bba3f23637dd67a1557203c5ed1b93a6cb044870
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 91%

---

# その他の設定 {#mc-additional-configurations}



## しきい値の監視 {#monitoring-thresholds}

**Message Center のサービスレベル**&#x200B;と **Message Center の処理時間**&#x200B;のレポートに表示される指標について、警告しきい値（オレンジ）とアラートしきい値（赤）を設定できます。[トランザクションメッセージレポートへのアクセス](../../message-center/using/about-transactional-messaging-reports.md)を参照してください。

これを行うには、次の手順に従います。

1. **実行インスタンス**&#x200B;でデプロイウィザードを開きます。

1. **[!UICONTROL Message Center]** ページに移動します。

1. 矢印でしきい値を変更します。

   ![](assets/messagecenter_monitor_events_001.png)

>[!NOTE]
>
>キュー内の保留中のイベント数が、Adobe Campaign のプロセス監視ページの「[システム指標](../../production/using/monitoring-processes.md#system-indicators)」セクションに表示されます。デプロイウィザードについて詳しくは、[この節](../../installation/using/deploying-an-instance.md#deployment-assistant)を参照してください。

## イベントのパージ {#purging-events}

[デプロイメントウィザード](../../production/using/database-cleanup-workflow.md#deployment-assistant)を使用し、データをデータベース上に保存する期間を設定できます。

イベントのパージは、[データベースクリーンアップワークフロー](../../production/using/database-cleanup-workflow.md)によって自動的に実行されます。このワークフローは、実行インスタンスが受信し保存したイベントおよびコントロールインスタンスがアーカイブしたイベントをパージします。

矢印を使用し、必要に応じてパージの設定を変更します。

コントロールインスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_001.png)

実行インスタンスのイベントパージ設定：

![](assets/messagecenter_delete_events_002.png)

データベースのクリーンアップワークフローについて詳しくは、[この節](../../production/using/database-cleanup-workflow.md)を参照してください。


## テクニカルワークフロー {#technical-workflows}

トランザクションメッセージテンプレートをデプロイする前に、コントロールインスタンスおよびそれぞれの実行インスタンス上にてテクニカルワークフローが作成され、開始されていることを確認する必要があります。

トランザクションメッセージ（Message Center）に関連する様々なテクニカルワークフローは、コントロールインスタンスと実行インスタンスとに分類されます。

### コントロールインスタンスのワークフロー {#control-instance-workflows}

コントロールインスタンスで、登録されている実行インスタンスが 1 つか複数かにかかわらず、**[!UICONTROL Message Center の実行インスタンス]**&#x200B;外部アカウントごとに 1 つのアーカイブワークフローを作成する必要があります。「**[!UICONTROL アーカイブワークフローを作成]**」ボタンをクリックし、ワークフローを作成して開始します。

![](assets/messagecenter_archiving_002.png)

これらのワークフローは、**管理／プロダクション／Message Center** フォルダーからアクセスできます。アーカイブワークフローは作成されると自動的に開始されます。

<!--**Minimal architecture**

Once the control and execution modules are installed on the same instance, you must create the archiving workflow using the deployment wizard. Click the **[!UICONTROL Create the archiving workflow]** button to create and start the workflow.

![](assets/messagecenter_archiving_001.png)-->

### 実行インスタンスのワークフロー {#execution-instance-workflows}

実行インスタンスでは、**管理／プロダクション／Message Center** フォルダーからトランザクションメッセージのテクニカルワークフローにアクセスできます。必要な操作は、ワークフローを開始することだけです。リストに含まれるワークフローは以下のとおりです。

* **[!UICONTROL バッチイベントの処理]**（内部名：**[!UICONTROL batchEventsProcessing]**）：このワークフローは、メッセージテンプレートにリンクされる前にキュー内のバッチイベントを分類することができます。
* **[!UICONTROL リアルタイムイベントの処理]**（内部名：**[!UICONTROL rtEventsProcessing]**）：このワークフローは、メッセージテンプレートにリンクされる前にキュー内のリアルタイムイベントを分類することができます。
* **[!UICONTROL イベントステータスを更新]**（内部名：**[!UICONTROL updateEventStatus]**）：このワークフローは、ステータスをイベントに関連付けることができます。

  イベントステータスには以下のものがあります。

   * **[!UICONTROL 保留中]**：イベントはキューの中です。イベントにはまだメッセージテンプレートが割り当てられていません。
   * **[!UICONTROL 配信保留]**：イベントはキューの中で、メッセージテンプレートが割り当てられ、配信による処理中です。
   * **[!UICONTROL 送信済み]**：このステータスは配信ログからコピーされます。配信が送信されたことを示します。
   * **[!UICONTROL 配信で無視]**：このステータスは配信ログからコピーされます。配信が無視されたことを意味しています。
   * **[!UICONTROL 配信に失敗]**：このステータスは配信ログからコピーされます。配信が失敗したことを意味しています。
   * **[!UICONTROL 処理不可なイベント]**：イベントをメッセージテンプレートにリンクすることができませんでした。イベントの処理はおこなわれません。

### アーカイブワークフローのスケジュール

コントロールインスタンスで実行する&#x200B;**アーカイブワークフロー**&#x200B;のスケジュールの変更を回避します。そうしないと、実行インスタンスから取り込まれた一部のトラッキングデータが失われる可能性があります。

アーカイブワークフローのスケジュールを変更する場合は、コントロールインスタンスのアーカイブワークフローのスケジュールと一致するように、実行インスタンスの&#x200B;**トラッキングワークフロー**&#x200B;のスケジュールも変更する必要があります。

## マルチブランディングの設定 {#configuring-multibranding}

この節では、Adobe Campaign でのトランザクションメッセージのために、トラッキングとミラーページの URL をブランドごとに設定するソリューションの 1 つを説明します。

### 互換性に関する注意事項 {#compatibility-note}

この従来のブランディング設定は、Campaign v8 で導入された新しい [&#x200B; 一元管理されたブランディング &#x200B;](https://experienceleague.adobe.com/docs/campaign-web/v8/conf/branding/branding-gs.html){target="_blank"} モデルとは互換性がありません。

既存の環境でこのレガシー設定を使用している場合は、新しい一元化されたブランディングモデルに直接移行することはできません。 新しいシステムを採用するには、ブランディング設定の完全な再実装が必要です。

### 前提条件 {#prerequisites}

* すべてのホストをインスタンスの設定ファイル（`config-<instance>.xml`）に追加する必要があります。
* 各ブランドはそれぞれ 1 つのサブドメインに割り当てられていなければなりません。
* HTTPS ページで Web トラッキングをしている場合、すべてのブランドについて HTTPS 証明証を持っていなければなりません。

マルチブランディングを設定するには、実行インスタンスとコントロールインスタンスの両方を設定する必要があります。

### 実行インスタンス {#execution-instance}

実行インスタンスでは、次の手順に従います。

1. ブランドごとに 1 つの外部アカウントを作成します。

   >[!NOTE]
   >
   >実行インスタンスタイプの外部アカウントを作成する方法については、[この節](../../message-center/using/configuring-instances.md#control-instance)を参照してください。

1. nms:extAccount スキーマを拡張してトラッキング URL を追加します。

   ```
   <attribute advanced="true" desc="URL of the tracking servers" label="Tracking server URL"
   length="100" name="trackingURL" type="string"/>
   ```

   >[!NOTE]
   >
   >既存のスキーマを拡張する方法については、[スキーマの拡張](../../configuration/using/extending-a-schema.md)の節を参照してください。

1. nms:extAccount フォームを変更します。

   ```
   <container label="Message domain branding" type="frame">
        <static type="help"> These parameters are used to override the DNS alias and addresses used during message delivery. When not populated, the values of the 'NmsServer_MirrorPageUrl' and 'NmsEmail_DefaultErrorAddr' options are used.</static>
        <input xpath="@mirrorURL"/>
        <input xpath="@trackingURL"/>
        <input img="nms:sendemail.png" menuId="deliveryMenuBuilder" type="scriptEdit">
               xpath="errorAddress"/>
      </container>
   ```

1. NmsTracking_OpenFormula および NmsTracking_ClickFormula オプションを変更し、グローバルオプションの代わりに外部アカウントを使用するようにします。

   これには、

   ```
   <%@ include option='NmsTracking_ServerUrl' %>
   ```

   を以下で置き換えます。

   ```
   <%@ value object="provider" xpath="@trackingURL" %>
   ```

   >[!IMPORTANT]
   >
   >これらの変更は、アップグレードの際に競合を引き起こすことがあります。これらの数式と新しいバージョンの数式とを手動で統合させなければならない可能性があります。

### コントロールインスタンス {#control-instance}

コントロールインスタンスでは、配信テンプレートと外部アカウントをリンクします。

これを行うには、次の手順に従います。

1. [実行インスタンス](#execution-instance)で定義したもの（手順 1）と同じ内部名で、ブランドごとに 1 つの外部アカウントを作成します。

1. ブランドごとに配信テンプレートを作成します。 [Campaign v8 ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/campaign/campaign-v8/send/create-templates.html?lang=ja){target="_blank"} を参照してください。

1. 配信テンプレートの&#x200B;**[!UICONTROL プロパティ]**&#x200B;で、ブランドの外部アカウントへのルーティングを設定します。
