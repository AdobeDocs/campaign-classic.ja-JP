---
product: campaign
title: 設定
description: 設定
audience: configuration
content-type: reference
topic-tags: navigation-hierarchy
exl-id: c7ae7240-0c12-4420-bbb3-4268c9ade3e7
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 3%

---

# Campaign エクスプローラーのナビゲーションツリーの設定{#configuration}

![](../../assets/v7-only.svg)

エキスパートユーザーは、エクスプローラーツリーにフォルダーを追加し、カスタマイズできます。

Campaign エクスプローラーとナビゲーション階層 [ について詳しくは、この節 ](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy) を参照してください。

ナビゲーションリストで使用されるフォルダーの種類は、**xtk:navtree** スキーマの文法に従った XML ドキュメントで記述されています。

XML ドキュメントの構造は次のようになります。

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

XML ドキュメントには、**name** 属性と **namespace** 属性を持つ **`<navtree>`** ルート要素が含まれ、ドキュメントの名前と名前空間を指定します。 名前と名前空間は、ドキュメントの識別キーを構成します。

アプリケーションのグローバルコマンドは、ドキュメント内の **`<commands>`** 要素から宣言されます。

ファイルタイプの宣言は、次の要素を含むドキュメント内で構造化されます。**`<model>`** と **`<nodemodel>`**。

## グローバルコマンド {#global-commands}

グローバルコマンドを使用すると、アクションを開始できます。 このアクションは、入力フォームまたは SOAP 呼び出しです。

グローバルコマンドは、メインの **[!UICONTROL ツール]** メニューからアクセスできます。

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

グローバルコマンドの説明は、次のプロパティを持つ **`<command>`** 要素に入力されます。

* **名前**:コマンドの内部名：名前は入力され、一意である必要があります
* **ラベル**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **フォーム**:起動するフォーム：入力する値は、入力フォームの識別キーです ( 例：&quot;cus:recipient&quot;)
* **権限**:このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。使用可能な権限のリストには、**[!UICONTROL 管理/アクセス管理/ネームド権限]** フォルダーからアクセスできます。
* **promptLabel**:コマンドを実行する前に確認ボックスを表示します。

**`<command>`** 要素には、**`<command>`** サブ要素を含めることができます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言されているのと同じ順序で表示されます。

コマンド区切り文字を使用すると、コマンド間に分離バーを表示できます。 この値は、コマンドラベルに含まれる **&#39;-&#39;** 値で識別されます。

**`<soapcall>`** タグとその入力パラメーターを任意に指定すると、実行する SOAP メソッドの呼び出しが定義されます。 SOAP API について詳しくは、[Campaign JSAPI のドキュメント ](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html) を参照してください。

**`<enter>`** タグを使用した初期化時に、フォームコンテキストを更新できます。 このタグについて詳しくは、入力フォームに関するドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するグローバルコマンドの宣言：

   ```
   <command desc="Start the data import wizard" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
   ```

   キーボードショートカットは、コマンドラベルに **&amp;** が存在することで、&#39;I&#39;文字に宣言されます。

* 区切り文字付きサブメニューの例：

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

* SOAP メソッドの実行：

   ```
   <command name="cmd3" label="Example 3" promptLabel="Do you really want to execute the command?">
     <soapCall name="Execute" service="xtk:sql"/>
   </command>
   ```

## フォルダーの種類 {#folder-type}

フォルダータイプを使用すると、スキーマのデータにアクセスできます。 フォルダーに関連付けられたビューは、リストと入力フォームで構成されます。

フォルダータイプの設定構造を次に示します。

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

フォルダータイプの宣言は、**`<model>`** 要素の下に入力する必要があります。 この要素を使用すると、**[!UICONTROL 新しいフォルダーを追加]** メニューから表示できる階層組織を定義できます。 **`<model>`** 要素には、**`<nodemodel>`** 要素と他の **`<model>`** 要素を含める必要があります。

**name** および **label** 属性は、要素の内部名と **[!UICONTROL 新しいフォルダーを追加]** メニューに表示されるラベルを設定します。

**`<nodemodel>`** 要素には、次のプロパティを持つフォルダータイプの説明が含まれます。

* **名前**:内部名
* **ラベル**:「新規フォルダーを追 **[!UICONTROL 加」メニ]** ューで、フォルダー挿入時のデフォルトラベルとして使用されるラベル。
* **img**:フォルダー挿入時のデフォルト画像。
* **hiddenCommands**:マスクするコマンドのリスト（コンマ区切り）。可能な値：&quot;adbnew&quot;、&quot;adbsave&quot;、&quot;adbcancel&quot;、&quot;adbdup&quot;
* **newFolderShortCuts**:フォルダー作成時のモデル (**`<nodemodel>`** コンマ区切り ) のショートカットのリスト。
* **insertRight**、 **editRight**、 **deleteRight**:フォルダーの挿入、編集、削除の権限

**`<nodemodel>`** 要素の下の **`<view>`** 要素には、ビューに関連付けられたリストの設定が含まれます。 リストのスキーマは、**`<view>`** 要素の **schema** 属性に入力されます。

リストのレコードを編集する場合、リストスキーマと同じ名前の入力フォームが暗黙的に使用されます。 **`<view>`** 要素の **type** 属性は、フォームの表示に影響します。 次のような値を選択できます。

* **listdet**:リストの下部にフォームを表示します。
* **リスト**:リストのみを表示します。フォームは、ダブルクリックするか、リストを選択するメニューの「開く」を使用して起動します。
* **フォーム**:読み取り専用フォームを表示します。
* **editForm**:編集モードでフォームを表示します。

>[!NOTE]
>
>**`<view>`** 要素に **form** 属性を入力すると、入力フォームの名前がオーバーロードされます。

リスト列のデフォルト設定は、**`<columns>`** 要素を使用して入力します。 列が **xpath** 属性を含む **`<node>`** 要素で宣言され、スキーマ内で参照されるフィールドが値として使用されます。

**例**:「nms:recipient」スキーマでのフォルダータイプの宣言。

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

対応するフォルダー挿入メニュー：

![](assets/d_ncs_integration_navigation_exemple2.png)

フィルタリングと並べ替えは、リストの読み込み時に適用できます。

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

ショートカットコマンドを使用すると、リストの選択に関するアクションを開始できます。 アクションは、入力フォームまたは SOAP 呼び出しです。

コマンドには、リストの **[!UICONTROL アクション]** メニューまたは関連するメニューボタンからアクセスできます。

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

コマンドの説明は、次のプロパティを持つ **`<command>`** 要素に入力します。

* **名前**:コマンドの内部名：名前は入力され、一意である必要があります。
* **ラベル**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **フォーム**:起動するフォーム：入力する値は、入力フォームの識別キーです ( 例：&quot;cus:recipient&quot;) と呼ばれます。
* **権限**:このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。使用可能な権限のリストには、**[!UICONTROL 管理/アクセス管理/ネームド権限]** フォルダーからアクセスできます。
* **promptLabel**:コマンドを実行する前に確認ボックスを表示
* **monoSelection**:モノラル選択を強制します（デフォルトでは複数選択）。
* **refreshView**:コマンドの実行後に、リストを強制的に再読み込みします。
* **enabledIf**:入力した式に応じて、コマンドをアクティブにします。
* **img**:を指定すると、リストツールバーからコマンドにアクセスできる画像が表示されます。

**`<command>`** 要素には、**`<command>`** サブ要素を含めることができます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言されているのと同じ順序で表示されます。

コマンド区切り文字を使用すると、コマンド間に分離バーを表示できます。 この値は、コマンドラベルに含まれる **&#39;-&#39;** 値で識別されます。

**`<soapcall>`** タグとその入力パラメーターを任意に指定すると、実行する SOAP メソッドの呼び出しが定義されます。 SOAP API について詳しくは、[Campaign JSAPI のドキュメント ](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html) を参照してください。

フォームコンテキストは、初期化時に **`<enter>`** タグを使用して更新できます。 このタグについて詳しくは、入力フォームのドキュメントを参照してください。

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

フォルダー管理操作には、次の 2 つのタイプがあります。

1. フォルダーはビューです。このリストには、スキーマに関連付けられているすべてのレコードが表示され、フォルダーのプロパティに入力したシステムフィルタリングが可能です。
1. フォルダーがリンクされます。リスト内のレコードは、フォルダーリンク上で暗黙的にフィルタリングされます。

リンクされたフォルダーの場合は、**`<nodemodel>`** 要素の **folderLink** 属性を設定する必要があります。 この属性には、データスキーマで設定したフォルダー上のリンクの名前が含まれます。

データスキーマ内のリンクされたフォルダーの宣言の例：

```
<element default="DefaultFolder('nmsFolder', [@_folder-id])" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="define" revLabel="Recipients" target="xtk:folder" type="link"/>
```

「folder」という名前のフォルダーのリンク上の **`<nodemodel>`** の設定は次のとおりです。

```
<nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
  img="nms:folder.png" insertRight="folderInsert" label="Recipients" name="nmsFolder">
...
</nodeModel>
```
