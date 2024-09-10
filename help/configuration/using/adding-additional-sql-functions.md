---
product: campaign
title: SQL 関数の追加
description: 追加の SQL 関数を定義する方法を説明します
feature: Configuration, Instance Settings
role: Data Engineer, Developer
exl-id: 04b0a0e5-d6df-447c-ac67-66adb1bdf717
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# 追加の SQL 関数の定義{#adding-additional-sql-functions}

Adobe Campaignでは、SQL 関数にアクセスできる **独自の関数** を定義できます。この SQL 関数は、データベースで提供される関数と、まだコンソールで使用できない関数の両方です。 例えば、サーバー上でのみ計算できる集計関数（平均、最大、合計）や、コンソールに式を「手動」で書く（日付管理など）よりも、特定の関数をデータベースが簡単に実装できる場合に役立ちます。

この機能は、Adobe Campaign コンソールではまだ提供されていない、最新のまたは一般的でないデータベースエンジンの SQL 関数を使用する場合にも使用できます。

これらの関数を追加すると、他の事前定義済み関数と同様に、式エディターに表示されます。

>[!IMPORTANT]
>
>コンソール内の SQL 関数呼び出しは、サーバーに自然に送信されなくなりました。 したがって、ここで説明するメカニズムは、予定外の SQL 関数サーバーで **呼び出す唯一の方法** になります。

## インストール {#installation}

追加する関数は、次の段落で説明するように **XML 形式の** package」ファイルに含まれています。

コンソールからインストールするには、メニューから **ツール/詳細/読み込みパッケージ** オプションを選択し、次に **[!UICONTROL ファイルからインストール]** を選択して、読み込みアシスタントの指示に従います。

>[!IMPORTANT]
>
>警告：インポートされた関数のリストが関数エディタにすぐに表示されても、Adobe Campaignを再起動するまで使用できません。

## インポートするパッケージの一般的な構造 {#general-structure-of-package-to-import}

追加する関数は、XML 形式の **「パッケージ」ファイル** あります。 次に例を示します。

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

* **name**、**namespace** および **label** は情報提供のみを目的としています。 これにより、インストール済みパッケージのリスト（エクスプローラー/管理/パッケージ管理/インストール済みパッケージ）にパッケージの概要を表示できます。
* **buildVersion** および **buildNumber** フィールドは必須です。 これらは、コンソールが接続されているサーバー番号に対応している必要があります。 この情報は、「ヘルプ/バージョン情報」ボックスにあります。
* 次のブロック **entities** および **funclist** は必須です。 funcList では、「name」フィールドと「namespace」フィールドは必須ですが、ユーザーが決める名前が残っており、機能リストを一意に指定します。

  つまり、同じ名前空間と名前のペアを持つ関数の別のリスト（ここでは「cus::myList」）が読み込まれると、以前に読み込まれた関数は削除されます。 逆に、この名前空間と名前のペアを変更すると、新しいインポートされた一連の関数が前の関数に追加されます。

* **group** 要素を使用すると、インポートされた関数が関数エディタに表示される関数グループを指定できます。 @name 属性には、既に存在する名前（この場合、関数は考慮されるグループに追加されます）または新しい名前（この場合、新しいグループに表示されます）を指定できます。
* リマインダー：`<group>` 要素の@name 属性に指定可能な値は次のとおりです。

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
>@label 属性を完了してください。これは、使用可能な関数のリストに表示される名前です。 何も入力しない場合、グループには名前が付きません。 ただし、既存の名前以外の名前を入力すると、グループ全体の名前が変更されます。

複数の異なるグループに関数を追加する場合は、複数の `<group>` 要素を同じリスト内でトラッキングできます。

最後に、`<group>` 要素には、パッケージファイルの目的である 1 つまたは複数の関数の定義を含めることができます。 `<function>`   この要素について詳しくは、次の段落を参照してください。

## 関数記述子 &lt;function>&lt;/function> {#function-descriptor--function-}

ここに示す事例は、「関数の実装 **を提供したい一般的な事例** す。

以下に、「相対成熟度」関数の例を示します。この関数は、年齢を使用して、個人が成熟したと見なされた年数を示します。

```
 <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
              minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
       <providerPart provider="PostgreSQL" body="extract(year from age($1))-18"/>
       <providerPart provider="MSSQL,Sybase,Teradata" body="[Other implementation]"/>
    </function>
```

**@name** フィールドは関数の名前を指し、「args」は説明に表示されるパラメーターのリストです。 この場合、関数は関数選択ウィンドウに「relativeMaturity （`<age>`）」として表示されます。

* **help** は、式エディターウィンドウの下部に表示されるフィールドです。
* **@display** は、情報を提供するメッセージです。

  >[!NOTE]
  >
  >@help 属性と@display 属性では、文字列「$1」は、最初の関数パラメーターで指定された名前（ここでは「Age」）を表します。 $2、$3...は、次のパラメーターを表します。 以下で説明する@body 属性では、$1 は呼び出し時に関数に渡される引数値を指定します。

  >[!NOTE]
  >
  >説明は、有効な XML 文字の文字列である必要があります。&lt; と > ではなく、&#39;&lt;&#39;と&#39;>&#39;を使用してください。

* **@type** は関数の戻り値の型で、標準値（long、string、byte、datetime など）です。 省略した場合、サーバは関数を実装する式内で利用可能な型の中から最適な型を決定します。
* **@minArgs** and **maxArgs** は、パラメータのパラメータ数（最小値と最大値）を指定します。 例えば、2 つのパラメーターを持つ関数の場合、minArgs と maxArgs は 2 と 2 になります。 3 つのパラメーターに 1 つのオプションを加えた場合、それぞれ 3 と 4 になります。
* 最後に、**providerPart** 要素は関数の実装を提供します。

   * **provider** 属性は必須で、実装が提供されるデータベースシステムを指定します。 例に示すように、式の構文や基になる関数が異なる場合は、データベースに応じて代替実装を指定できます。
   * **@body** 属性には、関数の実装が含まれます。 注意：この実装は、（コードブロックではなく）データベース言語の式である必要があります。 データベースに応じて、式は、1 つの値のみを返すサブクエリ（「（select column from table where...）」など）にすることができます。 例えば、これはOracleの場合です（クエリは角括弧で記述する必要があります）。

  >[!NOTE]
  >
  >関数でクエリされるデータベースが 1 つか 2 つだけの場合は、常にこれらのデータベースに対応する定義のみを指定できます。

## 「パススルー」関数記述子 {#pass-through--function-descriptor}

特別な関数記述子は、未指定の「provider」データベースシステムを持つ **「パススルー」** ブロックです。 この場合、「body」実装には、使用されるデータベースに依存しない構文を持つ単一の関数呼び出しのみを含めることができます。 一方、「ProviderPart」ブロックは一意です。

```
    <function name="CountAll" args="()" help="Counts the values returned (all fields together)"
              type="long" minArgs="0" maxArgs="0">
      <providerPart body="Count(*)"/>
    </function>
```

この場合、関数の追加は、デフォルトでは使用できなかったデータベース関数をクライアントに表示するためにのみ機能します。

## 例 {#examples}

その他の関数の例については、定義済みのパッケージ「xtkdatakitfuncList.xml」を参照してください。
