---
product: campaign
title: Campaign エクスプローラーナビゲーションツリーの設定
feature: Application Settings
description: Campaign エクスプローラーのナビゲーションツリーを設定する方法を学ぶ
role: Data Engineer, Developer
exl-id: c7ae7240-0c12-4420-bbb3-4268c9ade3e7
source-git-commit: d56038fc8baf766667d89bb73747c20ec041124c
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 1%

---

# Campaign エクスプローラーナビゲーションツリーの設定{#configuration}

エキスパートユーザーは、エクスプローラーツリーにフォルダーを追加してカスタマイズできます。

Campaign ユーザーインターフェイスについて詳しくは、[Adobe Campaign v8 （コンソール）ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/new/campaign-ui){target=_blank} を参照してください。

ナビゲーションリストで使用されるフォルダーのタイプは、**xtk:navtree** スキーマの文法に従う XML 文書に記述されます。

XML ドキュメントは、次のような構造になっています。

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

XML ドキュメントには、ドキュメントの名前と名前空間を指定する **`<navtree>`** name **属性と** namespace **属性を持つ** ルート要素が含まれています。 名前と名前空間は、ドキュメント ID キーを構成します。

アプリケーションのグローバルコマンドは、**`<commands>`** 要素からドキュメント内で宣言されます。

ファイルタイプの宣言は、**`<model>`** および **`<nodemodel>`** の要素を持つドキュメント内で構造化されます。

## グローバルコマンド {#global-commands}

グローバルコマンドを使用すると、アクションを開始できます。 このアクションは、入力フォームまたはSOAP呼び出しにすることができます。

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

グローバルコマンドの説明は、次のプロパティを使用して **`<command>`** 要素に入力します。

* **name**: コマンドの内部名：名前は一意で入力する必要があります
* **label**: コマンドのラベル。
* **desc**: メイン画面のステータスバーに表示される説明。
* **form**：起動するフォーム：入力する値は、入力フォームの識別キー（例：「cus:recipient」）です
* **rights**：このコマンドへのアクセスを許可するネームド権限のリスト （コンマ区切り）。 使用可能な権限のリストには、**[!UICONTROL 管理/アクセス管理/ネームド権限]** フォルダーからアクセスできます。
* **promptLabel**: コマンドを実行する前に確認ボックスを表示します。

**`<command>`** 要素には、**`<command>`** 個のサブ要素を含めることができます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言される順序と同じ順序で表示されます。

コマンド区切り記号を使用すると、コマンド間に区切りバーを表示できます。 コマンドラベルに含まれる **&#39;-&#39;** 値によって識別されます。

入力パラメーターを含む **`<soapcall>`** タグがオプションで存在する場合は、実行するSOAP メソッドの呼び出しを定義します。 SOAP API について詳しくは、[Campaign JSAPI ドキュメント ](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja) を参照してください。

フォームコンテキストは、**`<enter>`** タグからの初期化時に更新できます。 このタグについて詳しくは、入力フォームのドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するグローバルコマンドの宣言

  ```
  <command desc="Start the data import assistant" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
  ```

  キーボードショートカットは、コマンドラベルに **&amp;** が存在することにより、「I」文字で宣言されます。

* 区切り記号を含むサブメニューの例：

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

## フォルダータイプ {#folder-type}

フォルダータイプを使用すると、スキーマのデータへのアクセス権を付与できます。 フォルダーに関連付けられたビューは、リストと入力フォームで構成されます。

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

フォルダータイプの宣言は、**`<model>`** 要素の下に入力する必要があります。 この要素を使用すると、「**[!UICONTROL 新規フォルダーを追加]** メニューから表示できる階層組織を定義できます。 **`<model>`** 要素には、**`<nodemodel>`** 要素と他の **`<model>`** 要素を含める必要があります。

**name** 属性と **label** 属性は、要素の内部名と、**[!UICONTROL 新しいフォルダーを追加]** メニューに表示されるラベルを設定します。

**`<nodemodel>`** 要素には、フォルダータイプの説明と次のプロパティが含まれます。

* **name**：内部名
* **label**: **[!UICONTROL 新しいフォルダーを追加]** メニューで使用されるラベルで、フォルダーの挿入時にデフォルトラベルとして使用されます。
* **img**：フォルダーの挿入時のデフォルト画像。
* **hiddenCommands**：マスクするコマンドのリスト（コンマ区切り）。 指定可能な値：&quot;adbnew&quot;、&quot;adbsave&quot;、&quot;adbcancel&quot;、&quot;adbdup&quot;
* **newFolderShortCuts**：フォルダー作成時のモデル上のショートカットのリスト（コンマ区切りの **`<nodemodel>`**）。
* **insertRight**、**editRight**、**deleteRight**：フォルダーの挿入、編集、削除の権限。

**`<view>`** 要素の下の **`<nodemodel>`** 要素には、ビューに関連付けられたリストの設定が含まれます。 リストのスキーマは、**要素の** schema **`<view>`** 属性に入力されます。

リストのレコードを編集するには、リストスキーマと同じ名前の入力フォームを暗黙的に使用します。 **要素の** type **`<view>`** 属性は、フォームの表示に影響します。 次のような値を選択できます。

* **listdet**：リストの下部にフォームを表示します。
* **リスト**：リストを単独で表示します。 フォームは、ダブルクリックするか、リストを選択するメニューの「開く」を介して起動されます。
* **form**：読み取り専用フォームを表示します。
* **editForm**：フォームを編集モードで表示します。

>[!NOTE]
>
>入力フォームの名前は、**要素に** form **`<view>`** 属性を入力することでオーバーロードできます。

リスト列のデフォルト設定は、**`<columns>`** 要素を介して入力されます。 **`<node>`** xpath **属性を含む** 要素で、列が宣言され、そのスキーマ内で参照されるフィールドがその値として設定されている。

**例**:「nms:recipient」スキーマのフォルダータイプの宣言。

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

ショートカットコマンドを使用すると、リストの選択時にアクションを開始できます。 アクションは、入力フォームまたはSOAP呼び出しです。

コマンドは、リストの **[!UICONTROL アクション]** メニューまたは関連するメニューボタンからアクセスできます。

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

コマンドの説明は、次のプロパティを使用して **`<command>`** 要素に入力します。

* **name**: コマンドの内部名：名前は一意で入力する必要があります。
* **label**: コマンドのラベル。
* **desc**: メイン画面のステータスバーに表示される説明。
* **form**：起動するフォーム：入力する値は、入力フォームの識別キー（例：「cus:recipient」）です。
* **rights**：このコマンドへのアクセスを許可するネームド権限のリスト （コンマ区切り）。 使用可能な権限のリストには、**[!UICONTROL 管理/アクセス管理/ネームド権限]** フォルダーからアクセスできます。
* **promptLabel**: コマンドの実行前に確認ボックスを表示します
* **monoSelection**：単一選択を強制します（デフォルトでは複数選択）。
* **refreshView**: コマンドの実行後に、リストを強制的にリロードします。
* **enabledIf**：入力された式に応じてコマンドをアクティブにします。
* **img**：リストツールバーからコマンドにアクセスできる画像を入力します。

**`<command>`** 要素には、**`<command>`** 個のサブ要素を含めることができます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言される順序と同じ順序で表示されます。

コマンド区切り記号を使用すると、コマンド間に区切りバーを表示できます。 コマンドラベルに含まれる **&#39;-&#39;** 値によって識別されます。

入力パラメーターを含む **`<soapcall>`** タグがオプションで存在する場合は、実行するSOAP メソッドの呼び出しを定義します。 SOAP API について詳しくは、[Campaign JSAPI ドキュメント ](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja) を参照してください。

フォームコンテキストは、初期化時に **`<enter>`** タグを使用して更新できます。 このタグについて詳しくは、入力フォームドキュメントを参照してください。

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

フォルダー管理操作には、次の 2 種類があります。

1. フォルダーはビューです。リストには、スキーマに関連付けられたすべてのレコードが表示され、フォルダーのプロパティにシステムフィルタリングが入力されている可能性があります。
1. フォルダーがリンクされている場合：リスト内のレコードは、フォルダーリンクで暗黙的にフィルタリングされます。

リンクされたフォルダーの場合は、**要素の** folderLink **`<nodemodel>`** 属性を設定する必要があります。 この属性には、データスキーマに設定されたフォルダー上のリンクの名前が格納されます。

データスキーマにおけるリンクされたフォルダーの宣言の例：

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
