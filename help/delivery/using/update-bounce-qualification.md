---
solution: Campaign Classic
product: campaign
title: ISP 機能停止後のバウンス認定条件の更新
description: ISP が機能停止した後にバウンスの認定条件を更新する方法を説明します。
audience: delivery
content-type: reference
topic-tags: monitoring-deliveries
hidefromtoc: true
exl-id: 34be23f7-17fa-475e-9663-2e353d76b172
translation-type: ht
source-git-commit: 3b5a6e6f03d9cb26ed372c3df069cbada36756a2
workflow-type: ht
source-wordcount: '486'
ht-degree: 100%

---

# ISP 機能停止後のバウンス認定条件の更新 {#update-bounce-qualification.md}

## コンテキスト

ISP が機能停止した場合、Campaign 経由で送信された E メールは、受信者に正常に届きません。これらの E メールは、誤ってバウンスと見なされます。

2020 年 12 月、Gmail の グローバルな問題により、Gmail の有効な E メールアドレスに送信された E メールメッセージの一部が、無効な E メールアドレスとして Gmail サーバーから誤ってハードバウンスされ、「*550-5.1.1 送信先の E メールアカウントは存在しません*」という応答が返されました。

Google は、この問題の原因となった Gmail の機能停止とサービス中断は米国東部標準時の 12 月 14 日午前 6 時 55 分に始まり、12 月 15 日午後 6 時 9 分に終了したと発表しています。 当社のデータ分析でも、米国東部標準時の 12 月 16 日の午前 2 時 6 分に Gmail のバウンスが瞬間的に急増しました。大部分は 12 月 15 日の午後 2 時から午後 6 時 30 分に発生しています。

>[!NOTE]
>
>[このページ](https://www.google.com/appsstatus#hl=ja&amp;v=status)で Google Workspace ステータスダッシュボードを確認できます。


Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この Gmail の問題の影響を受けた受信者を特定する場合や、他の ISP で同じ状況が発生した場合は、以下の手順を参照してください。

## 更新処理

強制隔離テーブルに対してクエリを実行して、機能停止の影響を受けた可能性のある Gmail（または他の ISP）の受信者をすべて除外する必要があります。それにより、該当する受信者を強制隔離リストから削除し、Campaign による今後の E メール配信の対象に含めることができるようになります。

インシデントの期間に基づいて、このクエリの推奨ガイドラインを以下に示します。

>[!IMPORTANT]
>
>これらの日時は、米国東部標準時（EST）に基づいています。 お使いのインスタンスのタイムゾーンに合わせて調整してください。

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドに SMTP バウンス応答情報が含まれている Campaign インスタンスの場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;に「550-5.1.1 The email account that you tried does not exist」が含まれ、かつ、**エラーテキスト（強制隔離テキスト）**&#x200B;に「support.google.com」が含まれる**
   * **更新ステータス（@lastModified）**&#x200B;が 2020 年 12 月 14 日午前 6 時 55 分以降
   * **更新ステータス（@lastModified）**&#x200B;が 2020 年 12 月 16 日午前 6 時 0 分以前

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドにインバウンド E メールのルール情報が含まれている Campaign インスタンスの場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;に「Momen_Code10_InvalidRecipient」が含まれる
   * **電子メールドメイン（@domain）**&#x200B;が「gmail.com」と等しい、または、電子メールドメイン（@domain）が「googlemail.com」と等しい
   * **更新ステータス（@lastModified）**&#x200B;が 2020 年 12 月 14 日午前 6 時 55 分以降
   * **更新ステータス（@lastModified）**&#x200B;が 2020 年 12 月 16 日午前 6 時 0 分以前

影響を受けた受信者のリストを取得したら、ステータスを&#x200B;**[!UICONTROL 有効]**&#x200B;に設定して&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローにより強制隔離リストから削除されるようにするか、テーブルからただ削除します。

**関連トピック：**
* [配信エラーについて](../../delivery/using/understanding-delivery-failures.md)
* [バウンスメールの認定](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)
