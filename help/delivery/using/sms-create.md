---
product: campaign
title: Campaign での SMS の作成
description: Campaign で SMS を作成する方法について説明します
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: SMS
role: User
exl-id: 94aa4628-d973-433d-b963-b078e2d6672b
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 100%

---

# SMS 配信の作成 {#creating-a-sms-delivery}

## 配信チャネルの選択 {#selecting-the-delivery-channel}

新しい SMS 配信を作成するには、次の手順に従います。

>[!NOTE]
>
>配信の作成に関するグローバルな概念については、[この節](steps-about-delivery-creation-steps.md)で説明しています。

1. 新しい配信を作成します（例えば、配信ダッシュボードから）。
1. 先ほど作成した配信テンプレート「**モバイルに送信済み（SMPP）**」を選択します。詳しくは、[配信テンプレートの変更](sms-set-up.md#changing-the-delivery-template)の節を参照してください。

   ![](assets/s_user_mobile_wizard.png)

1. ラベル、コードおよび説明を設定して配信を識別します。詳しくは、[この節](steps-create-and-identify-the-delivery.md#identifying-the-delivery)を参照してください。
1. 「**[!UICONTROL 続行]**」をクリックすると、入力した情報が確定され、メッセージ設定ウィンドウが表示されます。

## SMS コンテンツの定義 {#defining-the-sms-content}

SMS のコンテンツを作成するには、次の手順に従います。

1. ウィザードの「**[!UICONTROL テキストコンテンツ]**」セクションにメッセージのコンテンツを入力します。ツールバーのボタンで、コンテンツのインポート、保存、検索ができます。最後のボタンは、パーソナライゼーションフィールドを挿入するために使用します。

   ![](assets/s_ncs_user_wizard_sms01_138.png)

   パーソナライゼーションフィールドの使用方法について詳しくは、[パーソナライゼーションについて](about-personalization.md)の節で説明しています。

1. ページ下部の「**[!UICONTROL プレビュー]**」をクリックすると、メッセージにパーソナライゼーションを含めたレンダリング結果を表示して確認できます。プレビューを起動するには、ツールバーの&#x200B;**[!UICONTROL パーソナライゼーションをテスト]**&#x200B;ボタンで受信者を選択します。定義済みターゲットの中から受信者を選択することも、別の受信者を指定することもできます。

   ![](assets/s_ncs_user_wizard_sms01_139.png)

   SMS メッセージを承認したり、コンテンツエディターの右側に表示される携帯電話画面で SMS のコンテンツを表示したりできます。画面のクリックや、マウスによるコンテンツのスクロールが可能です。

   ![](assets/s_ncs_user_wizard_sms01_140.png)

1. 「**[!UICONTROL データ読み込み...]**」リンクをクリックすると、受信者に関する情報が表示されます。

   ![](assets/s_user_mobile_wizard_sms_02.png)

   >[!NOTE]
   >
   >SMS メッセージの文字数には制限があり、Latin-1（ISO-8859-1）コードページを使用する場合は 160 字以内です。メッセージが Unicode で作成されている場合、上限は 70 文字です。また、使用する文字によってメッセージの長さ制限が変化することがあります。メッセージの長さについて詳しくは、[SMS 文字の表記変更について](#about-character-transliteration)の節を参照してください。
   >
   >パーソナライゼーションフィールドまたは条件付きコンテンツが含まれる場合、メッセージのサイズは受信者によって異なります。メッセージの長さはパーソナライゼーションを適用した後の状態で評価する必要があります。
   >
   >分析を開始すると、メッセージの長さがチェックされ、制限を超える場合は警告が表示されます。

1. NetSize コネクタ、またはいずれかの SMPP コネクタを使用する場合は、配信の送信者名をパーソナライズできます。詳しくは、[詳細設定パラメーター](#advanced-parameters)の節を参照してください。

## ターゲット母集団の選択 {#selecting-the-target-population}

配信のターゲット母集団を選択する際の詳細なプロセスについては、[この節](steps-defining-the-target-population.md)を参照してください。

パーソナライゼーションフィールドの使用について詳しくは、[この節](about-personalization.md)を参照してください。

シードリストの追加については、[このページ](about-seed-addresses.md)を参照してください。
