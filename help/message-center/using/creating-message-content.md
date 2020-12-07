---
solution: Campaign Classic
product: campaign
title: メッセージコンテンツの作成
description: メッセージコンテンツの作成
audience: message-center
content-type: reference
topic-tags: message-templates
translation-type: ht
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: ht
source-wordcount: '272'
ht-degree: 100%

---


# メッセージコンテンツの作成{#creating-message-content}

トランザクションメッセージコンテンツの定義は、Adobe Campaign の通常の配信と同様です。例えば、E メール配信では、HTML またはテキストフォーマットでコンテンツを作成したり、添付ファイルを追加したり、配信オブジェクトをパーソナライズすることができます。詳しくは、[E メールの配信](../../delivery/using/about-email-channel.md)の章を参照してください。

>[!IMPORTANT]
>
>メッセージに含まれる画像は、公的にアクセス可能でなければなりません。Adobe Campaign には、トランザクションメッセージ用の画像アップロードのメカニズムがありません。\
>JSSP や Web アプリとは異なり、`<%=` にはデフォルトのエスケープ機能がありません。
>
>こうした場合は、イベントから取得されるそれぞれのデータを適切にエスケープする必要があります。このエスケープ方法は、このフィールドの使用方法によって異なります。例えば、URL 内では、encodeURIComponent を使用します。HTML に表示する場合は、escapeXMLString を使用できます。

メッセージのコンテンツを定義したら、メッセージ本文にイベントの情報を取り入れ、パーソナライズすることができます。イベントの情報は、パーソナライゼーションタグを使用してテキスト本文に挿入します。

![](assets/messagecenter_create_content_001.png)

* すべてのパーソナライゼーションフィールドはペイロードから取得されます。
* トランザクションメッセージ内では、1 つまたは複数のパーソナライゼーションブロックを参照できます。ブロックコンテンツは、実行インスタンスへのパブリッシュ中に配信コンテンツに追加されます。

パーソナライゼーションタグを E メールメッセージの本文に挿入するには、次の手順に従います。

1. メッセージのテンプレートで、E メールのフォーマットに合うタブをクリックします（HTML またはテキスト）。
1. メッセージの本文を入力します。
1. テキスト本文に&#x200B;**[!UICONTROL リアルタイムイベント／イベント XML]** メニューを使用してタグを挿入します。

   ![](assets/messagecenter_create_custo_002.png)

1. 下記に示すように、タグの入力には次の構文を利用します。**要素名**.@**属性名**

   ![](assets/messagecenter_create_custo_003.png)

