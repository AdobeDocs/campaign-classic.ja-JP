---
product: campaign
title: マーケティングキャンペーン配信
description: マーケティングキャンペーン配信の詳細
audience: campaign
content-type: reference
topic-tags: orchestrate-campaigns
exl-id: 1dd3c080-444d-45f8-9562-d2d01a9d2860
source-git-commit: 690f7c4e62203127da7a7055afa0ee8ad4a2bce4
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 100%

---

# マーケティングキャンペーン配信 {#marketing-campaign-deliveries}

配信は、キャンペーンダッシュボード、キャンペーンワークフローまたは配信の概要から直接作成できます。

キャンペーンから作成した配信は、このキャンペーンにリンクされ、キャンペーンレベルで統合されます。

![](assets/do-not-localize/how-to-video.png)[ 動画でこの機能を確認する](#create-email-video)

## 配信の作成 {#creating-deliveries}

キャンペーンにリンクされた配信を作成するには、キャンペーンダッシュボードの「**[!UICONTROL 配信を追加]**」リンクをクリックします。

![](assets/campaign_op_add_delivery.png)

各種の配信（ダイレクトメール、E メール、モバイルチャネル）に適した設定が提示されます。[詳細情報](../../delivery/using/steps-about-delivery-creation-steps.md)。

## 配信の開始 {#starting-a-delivery}

すべての承認が許可されたら、配信をいつでも開始できます。これ以降の配信手順は、配信の種類によって異なります。E メールまたはモバイルチャネルの配信については、[オンライン配信の開始](#starting-an-online-delivery)を、ダイレクトメール配信については、[オフライン配信の開始](#starting-an-offline-delivery)を参照してください。

### オンライン配信の開始 {#starting-an-online-delivery}

すべての承認リクエストが許可されたら、配信ステータスが「**[!UICONTROL 確認待ち]**」に変わり、オペレーターによって開始できるようになります。必要に応じて、配信を開始するレビュー担当者として割り当てられている Adobe Campaign オペレーター（またはオペレーターのグループ）に、配信をいつでも開始できることが通知されます。

>[!NOTE]
>
>配信のプロパティで、配信を開始するために特定のオペレーターまたはオペレーターのグループを指定している場合は、配信担当のオペレーターに送信の確認を許可することもできます。許可するには、**1** の値を入力することで、「**NMS_ActivateOwnerConfirmation**」オプションを有効化します。このオプションは、Adobe Campaign エクスプローラーの&#x200B;**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL オプション]**&#x200B;ノードから管理します。
>  
>このオプションを非アクティブ化するには、**0** の値を入力します。すると、送信確認プロセスがデフォルトとして機能します。つまり、配信プロパティで送信用に指定されたオペレーターまたはオペレーターのグループ（または管理者）のみが、送信を確認し、実行できるようになります。

![](assets/s_ncs_user_edit_del_to_start_from_del.png)

情報はキャンペーンダッシュボードにも表示されます。「**[!UICONTROL 配信を確定]**」リンクを使用して、配信を開始できます。

![](assets/s_ncs_user_edit_del_to_start.png)

確認メッセージが表示され、このアクションを確実に実行できます。

### オフライン配信の開始 {#starting-an-offline-delivery}

すべての承認が許可されたら、配信ステータスが「**[!UICONTROL 抽出を保留中]**」に変わります。抽出ファイルは特別なワークフローから作成されます。デフォルト設定では、このワークフローは、ダイレクトメール配信が抽出保留中の場合に自動的に開始されます。プロセスが進行中の場合、ダッシュボードに表示され、リンクから編集できます。

>[!NOTE]
>
>キャンペーンパッケージに関連するテクニカルワークフローは、[テクニカルワークフローのリスト](../../workflow/using/about-technical-workflows.md)を参照してください。

**手順 1 - ファイルの承認**

抽出ワークフローが正常に実行されたら、抽出ファイルを承認する必要があります（配信設定で抽出ファイルの承認が選択されている場合）。

詳しくは、[抽出ファイルの承認](../../campaign/using/marketing-campaign-approval.md#approving-an-extraction-file)を参照してください。

**手順 2 - サービスプロバイダーへのメッセージの承認**

* 抽出ファイルが承認されたら、発送担当への通知 E メールの配達確認を生成できます。この E メールメッセージは、配信テンプレートをベースとして構築されます。このメッセージは承認が必要です。

   >[!NOTE]
   >
   >この手順は、承認ウィンドウで配達確認の送信と検証が有効になっている場合にのみ使用できます。

![](assets/s_ncs_user_file_valid_select_BAT.png)


* 「**[!UICONTROL 配達確認を送信]**」ボタンをクリックして、配達確認を作成します。

   事前に配達確認のターゲットを定義しておく必要があります。

   配達確認を必要な数だけ作成できます。この配達確認には、配信の詳細の「**[!UICONTROL ダイレクトメール...]**」リンクからアクセスします。

   ![](assets/s_ncs_user_file_notif_submit_proof.png)

* 配信ステータスが「**[!UICONTROL 送信する]**」に変わります。「**[!UICONTROL 配達確認を送信]**」ボタンをクリックして、承認プロセスを開始します。

   ![](assets/s_ncs_user_file_notif_submit_proof_validation.png)

* 配信ステータスが「**[!UICONTROL 承認する配達確認]**」に変わります。ボタンを使用して承認を許可または却下できます。

   ![](assets/s_ncs_user_file_notif_supplier_link.png)

   この承認を許可／却下することも、抽出手順に戻ることもできます。

   ![](assets/s_ncs_user_file_notif_supplier_link_confirm.png)

* 抽出ファイルが発送担当に送信され、配信が完了します。

### コストと在庫の計算 {#calculation-of-costs-and-stocks}

ファイルを抽出すると、予算の計算と在庫の計算の 2 つの作業が開始されます。予算エントリが更新されます。

* 「**[!UICONTROL 予算]**」タブを使用して、キャンペーンの予算を管理できます。コストエントリの合計が、キャンペーンのメインタブおよびキャンペーンが所属するプログラムの「**[!UICONTROL 計算されたコスト]**」フィールドに表示されます。この金額は、キャンペーン予算にも反映されます。

   実際のコストは、発送担当が提供する情報から最終的に計算されます。実際に送信されたメッセージのみが請求対象です。

* 在庫はツリーの&#x200B;**[!UICONTROL 管理／キャンペーン管理／在庫]**&#x200B;ノードで定義され、コスト構造は&#x200B;**[!UICONTROL 管理／キャンペーン管理／サービスプロバイダー]**&#x200B;ノードで定義されます。

   在庫品目は「在庫」セクションに表示されます。初期在庫を定義するには、在庫品目を開きます。配信が実行されるたびに在庫は減少します。アラートレベルと通知を定義できます。

>[!NOTE]
>
>コスト計算と在庫管理について詳しくは、[プロバイダー、在庫、予算](../../campaign/using/providers--stocks-and-budgets.md)を参照してください。

## 関連付けられたドキュメントの管理 {#managing-associated-documents}

キャンペーンには、レポート、写真、web ページ、図などの様々なドキュメントを関連付けることができます。これらのドキュメントは、任意の形式（Microsoft Word、PowerPoint、PNG、JPG、Acrobat PDF など）にすることができます。ドキュメントをキャンペーンにリンクする方法については、](../../campaign/using/marketing-campaign-assets.md)こちらの節[を参照してください。

>[!IMPORTANT]
>
>このモードはサイズの小さいドキュメント専用です。

キャンペーン内で、プロモーション用のクーポンや、特定の支店または店舗に関連する特別オファーなど、他の項目を参照できます。これらの要素を概要に含めると、ダイレクトメール配信に関連付けることができます。[詳細情報](#associating-and-structuring-resources-linked-via-a-delivery-outline)。

>[!NOTE]
>
>MRM を使用している場合は、共同作業している複数の参加者が使用できるマーケティングリソースのライブラリも管理できます。[マーケティングリソースの管理](../../mrm/using/managing-marketing-resources.md)を参照してください。

### ドキュメントの追加 {#adding-documents}

ドキュメントは、キャンペーンレベル（コンテキストドキュメント）でもプログラムレベル（一般ドキュメント）でも関連付けることができます。

「**[!UICONTROL ドキュメント]**」タブには次が含まれます。

* 適切な権限を持つ Adobe Campaign オペレーターがローカルにダウンロードできる、コンテンツに必要なすべてのドキュメント（テンプレート、画像など）のリスト。
* 発送担当向けの情報を含むドキュメント（該当する場合）。

ドキュメントは、**[!UICONTROL 編集／「ドキュメント」]**&#x200B;タブからプログラムまたはキャンペーンにリンクされます。

![](assets/s_ncs_user_op_add_document.png)

キャンペーンダッシュボードに表示されるリンクからも、ドキュメントをキャンペーンに追加できます。

![](assets/add_a_document_in_op.png)

ファイルの内容を表示し、情報を追加するには、「**[!UICONTROL 詳細]**」アイコンをクリックします。

![](assets/s_ncs_user_op_add_document_details.png)

次の例に示すように、キャンペーンに関連付けられたドキュメントは、ダッシュボードの「**[!UICONTROL ドキュメント]**」セクションにまとめられます。

![](assets/s_ncs_user_op_edit_document.png)

このビューからドキュメントを編集および変更することもできます。

### 配信の概要からのリンク済みリソースの関連付けと構造化 {#associating-and-structuring-resources-linked-via-a-delivery-outline}

>[!NOTE]
>
>配信の概要は、ダイレクトメールキャンペーンのコンテキストでのみ使用します。

配信の概要は、企業内で特定のキャンペーン用に作成され、構造化された一連の要素（ドキュメント、支店／店舗、プロモーション用クーポンなど）を表します。

これらの要素は配信の概要にまとめられ、特定の配信の概要が配信に関連付けられます。この配信の概要は、配信に添付するために、**サービスプロバイダー**&#x200B;に送信される抽出ファイル内で参照されます。例えば、ある支店と、その支店が使用するマーケティングカタログを参照する配信の概要を作成できます。

キャンペーンでは、配信の概要を使用して、関連する支店、提供するプロモーションオファー、ローカルイベントへの招待など、特定の条件に応じて配信に関連付ける外部要素を構造化できます。

#### 概要の作成 {#creating-an-outline}

概要を作成するには、関連するキャンペーンの&#x200B;**[!UICONTROL 編集／「ドキュメント」]**&#x200B;タブで「**[!UICONTROL 配信の概要]**」サブタブをクリックします。

>[!NOTE]
>
>このタブが表示されていない場合、このキャンペーンではこの機能を使用できません。キャンペーンテンプレートの設定を参照してください。
>   
>詳しくは、[キャンペーンテンプレート](../../campaign/using/marketing-campaign-templates.md#campaign-templates)を参照してください。

![](assets/s_ncs_user_op_composition_link.png)

次に、「**[!UICONTROL 配信の概要を追加]**」をクリックし、次の手順でキャンペーンの概要の階層を作成します。

1. ツリーのルートを右クリックし、**[!UICONTROL 新規／配信の概要]**&#x200B;を選択します。
1. 作成した概要を右クリックし、**[!UICONTROL 新規／項目]**&#x200B;または&#x200B;**[!UICONTROL 新規／パーソナライゼーションフィールド]**&#x200B;を選択します。

![](assets/s_ncs_user_op_add_composition.png)

概要には、項目、パーソナライゼーションフィールド、リソースおよびオファーを含めることができます。

* 項目には、ここで参照および記述し、配信に添付する物理的なドキュメントなどを指定できます。
* パーソナライゼーションフィールドを使用して、受信者ではなく配信に関連したパーソナライゼーション要素を作成できます。これにより、特定のターゲット向けの配信（ウェルカムオファーやディスカウントなど）で使用する値を作成できます。こうした値は Adobe Campaign で作成し、「**[!UICONTROL パーソナライゼーションフィールドをインポート...]**」リンクから概要にインポートします。

   ![](assets/s_ncs_user_op_add_composition_field.png)

   パーソナライゼーション要素は、リスト領域の右側の&#x200B;**[!UICONTROL 追加]**&#x200B;アイコンをクリックして、概要内で直接作成することもできます。

   ![](assets/s_ncs_user_op_add_composition_field_button.png)

* リソースは、「**[!UICONTROL キャンペーン]** 」タブの「**[!UICONTROL リソース]**」リンクからアクセスできるマーケティングリソースダッシュボードで生成されたマーケティングリソースです。

   ![](assets/s_ncs_user_mkg_resource_ovv.png)

   >[!NOTE]
   >
   >マーケティングリソースについて詳しくは、[マーケティングリソースの管理](../../mrm/using/managing-marketing-resources.md)を参照してください。

#### 概要の選択 {#selecting-an-outline}

次の例に示すように、配信ごとに、抽出の概要専用のセクションから関連付ける概要を選択できます。

![](assets/s_ncs_user_op_select_composition.png)

選択された概要が、ウィンドウの下部セクションに表示されます。この概要は、フィールドの右側のアイコンを使用して編集したり、ドロップダウンリストを使用して変更したりできます。

![](assets/s_ncs_user_op_select_composition_b.png)

配信の「**[!UICONTROL 概要]**」タブにもこの情報が表示されます。

![](assets/s_ncs_user_op_select_composition_c.png)

#### 抽出結果 {#extraction-result}

抽出され、サービスプロバイダーに送信されたファイル内では、サービスプロバイダーに関連付けられたエクスポートテンプレートの情報に従って、概要名および必要に応じてその特性（コスト、説明など）がコンテンツに追加されます。

次の例では、配信に関連付けられた概要のラベル、推定コスト、説明が抽出ファイルに追加されます。

![](assets/s_ncs_user_op_composition_in_export_template.png)

エクスポートモデルは、該当する配信用に選択されたサービスプロバイダーに関連付ける必要があります。[サービスプロバイダーとそのコスト構造の作成](../../campaign/using/providers--stocks-and-budgets.md#creating-service-providers-and-their-cost-structures)を参照してください。

>[!NOTE]
>
>詳しくは、[はじめに](../../platform/using/get-started-data-import-export.md)の節を参照してください。

#### チュートリアルビデオ {#create-email-video}

このビデオでは、Adobe Campaign でキャンペーンと E メールを作成する方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25604?quality=12)

Campaign に関するその他のハウツービデオは[こちら](https://experienceleague.adobe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
