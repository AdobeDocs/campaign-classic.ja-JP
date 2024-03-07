---
product: campaign
title: ISP の機能停止後にバウンス認定条件を更新
description: ISP が機能停止した後にバウンスの認定条件を更新する方法を学ぶ
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Deliverability
hide: true
hidefromtoc: true
exl-id: 7a9afe0a-0219-40f1-9fe2-6374db8d555c
source-git-commit: 209ccbcac20052826dad0c55b35173be20b10114
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 88%

---

# ISP の機能停止後の誤ったハードバウンスの更新 {#update-bounces}



## コンテキスト{#update-bounce-context}

ISP が機能停止した場合、Campaign 経由で送信されたメールは、受信者に正常に届きません。これらのメールは、誤ってバウンスと見なされます。

例えば、Apple や Gmail でのグローバルな問題により、有効な Apple や Gmail のメールアドレスに送信された一部のメールメッセージが、ISP サーバーによって無効なメールアドレスとして誤ってハードバウンスされ、次の応答でバウンスされる可能性があります。

* 「550 5.1.1 &#39;メールアドレス&#39;: ユーザー検索は成功しましたが、ユーザーレコードが見つかりませんでした。」

* &quot;550 &#39;E メールアドレス&#39;受信者が却下されました&quot;

「452 requested action aborted: try again later」というメッセージを含む遅延バウンスが発生した場合は、自動的に再試行され、アクションは不要です。 ISP の処理能力が完全に回復すると、これらは改善されます。

>[!NOTE]
>
>[このページ](https://www.apple.com/jp/support/systemstatus/){_blank}で Apple システム状況ダッシュボードを確認できます。
>
>[このページ](https://www.google.com/appsstatus#hl=ja&amp;v=status){_blank}で Google Workspace ステータスダッシュボードを確認できます。
>

## 影響{#update-bounce-impact}

ISP が機能停止した場合、Campaign を通じて送信されたメールは、受信者に正常に届きません。これらのメールは誤ってバウンスと見なされます。

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この問題の影響を受けた受信者を見つけるには、以下の手順を参照してください。

## 更新処理{#update-bounce-update}

強制隔離テーブルに対してクエリを実行して、機能停止の影響を受けた可能性のあるすべての受信者（例えば、Apple の場合、@icloud.com、@me.com、@mac.com を含むアドレス）をすべて除外する必要があります。それにより、該当する受信者を強制隔離リストから削除し、Campaign による今後のメール配信の対象に含めることができるようになります。

インシデントの期間と ISP に基づいた、このクエリの推奨ガイドラインを以下に示します。

* 強制隔離リストの「**[!UICONTROL エラーテキスト]**」フィールドにインバウンドメールルール情報が含まれている Campaign 環境の場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;に「Momen_Code10_InvalidRecipient」が含まれる
   * **メールドメイン（@domain）**&#x200B;が domain1.com と等しい、または&#x200B;**メールドメイン（@domain）**&#x200B;が domain2.com と等しい、または&#x200B;**メールドメイン（@domain）**&#x200B;が domain3.com と等しい
   * **ステータスを更新 (@lastModified)** 以降 `MM/DD/YYYY HH:MM:SS AM`
   * **ステータスを更新 (@lastModified)** 以前 `MM/DD/YYYY HH:MM:SS PM`

* 強制隔離リストの「**[!UICONTROL エラーテキスト]**」フィールドに SMTP バウンス応答情報が含まれている Campaign 環境の場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;には、「550-5.1.1」が含まれ、かつ&#x200B;**エラーテキスト（強制隔離テキスト）**&#x200B;には、「support.ISP.com」が含まれている

     例えば、「support.ISP.com」は「support.apple.com」または「support.google.com」になります

   * **ステータスを更新 (@lastModified)** 以降 `MM/DD/YYYY HH:MM:SS AM`
   * **ステータスを更新 (@lastModified)** 以前  `MM/DD/YYYY HH:MM:SS PM`


影響を受けた受信者のリストを取得したら、ステータスを&#x200B;**[!UICONTROL 有効]**&#x200B;に設定して&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローにより強制隔離リストから削除されるようにするか、テーブルからただ削除します。

**関連トピック：**
* [配信エラーについて](understanding-delivery-failures.md)
* [バウンスメールの認定](understanding-delivery-failures.md#bounce-mail-qualification)
