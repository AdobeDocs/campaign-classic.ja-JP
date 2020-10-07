---
title: 連続配信
seo-title: 連続配信
description: 連続配信
seo-description: null
page-status-flag: never-activated
uuid: af8b4582-299e-47f9-9819-987b35db94ab
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: action-activities
discoiquuid: 9d80be19-8dde-4278-ab5f-23f364fe422e
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 100%

---


# 連続配信{#continuous-delivery}

「**連続配信**」タイプアクションでは、既存の配信に新しい受信者を追加できます。この配信タイプにより、毎回新しい配信を作成する必要がなくなります。このモードは、特に、容量不足のアラートや通知の送信が必要になった場合などに効率的です。配信テンプレートレベルで、関連する配信のラベル（およびキャンペーンフォルダー）を計算するスクリプトを指定できます。スクリプトがまだ存在しない配信を計算すると、その配信が計算中に作成されます。

![](assets/edit_diffusion_fil.png)

「**[!UICONTROL エラーを処理]**」オプションは、エラーが生成された場合に有効化される特定のトランジションを表示します。この場合、ワークフローはエラーモードに入らず、実行は継続されます。

対象となるエラーは、ファイルシステムエラーです（ファイルを移動できない、ディレクトリにアクセスできない、など）。

このオプションは、無効な値など、アクティビティの設定に関するエラーは処理しません。

## 入力パラメーター {#input-parameters}

* tableName
* schema

各インバウンドイベントは、これらのパラメーターによって定義されるターゲットを指定する必要があります。

「**[!UICONTROL インバウンドイベントで指定]**」オプションが選択されている場合のみ。

## 出力パラメーター {#output-parameters}

* tableName
* schema
* recCount

この 3 つの値セットは、オンザフライ配信によって生成されたターゲットを識別します。**[!UICONTROL tableName]** はターゲットの識別子を記憶するテーブル名、**[!UICONTROL schema]** は母集団のスキーマ（通常は nms:recipient）、**[!UICONTROL recCount]** はテーブル内の要素の数です。

補集合に関連付けられたトランジションは、同じパラメーターを持ちます。

## 連続配信の設定方法

この節では、連続配信を設定する方法について説明します。

**連続配信**&#x200B;では、既存の配信に新しい受信者を追加できるので、新しい受信者を追加するたびに新しい配信を作成する必要がありません。クリエイティブはキャンペーンワークフローで直接更新でき、配信テンプレートのリソースフォルダー内のテンプレートが更新されます。

連続配信は、単一の配信と配信ログ（broadLog）を作成し、その配信を参照するトラッキングログは、実行のたびに 1 つ追加されます。

![連続配信](assets/delivery_continuous.jpg)

このビデオでは、増分処理クエリを使用して連続配信を設定する方法について説明します。

>[!VIDEO](https://video.tv.adobe.com/v/25039?quality=12)
