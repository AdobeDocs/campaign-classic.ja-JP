---
product: campaign
title: 要素と属性 – srcschema 要素
description: 要素と属性
feature: Schema Extension
audience: configuration
content-type: reference
topic-tags: schema-reference
exl-id: bc4329b4-d272-4d32-bdaa-290cb9912af4
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# srcschema 要素 {#srcschema--element}

![](../../../assets/v7-only.svg)

## コンテンツモデル {#content-model-14}

srcSchema:==（attribute | createdBy | データ |要素 |列挙 | ヘルプ | インターフェイス | メソッド | modifiedBy）

## 属性 {#attributes-14}

created （datetime）、createdBy-id （long）、desc （string）、entitySchema （string）、extendedSchema （string）、img （string）、implements （string）、label （string）、labelSingular （string）、lastModified （datetime）、library （boolean）、mappingType （string）、modifiedBy-id （long）、name （string）、namespace （string）、useRecycleBin （boolean）、view （boolean）、xtkschema （string）

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

`<srcschema>` はスキーマのルート要素です。 これは、スキーマの定義の入力ポイントです。

## 用途および使用コンテキスト {#use-and-context-of-use-9}

スキーマの表示は、[ スキーマ参照について ](../../../configuration/using/about-schema-reference.md) および [ スキーマ構造 ](../../../configuration/using/schema-structure.md) で使用できます。

## 属性の説明 {#attribute-description-14}

* **created （datetime）**：この属性は、スキーマ作成の日時に関する情報を提供します。 「日時」フォームがあります。 表示される値は、サーバーから取得されます。 時間は UTC 形式で表示されます。
* **createdBy-id （long）**：スキーマを作成したオペレーターの識別子です。
* **desc （string）**: スキーマの説明
* **entitySchema （string）**：構文と承認の基になる基本スキーマ（Adobe Campaignの場合、デフォルトでは xtk:srcSchema）。 現在のスキーマを保存すると、Adobe Campaignは、@xtkschema 属性で宣言されたスキーマを使用して文法を承認します。
* **extendedSchema （string）**：現在のスキーマ拡張の基になっている標準スキーマの名前を受け取ります。 形式は「namespace:name」です。
* **img （文字列）**：スキーマにリンクされたアイコン（スキーマ作成アシスタントで定義できる場合があります）。
* **label （文字列）**：スキーマラベル。
* **labelSingular （string）**: インターフェイスに表示するラベル（単数）。
* **lastModified （datetime）**：この属性は、最終変更日時に関する情報を提供します。 「日時」フォームがあります。 表示される値は、サーバーから取得されます。 時間は UTC 形式で表示されます。
* **library （ブール値）**：スキーマをエンティティではなくライブラリとして使用します。 したがって、「@ref」属性と「@template」属性により、このスキーマは他のスキーマによって参照される可能性があります。
* **mappingType （文字列）**:

   * 「sql」：データベースマッピング
   * 「textFile」：テキストファイルのマッピング
   * 「xmlFile」:XML 形式テキストファイルのマッピング
   * &quot;binaryFile&quot;：バイナリファイルマッピング

* **modifiedBy-id （long）**：スキーマを変更したオペレーターの識別子に一致します。
* **name （string）**：一意のスキーマ名。
* **namespace （string）**：スキーマの名前空間（デフォルト：nms、xtk、nl）。 プロジェクトの新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin （boolean）**：アプリケーション内のごみ箱機能をアクティブにします。 削除されたレコードは、最終的に削除される前にごみ箱に配置されます。 この関数は、「配信」モードでのみ使用できます。
* **ビュー（ブール値）**：アクティブ化された場合（@view=&quot;true&quot;）、スキーマはビューとして使用されます。 データベース構造更新ウィザードでは、スキーマは考慮されません。 このオプションは、主に外部テーブルを参照するために使用されます。
* **xtkschema （string）**：スキーマ文法を定義するスキーマの名前（デフォルトでは xtk:srcSchema）。

## 例 {#examples-11}

標準スキーマの「nms:delivery」の `<srcschema>` 要素

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```
