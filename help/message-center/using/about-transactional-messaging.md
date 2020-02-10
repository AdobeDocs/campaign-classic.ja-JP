---
title: トランザクションメッセージについて
seo-title: トランザクションメッセージについて
description: トランザクションメッセージについて
seo-description: null
page-status-flag: never-activated
uuid: c854daac-8756-44f3-a4e2-be31177ab9d1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: introduction
discoiquuid: 97df4bd5-a8e3-48f4-87c8-fa090ea3f771
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 833907c7a7b84b94a00b131738c73ff54a744a40

---


# トランザクションメッセージについて{#about-transactional-messaging}

トランザクションメッセージ（Message Center）は、トリガーメッセージを管理するために設計されたキャンペーンモジュールです。これらのメッセージは、情報システムからトリガーされたイベントから生成されます。例えば、請求書、オーダー確認、出荷確認、パスワード変更、製品入手不可通知、アカウントステートメント、Web サイトアカウント作成などのメッセージがあります。

>[!CAUTION]
>
>トランザクションメッセージングには特定のライセンスが必要です。 使用許諾契約書を確認してください。

Adobe Campaign Message Center モジュールは、情報システムに統合され、その情報システムが返すイベントをパーソナライズされたトランザクションメッセージへと変換します。これらのメッセージは、個々に、またはまとめて、E メール、SMS またはプッシュ通知経由で送信することができます。

この特定のアーキテクチャでは、実行セルがコントロールインスタンスから分離されています。これにより、高い可用性と優れた負荷管理が実現されます。

>[!NOTE]
>
>Adobe Cloud でホストされる Message Center 実行インスタンスの新しいユーザーを作成するには、アドビカスタマーケアに連絡する必要があります。Message Center ユーザーは、「リアルタイムイベント」（nmsRtEvent）フォルダーにアクセスするための専用の権限を必要とする特定のオペレーターです。
