---
product: campaign
title: ACS コネクタのトラブルシューティング
description: ACS コネクタのトラブルシューティング
feature: ACS Connector, Troubleshooting
audience: integrations
content-type: reference
topic-tags: acs-connector
hide: true
exl-id: 4693dca1-ee55-43f0-b3dc-62a5b67a8058
TQID: https://experienceleague.adobe.com/hqQ4rSZpOoCMn9sA0yu2VsHFxTGEnwGwOMi6cu6e-1Q
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
  - id: d5ef99fa-df0c-4153-bf94-105ad0724167
subfeature_v2:
  - id: cbcf4d90-26be-46e2-b16a-aebc529dc41e
  - id: df0d6518-6f49-46e2-b46e-3bcc513f553f
  - id: eb007b6d-6e57-46ab-9485-3f24d6102304
  - id: b1fd1501-3105-4d6b-b4d4-9af53126df75
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 901
ht-degree: 93%

---

# ACS コネクタのトラブルシューティング{#troubleshooting-the-acs-connector}



実装によっては、一般的な問題に直面する可能性があります。

* **Campaign Standard と Campaign v7 の UI には、どんな違いがありますか。**

  Campaign Standard と Campaign v7 は、非常に似た方法で動作します。 ほとんどの概念は同じですが、場合によっては、アプローチがわずかに異なる可能性があります。 以下の概念は、ACS コネクタのコンテキストでは異なる場合があります。

<table> 
 <thead> 
  <tr> 
   <th> Campaign v7<br /> </th> 
   <th> Campaign Standard<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> 受信者（またはその他のプロファイルディメンション）<br /> </td> 
   <td> プロファイル<br /> </td> 
  </tr> 
  <tr> 
   <td> リスト<br /> </td> 
   <td> オーディエンス<br /> </td> 
  </tr> 
  <tr> 
   <td> キャンペーンワークフロー、ターゲティングワークフロー<br /> </td> 
   <td> ワークフロー<br /> </td> 
  </tr> 
  <tr> 
   <td> 操作<br /> </td> 
   <td> キャンペーン<br /> </td> 
  </tr> 
  <tr> 
   <td> Web アプリケーション<br /> </td> 
   <td> ランディングページ<br /> </td> 
  </tr> 
  <tr> 
   <td> カスタムテーブルおよびスキーマ拡張<br /> </td> 
   <td> カスタムリソースおよびリソース拡張<br /> </td> 
  </tr> 
  <tr> 
   <td> シードメンバー<br /> </td> 
   <td> テストプロファイル<br /> </td> 
  </tr> 
 </tbody> 
</table>

* **Campaign v7 インスタンスの受信者が、Campaign Standard で同期されない、または表示されません。**

  この事例は、様々な理由で発生する可能性があります。

   * 受信者が Campaign v7 で作成されたばかり、または更新されたばかりである。 同期は、15 分ごとにトリガーされます。 つまり、更新または新しく作成された受信者は、次の同期後に Campaign Standard に表示されます。
   * 実装が、特定のフォルダーからの受信者のみを同期するように設定されている可能性がある。 他のフォルダーの受信者は同期されません。
   * 受信者は同期できるが、Campaign Standard で表示されない。 フォルダー権限のマッピングを確認します。

* **Campaign Standard でクエリのベースにする必要があるプロファイルフィールドが見つかりません。**

  デフォルトでは、nms:recipient テーブルの20 フィールドがCampaign Standardと同期されます。 同期されたフィールドの詳細なリストを参照してください。 Campaign Standard で取得する必要がある追加のフィールドは、コンサルタントによってマッピングおよび設定される必要があります。

  使用したいフィールドが利用可能であることを確認する場合は、**[!UICONTROL 管理／開発／診断／データスキーマ]**&#x200B;で、プロファイルリソース定義を確認できます。

  また、受信者に添付され、nms:recipientsに関連するテーブルに保存されているすべてのデータは、デフォルトではCampaign Standardに同期されません。

  関連するデータを使用できるようにするには、[オーディエンスの同期](../../integrations/using/synchronizing-audiences.md)の節で説明したように、Campaign v7 でターゲティングを実行して、追加データを追加するか、コンサルタントに問い合わせて、カスタマイズの可能性を探ることができます。

* **Campaign v7でデフォルトのnms:recipient以外のプロファイルディメンションを使用している。Campaign Standardと同期するにはどうすればよいですか？**

  Campaign Standard は、**プロファイル**&#x200B;という名前の独自のターゲティングリソースを使用します。 Campaign Standard 接続機能の基本的な実装では、Campaign v7 受信者と Campaign Standard プロファイルの間のデフォルトマッピングを提供します。

  Campaign v7 で別のプロファイルディメンションを使用する場合、またはいくつかのプロファイルディメンションを使用する場合、それらすべてが Campaign Standard プロファイルにマッピングされている必要があります。 この特定のニーズに対処するには、コンサルタントにお問い合わせください。

* **ワークフローを通じて Campaign Standard でプロファイルのリストを共有したいのですが、Campaign Standard でオーディエンスが見つかりません。**

  オーディエンスは、Campaign Standard の&#x200B;**[!UICONTROL オーディエンス]**&#x200B;メニューで見つけることができます。 Campaign v7 ワークフローの「**[!UICONTROL リストの更新]**」アクティビティで指定したラベルがあります。 それらは、実装時に定義されたフォルダーマッピングに依存します。

  最初に確認すべきことは、ワークフローがエラーなしで完了したかどうかです。 「**[!UICONTROL リストの更新]**」アクティビティにエラーがある場合、Campaign Standard との同期が失敗している可能性があります。 問題の詳細を確認するには、**[!UICONTROL 管理]**／**[!UICONTROL ACS コネクタ]**／**[!UICONTROL プロセス]**／**[!UICONTROL 診断]**&#x200B;に移動します。 このフォルダーには、「**[!UICONTROL リストの更新]**」アクティビティの実行でトリガーされる同期ワークフローが含まれています。

  また、「**[!UICONTROL リストの更新]**」アクティビティで「**[!UICONTROL ACS と共有]**」オプションがオンになっていることと、ワークフローが正しく実行されたことを確認します。

  リストに含まれる受信者プロファイルは、ワークフローの実行前に Campaign Standard と同期されている必要があります。 Campaign Standard と同期すると、リストの受信者は Campaign Standard プロファイルに紐付けされます。つまり、そこに存在する必要があります。 Campaign Standard のプロファイルと紐付けできないリストからの受信者は、無視されます。

  プロファイルから成るリストを共有する場合で、何も Campaign Standard と同期していない場合、使用できない空のクエリオーディエンスが Campaign Standard で作成されます。

* **同期ワークフローがエラー状態であることを示す通知を受け取りました。 どうすればよいですか。**

  接続をテストして、Campaign Standard と Campaign v7 の両方で外部アカウント設定を確認します。

   * Campaign Standard では **[!UICONTROL acsDefaultRelayAccount]**。
   * Campaign v7 では **[!UICONTROL acsDefaultAccount]**。

* **Campaign v7 と Campaign Standard の間でフォルダーをマッピングする際に使用可能なセキュリティグループがありません。**

  最初に、**[!UICONTROL 管理／ACS コネクタ／権限管理／セキュリティグループ]**&#x200B;で、セキュリティグループを同期する必要があります。 このアクションにより、Campaign Standard で使用可能なセキュリティグループを確認します。 同期すると、フォルダーマッピングを設定する際にセキュリティグループを検索できます。

* **Campaign Standard で、プロファイル、オーディエンスまたはランディングページキャンペーンを編集できません。 これはどういう意味ですか。**

  Campaign v7 から同期したリソースは、データ整合性を確保するために、Campaign Standard では読み取り専用モードになります。 これらの要素のいずれかを編集する必要がある場合は、Campaign v7 で編集してから Campaign Standard で変更をレプリケートできます。

* **[ACS] プロファイル配信ログのレプリケーションワークフローでエラーが発生します。 どうすればよいですか？**

  Campaign Classic インスタンスと Campaign Standard インスタンスの両方を使用してトラッキングされる URL でメールを送信する場合、同期中に URL tagIds の重複に関する問題が発生する可能性があります。 この場合、**[ACS] プロファイル配信ログのレプリケーション**（newRcpDeliveryLogReplication）ワークフローは、次のエラーで失敗します。

  `PGS-220000 PostgreSQL error: ERROR: duplicate key value violates unique constraint "nmstrackingurl_tagid" DETAIL: Key (stagid) = (1c7bdec2) already exists.`

  問題を解決し、再び発生しないようにするには、ワークフローの&#x200B;**トラッキング URL を更新**（writerTrackingUrls）アクティビティを更新し、@tagId ソース式に「ACS」接頭辞を追加します。
