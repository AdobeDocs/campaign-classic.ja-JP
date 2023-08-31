---
product: campaign
title: Campaign エクスプローラーのナビゲーションツリーを設定
feature: Application Settings
description: Campaign エクスプローラーのナビゲーションツリーの設定方法を説明します
role: Data Engineer, Developer
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
exl-id: c7ae7240-0c12-4420-bbb3-4268c9ade3e7
source-git-commit: 28638e76bf286f253bc7efd02db848b571ad88c4
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 3%

---

# Campaign エクスプローラーのナビゲーションツリーを設定{#configuration}

エキスパートユーザーは、エクスプローラーツリーにフォルダーを追加し、カスタマイズできます。

Campaign エクスプローラーとナビゲーション階層の詳細を説明します [この節](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy).

ナビゲーションリストで使用されるフォルダの種類は、 **xtk:navtree** スキーマ。

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

XML ドキュメントには **`<navtree>`** ルート要素 **名前** および **名前空間** 属性を使用して、ドキュメント名と名前空間を指定します。 名前と名前空間がドキュメント識別キーを構成します。

アプリケーションのグローバルコマンドは、ドキュメント内の **`<commands>`** 要素を選択します。

ファイルタイプの宣言は、次の要素を持つドキュメント内で構造化されます。 **`<model>`** および **`<nodemodel>`**.

## グローバルコマンド {#global-commands}

グローバルコマンドを使用すると、アクションを開始できます。 このアクションは、入力フォームまたは SOAP 呼び出しです。

グローバルコマンドには、メインからアクセスできます **[!UICONTROL ツール]** メニュー。

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

グローバルコマンドの説明は、 **`<command>`** 要素を次のプロパティで指定します。

* **名前**：コマンドの内部名：名前を入力し、一意である必要があります
* **ラベル**：コマンドのラベル。
* **desc**：メイン画面のステータスバーに表示される説明。
* **フォーム**：起動するフォーム：入力する値は、入力フォームの ID キーです（例：「cus:recipient」）。
* **権限**：このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。 使用可能な権限のリストには、 **[!UICONTROL 管理/アクセス管理/ネームド権限]** フォルダー。
* **promptLabel**：コマンドを実行する前に確認ボックスを表示します。

A **`<command>`** 要素に含めることができる要素 **`<command>`** サブ要素 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言されているのと同じ順序で表示されます。

コマンド区切り文字を使用すると、コマンド間に分離バーを表示できます。 これは、 **&#39;-&#39;** の値を指定します。

オプションで **`<soapcall>`** タグに入力パラメーターを指定し、実行する SOAP メソッドの呼び出しを定義します。 SOAP API について詳しくは、 [Campaign JSAPI ドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja).

初期化時に、 **`<enter>`** タグを使用します。 このタグについて詳しくは、入力フォームに関するドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するためのグローバルコマンドの宣言：

  ```
  <command desc="Start the data import wizard" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
  ```

  キーボードショートカットは、「I」文字に対して、 **&amp;** 」と入力します。

* 区切り文字付きのサブメニューの例：

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

フォルダータイプの宣言は、 **`<model>`** 要素を選択します。 この要素を使用すると、 **[!UICONTROL 新しいフォルダーを追加]** メニュー。 A **`<model>`** 要素に次を含める必要があります **`<nodemodel>`** 要素とその他 **`<model>`** 要素。

The **名前** および **ラベル** 属性は、要素の内部名と、 **[!UICONTROL 新しいフォルダーを追加]** メニュー。

The **`<nodemodel>`** element には、次のプロパティを持つフォルダータイプの説明が含まれます。

* **名前**：内部名
* **ラベル**：で使用されるラベル **[!UICONTROL 新しいフォルダーを追加]** メニューおよびを、フォルダー挿入時のデフォルトのラベルとして使用できます。
* **img**：フォルダー挿入時のデフォルトの画像。
* **hiddenCommands**：マスクするコマンドのリスト（コンマ区切り）です。 可能な値は、「adbnew」、「adbsave」、「adbcancel」および「adbdup」です。
* **newFolderShortCuts**：モデル上のショートカットのリスト (**`<nodemodel>`** （コンマで区切って）フォルダー作成で使用します。
* **insertRight**, **editRight**, **deleteRight**：フォルダーの挿入、編集および削除の権限。

The **`<view>`** の下の要素 **`<nodemodel>`** element には、ビューに関連付けられたリストの設定が含まれます。 リストのスキーマは、 **スキーマ** の属性 **`<view>`** 要素を選択します。

リストのレコードを編集する場合、リストスキーマと同じ名前の入力フォームが暗黙的に使用されます。 The **type** 属性 **`<view>`** 要素は、フォームの表示に影響を与えます。 次のような値を選択できます。

* **listdet**：フォームをリストの下部に表示します。
* **リスト**：リストのみを表示します。 フォームは、ダブルクリックするか、リストを選択するメニューの「開く」を使用して起動します。
* **フォーム**：読み取り専用フォームを表示します。
* **editForm**：フォームを編集モードで表示します。

>[!NOTE]
>
>入力フォームの名前は、 **フォーム** 属性 **`<view>`** 要素を選択します。

リスト列のデフォルト設定は、 **`<columns>`** 要素を選択します。 列が **`<node>`** を含む要素 **xpath** 属性の値は、スキーマ内で参照されるフィールドに含まれます。

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

コマンドは、 **[!UICONTROL アクション]** リストのメニューまたは関連するメニューボタン。

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

コマンドの説明は、 **`<command>`** 要素を次のプロパティで指定します。

* **名前**：コマンドの内部名：名前は入力し、一意である必要があります。
* **ラベル**：コマンドのラベル。
* **desc**：メイン画面のステータスバーに表示される説明。
* **フォーム**：起動するフォーム：入力する値は、入力フォームの ID キーです（例：「cus:recipient」）。
* **権限**：このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。 使用可能な権限のリストには、 **[!UICONTROL 管理/アクセス管理/ネームド権限]** フォルダー。
* **promptLabel**：コマンドを実行する前に確認ボックスを表示します
* **monoSelection**：単一選択を強制します（デフォルトでは複数選択）。
* **refreshView**：コマンドの実行後に、リストを強制的に再読み込みします。
* **enabledIf**：入力された式に応じて、コマンドをアクティブにします。
* **img**：リストツールバーからコマンドにアクセスできる画像を入力します。

A **`<command>`** 要素に含めることができる要素 **`<command>`** サブ要素 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XML ドキュメントで宣言されているのと同じ順序で表示されます。

コマンド区切り文字を使用すると、コマンド間に分離バーを表示できます。 これは、 **&#39;-&#39;** の値を指定します。

オプションで **`<soapcall>`** タグに入力パラメーターを指定し、実行する SOAP メソッドの呼び出しを定義します。 SOAP API について詳しくは、 [Campaign JSAPI ドキュメント](https://experienceleague.adobe.com/developer/campaign-api/api/index.html?lang=ja).

フォームコンテキストは、初期化時に、 **`<enter>`** タグを使用します。 このタグについて詳しくは、入力フォームのドキュメントを参照してください。

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

フォルダー管理操作には次の 2 つのタイプがあります。

1. フォルダーはビューです。リストには、スキーマに関連付けられているすべてのレコードが表示され、フォルダーのプロパティに入力したシステムフィルターを使用できます。
1. フォルダーはリンクされています。リスト内のレコードはフォルダーリンク上で暗黙的にフィルターされます。

リンクされたフォルダーの場合、 **folderLink** 属性 **`<nodemodel>`** 要素を入力する必要があります。 この属性には、データスキーマで設定されたフォルダー上のリンクの名前が含まれます。

データスキーマ内のリンクされたフォルダーの宣言例：

```
<element default="DefaultFolder('nmsFolder', [@_folder-id])" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="define" revLabel="Recipients" target="xtk:folder" type="link"/>
```

の設定 **`<nodemodel>`** 「folder」という名前のフォルダーのリンク上には、次のように表示されます。

```
<nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
  img="nms:folder.png" insertRight="folderInsert" label="Recipients" name="nmsFolder">
...
</nodeModel>
```
