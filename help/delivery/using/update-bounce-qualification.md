---
product: campaign
title: Apple 2021 の機能停止後にバウンス認定条件を更新
description: Apple 2021 の機能停止後にバウンス認定条件を更新する方法を学ぶ
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Deliverability
exl-id: 34be23f7-17fa-475e-9663-2e353d76b172
source-git-commit: d2f5f2a662c022e258fb3cc56c8502c4f4cb2849
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 92%

---

# Apple 停止後の誤ったハードバウンスの更新 {#update-bounce-qualification.md}

## コンテキスト

2021 年 4 月 26 日、Apple のグローバルな問題により、Apple の有効なメールアドレスに送信された一部のメールメッセージが、無効なメールアドレスとして Apple のサーバーから誤ってハードバウンスされ、「550 5.1.1 [メールアドレス]: user lookup success but no user record found.（ユーザー参照に成功しましたが、ユーザーレコードが見つかりませんでした）」というバウンス応答が返される障害が発生しました。

この問題は 4 月 26 日に発生し、米国東部標準時（EST）の午前 7 時から午後 1 時まで続きました。

>[!NOTE]
>
>[このページ](https://www.apple.com/jp/support/systemstatus/)で Apple システム状況ダッシュボードを確認できます。

ISP が機能停止した場合、Campaign を通じて送信されたメールは、受信者に正常に届きません。これらのメールは誤ってバウンスと見なされます。

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この問題の影響を受けた受信者を特定する場合や、他の ISP で同じ状況が発生する場合は、以下の手順を参照してください。

## 更新処理

強制隔離テーブルに対してクエリを実行して、機能停止の影響を受けた可能性のある Apple の受信者（@icloud.com、@me.com、@mac.com を含む）をすべて除外する必要があります。それにより、該当する受信者を強制隔離リストから削除し、Campaign による今後のメール配信の対象に含めることができるようになります。

インシデントの期間に基づいて、このクエリの推奨ガイドラインを以下に示します。

>[!IMPORTANT]
>
>これらの日時は、米国東部標準時（EST）に基づいています。 インスタンスのタイムゾーンに合わせて調整してください。

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドに SMTP バウンス応答情報が含まれている Campaign インスタンスの場合：

   * **エラーテキスト（強制隔離テキスト）** に「ユーザー検索成功が含まれるが、ユーザーレコードが見つかりません」という AND が含まれる **エラーテキスト（強制隔離テキスト）** 「support.apple.com」が含まれる
   * **更新ステータス（@lastModified）**&#x200B;が 2021 年 4 月 26 日午前 07:00:00 以降
   * **更新ステータス（@lastModified）**&#x200B;が 2021 年 4 月 26 日午後 01:00:00 以前

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドにインバウンド E メールのルール情報が含まれている Campaign インスタンスの場合：

   * **エラーテキスト（強制隔離テキスト）** に「Momen_Code10_InvalidRecipient」が含まれる
   * **メールドメイン（@domain）**&#x200B;が icloud.com と等しいか、または&#x200B;**メールドメイン（@domain）**&#x200B;が me.com と等しいか、または&#x200B;**メールドメイン（@domain）**&#x200B;が mac.com と等しい
   * **更新ステータス（@lastModified）**&#x200B;が 2021 年 4 月 26 日午前 07:00:00 以降
   * **更新ステータス（@lastModified）**&#x200B;が 2021 年 4 月 26 日午後 01:00:00 以前

影響を受けた受信者のリストを取得したら、ステータスを&#x200B;**[!UICONTROL 有効]**&#x200B;に設定して&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローにより強制隔離リストから削除されるようにするか、テーブルからただ削除します。

**関連トピック：**
* [配信エラーについて](understanding-delivery-failures.md)
* [バウンスメールの認定](understanding-delivery-failures.md#bounce-mail-qualification)
