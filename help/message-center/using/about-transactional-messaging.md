---
solution: Campaign Classic
product: campaign
title: トランザクションメッセージについて
description: '情報システムから生成されたイベントに基づいて、トリガーメッセージを送信します。 '
audience: message-center
content-type: reference
topic-tags: introduction
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '164'
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
>Adobe Cloud でホストされる Message Center 実行インスタンスの新しいユーザーを作成するには、アドビカスタマーケアに連絡する必要があります。Message Center ユーザーは、「リアルタイムイベント」（nmsRtEvent）フォルダーにアクセスするための専用の権限を必要とする特定のオペレーターです。
