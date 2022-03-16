---
product: campaign
title: 要素と属性 — srcschema 要素
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bc4329b4-d272-4d32-bdaa-290cb9912af4
source-git-commit: 40da5774c8a6a228992c4aa400e2d9924215611e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# srcschema 要素 {#srcschema--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-14}

srcSchema:==(attribute | createdBy | data |要素 |列挙 |ヘルプ |インターフェイス |メソッド | modifiedBy)

## 属性 {#attributes-14}

created(datetime)、createdBy-id(long)、desc(string)、entitySchema(string)、extendedSchema(string)、img(string)、implements(string)、label(string)、labelSingular(string)、lastModified(string)、library(boolean)、mappingType(string)、modifiedBy-id(long)、name(string)、namespace(string)、stringuseRecycleBin(boolean)、view(boolean)、xtkschema(string)

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

この `<srcschema>` は、スキーマのルート要素です。 これは、スキーマの定義の入力ポイントです。

## 使用と使用のコンテキスト {#use-and-context-of-use-9}

スキーマの表示は、 [スキーマリファレンスについて](../../../configuration/using/about-schema-reference.md) および [スキーマ構造](../../../configuration/using/schema-structure.md).

## 属性の説明 {#attribute-description-14}

* **created (datetime)**:この属性は、スキーマの作成日時に関する情報を提供します。 「日時」の形式があります。 表示される値は、サーバーから取得されます。 時刻は UTC 形式で表示されます。
* **createdBy-id (long)**:は、スキーマを作成したオペレーターの識別子です。
* **desc （文字列）**:スキーマの説明
* **entitySchema （文字列）**:構文と承認が基づいている基本スキーマ (Adobe Campaignのデフォルトは：xtk:srcSchema) と同じです。 現在のスキーマを保存すると、Adobe Campaignは@xtkschema属性で宣言されたスキーマを使用して文法を承認します。
* **extendedSchema (string)**:は、現在のスキーマ拡張の基になっている標準のスキーマの名前を受け取ります。 フォームは「namespace:name」です。
* **img （文字列）**:スキーマにリンクされたアイコン（スキーマ作成ウィザードで定義する場合があります）。
* **label （文字列）**:スキーマラベル。
* **labelSingular （文字列）**:インターフェイスに表示するラベル（単数形）。
* **lastModified (datetime)**:この属性は、最後の変更の日時に関する情報を提供します。 「日時」の形式があります。 表示される値は、サーバーから取得されます。 時刻は UTC 形式で表示されます。
* **ライブラリ（ブール値）**:エンティティではなく、ライブラリとしてのスキーマの使用。 したがって、「@ref」および「@template」属性を使用して、このスキーマが他のスキーマから参照される場合があります。
* **mappingType (string)**:

   * &quot;sql&quot;:データベースマッピング
   * &quot;textFile&quot;:テキストファイルマッピング
   * &quot;xmlFile&quot;:XML 形式のテキストファイルマッピング
   * &quot;binaryFile&quot;:バイナリファイルマッピング

* **modifiedBy-id (long)**:は、スキーマを変更した演算子の識別子を照合します。
* **name（文字列）**:一意のスキーマ名。
* **namespace（文字列）**:スキーマの名前空間 ( デフォルト：nms、xtk、nl)。 プロジェクト用に新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin (boolean)**:アプリケーションのごみ箱機能をアクティブにします。 削除されたレコードは、最終的に削除される前にごみ箱に入れられます。 この関数は、「配信」モードでのみ使用できます。
* **表示（ブール値）**:有効化されている場合 (@view=&quot;true&quot;)、スキーマはビューとして使用されます。 データベース構造の更新ウィザードでは、スキーマは考慮されません。 このオプションは、主に外部テーブルを参照するために使用されます。
* **xtkschema （文字列）**:スキーマの文法を定義するスキーマの名前（デフォルトは xtk:srcSchema）。

## 例 {#examples-11}

`<srcschema>` 標準の「nms:delivery」スキーマの要素

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```
