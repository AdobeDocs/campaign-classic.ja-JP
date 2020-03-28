---
title: ACS コネクタのトラブルシューティング
seo-title: ACS コネクタのトラブルシューティング
description: ACS コネクタのトラブルシューティング
seo-description: null
page-status-flag: never-activated
uuid: aef85b74-0388-44f8-b864-21db136a692c
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: acs-connector
discoiquuid: 538d3b48-ff39-463f-878d-ebe085057129
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 0745b9c9d72538b8573ad18ff4054ecf788905f2

---


# ACS コネクタのトラブルシューティング{#troubleshooting-the-acs-connector}

実装によっては、一般的な問題に直面する可能性があります。

* **Campaign Standard と Campaign v7 の UI には、どんな違いがありますか。**

   Campaign Standard と Campaign v7 は、非常に似た方法で動作します。ほとんどの概念は同じですが、場合によっては、アプローチがわずかに異なる可能性があります。以下の概念は、ACS コネクタのコンテキストでは異なる場合があります。

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

   * 受信者が Campaign v7 で作成されたばかり、または更新されたばかりである。同期は、15 分ごとにトリガーされます。つまり、更新または新しく作成された受信者は、次の同期後に Campaign Standard に表示されます。
   * 実装が、特定のフォルダーからの受信者のみを同期するように設定されている可能性がある。他のフォルダーの受信者は同期されません。
   * 受信者は同期できるが、Campaign Standard で表示されない。フォルダー権限のマッピングを確認します。

* **Campaign Standard でクエリのベースにする必要があるプロファイルフィールドが見つかりません。**

   デフォルトでは、nms:recipient テーブルからの 20 個のフィールドが Campaign Standard と同期されます。同期されたフィールドの詳細なリストを参照してください。Campaign Standard で取得する必要がある追加のフィールドは、コンサルタントによってマッピングおよび設定される必要があります。

   使用したいフィールドが利用可能であることを確認する場合は、**[!UICONTROL 管理／開発／診断／データスキーマ]**&#x200B;で、プロファイルリソース定義を確認できます。

   さらに、受信者に添付され、nms:recipient に関連するテーブルに格納されたすべてのデータは、デフォルトでは Campaign Standard に同期されません。

   関連するデータを使用できるようにするには、[オーディエンスの同期](../../integrations/using/synchronizing-audiences.md)の節で説明したように、Campaign v7 でターゲティングを実行して、追加データを追加するか、コンサルタントに問い合わせて、カスタマイズの可能性を探ることができます。

* **Campaign v7 で、デフォルトの nms:recipient ではなく、別のプロファイルディメンションを使用していますが、Campaign Standard と同期するにはどうしたらよいですか。**

   Campaign Standard は、**プロファイル**&#x200B;という名前の独自のターゲティングリソースを使用します。Campaign Standard 接続機能の基本的な実装では、Campaign v7 受信者と Campaign Standard プロファイルの間のデフォルトマッピングを提供します。

   Campaign v7 で別のプロファイルディメンションを使用する場合、またはいくつかのプロファイルディメンションを使用する場合、それらすべてが Campaign Standard プロファイルにマッピングされている必要があります。この特定のニーズに対処するには、コンサルタントにお問い合わせください。

* **ワークフローを通じて Campaign Standard でプロファイルのリストを共有したいのですが、Campaign Standard でオーディエンスが見つかりません。**

   オーディエンスは、Campaign Standard の&#x200B;**[!UICONTROL オーディエンス]**&#x200B;メニューで見つけることができます。Campaign v7 ワークフローの「**[!UICONTROL リストの更新]**」アクティビティで指定したラベルがあります。それらは、実装時に定義されたフォルダーマッピングに依存します。

   最初に確認すべきことは、ワークフローがエラーなしで完了したかどうかです。「**[!UICONTROL リストの更新]**」アクティビティにエラーがある場合、Campaign Standard との同期が失敗している可能性があります。問題の詳細を確認するには、**[!UICONTROL 管理]**／**[!UICONTROL ACS コネクタ]**／**[!UICONTROL プロセス]**／**[!UICONTROL 診断]**&#x200B;に移動します。このフォルダーには、「**[!UICONTROL リストの更新]**」アクティビティの実行でトリガーされる同期ワークフローが含まれています。

   また、「**[!UICONTROL リストの更新]**」アクティビティで「**[!UICONTROL ACS と共有]**」オプションがオンになっていることと、ワークフローが正しく実行されたことを確認します。

   リストに含まれる受信者プロファイルは、ワークフローの実行前に Campaign Standard と同期されている必要があります。Campaign Standard と同期すると、リストの受信者は Campaign Standard プロファイルに紐付けされます。つまり、そこに存在する必要があります。Campaign Standard のプロファイルと紐付けできないリストからの受信者は、無視されます。

   プロファイルから成るリストを共有する場合で、何も Campaign Standard と同期していない場合、使用できない空のクエリオーディエンスが Campaign Standard で作成されます。

* **同期ワークフローがエラー状態であることを示す通知を受け取りました。どうすればよいですか。**

   接続をテストして、Campaign Standard と Campaign v7 の両方で外部アカウント設定を確認します。

   * Campaign Standard では **[!UICONTROL acsDefaultRelayAccount]**。
   * Campaign v7 では **[!UICONTROL acsDefaultAccount]**。

* **Campaign v7 と Campaign Standard の間でフォルダーをマッピングする際に使用可能なセキュリティグループがありません。**

   最初に、**[!UICONTROL 管理／ACS コネクタ／権限管理／セキュリティグループ]**&#x200B;で、セキュリティグループを同期する必要があります。この操作により、Campaign Standard で使用可能なセキュリティグループを確認します。同期すると、フォルダーマッピングを設定する際にセキュリティグループを検索できます。

* **Campaign Standard で、プロファイル、オーディエンスまたはランディングページキャンペーンを編集できません。これはどういう意味ですか。**

   Campaign v7 から同期したリソースは、データ整合性を確保するために、Campaign Standard では読み取り専用モードになります。これらの要素のいずれかを編集する必要がある場合は、Campaign v7 で編集してから Campaign Standard で変更をレプリケートできます。

