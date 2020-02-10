---
title: 設定
seo-title: 設定
description: 設定
seo-description: null
page-status-flag: never-activated
uuid: 0f2aadc3-5199-476c-9956-6e39b899a7d0
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: configuration
content-type: reference
topic-tags: navigation-hierarchy
discoiquuid: b781fd52-828c-4582-a546-a1fee7e5a26d
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 912507f25c5bc3c1ca7121b0df8182176900f4c0

---


# 設定{#configuration}

ナビゲーションリストで使用されるフォルダの種類は、 **xtk:navtreeスキーマの文法に従ったXML文書で記述されています** 。

XMLドキュメントの構造は次のようになります。

```
<navtree name="name" namespace="name_space">
  <!-- Global commands -->
  <commands>
      ...
  </commands>
  
  <!-- Structured space for adding a folder -->
  <model name="<name>" label="<Label>">
    <!-- Folder type -->
    <nodeModel>
      ...
    </nodeModel>
<model name="<name>" label="<Sub model>">
      ...
    </model>
  </model> 
</navtree>
```

XMLドキュメントには、ドキュメント名と名 **`<navtree>`** 前空間を指定する **name** 属性とnamespace属性を持つ **** root要素が含まれています。 ドキュメントIDキーは、名前と名前空間で構成されます。

アプリケーションのグローバルコマンドは、ドキュメント内で要素から宣言さ **`<commands>`** れます。

ファイルタイプの宣言は、ドキュメント内で次の要素を持つ構造化されています。 **`<model>`** と **`<nodemodel>`**。

## グローバルコマンド {#global-commands}

グローバルコマンドを使用すると、アクションを起動できます。 このアクションは、入力フォームまたはSOAP呼び出しです。

グローバルコマンドはメインメニューからアクセス **[!UICONTROL Tools]** できます。

コマンドの設定構造は次のとおりです。

```
<commands>
  <!-- Description of a command -->
  <command name="<name>" label="<label>" desc="<Description>" form="<form>" rights="<rights>">
    <soapCall name="<name>" service="<schema>">
      <param type="<type>" exprIn="<xpath>"/>  
        ...
    </soapCall>
    <enter>
      ...
    </enter>
  </command>
  <!-- Separator -->
  <command label="-" name="<name>"/>
  <!-- Command structure -->
  <command name="<name>" label="<Label>">
    <command...
  </command>
</commands>
```

グローバルコマンドの説明は、次のプロパティを使用し **`<command>`** て要素に入力します。

* **name**:コマンドの内部名：名前を入力し、一意にする必要があります
* **label**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **form**:起動するフォーム：入力する値は、入力フォームのIDキー(&quot;cus:recipient&quot;)
* **rights**:このコマンドへのアクセスを許可する名前付き権限のリスト（コンマ区切り）。 使用可能な権限のリストは、フォルダーからアクセスで **[!UICONTROL Administration > Access management > Named rights]** きます。
* **promptLabel**:コマンドを実行する前に、確認ボックスを表示します。

要素に **`<command>`** はサブ要素を含め **`<command>`** ることができます。 この場合、親要素を使用して、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XMLドキュメントで宣言されている順序で表示されます。

コマンドセパレーターを使用すると、コマンド間に区切りバーを表示できます。 この値は、コマンドラ **ベルに含まれる** &#39;-&#39;値で識別されます。

入力パラメーターを含むタ **`<soapcall>`** グのオプションの存在は、実行するSOAPメソッドの呼び出しを定義します。 SOAP APIについて詳しくは、「キャンペーンJSAPIドキュメント」 [を参照してください](http://docs.campaign.adobe.com/doc/AC/en/jsapi/index.html)。

初期化時に、タグからフォームコンテキストを更新で **`<enter>`** きます。 このタグの詳細については、入力フォームに関するドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するグローバルコマンドの宣言：

   ```
   <command desc="Start the data import wizard" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
   ```

   キーボードショートカットは、コマンドラベルに **&amp;を入力すると&#39;I&#39;文字で宣言され** ます。

* セパレーター付きのサブメニューの例：

   ![](assets/d_ncs_integration_navigation_exemple1.png)

   ```
   <command label="Administration" name="admin">
     <command name="cmd1" label="Example 1" form="cus:example1"/>
     <command name="sep" label="-"/>
     <command name="cmd1" label="Example 2" form="cus:example2">
       <enter>
         <set xpath="@type" expr="1"/>
       </enter>
     </command>
   </command>
   ```

* SOAPメソッドの実行：

   ```
   <command name="cmd3" label="Example 3" promptLabel="Do you really want to execute the command?">
     <soapCall name="Execute" service="xtk:sql"/>
   </command>
   ```

## フォルダタイプ {#folder-type}

フォルダータイプを使用すると、スキーマのデータにアクセスできます。 フォルダーに関連付けられたビューは、リストと入力フォームで構成されます。

フォルダータイプの設定構造は次のとおりです。

```
<!-- Structured location to add the folder -->
<model name="name" label="Labelled">
  <!-- Type of folder -->
  <nodeModel name="<name>" label="<Labelled>" img="<image>">
    <view name="<name>" schema="<schema>" type="<listdet|list|form|editForm>">
      <columns>
        <node xpath="<field1>"/>
        ...
    </columns>
    </view> 
  </nodeModel>
  <model name="<name>" label="<Sous modèle>">
    ...
  </model>
</model>
```

フォルダー型宣言は要素の下に入力する必要があ **`<model>`** ります。 この要素を使用すると、メニューに表示される階層構成を定義で **[!UICONTROL Add new folder]** きます。 要素には **`<model>`** 要素と他の要素を含め **`<nodemodel>`** る必要があ **`<model>`** ります。

name属性と **label属** 性は **、メニューに表示される要素の内部名とラベルを設定****[!UICONTROL Add new folder]** します。

この要 **`<nodemodel>`** 素には、次のプロパティを持つフォルダータイプの説明が含まれます。

* **name**:内部名
* **label**:ラベルを指定します。ラベルは、メニ **[!UICONTROL Add new folder]** ューで使用され、フォルダーの挿入時にデフォルトのラベルとして使用されます。
* **img**:フォルダ挿入時の初期設定の画像。
* **hiddenCommands**:マスクするコマンドのリスト（コンマ区切り）。 可能な値：&quot;insert&quot;、&quot;delete&quot;、&quot;update&quot;、&quot;duplicate&quot;
* **newFolderShortCuts**:フォルダー作成時のモデルのシ&#x200B;**`<nodemodel>`** ョートカットのリスト（コンマで区切る）。
* **insertRight**、 **editRight**、 **deleteRight**:フォルダの挿入、編集、削除の権限。

要素 **`<view>`** の下の要素に **`<nodemodel>`** は、ビューに関連付けられたリストの設定が含まれます。 リストのスキーマは、要素の **schema** 属性に入力され **`<view>`** ます。

リストのレコードを編集する場合、リストスキーマと同じ名前の入力フォームが暗黙的に使用されます。 要素 **の** type属性は **`<view>`** 、フォームの表示に影響を与えます。 次のような値を選択できます。

* **listdet**:リストの一番下にフォームを表示します。
* **list**:リストのみを表示します。 フォームは、ダブルクリックするか、リストを選択するメニューの「開く」を使用して起動します。
* **form**:読み取り専用フォームを表示します。
* **editForm**:フォームを編集モードで表示します。

>[!NOTE]
>
>入力フォームの名前は、要素にform属性を入力することで **オーバーロー** ドで **`<view>`** きます。

リスト列のデフォルト設定は、要素を介して入力さ **`<columns>`** れます。 xpath属性を含む要素で列が宣言さ **`<node>`** れ、スキーマで **** 参照されるフィールドが値として指定されます。

**例**:&quot;nms:recipient&quot;スキーマでのフォルダータイプの宣言。

```
<model label="Profiles and targets" name="nmsProfiles">
  <nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
             img="nms:folder.png" insertRight="folderInsert" label="Recipients"
             name="nmsFolder">
    <view name="listdet" schema="nms:recipient" type="listdet">
      <columns>
        <node xpath="@firstName"/>
        <node xpath="@lastName"/>
        <node xpath="@email"/>
        <node xpath="@account"/>
      </columns>
    </view>
  </nodeModel>
  <nodeModel name="nmsGroup" label="Groups"...
</model>
```

対応するフォルダ挿入メニュー：

![](assets/d_ncs_integration_navigation_exemple2.png)

フィルタリングと並べ替えは、リストの読み込み中に適用できます。

```
<view name="listdet" schema="nms:recipient" type="listdet">
  <columns>
    ...
  </columns>

  <orderBy>
    <node expr="@lastName" desc="true"/>
</orderBy>
  <sysFilter>
    <condition expr="@type = 1"/>
  </sysFilter>
</view>  
```

### ショートカットコマンド {#shortcut-commands}

ショートカットコマンドを使用すると、リストの選択時にアクションを起動できます。 アクションは、入力フォームまたはSOAP呼び出しです。

コマンドは、リストのメニューま **[!UICONTROL Action]** たは関連するメニューボタンからアクセスできます。

コマンドの設定構造は次のとおりです。

```
<nodeModel...
  ...
  <command name="<name>" label="<label>" desc="<Description>" form="<form>" rights="<rights>">
    <soapCall name="<name>" service="<schema>">
      <param type="<type>" exprIn="<xpath>"/>  
        ...
    </soapCall>
    <enter>
      ...
    </enter>
  </command>
</nodeModel>
```

コマンドの説明は、次のプロパティを使用して要 **`<command>`** 素に入力します。

* **name**:コマンドの内部名：名前を入力し、一意にする必要があります。
* **label**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **form**:起動するフォーム：入力する値は、入力フォームのIDキー(「cus:recipient」)。
* **rights**:このコマンドへのアクセスを許可する名前付き権限のリスト（コンマ区切り）。 使用可能な権限のリストは、フォルダーからアクセスで **[!UICONTROL Administration > Access management > Named rights]** きます。
* **promptLabel**:コマンドを実行する前に確認ボックスを表示する
* **monoSelection**:モノラル選択（デフォルトでは複数選択）を強制します。
* **refreshView**:コマンドの実行後にリストを強制的に再読み込みします。
* **enabledIf**:入力した式に応じてコマンドをアクティブにします。
* **img**:リストツールバーからコマンドにアクセスできるイメージを入力します。

要素に **`<command>`** はサブ要素を含め **`<command>`** ることができます。 この場合、親要素を使用して、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XMLドキュメントで宣言されている順序で表示されます。

コマンドセパレーターを使用すると、コマンド間に区切りバーを表示できます。 この値は、コマンドラ **ベルに含まれる** &#39;-&#39;値で識別されます。

入力パラメーターを含むタ **`<soapcall>`** グのオプションの存在は、実行するSOAPメソッドの呼び出しを定義します。 SOAP APIについて詳しくは、「キャンペーンJSAPIドキュメン [ト」を参照してください](http://docs.campaign.adobe.com/doc/AC/en/jsapi/index.html)。

フォームコンテキストは、タグを使用した初期化時に更新で **`<enter>`** きます。 このタグの詳細については、入力フォームのドキュメントを参照してください。

**例**：

```
<command desc="Cancel execution of the job" enabledIf="EV(@status, 'running')"
         img="nms:difstop.bmp" label="Cancel..." name="cancelJob" 
         promptLabel="Do you really want to cancel this job?" refreshView="true">
  <soapCall name="Cancel" service="xtk:jobInterface"/>
</command>
<command label="-" name="sep1"/>
<command desc="Execute selected template" form="cus:form" lmonoSelection="true" name="executeModel"
         rights="import,export,aggregate">
  <enter>
    <set expr="0" xpath="@status"/>
  </enter>
</command>
```

### リンクされたフォルダー {#linked-folder}

フォルダー管理操作には2種類あります。

1. フォルダはビューです。このリストには、スキーマに関連付けられたすべてのレコードが表示され、フォルダーのプロパティに入力されたシステムフィルターが適用される可能性があります。
1. フォルダーがリンクされます。リスト内のレコードは、フォルダーリンクで暗黙的にフィルターされます。

リンクされたフォルダーの場合は、要 **素のfolderLink** 属性を入力 **`<nodemodel>`** する必要があります。 この属性には、データスキーマで設定されたフォルダー上のリンクの名前が含まれます。

データスキーマ内のリンクフォルダーの宣言の例：

```
<element default="DefaultFolder('nmsFolder')" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="own" revLabel="Recipients" target="xtk:folder" type="link"/>
```

「folder」という名前の **`<nodemodel>`** フォルダーのリンク上ののの設定は次のとおりです。

```
<nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
  img="nms:folder.png" insertRight="folderInsert" label="Recipients" name="nmsFolder">
...
</nodeModel>
```

