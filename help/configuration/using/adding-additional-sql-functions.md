---
product: campaign
title: SQL 関数の追加
description: 追加の SQL 関数の定義方法を説明します
feature: Configuration, Instance Settings
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: 04b0a0e5-d6df-447c-ac67-66adb1bdf717
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 1%

---

# 追加の SQL 関数の定義{#adding-additional-sql-functions}

Adobe Campaignを使用すると、 **独自の機能** データベースが提供する関数と、コンソールでまだ使用できない関数の両方で、SQL 関数にアクセスできます。 これは、集計関数（平均、最大、合計）などで役立ちます。この関数は、サーバー上でのみ計算でき、コンソールに式を「手動」で書き込むよりも、特定の関数を実装する方法がデータベースで提供される場合に便利です。

このメカニズムは、まだAdobe Campaignコンソールで提供されていない、最新または一般的でないデータベースエンジンの SQL 関数を使用する場合にも使用できます。

これらの関数が追加されると、他の事前定義された関数と同様に、式エディターに表示されます。

>[!IMPORTANT]
>
>コンソールの SQL 関数呼び出しが、サーバーに自然に送信されなくなりました。 ここで説明するメカニズムは、次のようになります。 **～を呼ぶ唯一の方法** （計画外の SQL ファンクション・サーバ）

## インストール {#installation}

追加する関数は、 **XML フォーマットの&quot;package&quot;ファイル**（構造の詳細は、次の段落で説明します）。

コンソールからインストールするには、「 **ツール/高度なツール/パッケージをインポート** メニューからオプションを選択し、 **[!UICONTROL ファイルからインストール]** をクリックし、インポートウィザードの指示に従います。

>[!IMPORTANT]
>
>警告：読み込んだ関数のリストがすぐに関数エディターに表示されても、Adobe Campaignが再起動されるまで使用できません。

## インポートするパッケージの一般的な構造 {#general-structure-of-package-to-import}

追加する関数は、 **&quot;package&quot;ファイル** を XML 形式で指定します。 次に例を示します。

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

* The **名前**, **名前空間** および **ラベル** は情報提供の目的でのみ使用します。 インストール済みパッケージのリストにパッケージの概要が表示されます（エクスプローラー/管理/パッケージ管理/インストール済みパッケージ）。
* The **buildVersion** および **buildNumber** フィールドは必須です。 これらは、コンソールが接続されているサーバー番号に対応している必要があります。 この情報は、「ヘルプ/バージョン情報」ボックスにあります。
* 次のブロックは **エンティティ** および **funclist** は必須です。 funcList では、&quot;name&quot;と&quot;namespace&quot;のフィールドは必須ですが、名前はユーザーが決定する必要があり、関数リストを一意に指定します。

  つまり、同じ名前空間/名前のペアを持つ関数の別のリスト（ここでは「cus::myList」）が読み込まれると、以前に読み込まれた関数は削除されます。 逆に、この名前空間と名前のペアを変更すると、新しい読み込まれた一連の関数が前の関数に追加されます。

* The **グループ** element を使用すると、読み込んだ関数を関数エディターに表示する関数グループを指定できます。 @name属性は、既に存在する名前（対象のグループに関数が追加される場合）または新しい名前（新しいグループに関数が表示される場合）のどちらかです。
* リマインダー： @name属性に指定できる値 ( `<group>` 要素は次のとおりです。

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
>@label属性を必ず入力してください。これは、使用可能な関数のリストに表示される名前です。 何も入力しない場合、グループには名前が付きません。 ただし、既存の名前以外の名前を入力すると、グループ全体の名前が変更されます。

複数の異なるグループに関数を追加する場合は、 `<group>`  要素は同じリスト内で追跡されます。

最後に、 `<group>` 要素には、パッケージファイルの目的である 1 つまたは複数の関数の定義を含めることができます。 The  `<function>`   要素について詳しくは、次の段落で説明します。

## 関数記述子 &lt;function>&lt;/function> {#function-descriptor--function-}

ここに示す事例は、私たちが提供したい一般的な事例です **関数の実装**.

以下は、年齢を用いて、成年と見なされた年数を示す「相対成熟度」関数の例です。

```
 <function name="relativeMaturity" type="long" args="(<Âge>)" help="Returns the difference between a date and 18 years"
              minArgs="1" maxArgs="1" display="Relative maturity of the person born on the date $1">
       <providerPart provider="PostgreSQL" body="extract(year from age($1))-18"/>
       <providerPart provider="MSSQL,Sybase,Teradata" body="[Other implementation]"/>
    </function>
```

The **@name** field は関数の名前を参照し、 args は説明に表示されるパラメータのリストです。 この場合、関数は&quot;relativeMurity ( `<age>` )」と入力します。

* **ヘルプ** は、式エディターウィンドウの下部に表示されるフィールドです。
* **@display** は、情報を提供するメッセージです。

  >[!NOTE]
  >
  >@help属性と@display属性で、文字列「$1」は、最初の関数パラメーター（ここでは「Age」）で指定された名前を表します。 $2、$3...は、次のパラメーターを表します。 以下に説明する@body属性で、$1 は呼び出し中に関数に渡される引数値を指定します。

  >[!NOTE]
  >
  >説明は、有効な XML 文字の文字列である必要があります。&lt; および > の代わりに「&lt;」と「>」が使用されていることに注意してください。

* **@type** は関数の戻り値の型で、標準の値です (long、string、byte、datetime...)。 省略した場合、サーバーは関数を実装する式内の使用可能な型の中で最適な型を判断します。
* **@minArgs** および **maxArgs** は、パラメータのパラメータの数（最小値と最大値）を指定します。 たとえば、2 つのパラメータを持つ関数の場合、minArgs と maxArgs は 2 と 2 になります。 3 つのパラメーターと 1 つのオプションの場合、それぞれ 3 と 4 になります。
* 最後に、 **providerPart** 要素は、関数の実装を提供します。

   * The **プロバイダー** 属性は必須です。この属性は、実装が提供されるデータベースシステムを指定します。 この例で示すように、式の構文や基になる関数が異なる場合、データベースに応じて代替実装を提供できます。
   * The **@body** 属性には、関数の実装が含まれます。 注意：この実装は、（コードブロックではなく）データベース言語の式である必要があります。 データベースに応じて、式はサブクエリ (「（テーブルから選択列の場所…）」) で、1 つの値のみを返すことができます。 例えば、Oracleの場合です（クエリは角括弧で囲む必要があります）。

  >[!NOTE]
  >
  >定義した関数でクエリが実行されるデータベースが 1 つまたは 2 つだけの場合、常にこれらのデータベースに対応する定義のみを提供できます。

## 「パススルー」関数記述子 {#pass-through--function-descriptor}

特殊な関数記述子は、 **&quot;パススルー&quot;** ブロック（「プロバイダ」データベースシステムが指定されていない） この場合、「body」実装には、使用するデータベースに依存しない構文を持つ 1 つの関数呼び出しのみを含めることができます。 一方、「ProviderPart」ブロックは一意です。

```
    <function name="CountAll" args="()" help="Counts the values returned (all fields together)"
              type="long" minArgs="0" maxArgs="0">
      <providerPart body="Count(*)"/>
    </function>
```

この場合、関数を追加すると、デフォルトでは使用できなかったデータベース関数が作成され、クライアントに対して表示されるようになります。

## 例 {#examples}

その他の関数の例は、事前定義済みパッケージ「xtkdatakitfuncList.xml」に記載されています。
