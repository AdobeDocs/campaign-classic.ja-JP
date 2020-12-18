---
solution: Campaign Classic
product: campaign
title: SQL 関数の追加
description: SQL 関数の追加
audience: configuration
content-type: reference
topic-tags: api
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 1%

---


# SQL 関数の追加{#adding-additional-sql-functions}

## はじめに {#introduction}

Adobe Campaignでは、SQL関数にアクセスできる&#x200B;**独自の関数**&#x200B;を定義できます。この関数は、データベースから提供される関数と、コンソールにまだ存在しない関数の両方です。 これは、集計関数（平均、最大、合計）で役立ちます。例えば、サーバー上でのみ計算できる関数や、データベースが特定の関数をより簡単に実装でき、コンソールに式を「手動」で書き込む必要はありません（日付管理など）。

このメカニズムは、Adobe Campaign・コンソールではまだ提供されていない、最新または一般的でないデータベース・エンジンのSQL関数を使用する場合にも使用できます。

これらの関数を追加すると、あらかじめ定義された他の関数と同様に、式エディターに表示されます。

>[!IMPORTANT]
>
>コンソール内のSQL関数呼び出しが、サーバーに自動的に送信されることはなくなりました。 したがって、ここで説明するメカニズムは、計画外のSQLファンクションサーバで&#x200B;**を呼び出す唯一の方法になります。**

## インストール {#installation}

追加する関数は、XML形式&#x200B;**の**&quot;package&quot;ファイルに含まれています。このファイルの構造は、次の段落で詳しく説明します。

コンソールからインストールするには、メニューから「**ツール/詳細/パッケージをインポート**」オプションを選択し、**[!UICONTROL ファイルからインストール]**&#x200B;を選択して、インポートウィザードの指示に従います。

>[!IMPORTANT]
>
>警告：読み込まれた関数のリストが関数エディタにすぐに表示された場合でも、Adobe Campaignを再起動するまで使用できません。

## {#general-structure-of-package-to-import}をインポートするパッケージの一般的な構造

追加する関数は、**&quot;package&quot;ファイル**&#x200B;にXML形式で記載されています。 次に例を示します。

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

* **name**、**名前空間**、**label**&#x200B;は、情報の提供のみを目的としています。 インストール済みのパッケージリストー(Explorer/Administration/Package management/Installed packages)に、パッケージの概要を表示できます。
* **buildVersion**&#x200B;フィールドと&#x200B;**buildNumber**&#x200B;フィールドは必須です。 これらは、コンソールが接続されているサーバー番号に対応している必要があります。 この情報は、「ヘルプ/バージョン情報」ボックスにあります。
* 次のブロック&#x200B;**エンティティ**&#x200B;と&#x200B;**関数リスト**&#x200B;は必須です。 funcListでは、「name」と「名前空間」の各フィールドは必須ですが、名前はユーザーに任せられ、関数のリストを一意に指定します。

   つまり、同じ名前空間/名前のペアを持つ別のリストの関数（ここでは「cus::myList」）が読み込まれると、以前に読み込まれた関数は削除されます。 逆に、この名前空間と名前のペアを変更すると、読み込まれた新しい関数群が前の関数群に追加されます。

* **group**&#x200B;要素を使用すると、読み込んだ関数を関数エディターに表示する関数グループを指定できます。 @name属性は、既に存在する名前（この場合、関数は考慮するグループに追加されます）または新しい名前（この場合、新しいグループに表示されます）にすることができます。
* Reminder:`<group>`要素の@name属性に指定できる値は次のとおりです。

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
>@label属性を必ず完成させます。これは、使用可能な関数のリストに表示される名前です。 何も入力しないと、グループに名前は付きません。 ただし、既存の名前以外の名前を入力すると、グループ全体の名前が変更されます。

複数の異なるグループに関数を追加する場合は、同じリスト内で複数の`<group>`要素を追跡するように設定できます。

最後に、`<group>`要素には、パッケージファイルの目的である1つまたは複数の関数の定義を含めることができます。 `<function>`   の要素については、次の段落で説明します。

## 関数記述子&lt;関数>&lt;/関数> {#function-descriptor--function-}

ここで示す例は、**関数の実装**&#x200B;を提供したいと思う一般的な例です。

以下は、年齢を用いて、何年に達したと見なされたかを示す「相対的成熟度」関数の例である。

```
 <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
              minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
       <providerPart provider="PostgreSQL" body="extract(year from age($1))-18"/>
       <providerPart provider="MSSQL,Sybase,Teradata" body="[Other implementation]"/>
    </function>
```

**@name**&#x200B;フィールドは関数の名前を参照し、「args」は説明に表示されるパラメーターのリストです。 この場合、関数は関数選択ウィンドウに「relativeMaturity ( `<age>` )」と表示されます。

* **式エ** ディタウィンドウの下部に表示されるフィールドです。
* **@** displaysは情報メッセージです。

   >[!NOTE]
   >
   >@helpおよび@display属性では、文字列&quot;$1&quot;は、最初の関数パラメータ（ここでは&quot;Age&quot;）で指定された名前を表します。 $2, $3...は、次のパラメーターを表します。 以下に示す@body属性で、$1は呼び出し中に関数に渡す引数値を指定します。

   >[!NOTE]
   >
   >説明は、有効なXML文字の文字列である必要があります。&lt;と>の代わりに「&lt;」と「>」を使用することに注意してください。

* **@** typeは関数の戻り値の型で、標準値です(long、string、byte、datetime...)。この引数を省略すると、関数を実装する式内で使用可能な型の中で、最適な型がサーバによって決定されます。
* **@** minArgsand  **** maxArgsは、パラメータのパラメータ数（最小と最大）を指定します。例えば、2つのパラメーターを持つ関数の場合、minArgsとmaxArgsは2と2になります。 3つのパラメーターの場合、および1つのオプションの場合、それぞれ3と4になります。
* 最後に、**providerPart**&#x200B;要素が関数の実装を提供します。

   * **provider**&#x200B;属性は必須です。実装が提供されるデータベースシステムを指定します。 この例で示すように、式構文や基になる関数が異なる場合、データベースに従って別の実装を提供できます。
   * **@body**&#x200B;属性には、関数の実装が含まれます。 注意：この実装は、（コードのブロックではなく）データベース言語での式である必要があります。 データベースに応じて、式をサブクエリ(「（テーブルからの列を選択します。...」）」)にして、1つの値のみを返すことができます。 例えば、Oracleの場合は、クエリを角括弧で囲む必要があります。

   >[!NOTE]
   >
   >1つまたは2つのデータベースのみが、定義された関数によって照会される可能性がある場合、常にこれらのデータベースに対応する定義のみを指定できます。

## &#39;パススルー&#39;関数記述子{#pass-through--function-descriptor}

特殊な関数記述子は&#x200B;**&quot;パススルー&quot;**&#x200B;ブロックで、指定されていない&quot;provider&quot;データベースシステムを持ちます。 この場合、&quot;body&quot;実装には、使用するデータベースに依存しない構文を使用した1つの関数呼び出しのみを含めることができます。 一方、「ProviderPart」ブロックは一意です。

```
    <function name="CountAll" args="()" help="Counts the values returned (all fields together)"
              type="long" minArgs="0" maxArgs="0">
      <providerPart body="Count(*)"/>
    </function>
```

この場合、関数の追加は、デフォルトでは使用できなかったデータベース関数をクライアントに表示できるようにするためにのみ機能します。

## 例 {#examples}

その他の関数の例は、定義済みパッケージ「xtkdatakitfuncList.xml」にあります。
