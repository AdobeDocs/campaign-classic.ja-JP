---
solution: Campaign Classic
product: campaign
title: Adobe Campaign Classic のモバイルアプリチャネルについて
description: ここでは、Adobe Campaign Classic のモバイルアプリチャネルに関する一般情報を提供します。
audience: delivery
content-type: reference
topic-tags: sending-push-notifications
translation-type: tm+mt
source-git-commit: a9d58e25ab17baaabf4ff8c109b53e83c7d93218
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 98%

---


# モバイルアプリチャネルについて{#about-mobile-app-channel}

>[!CAUTION]
>
>このドキュメントは、モバイルアプリケーションを Adobe Campaign プラットフォームに統合するプロセスについて説明しています。モバイルアプリケーションの作成方法や、通知を管理するためのモバイルアプリケーションの設定方法については説明していません。詳しくは、Apple [ドキュメント](https://developer.apple.com/jp/)および Android [ドキュメント](https://developer.android.com/index.html)を参照してください。

以下の節で提供するのは、モバイルアプリチャネルに限定した情報です。

配信の作成方法に関する全般的な情報については、[この節](../../delivery/using/steps-about-delivery-creation-steps.md)を参照してください。

**モバイルアプリチャネル**&#x200B;では、Adobe Campaign プラットフォームを使用して iOS および Android の端末にパーソナライズされた通知をアプリ経由で送信できます。2 つの配信チャネルが使用可能です。

* Apple のモバイルデバイスへの通知の送信を有効にする iOS チャネル：

   ![](assets/nmac_intro_2.png)

* Android のモバイルデバイスへのデータメッセージの送信を有効にする Android チャネル。

   ![](assets/nmac_intro_1.png)

これら 2 つのチャネルに対応して、キャンペーンワークフローには 2 つの配信アクティビティがあります。

![](assets/nmac_intro_3.png)

>[!NOTE]
>
>また、トランザクションメッセージに使用できるトランザクションメッセージテンプレートも 2 つあります。

ユーザーがアプリケーションのコンテキストに一致する画面を表示するための通知を有効化した場合のアプリケーションの動作を定義することもできます。次に例を示します。

* 荷物が倉庫から出荷されたことを顧客に知らせるために通知を送信します。顧客が通知を有効にすると、配信関連の情報が記載されたページが開きます。
* ユーザーがカートに商品を追加したものの、購入を完了することなくアプリケーションを終了した場合、カートの内容が破棄されたことを知らせる通知を送信します。ユーザーが通知を有効化すると、画面にその商品が表示されます。

>[!CAUTION]
>
>* モバイルアプリケーションに送信する通知が、Apple（Apple プッシュ通知サービス）および Google（Firebase Cloud Messaging）によって指定されている前提条件や要件を満たしていることを確認する必要があります。
>* 警告：国によっては、モバイルアプリケーションから収集するデータタイプとその処理の目的についてユーザーに知らせることが法律によって定められている場合があります。法律を確認する必要があります。


**[!UICONTROL NMAC オプトアウト管理]**（mobileAppOptOutMgt）ワークフローにより、モバイルデバイスでの通知購読解除が更新されます。このワークフローの詳細については、[テクニカルワークフローのリスト](../../workflow/using/about-technical-workflows.md)を参照してください。

Adobe Campaign はバイナリと HTTP/2 APNs の両方に対応しています。設定手順の詳細については、[Adobe Campaign でのモバイルアプリケーションの設定](../../delivery/using/configuring-the-mobile-application.md)の節を参照してください。

## データパス {#data-path}

後述のスキーマでは、モバイルアプリケーションが Adobe Campaign とデータをやり取りできるようにするステップを説明しています。このプロセスには 3 つのエンティティが含まれます。

* モバイルアプリケーション
* 通知サービス：Apple 用の APNs（Apple Push Notification Service）と Android 用の FCM（Firebase Cloud Messaging）
* Adobe Campaign

通知プロセスの 3 つの主要なステップは、Adobe Campaign でのアプリケーションの登録（購読コレクション）、配信およびトラッキングです。

### 手順 1：購読コレクション {#step-1--subscription-collection}

モバイルアプリケーションが、App Store または Google Play からユーザーによってダウンロードされます。このアプリケーションには、接続設定（iOS 証明書および Android のプロジェクトキー）と統合キーが含まれます。アプリケーションを最初に開いた際に、（設定に応じて）ユーザーは登録情報（@userKey：例えば E メールやアカウント番号）を入力するように求められる場合があります。同時に、アプリケーションは通知サービスに対し、通知 ID（プッシュ ID）収集の問い合わせをおこないます。これらすべての情報（接続設定、統合キー、通知識別子、userKey）は、Adobe Campaign に送信されます。

![](assets/nmac_register_view.png)

### 手順 2：配信 {#step-2--delivery}

マーケティング担当者は、アプリケーションの利用者をターゲットにします。配信プロセスは、通知サービス（iOS 証明書および Android のプロジェクトキー）に対する接続設定、通知 ID（プッシュ ID）および通知の内容を送信します。通知サービスは、ターゲットとなる端末に通知を送信します。

次の情報が Adobe Campaign で使用可能です。

* Android のみ：通知を表示したデバイスの数（インプレッション数）
* Android および iOS：通知のクリック数

![](assets/nmac_delivery_view.png)

Adobe Campaign サーバーが、次のポートで APNs サーバーと通信できる必要があります。

* iOS バイナリコネクタの場合：2195（送信）および 2186（フィードバックサービス）
* iOS HTTP/2 コネクタの場合：443

   >[!NOTE]
   >
   > Campaign 20.3 リリース以降、iOS レガシーバイナリコネクタは非推奨となりました。このコネクタを使用する場合は、それに応じて実装を適応させる必要があります。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/migrate-to-apns-http2.html)

正しく動作することを確認するには、次のコマンドを使用します。

* テスト用：

   ```
   telnet gateway.sandbox.push.apple.com
   ```

* 本番：

   ```
   telnet gateway.push.apple.com
   ```

iOS バイナリコネクタを使用した場合、MTA および web サーバーはポート 2195（送信）で、ワークフローサーバーはポート 2196（フィードバックサービス）でそれぞれ APNs と通信できる必要があります。

iOS HTTP/2 コネクタを使用した場合、MTA、web サーバーおよびワークフローサーバーは、ポート 443 で APNs と通信できる必要があります。

