---
product: campaign
title: ターゲットマッピングの選択
description: ターゲットマッピングの方法を説明します
feature: Delivery Templates
hide: true
role: User
exl-id: b5514fa3-1e65-45dc-8e40-d1ba3b673e7a
TQID: https://experienceleague.adobe.com/VpmfQdFoJ2Lfzetqx-s5MAdFdTTEsHxz2ISL15wNXIo
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 178
ht-degree: 100%

---

# ターゲットマッピングの選択{#selecting-a-target-mapping}

配信テンプレートのデフォルトのターゲットは「**[!UICONTROL 受信者]**」です。 したがって、ターゲットマッピングには **nms:recipient:recipient** テーブルのフィールドが使用されます。 Adobe Campaign では、必要に応じて、これ以外のターゲットマッピングを配信に使用することもできます。

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
>新しいターゲットマッピングを作成することもできます。 ただし、この操作はエキスパートユーザー向け機能として用意されています。 詳しくは、[この節](../../configuration/using/target-mapping.md)を参照してください。
