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
translation-type: tm+mt
source-git-commit: ad7f0725a5ce1dea9b5b3ab236c839a816b29382
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 62%

---

# ISP 機能停止後のバウンス認定条件の更新 {#update-bounce-qualification.md}

## コンテキスト

ISP が機能停止した場合、Campaign 経由で送信された E メールは、受信者に正常に届きません。これらの E メールは、誤ってバウンスと見なされます。

2021年4月26日、Appleのグローバルな問題により、有効なAppleの電子メールアドレスに送信された一部の電子メールメッセージが、Appleのサーバーから無効な電子メールアドレスとして誤ってハードバウンスされ、次のバウンスが返されました。*&quot;550 5.1.1 <email address>:ユーザー参照に成功しましたが、ユーザーレコードが見つかりませんでした。」*この問題は2016年4月27日に発生し、継続は米国東部標準時の午前7時～午後1時です。

>[!NOTE]
>
>[このページ](https://www.apple.com/support/systemstatus/)でAppleのシステムステータスダッシュボードを確認できます。

Adobe Campaignは、標準のバウンス処理ロジックに従って、これらの受信者を強制隔離リストに自動的に追加し、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 強制隔離]**&#x200B;に設定しました。 この問題を修正するには、Campaign の強制隔離テーブルを更新する必要があります。それには、該当する受信者を特定して削除するか、**[!UICONTROL ステータス]**&#x200B;を&#x200B;**[!UICONTROL 有効]**&#x200B;に変更して、夜間のクリーンアップワークフローで削除する必要があります。

この の問題の影響を受けた受信者を特定する場合や、他の ISP で同じ状況が発生した場合は、以下の手順を参照してください。

## 更新処理

強制隔離テーブルでクエリを実行し、@icloud.com、@me.com、@mac.comなど、強制隔離リストから削除したり、今後のキャンペーンの電子メール配信に含まれる機能停止の影響を受けた可能性のあるすべてのApple受信者を除外する必要があります。

インシデントの期間に基づいて、このクエリの推奨ガイドラインを以下に示します。

>[!IMPORTANT]
>
>これらの日時は、米国東部標準時（EST）に基づいています。 お使いのインスタンスのタイムゾーンに合わせて調整してください。

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドに SMTP バウンス応答情報が含まれている Campaign インスタンスの場合：

   * **エラーテキスト(強制隔離テキスト)** に「ユーザー参照成功、ユーザーレコードが見つかりません」が **含まれ、AND** エラーテキスト(強制隔離テキスト)に「support.apple.com」が含まれています**
   * **更新ステータス（@lastModified）**&#x200B;が 2021 年 4 月 26 日午前 07 時 00 分以降
   * **更新ステータス(@lastModified)** が2021年4月26日01:00:00 PM以前に

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドにインバウンド E メールのルール情報が含まれている Campaign インスタンスの場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;に「Momen_Code10_InvalidRecipient」が含まれる
   * **電子メールドメイン(@domain)** がicloud.comに等しい、または電子メールドメイン(@domain)がme.comに等しい」または「電子メールドメイン(@domain)がmac.comに等しい」
   * **更新ステータス（@lastModified）**&#x200B;が 2021 年 4 月 26 日午前 07 時 00 分以降
   * **更新ステータス(@lastModified)** が2021年4月26日01:00:00 PM以前に

影響を受けた受信者のリストを取得したら、ステータスを&#x200B;**[!UICONTROL 有効]**&#x200B;に設定して&#x200B;**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローにより強制隔離リストから削除されるようにするか、テーブルからただ削除します。

**関連トピック：**
* [配信エラーについて](../../delivery/using/understanding-delivery-failures.md)
* [バウンスメールの認定](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)
