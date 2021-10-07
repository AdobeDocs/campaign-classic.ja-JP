---
product: campaign
title: SQL 関数の追加
description: SQL 関数の追加
audience: configuration
content-type: reference
topic-tags: api
exl-id: 04b0a0e5-d6df-447c-ac67-66adb1bdf717
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---

# SQL 関数の追加{#adding-additional-sql-functions}

![](../../assets/v7-only.svg)

## はじめに {#introduction}

Adobe Campaignでは、SQL 関数にアクセスできる **独自の関数** を定義できます。この関数は、データベースで提供される関数と、コンソールでまだ使用できない関数の両方です。 これは、集計関数（平均、最大、合計）に便利です。例えば、サーバー上でのみ計算できる場合や、コンソールに式を「手動で」書き込む（日付管理など）よりも、データベースで特定の関数を実装する方が簡単な場合に便利です。

このメカニズムは、まだAdobe Campaignコンソールで提供されていない、最新または一般的でないデータベースエンジンの SQL 関数を使用する場合にも使用できます。

これらの関数が追加されると、他の事前定義された関数と同様に、式エディターに表示されます。

>[!IMPORTANT]
>
>コンソール内の SQL 関数呼び出しは、サーバーに自然に送信されなくなりました。 したがって、ここで説明するメカニズムは、予期しない SQL ファンクション・サーバで **を呼び出す唯一の方法になります。**

## インストール {#installation}

追加する関数は、XML 形式 **の**&quot;package&quot;ファイルに含まれます。このファイルの構造は、次の段落で詳しく説明します。

コンソールからインストールするには、メニューから「**ツール/詳細/パッケージをインポート**」オプションを選択し、「**[!UICONTROL ファイルからインストール]**」を選択して、インポートウィザードの指示に従います。

>[!IMPORTANT]
>
>警告：読み込んだ関数のリストがすぐに関数エディターに表示されても、Adobe Campaignを再起動するまで使用できません。

## インポートするパッケージの一般的な構造 {#general-structure-of-package-to-import}

追加する関数は、XML 形式の **&quot;package&quot;ファイル** にあります。 次に例を示します。

```
<?xml version="1.0" encoding='ISO-8859-1' ?>
<!-- ===========================================================================
  Additional SQL functions for Adobe Campaign
  ========================================================================== -->
<package
  namespace   = "nms"
  name        = "package-additional-funclist"
  label       = "Additional functions"
  buildVersion= "6.1"
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

* **name**、**namespace** および **label** は、情報提供のみを目的としています。 インストール済みパッケージのリストにパッケージの概要を表示できます（エクスプローラー/管理/パッケージ管理/インストール済みパッケージ）。
* **buildVersion** と **buildNumber** のフィールドは必須です。 これらは、コンソールが接続されているサーバー番号に対応している必要があります。 この情報は「ヘルプ/バージョン情報」ボックスにあります。
* 次のブロック **entities** と **funclist** は必須です。 funcList では、「name」と「namespace」の各フィールドは必須ですが、名前はユーザーが決定するものにし、関数リストを一意に指定します。

   つまり、同じ名前空間/名前のペア（ここでは「cus::myList」）を持つ関数の別のリストがインポートされると、以前にインポートされた関数は削除されます。 逆に、この名前空間と名前のペアを変更すると、新しい一連の読み込み関数が前の関数に追加されます。

* **group** 要素を使用して、読み込んだ関数を関数エディターに表示する関数グループを指定できます。 @name属性は、既に存在する名前（対象のグループに関数が追加される場合）か、新しい名前（新しいグループに表示される場合）のどちらかです。
* 注意：`<group>` 要素内の@name属性に指定できる値は次のとおりです。

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
>次の@label属性を必ず完了してください。これは、使用可能な関数のリストに表示される名前です。 何も入力しない場合、グループには名前が付きません。 ただし、既存の名前以外の名前を入力すると、グループ全体の名前が変更されます。

複数の異なるグループに関数を追加する場合は、同じリスト内で複数の `<group>` 要素を追跡することができます。

最後に、`<group>` 要素には、1 つ以上の関数の定義（パッケージファイルの目的）を含めることができます。 `<function>`   要素について詳しくは、次の段落で説明します。

## 関数記述子 &lt;function>&lt;/function> {#function-descriptor--function-}

ここで紹介するケースは、**関数実装** を提供したい一般的なケースです。

年齢を用いて、成年と見なされた年数を示す「相対成熟度」関数の例を以下に示します。

```
 <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
              minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
       <providerPart provider="PostgreSQL" body="extract(year from age($1))-18"/>
       <providerPart provider="MSSQL,Sybase,Teradata" body="[Other implementation]"/>
    </function>
```

**@name** フィールドは関数の名前を参照し、「args」は説明に表示されるパラメータのリストです。 この場合、関数は関数選択ウィンドウで「relativeMaturity ( `<age>` )」と表示されます。

* **** help は、式エディターウィンドウの下部に表示されるフィールドです。
* **@display は** 情報メッセージです。

   >[!NOTE]
   >
   >@help属性と@display属性の文字列&quot;$1&quot;は、最初の関数パラメータ（ここでは「Age」）で与えられた名前を表します。 $2、$3...は、次のパラメーターを表します。 以下に説明する@body属性では、呼び出し時に関数に渡す引数値を$1 で指定します。

   >[!NOTE]
   >
   >説明は、有効な XML 文字の文字列である必要があります。&lt; と > の代わりに「&lt;」と「>」が使用されていることに注意してください。

* **@type** は、関数の戻り値の型で、標準値（long、string、byte、datetime など）です。省略した場合、サーバーは関数を実装する式内で使用可能な型の中で最適な型を判断します。
* **@minArgsand maxArgs** は、パ **** ラメータのパラメータの数（最小値と最大値）を指定します。例えば、2 つのパラメータを持つ関数の場合、 minArgs と maxArgs は 2 と 2 です。 3 つのパラメーターの場合、+ 1 オプションの場合、それぞれ 3 と 4 です。
* 最後に、**providerPart** 要素が関数の実装を提供します。

   * **provider** 属性は必須で、実装に使用するデータベースシステムを指定します。 この例で示すように、式の構文や基礎となる関数が異なる場合は、データベースに応じて代替実装を提供できます。
   * **@body** 属性には、関数の実装が含まれます。 注意：この実装は、（コードのブロックではなく）データベース言語の式である必要があります。 データベースに応じて、式はサブクエリ (「（テーブルから選択列…）」) で、1 つの値のみを返すことができます。 例えば、Oracleの場合は次のようになります（クエリは角括弧で囲む必要があります）。

   >[!NOTE]
   >
   >定義した関数によってクエリが実行されるデータベースが 1 つまたは 2 つだけの場合、常にこれらのデータベースに対応する定義のみを提供できます。

## &#39;パススルー&#39;関数記述子 {#pass-through--function-descriptor}

特別な関数記述子は、「プロバイダ」データベースシステムが指定されていない **「パススルー」** ブロックです。 この場合、「body」実装には、使用するデータベースに依存しない構文を使用した 1 つの関数呼び出しのみを含めることができます。 一方、「ProviderPart」ブロックは一意です。

```
    <function name="CountAll" args="()" help="Counts the values returned (all fields together)"
              type="long" minArgs="0" maxArgs="0">
      <providerPart body="Count(*)"/>
    </function>
```

この場合、関数を追加すると、デフォルトでは使用できなかったデータベース機能がクライアントに表示されるようになります。

## 例 {#examples}

その他の関数の例は、事前定義済みパッケージ「xtkdatakitfuncList.xml」に記載されています。
