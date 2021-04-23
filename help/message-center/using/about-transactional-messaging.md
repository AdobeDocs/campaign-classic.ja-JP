---
solution: Campaign Classic
product: campaign
title: トランザクションメッセージについて
description: '情報システムから生成されたイベントに基づいて、トリガーメッセージを送信します。 '
audience: message-center
content-type: reference
topic-tags: introduction
exl-id: dc52e789-d0bf-4e8f-b448-9d69a2762cc1
translation-type: ht
source-git-commit: 6854d06f8dc445b56ddfde7777f02916a60f2b63
workflow-type: ht
source-wordcount: '171'
ht-degree: 100%

---

# トランザクションメッセージについて{#about-transactional-messaging}

トランザクションメッセージ（Message Center）は、トリガーメッセージを管理するために設計されたキャンペーンモジュールです。これらのメッセージは、情報システムからトリガーされたイベントから生成されます。例えば、請求書、オーダー確認、出荷確認、パスワード変更、製品入手不可通知、アカウントステートメント、Web サイトアカウント作成などのメッセージがあります。

>[!IMPORTANT]
>
>トランザクションメッセージを利用するには特定のライセンスが必要です。使用許諾契約書を確認してください。

Adobe Campaign Message Center モジュールは、情報システムに統合され、その情報システムが返すイベントをパーソナライズされたトランザクションメッセージへと変換します。これらのメッセージは、個々に、またはまとめて、E メール、SMS またはプッシュ通知経由で送信することができます。

この特定のアーキテクチャでは、実行セルがコントロールインスタンスから分離されています。これにより、高い可用性と優れた負荷管理が実現されます。

>[!NOTE]
>
>Adobe Cloud でホストされる Message Center 実行インスタンスの新しいユーザーを作成するには、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に連絡する必要があります。Message Center ユーザーは、「リアルタイムイベント」（nmsRtEvent）フォルダーにアクセスするための専用の権限を必要とする特定のオペレーターです。
