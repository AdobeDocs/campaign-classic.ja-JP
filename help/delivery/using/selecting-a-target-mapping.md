---
product: campaign
title: ターゲットマッピングの選択
description: ターゲットマッピングの方法を説明します
badge-v7: label="v7" type="Informative" tooltip="Campaign Classic v7 に適用されます"
badge-v8: label="v8" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Delivery Templates
role: User
exl-id: b5514fa3-1e65-45dc-8e40-d1ba3b673e7a
source-git-commit: abaeef25b03a9699a4851786380d467bfa299c9f
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 100%

---

# ターゲットマッピングの選択{#selecting-a-target-mapping}

配信テンプレートのデフォルトのターゲットは「**[!UICONTROL 受信者]**」です。したがって、ターゲットマッピングには **nms:recipient** テーブルのフィールドが使用されます。Adobe Campaign では、必要に応じて、これ以外のターゲットマッピングを配信に使用することもできます。

![](assets/delivery_select_mapping.png)

マッピングの選択肢は次のとおりです。

| 名前 | 用途 | 標準スキーマ |
|---|---|---|
| 受信者 | Adobe Campaign データベースの受信者に対する配信 | nms:recipient |
| 訪問者 | 訪問者、つまりリファラル（バイラルマーケティング）やソーシャルネットワーク（Facebook、X - 旧 Twitter）などの方法でプロファイルを収集した訪問者に配信します。 | mns:visitor |
| 購読 | ニュースレターなどの情報サービスを購読している受信者に対する配信 | nms:subscription |
| 訪問者の購読 | 情報サービスを購読している訪問者に対する配信 | nms:visitorSub |
| サービス | X アカウントや Facebook ページでの公開 | nms:service |
| オペレーター | Adobe Campaign オペレーターに対する配信 | nms:operator |
| 外部ファイル | 配信に必要な情報をすべて含んだファイルを経由しての配信 | リンクされるスキーマなし、入力されるターゲットなし |

>[!NOTE]
>
>新しいターゲットマッピングを作成することもできます。ただし、この操作はエキスパートユーザー向け機能として用意されています。詳しくは、[この節](../../configuration/using/target-mapping.md)を参照してください。
