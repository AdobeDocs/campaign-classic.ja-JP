---
product: campaign
title: SQL 関数の追加
description: 追加のSQL関数を定義する方法を説明します
feature: Configuration, Instance Settings
role: Developer
exl-id: 04b0a0e5-d6df-447c-ac67-66adb1bdf717
source-git-commit: 9f5205ced6b8d81639d4d0cb6a76905a753cddac
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---

# 追加のSQL関数の定義{#adding-additional-sql-functions}

Adobe Campaignでは、データベースが提供するSQL関数と、コンソールで使用できないSQL関数の両方にアクセスできる&#x200B;**独自の関数**&#x200B;を定義できます。 これは、集計関数（平均、最大、合計）で便利です。例えば、サーバーでのみ計算できる場合や、データベースが特定の関数を実装する簡単な方法を提供する場合にのみ、コンソールに式を「手動」で書き込む場合（日付管理など）には便利です。

このメカニズムは、Adobe Campaign コンソールがまだ提供していない最近のデータベース エンジン SQL関数または一般的でないデータベース エンジン SQL関数を使用する場合にも使用できます。

これらの関数を追加すると、他の定義済み関数と同様に、式エディターに表示されます。

>[!IMPORTANT]
>
>コンソール内のSQL関数呼び出しは、サーバーに自然に送信されなくなりました。 したがって、ここで説明するメカニズムは、計画外のSQL関数サーバーで&#x200B;**を呼び出す唯一の方法は**&#x200B;になります。

## インストール {#installation}

追加する関数は、XML形式&#x200B;**の** 「パッケージ」ファイルにあり、その構造は次の段落で詳しく説明されています。

コンソールからインストールするには、メニューから「**ツール/詳細/インポートパッケージ**」オプションを選択し、「**[!UICONTROL ファイルからインストール]**」を選択して、インポートアシスタントの指示に従います。

>[!IMPORTANT]
>
>警告：読み込まれた関数のリストが関数エディターにすぐに表示される場合でも、Adobe Campaignが再起動するまで使用できません。

## インポートするパッケージの一般的な構造 {#general-structure-of-package-to-import}

追加する関数は、XML形式の&#x200B;**「パッケージ」ファイル**&#x200B;にあります。 次に例を示します。

```
<?xml version="1.0" encoding='ISO-8859-1' ?>
<!-- ===========================================================================
  Additional SQL functions for Adobe Campaign
  ========================================================================== -->
<package
  namespace   = "nms"
  name        = "package-additional-funclist"
  label       = "Additional functions"
  buildVersion= "7.1"
  buildNumber = "10000">

  <entities schema="xtk:funcList">
    <funcList name="myList" namespace="cus">
      <group name="date" label="Personalized date">
        <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
                  minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
          <providerPart provider="MSSQL,Sybase,PostgreSQL" body="extract(year from age($1))-18"/>
        </function>
      </group>
    </funcList>
  </entities>
</package>
```

* **name**、**名前空間**&#x200B;および&#x200B;**ラベル**&#x200B;は、情報提供のみを目的としています。 インストールパッケージのリスト（エクスプローラー/管理/パッケージ管理/インストール済みパッケージ）にパッケージの概要を表示できます。
* **buildVersion**&#x200B;および&#x200B;**buildNumber** フィールドは必須です。 これらは、コンソールが接続されているサーバー番号に対応している必要があります。 この情報は、「ヘルプ/概要」ボックスにあります。
* 次のブロック、**entities**&#x200B;および&#x200B;**funclist**&#x200B;は必須です。 funcListでは、「name」フィールドと「namespace」フィールドは必須ですが、その名前はユーザーが決定し、関数リストを一意に指定します。

  つまり、同じ名前空間と名前のペアを持つ別の関数のリスト（ここでは「cus::myList」）が読み込まれた場合、以前に読み込まれた関数は削除されます。 逆に、この名前空間と名前のペアを変更すると、インポートされた新しい一連の関数が前の関数に追加されます。

* **group**&#x200B;要素を使用すると、読み込まれた関数が関数エディターに表示される関数グループを指定できます。 @name属性には、既に存在する名前（この場合、関数が考慮されるグループに追加されます）または新しい名前（この場合、新しいグループに表示されます）を指定できます。
* リマインダー：`<group>`要素の@name属性に使用できる値は次のとおりです。

  ```
    name="aggregate"      ( label="Aggregates"         )
    name="string"             ( label="String"           )
    name="date"               ( label="Date"             )
    name="numeric"          ( label="Numeric"        )
    name="geomarketing" ( label="Geomarketing"     )
    name="other"              ( label="Others"           )
    name="window"          ( label="Windowing functions" )
  ```

>[!IMPORTANT]
>
>必ず@label属性を完了してください。これは、使用可能な関数のリストに表示される名前です。 何も入力しない場合、グループには名前がありません。 ただし、既存の名前以外の名前を入力すると、グループ全体の名前が変更されます。

複数の異なるグループに関数を追加する場合は、同じリストで複数の`<group>`要素を追跡できます。

最後に、`<group>`要素には、1つまたは複数の関数の定義を含めることができます。これは、パッケージファイルの目的です。 `<function>`要素について詳しくは、次の段落を参照してください。

## 関数記述子&lt;function>&lt;/function> {#function-descriptor--function-}

ここに示すケースは、**関数実装**&#x200B;を提供する一般的なケースです。

以下は、年齢を使用して、その人が成熟したと見なされた何年を示す「相対的な成熟度」関数の例です。

```
 <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
              minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
       <providerPart provider="PostgreSQL" body="extract(year from age($1))-18"/>
       <providerPart provider="MSSQL,Sybase,Teradata" body="[Other implementation]"/>
    </function>
```

**@name** フィールドは関数の名前を表し、「args」は説明に表示されるパラメーターのリストです。 この場合、関数は関数選択ウィンドウに「relativeMaturity （`<age>`）」として表示されます。

* **help**&#x200B;は、式エディターウィンドウの下部に表示されるフィールドです。
* **@display**&#x200B;は有益なメッセージです。

  >[!NOTE]
  >
  >@helpおよび@display属性では、文字列「$1」は、最初の関数パラメーター（ここでは「Age」）で指定された名前を表します。 $2、$3...は次のパラメータを表します。 以下に説明する@body属性では、$1は呼び出し中に関数に渡される引数値を指定します。

  >[!NOTE]
  >
  >説明は、有効なXML文字の文字列である必要があります。&lt; and >の代わりに「&lt;」と「>」を使用してください。

* **@type**&#x200B;は関数の戻り値の型で、標準値（long、string、byte、datetime...）です。 省略すると、サーバーは、関数を実装する式の中で使用可能な型の中で最適な型を決定します。
* **@minArgs**&#x200B;および&#x200B;**maxArgs**&#x200B;は、パラメーターのパラメーター数（最小および最大）を指定します。 例えば、2つのパラメーターを持つ関数の場合、minArgsとmaxArgsは2と2になります。 3つのパラメータと1つのオプションの場合、それぞれ3と4になります。
* 最後に、**providerPart**&#x200B;要素が関数の実装を提供します。

   * **provider**&#x200B;属性は必須です。この属性は、実装が提供されるデータベース システムを指定します。 例に示すように、式の構文または基になる関数が異なる場合は、データベースに従って代替実装を提供できます。
   * **@body**&#x200B;属性には、関数の実装が含まれています。 注意：この実装は、データベース言語（コードブロックではなく）の式である必要があります。 データベースに応じて、式はサブクエリにすることができます（「（テーブルから列を選択します）」） 単一の値のみを返します。 例えば、これはOracleの場合です（クエリは角括弧で書く必要があります）。

  >[!NOTE]
  >
  >1つまたは2つのデータベースのみが定義された関数によってクエリされる可能性が高い場合は、常にこれらのデータベースに対応する定義のみを提供できます。

## &#39;Pass-through&#39;関数記述子 {#pass-through--function-descriptor}

特殊な関数記述子は、**&quot;pass-through&quot;** ブロックで、指定されていない&quot;provider&quot; データベースシステムを持ちます。 この場合、「body」実装には、使用されるデータベースに依存しない構文を持つ1つの関数呼び出しのみを含めることができます。 一方、「ProviderPart」ブロックは一意です。

```
    <function name="CountAll" args="()" help="Counts the values returned (all fields together)"
              type="long" minArgs="0" maxArgs="0">
      <providerPart body="Count(*)"/>
    </function>
```

この場合、関数を追加することは、デフォルトでは使用できなかったであろうデータベース関数を作成するためにのみ機能します。これは、クライアントに表示されます。

## 例 {#examples}

さらに関数の例は、定義済みのパッケージ「xtkdatakitfuncList.xml」にあります。
