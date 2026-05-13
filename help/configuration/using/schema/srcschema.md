---
product: campaign
title: 要素と属性 – srcschema要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bc4329b4-d272-4d32-bdaa-290cb9912af4
TQID: https://experienceleague.adobe.com/nUdM-iVzh7yI2Z3ZnFh5JK8FDZpmHAR1crzEb9S5xYg
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
subfeature_v2: id: a72a22e0-8c8d-4019-ba42-3f2644aa91a3id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 1%

---

# srcschema要素 {#srcschema--element}


## コンテンツモデル {#content-model-14}

srcSchema:==（attribute | createdBy | data | element | enumeration | help | interface | methods | modifiedBy）

## 属性 {#attributes-14}

created （datetime）, createdBy-id （long）, desc （string）, entitySchema （string）, extendedSchema （string）, img （string）, implements （string）, label （string）, labelSingular （string）, lastModified （datetime）, library （boolean）, mappingType （string）, modifiedBy-id （long）, name （string）, namespace （string）, useRecycleBin （boolean）, view （boolean）, xtkschema （string）

## 親 {#parents-14}

なし

## 子 {#children-14}

* `<attribute>`
* `<createdby>`
* `<data>`
* `<element>`
* `<enumeration>`
* `<help>`
* `<interface>`
* `<methods>`
* `<modifiedby>`

## 説明 {#description-14}

`<srcschema>`はスキーマのルート要素です。 スキーマの定義の入力ポイントです。

## 用途と使用状況 {#use-and-context-of-use-9}

スキーマのプレゼンテーションは、[ スキーマ参照](../../../configuration/using/about-schema-reference.md)および[ スキーマ構造](../../../configuration/using/schema-structure.md)で利用できます。

## 属性の説明 {#attribute-description-14}

* **created （datetime）**：この属性は、スキーマ作成の日時に関する情報を提供します。 「Date Time」フォームがあります。 表示される値はサーバーから取得されます。 時刻はUTC形式で表示されます。
* **createdBy-id （long）**：は、スキーマを作成した演算子の識別子です。
* **desc （文字列）**: スキーマの説明
* **entitySchema （文字列）**：構文と承認の基となる基本スキーマ （Adobe Campaignのデフォルトはxtk:srcSchema）。 現在のスキーマを保存すると、Adobe Campaignは@xtkschema属性で宣言されたスキーマで文法を承認します。
* **extendedSchema （文字列）**：現在のスキーマ拡張機能の基になっている、標準スキーマの名前を受け取ります。 フォームは「名前空間:name」です。
* **img （文字列）**: スキーマにリンクされたアイコン（スキーマ作成アシスタントで定義できます）。
* **label （文字列）**: スキーマラベル。
* **labelSingular （string）**: インターフェイスに表示するラベル （singular）。
* **lastModified （datetime）**：この属性は、最終変更の日時に関する情報を提供します。 「Date Time」フォームがあります。 表示される値はサーバーから取得されます。 時刻はUTC形式で表示されます。
* **ライブラリ （ブール値）**: スキーマをエンティティではなくライブラリとして使用します。 したがって、このスキーマは、「@ref」属性と「@template」属性のおかげで、他のスキーマで参照される可能性があります。
* **mappingType （文字列）**:

   * &quot;sql&quot;: データベースマッピング
   * &quot;textFile&quot;: テキストファイルマッピング
   * &quot;xmlFile&quot;: XML形式のテキストファイルマッピング
   * &quot;binaryFile&quot;: バイナリファイルマッピング

* **modifiedBy-id （long）**: スキーマを変更した演算子の識別子と一致します。
* **name （文字列）**：一意のスキーマ名。
* **名前空間（文字列）**: スキーマの名前空間（デフォルト：nms、xtk、nl）。 プロジェクトの新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin （ブール値）**: アプリケーション内のごみ箱の機能をアクティブにします。 削除されたレコードは、最終的な削除の前にゴミ箱に入れられます。 この機能は、「配信」モードでのみ使用できます。
* **ビュー（ブール値）**：アクティブ化されている場合（@view=&quot;true&quot;）、スキーマはビューとして使用されます。 データベース構造更新アシスタントは、スキーマを考慮しません。 このオプションは、主に外部テーブルの参照に使用されます。
* **xtkschema （string）**: スキーマ文法を定義するスキーマの名前（デフォルトではxtk:srcSchema）。

## 例 {#examples-11}

標準スキーマの「nms:delivery」の`<srcschema>`要素

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```
