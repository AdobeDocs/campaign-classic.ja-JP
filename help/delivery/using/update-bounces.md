---
product: campaign
title: ISP の機能停止後にバウンス認定条件を更新
description: ISP が機能停止した後にバウンスの認定条件を更新する方法を学ぶ
feature: Deliverability
hide: true
hidefromtoc: true
exl-id: 7a9afe0a-0219-40f1-9fe2-6374db8d555c
source-git-commit: 165797105affc9b5d4e4332f7f158031579bf91c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 37%

---

# ISP の停止後に誤ったハードバウンスを更新する {#update-bounces}

![](../../assets/common.svg)

## コンテキスト{#update-bounce-context}

ISP が機能停止した場合、Campaign 経由で送信された E メールは、受信者に正常に届きません。これらの E メールは、誤ってバウンスと見なされます。

Appleや Gmail のグローバルな問題などにより、有効なAppleや Gmail の電子メールアドレスに送信された一部の電子メールメッセージが、次の応答のバウンスを持つ ISP サーバーによって、誤って無効な電子メールアドレスとしてハードバウンスされる場合があります。

* &quot;550 5.1.1 &#39;メールアドレス&#39;:ユーザー参照が成功しましたが、ユーザーレコードが見つかりませんでした。」

* &quot;550 &#39;E メールアドレス&#39;受信者が却下されました&quot;

「452 requested action aborted」というメッセージが表示された遅延バウンスが中止された場合は、次の点に注意してください。後でもう一度試す」というメッセージが表示されます。これらは自動的に再試行され、アクションは不要です。 ISP が最大容量を回復するにつれて、改善する必要があります。

>[!NOTE]
>
>Apple System Status ダッシュボードは、 [このページ](https://www.apple.com/jp/support/systemstatus/){_blank}.
>
>Google Workspace ステータスダッシュボードは、 [このページ](https://www.google.com/appsstatus#hl=ja&amp;v=status){_blank}.

## 影響{#update-bounce-impact}

ISP が機能停止した場合、Campaign を通じて送信されたメールは、受信者に正常に届きません。これらのメールは誤ってバウンスと見なされます。

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この問題の影響を受けた受信者を見つけるには、以下の手順を参照してください。

## 更新処理{#update-bounce-update}

強制隔離テーブルに対してクエリを実行して、Apple、停止の影響を受けた可能性のあるアドレス（強制隔離リストから削除し、今後の Campaign E メール配信に含まれる）など、影響を受けたすべての受信者を除外する必要があります。

インシデントの時間枠と ISP に基づき、このクエリで推奨されるガイドラインを次に示します。

* インバウンド E メールルール情報が含まれる Campaign 環境の場合： **[!UICONTROL エラーテキスト]** 強制隔離リストのフィールド：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;に「Momen_Code10_InvalidRecipient」が含まれる
   * **E メールドメイン (@domain)** domain1.com と等しい **E メールドメイン (@domain)** domain2.com と等しい **E メールドメイン (@domain)** domain3.com と等しい
   * **ステータスを更新 (@lastModified)** MM/DD/YYYY HH 以降:MM:午前
   * **ステータスを更新 (@lastModified)** MM/DD/YYYY HH の前またはそれ以前:MM:午後 (SS)

* SMTP バウンス応答情報が **[!UICONTROL エラーテキスト]** 強制隔離リストのフィールド：

   * **エラーテキスト（強制隔離テキスト）** には、「550-5.1.1」およびが含まれます。 **エラーテキスト（強制隔離テキスト）** には、「support.ISP.com」が含まれます。

      ここで、「support.ISP.com」は次のようになります。例えば、「support.apple.com」または「support.google.com」と入力します。

   * **ステータスを更新 (@lastModified)** MM/DD/YYYY HH 以降:MM:午前
   * **ステータスを更新 (@lastModified)** MM/DD/YYYY HH の前またはそれ以前:MM:午後 (SS)


影響を受けた受信者のリストを取得したら、ステータスを&#x200B;**[!UICONTROL 有効]**&#x200B;に設定して&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローにより強制隔離リストから削除されるようにするか、テーブルからただ削除します。

**関連トピック：**
* [配信エラーについて](understanding-delivery-failures.md)
* [バウンスメールの認定](understanding-delivery-failures.md#bounce-mail-qualification)
