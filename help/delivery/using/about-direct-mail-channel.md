---
product: campaign
title: ダイレクトメールチャネルについて
description: ダイレクトメールチャネルについて
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Direct Mail
role: User
exl-id: 6474cf2e-c4db-4430-b001-18bf4911b0ea
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 97%

---

# ダイレクトメールチャネルについて{#about-direct-mail-channel}


Adobe Campaign では、パーソナライズした文書を大量配送するためのファイルを作成できます。受信者のプロファイルには、少なくとも受信者の名前と郵送先住所が登録されている必要があります。

>[!NOTE]
>
>郵送先住所は、計算フィールドです。1 つのアドレスは、デフォルトで最大 6 つの行から構成されます。最初の行には名前の姓および名、続く数行には郵送先住所の番地など、最後の行には、郵便番号や市区町村が含まれます。デフォルトで計算済みの postalAddress フィールドの定義は、nms:recipient スキーマで確認できます。
>
>名前、郵便番号、市区町村フィールドが空でない場合、アドレスは完全に入力されているとみなされます。アドレスが不完全な受信者はダイレクトメールの配信から除外されます。

以下の節では、ダイレクトメールチャネルに関する情報を提供します。配信の作成および送信方法に関する全般的な情報については、[この節](steps-about-delivery-creation-steps.md)を参照してください。
