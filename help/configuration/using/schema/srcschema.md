---
solution: Campaign Classic
product: campaign
title: 要素と属性
description: 要素と属性
audience: configuration
content-type: reference
topic-tags: schema-reference
translation-type: tm+mt
source-git-commit: 922257b157f8d76d6e703b0510ff689d1aa4d067
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---


# srcschema要素{#srcschema--element}

## コンテンツモデル{#content-model-14}

srcSchema:=(attribute) | createdBy | data |要素 |定義済みリスト |ヘルプ |インターフェイス |メソッド | modifiedBy)

## 属性 {#attributes-14}

created(datetime)、createdBy-id(long)、desc(string)、entitySchema(string)、extendedSchema(string)、implements(string)、label(string)、labelSingular(string)、library(boolean)、mappingType(string)、modifiedBy-id(long)、name(name(string)、名前空間(string)、useRecycleBin (boolean)、表示(boolean)、xtkschema (string)

## 親{#parents-14}

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

`<srcschema>`は、スキーマのルート要素です。 スキーマの定義の入力ポイントです。

## 使用と使用のコンテキスト{#use-and-context-of-use-9}

スキーマのプレゼンテーションは、[スキーマ参照](../../../configuration/using/about-schema-reference.md)と[スキーマ構造](../../../configuration/using/schema-structure.md)にあります。

## 属性の説明{#attribute-description-14}

* **作成日（日時）**:この属性は、スキーマの作成日時に関する情報を提供します。「日付時間」のフォームがあります。 表示される値は、サーバーから取得されます。 時刻はUTC形式で表示されます。
* **createdBy-id (long)**:は、スキーマを作成した演算子の識別子です。
* **desc（文字列）**:スキーマの説明
* **entitySchema (string)**:基本的な構文とAdobe Campaignが基になるスキーマ（デフォルトでは次の構文が使用されます）。xtk:srcSchema)。現在のスキーマを保存すると、Adobe Campaignは、@xtkschema属性で宣言されたスキーマを使用して、文法を承認します。
* **extendedSchema (string)**:は、現在のスキーマ拡張が基にしている、標準搭載されたスキーマの名前を受け取ります。フォームは「名前空間：名前」です。
* **img （文字列）**:アイコンがスキーマにリンクされている場合(スキーマ作成ウィザードで定義できます)。
* **label (string)**:スキーマラベル
* **labelSingular (string)**:label（単数形）は、インターフェイスで表示します。
* **lastModified (datetime)**:この属性は、最後の変更の日時に関する情報を提供します。「日付時間」のフォームがあります。 表示される値は、サーバーから取得されます。 時刻はUTC形式で表示されます。
* **library (boolean)**:スキーマをライブラリとして使用し、エンティティとしては使用しない。したがって、このスキーマは「@ref」および「@template」属性により、他のスキーマから参照される場合があります。
* **mappingType (string)**:

   * &quot;sql&quot;:データベースマッピング
   * &quot;textFile&quot;:テキストファイルマッピング
   * &quot;xmlFile&quot;:XML形式のテキストファイルマッピング
   * &quot;binaryFile&quot;:バイナリファイルマッピング

* **modifiedBy-id (long)**:は、スキーマを変更した演算子の識別子に一致します。
* **name（文字列）**:一意のスキーマ名。
* **名前空間（文字列）**:スキーマの名前空間(デフォルト：nms、xtk、nl)。プロジェクト用に新しいスキーマを作成する場合は、専用の名前空間を使用することをお勧めします。
* **useRecycleBin (boolean)**:アプリケーションのごみ箱機能をアクティブにします。削除したレコードは、最終的に削除される前にごみ箱に入れられます。 この関数は、「配信」モードでのみ使用できます。
* **表示（ブール値）**:アクティブ化された場合(@表示=&quot;true&quot;)、スキーマは表示として使用されます。データベース構造の更新ウィザードでは、スキーマは考慮されません。 このオプションは、主に外部テーブルを参照するために使用します。
* **xtkschema （文字列）**:スキーマ文法を定義するスキーマの名前（デフォルトではxtk:srcSchema）。

## 例 {#examples-11}

`<srcschema>` 要素内の「nms:配信」を追加スキーマ

```
<srcSchema desc="Defines all the settings of a delivery (or delivery template)."  
           entitySchema="xtk:srcSchema" img="nms:campaign.png" implements="xtk:persist" 
           label="Diffusions" labelSingular="Diffusion" md5="DCD2164CD0276B1DCA6E1C9E2A75EC04"
           name="delivery" namespace="nms" useRecycleBin="true" xtkschema="xtk:srcSchema">
```
