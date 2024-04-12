---
product: campaign
title: Campaign エクスプローラーナビゲーションツリーの設定
feature: Application Settings
description: Campaign エクスプローラーのナビゲーションツリーを設定する方法を学ぶ
role: Data Engineer, Developer
exl-id: c7ae7240-0c12-4420-bbb3-4268c9ade3e7
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Campaign エクスプローラーナビゲーションツリーの設定{#configuration}

エキスパートユーザーは、エクスプローラーツリーにフォルダーを追加してカスタマイズできます。

Campaign エクスプローラーとナビゲーション階層の詳細 [この節](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy).

ナビゲーションリストで使用されるフォルダーのタイプは、 **xtk:navtree** スキーマ。

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

XML ドキュメントには、が含まれます。 **`<navtree>`** ルート要素 **名前** および **名前空間** ドキュメント名と名前空間を指定する属性。 名前と名前空間は、ドキュメント ID キーを構成します。

アプリケーションのグローバルコマンドは、 **`<commands>`** 要素。

ファイルタイプの宣言は、次の要素を持つドキュメント内で構造化されます。 **`<model>`** および **`<nodemodel>`**.

## グローバルコマンド {#global-commands}

グローバルコマンドを使用すると、アクションを開始できます。 このアクションは、入力フォームまたは SOAP 呼び出しにすることができます。

グローバルコマンドにはメインからアクセスできます **[!UICONTROL ツール]** メニュー。

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

グローバル コマンドの説明は、 **`<command>`** 次のプロパティを持つ要素：

* **名前**：コマンドの内部名：名前は一意で入力する必要があります
* **ラベル**: コマンドのラベル。
* **降順**：説明は、メイン画面のステータスバーから表示されます。
* **フォーム**：起動するフォーム：入力する値は、入力フォームの識別キー（例：「cus:recipient」）です
* **権限**：このコマンドへのアクセスを許可するネームド権限のリスト （コンマ区切り）。 使用可能な権限のリストには、 **[!UICONTROL 管理/ アクセス管理/ネームド権限]** フォルダー。
* **promptLabel**：コマンドを実行する前に確認ボックスを表示します。

A **`<command>`** 要素にはを含めることができます **`<command>`** サブ要素。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言される順序と同じ順序で表示されます。

コマンド区切り記号を使用すると、コマンド間に区切りバーを表示できます。 で識別されます **&#39;-&#39;** コマンドラベルに含まれる値。

のオプションの存在 **`<soapcall>`** 入力パラメーターを含むタグは、実行する SOAP メソッドの呼び出しを定義します。 SOAP API について詳しくは、次を参照してください。 [Campaign JSAPI ドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja).

フォームコンテキストは、の初期化時に **`<enter>`** タグ。 このタグについて詳しくは、入力フォームのドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するグローバルコマンドの宣言

  ```
  <command desc="Start the data import wizard" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
  ```

  キーボードショートカットは、 **&amp;** をコマンドラベルに追加します。

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

フォルダータイプの宣言は、 **`<model>`** 要素。 この要素を使用すると、 **[!UICONTROL 新規フォルダーを追加]** メニュー。 A **`<model>`** 要素にはを含める必要があります **`<nodemodel>`** 要素およびその他 **`<model>`** 要素。

この **名前** および **ラベル** 属性は、要素の内部名と、に表示されるラベルを設定します **[!UICONTROL 新規フォルダーを追加]** メニュー。

この **`<nodemodel>`** 要素には、フォルダータイプの説明と次のプロパティが含まれます。

* **名前**：内部名
* **ラベル**：で使用されるラベル **[!UICONTROL 新規フォルダーを追加]** フォルダーを挿入する際のデフォルトラベルとしておよびを使用します。
* **img**：フォルダー挿入時のデフォルト画像。
* **hiddenCommand**：マスクするコマンドのリスト（コンマ区切り）。 指定可能な値：&quot;adbnew&quot;、&quot;adbsave&quot;、&quot;adbcancel&quot;、&quot;adbdup&quot;
* **newFolderShortCuts**：モデルのショートカットのリスト（**`<nodemodel>`** フォルダー作成時はコンマで区切ります。
* **insertRight**, **editRight**, **deleteRight**：フォルダーの挿入、編集、削除の権限。

この **`<view>`** の下の要素 **`<nodemodel>`** 要素には、ビューに関連付けられたリストの設定が含まれます。 リストのスキーマは、 **スキーマ** 属性 **`<view>`** 要素。

リストのレコードを編集するには、リストスキーマと同じ名前の入力フォームを暗黙的に使用します。 この **タイプ** の属性 **`<view>`** 要素は、フォームの表示に影響します。 次のような値を選択できます。

* **listdet**：リストの下部にフォームを表示します。
* **list**：リストのみを表示します。 フォームは、ダブルクリックするか、リストを選択するメニューの「開く」を介して起動されます。
* **フォーム**：読み取り専用フォームを表示します。
* **editForm**：フォームを編集モードで表示します。

>[!NOTE]
>
>入力フォームの名前は、を入力してオーバーロードできます。 **フォーム** の属性 **`<view>`** 要素。

リスト列のデフォルト設定は、を介して入力されます。 **`<columns>`** 要素。 列は次で宣言されています **`<node>`** を含む要素 **xpath** 属性のスキーマで参照されるフィールドを値として設定します。

**例**:nms:recipient スキーマのフォルダータイプの宣言。

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

ショートカットコマンドを使用すると、リストの選択時にアクションを開始できます。 アクションは、入力フォームまたは SOAP 呼び出しです。

コマンドは、からアクセスできます **[!UICONTROL アクション]** リストのメニューまたは関連するメニューボタン。

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

コマンドの説明は、 **`<command>`** 次のプロパティを持つ要素：

* **名前**：コマンドの内部名：名前は一意で入力する必要があります。
* **ラベル**: コマンドのラベル。
* **降順**：説明は、メイン画面のステータスバーから表示されます。
* **フォーム**：起動するフォーム：入力する値は、入力フォームの識別キー（例：「cus:recipient」）です。
* **権限**：このコマンドへのアクセスを許可するネームド権限のリスト （コンマ区切り）。 使用可能な権限のリストには、 **[!UICONTROL 管理/ アクセス管理/ネームド権限]** フォルダー。
* **promptLabel**：コマンドの実行前に確認ボックスを表示します
* **monoSelection**：単一選択を強制します（デフォルトでは複数選択）。
* **refreshView**：コマンドの実行後に、リストを強制的にリロードします。
* **enabledIf**：入力した式に応じてコマンドをアクティブにします。
* **img**：リストツールバーからコマンドにアクセスできる画像を入力します。

A **`<command>`** 要素にはを含めることができます **`<command>`** サブ要素。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言される順序と同じ順序で表示されます。

コマンド区切り記号を使用すると、コマンド間に区切りバーを表示できます。 で識別されます **&#39;-&#39;** コマンドラベルに含まれる値。

のオプションの存在 **`<soapcall>`** 入力パラメーターを含むタグは、実行する SOAP メソッドの呼び出しを定義します。 SOAP API について詳しくは、次を参照してください： [Campaign JSAPI ドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja).

フォームコンテキストは、の初期化時に **`<enter>`** タグ。 このタグについて詳しくは、入力フォームドキュメントを参照してください。

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

リンクされたフォルダーの場合、 **folderLink** の属性 **`<nodemodel>`** 要素を入力する必要があります。 この属性には、データスキーマに設定されたフォルダー上のリンクの名前が格納されます。

データスキーマにおけるリンクされたフォルダーの宣言の例：

```
<element default="DefaultFolder('nmsFolder', [@_folder-id])" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="define" revLabel="Recipients" target="xtk:folder" type="link"/>
```

の設定 **`<nodemodel>`** 「folder」という名前のフォルダーのリンクでは、次のようになります。

```
<nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
  img="nms:folder.png" insertRight="folderInsert" label="Recipients" name="nmsFolder">
...
</nodeModel>
```
