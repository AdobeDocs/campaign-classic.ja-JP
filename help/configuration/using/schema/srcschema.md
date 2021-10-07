---
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bc4329b4-d272-4d32-bdaa-290cb9912af4
source-git-commit: 34404fbe935e68f3cc11d937839209443ad4ca60
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---

# srcschema 要素 {#srcschema--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-14}

srcSchema:==(attribute | createdBy | data |要素 |列挙 |ヘルプ |インターフェイス |メソッド | modifiedBy)

## 属性 {#attributes-14}

created (datetime), createdBy-id (long), desc (string), entitySchema (string), extendedSchema (string), img (string), implements (string), label (string), lastModified (string), lastModified (datetime), libry (string), namespace)useRecycleBin（ブール値）、view（ブール値）、xtkschema（文字列）

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

`<srcschema>` は、スキーマのルート要素です。 これは、スキーマの定義の入力ポイントです。

## 使用と使用のコンテキスト {#use-and-context-of-use-9}

スキーマの表示方法は、[ スキーマ参照について ](../../../configuration/using/about-schema-reference.md) および [ スキーマ構造 ](../../../configuration/using/schema-structure.md) で参照できます。

## 属性の説明 {#attribute-description-14}

* **作成（日時）**:この属性は、スキーマの作成日時に関する情報を提供します。「日付時刻」のフォームがあります。 表示される値は、サーバーから取得されます。 時刻は UTC 形式で表示されます。
* **createdBy-id (long)**:は、スキーマを作成したオペレーターの識別子です。
* **desc （文字列）**:スキーマの説明
* **entitySchema （文字列）**:構文と承認が基にする基本スキーマ (Adobe Campaignのデフォルトは：xtk:srcSchema) と同じです。現在のスキーマを保存すると、Adobe Campaignは@xtkschema属性で宣言されたスキーマを使用して文法を承認します。
* **extendedSchema (string)**:は、現在のスキーマ拡張の基になっている標準のスキーマの名前を受け取ります。フォームは「namespace:name」です。
* **img （文字列）**:スキーマにリンクされたアイコン（スキーマ作成ウィザードで定義できます）
* **label （文字列）**:スキーマラベル。
* **labelSingular（文字列）**:インターフェイスに表示するラベル（単数形）。
* **lastModified (datetime)**:この属性は、最後の変更の日時に関する情報を提供します。「日付時刻」のフォームがあります。 表示される値は、サーバーから取得されます。 時刻は UTC 形式で表示されます。
* **ライブラリ（ブール値）**:エンティティではなく、ライブラリとしてのスキーマの使用。したがって、このスキーマは、「@ref」属性と「@template」属性を使用して、他のスキーマから参照できます。
* **mappingType (string)**:

   * &quot;sql&quot;:データベースマッピング
   * &quot;textFile&quot;:テキストファイルマッピング
   * &quot;xmlFile&quot;:XML 形式のテキストファイルのマッピング
   * &quot;binaryFile&quot;:バイナリファイルマッピング

* **modifiedBy-id (long)**:は、スキーマを変更したオペレーターの識別子に一致します。
* **名前（文字列）**:一意のスキーマ名。
* **名前空間（文字列）**:スキーマの名前空間 ( デフォルト：nms、xtk、nl)。プロジェクト用に新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin（ブール値）**:アプリケーションのごみ箱機能をアクティブにします。削除されたレコードは、最終的に削除する前にごみ箱に入れられます。 この関数は、「配信」モードでのみ使用できます。
* **view (boolean)**:有効化された場合 (@view=&quot;true&quot;)、スキーマはビューとして使用されます。データベース構造の更新ウィザードでは、スキーマは考慮されません。 このオプションは主に外部テーブルの参照に使用されます。
* **xtkschema （文字列）**:スキーマの文法を定義するスキーマの名前（デフォルトは xtk:srcSchema）。

## 例 {#examples-11}

`<srcschema>` 標準スキーマの「nms:delivery」の要素

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```
