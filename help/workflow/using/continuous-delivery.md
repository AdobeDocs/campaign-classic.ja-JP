---
product: campaign
title: 連続配信
description: 連続配信
feature: Workflows, Channels Activity
hide: true
exl-id: 9c228cdb-331e-476e-a24c-3c7e23add3bf
TQID: https://experienceleague.adobe.com/ed2gcvqkoOttP8-f0EJlyxWZMc5J2VaZS5FIFo-a6jA
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: []
subfeature_v2: id: ee25c34b-ea50-427b-9369-ba0a160f7d70id: b5f0aaf4-1e48-400d-95ac-6eb3078cf22fid: d1110311-2ca4-442b-be37-088a6db845ee
source-git-commit: 38eab6b8da73163e4476e91c0ef73f25c3f57546
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 91%

---

# 連続配信{#continuous-delivery}



「**連続配信**」タイプアクションでは、既存の配信に新しい受信者を追加できます。 この配信タイプでは、毎回新しい配信を作成する必要がなくなります。このモードは、特に、容量不足のアラートや通知を必要に応じて送信する場合にはより効率的です。

![](assets/do-not-localize/how-to-video.png) [ビデオでこの機能を確認する](#continuous-delivery-video)

配信テンプレートレベルで、関連する配信のラベル（およびキャンペーンフォルダー）を計算するスクリプトを指定できます。 スクリプトがまだ存在しない配信を計算すると、その配信が計算中に作成されます。

![](assets/edit_diffusion_fil.png)

「**[!UICONTROL エラーを処理]**」オプションは、エラーが生成された場合に有効化される特定のトランジションを表示します。 この場合、ワークフローはエラーモードに入らず、実行は継続されます。

対象となるエラーは、ファイルシステムエラーです（ファイルを移動できない、ディレクトリにアクセスできない、など）。

このオプションは、無効な値など、アクティビティの設定に関するエラーは処理しません。

## 入力パラメーター {#input-parameters}

* tableName
* スキーマ

各インバウンドイベントは、これらのパラメーターによって定義されるターゲットを指定する必要があります。

「**[!UICONTROL インバウンドイベントで指定]**」オプションが選択されている場合のみ。

## 出力パラメーター {#output-parameters}

* tableName
* スキーマ
* recCount

この 3 つの値セットは、オンザフライ配信によって生成されたターゲットを識別します。 **[!UICONTROL tableName]**&#x200B;はターゲットの識別子を記憶するテーブルの名前で、**[!UICONTROL schema]**&#x200B;は母集団のスキーマ（通常はnms:recipient）で、**[!UICONTROL recCount]**&#x200B;はテーブル内の要素の数です。

補集合に関連付けられたトランジションは、同じパラメーターを持ちます。

## 連続配信の設定方法

この節では、連続配信を設定する方法について説明します。

**連続配信**&#x200B;では、既存の配信に新しい受信者を追加できるので、新しい受信者を追加するたびに新しい配信を作成する必要がありません。 クリエイティブはキャンペーンワークフローで直接更新でき、配信テンプレートのリソースフォルダー内のテンプレートが更新されます。

連続配信は、単一の配信と配信ログ（broadLog）を作成し、その配信を参照するトラッキングログは、実行のたびに 1 つ追加されます。

![連続配信](assets/delivery_continuous.jpg)

## チュートリアルビデオ {#continuous-delivery-video}

このビデオでは、増分処理クエリを使用して連続配信を設定する方法について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25039?quality=12)

Campaign Classic に関するその他のハウツービデオは[こちら](https://experienceleague.ad?lang=obe.com/docs/campaign-classic-learn/tutorials/overview.html?lang=ja)で参照できます。
