---
title: SQL関数の追加
seo-title: SQL関数の追加
description: SQL関数の追加
seo-description: null
page-status-flag: never-activated
uuid: d66b5ca2-ac7d-4654-9f0e-9bfe56490c19
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: api
discoiquuid: 728a95f8-46fe-49a8-a645-a0dd6eeb6615
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: dbff132e3bf88c408838f91e50e4b047947ee32a

---


# SQL関数の追加{#adding-additional-sql-functions}

## はじめに {#introduction}

Adobe Campaignでは、ユーザーはSQL関数にアクセスでき **る独自の関数を定義できます** 。この関数は、データベースから提供される関数と、コンソールでまだ使用できない関数の両方です。 これは、集計関数（平均、最大、合計）で役立ちます。例えば、サーバー上でのみ計算できる場合や、データベースで特定の関数を実装する方法が提供される場合に、コンソールに式を「手動」で書く（日付管理など）必要はありません。

このメカニズムは、Adobe Campaignコンソールではまだ提供されていない、最新のまたは一般的でないデータベースエンジンのSQL関数を使用する場合にも使用できます。

これらの関数が追加されると、その他の定義済み関数と同様に、式エディターに表示されます。

>[!IMPORTANT]
>
>コンソール内のSQL関数呼び出しが、自動的にサーバーに送信されることはなくなりました。 したがって、ここで説明するメカニズムは、 **予期しないSQLファンクション** ・サーバを呼び出す唯一の方法となります。

## インストール {#installation}

追加する関数は、XML形式の「パッケー **ジ」ファイルです**。このファイルの構造は次の段落で詳しく説明します。

コンソールからインストールするには、メニューから **Tools/Advanced/Import package** （ツール）オプションを選択し、次に **[!UICONTROL Install from file]** 、インポートウィザードの指示に従います。

>[!IMPORTANT]
>
>警告：読み込んだ関数のリストが関数エディターにすぐに表示されても、Adobe Campaignを再起動するまで使用できません。

## 読み込むパッケージの一般的な構造 {#general-structure-of-package-to-import}

追加する関数は、XML形式の「パッケージ」フ **ァイルにあります** 。 次に例を示します。

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

* 名前 **、名**&#x200B;前空間 **** 、ラ **ベルは** 情報を提供する目的でのみ使用します。 インストール済みパッケージのリストにパッケージの概要が表示されます（エクスプローラー/管理/パッケージ管理/インストール済みパッケージ）。
* buildVersionフィー **ルドとbuildNumberフ** ィールドは必須です **** 。 コンソールが接続されているサーバー番号に対応している必要があります。 この情報は「ヘルプ/バージョン情報」ボックスにあります。
* 次のブロック、エンティティ **** 、および **関数リストは必須です** 。 funcListでは、「name」と「namespace」の各フィールドは必須ですが、名前はユーザーに任せられ、関数リストを一意に指定します。

   つまり、同じ名前空間/名前のペアを持つ別の関数リスト（ここでは「cus::myList」）が読み込まれると、以前に読み込まれた関数が削除されます。 逆に、この名前空間と名前のペアを変更すると、インポートされた新しい関数群が前の関数に追加されます。

* group **要素を使用すると** 、読み込んだ関数を関数エディターに表示する関数グループを指定できます。 @name属性は、既に存在する名前（この場合、関数が対象のグループに追加されます）または新しい名前（この場合、新しいグループに表示されます）にすることができます。
* リマインダー：要素内の@name属性に指定できる値は次のと `<group>` おりです。

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

複数の異なるグループに関数を追加する場合は、同じリスト内で複数の要素を追 `<group>` 跡するように設定できます。

最後に、1つ `<group>` の要素に、パッケージファイルの目的である1つまたは複数の関数の定義を含めることができます。 この要 `<function>` 素については、次の段落で詳しく説明します。

## 関数記述子&lt;関数>&lt;/function> {#function-descriptor--function-}

ここに示すのは、機能実装を提供する一般的なケー **スです**。

以下に、年齢を用いて、成熟年数を示す「相対的成熟度」関数の例を示します。

```
 <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
              minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
       <providerPart provider="PostgreSQL" body="extract(year from age($1))-18"/>
       <providerPart provider="MSSQL,Sybase,Teradata" body="[Other implementation]"/>
    </function>
```

「 **@name** 」フィールドは関数の名前を参照し、「args」は説明に表示されるパラメーターのリストです。 この場合、関数は関数選択ウィンドウに「relativeMaturity ( `<age>` )」と表示されます。

* **helpは、** 式エディターウィンドウの下部に表示されるフィールドです。
* **@displayは情報を提供する** メッセージです。

   >[!NOTE]
   >
   >@helpおよび@display属性で、文字列「$1」は、最初の関数パラメーター（ここでは「Age」）で指定された名前を表します。 $2, $3...は、次のパラメーターを表します。 以下に示す@body属性で、$1は呼び出し中に関数に渡す引数値を指定します。

   >[!NOTE]
   >
   >説明は、有効なXML文字の文字列である必要があります。&lt;と>の代わりに「&lt;」と「>」を使用することに注意してください。

* **@typeは** 、関数の戻り値の型で、標準値(long、string、byte、datetime...)です。 この引数を省略すると、関数を実装する式内で使用可能な型の中で、最適な型がサーバーによって判断されます。
* **@minArgsと** maxArgs **** は、パラメーターのパラメーター数（最小値と最大値）を指定します。 例えば、2つのパラメーターを持つ関数の場合、minArgsとmaxArgsは2と2になります。 3つのパラメーターの場合、および1つのオプションの場合、それぞれ3と4になります。
* 最後に、 **providerPart要素が** 、関数の実装を提供します。

   * **provider属性は必須で** 、実装が提供されるデータベースシステムを指定します。 例に示すように、式の構文と基になる関数が異なる場合、データベースに従って代替実装を提供できます。
   * @body属 **性には** 、関数の実装が含まれます。 注意：この実装は、データベース言語（コードのブロックではなく）での式である必要があります。 データベースに応じて、式はサブクエリ(&quot;(テーブルから選択列(where...)&quot;)で、値を1つだけ返すことができます。 例えば、Oracleの場合はこのようです（クエリーは角括弧で囲む必要があります）。
   >[!NOTE]
   >
   >定義された関数によって1つまたは2つのデータベースのみが問い合わされる可能性が高い場合は、常にこれらのデータベースに対応する定義のみを指定できます。

## &#39;パススルー&#39;関数記述子 {#pass-through--function-descriptor}

特殊な関数記述子は、「 **パススルー** 」ブロックで、「プロバイダ」データベースシステムが指定されています。 この場合、「body」実装には、使用されるデータベースに依存しない構文を持つ関数呼び出しを1つだけ含めることができます。 一方、「ProviderPart」ブロックは一意です。

```
    <function name="CountAll" args="()" help="Counts the values returned (all fields together)"
              type="long" minArgs="0" maxArgs="0">
      <providerPart body="Count(*)"/>
    </function>
```

この場合、関数を追加すると、デフォルトでは使用できなかったデータベース機能がクライアントに表示されるようになります。

## 例 {#examples}

その他の関数の例は、定義済みのパッケージ「xtkdatakitfuncList.xml」に記載されています。
