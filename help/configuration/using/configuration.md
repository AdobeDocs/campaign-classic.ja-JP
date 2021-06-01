---
product: campaign
title: 設定
description: 設定
audience: configuration
content-type: reference
topic-tags: navigation-hierarchy
exl-id: c7ae7240-0c12-4420-bbb3-4268c9ade3e7
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 3%

---

# Campaignエクスプローラーのナビゲーションツリーの設定{#configuration}

エキスパートユーザーは、エクスプローラーツリーにフォルダーを追加してカスタマイズできます。

Campaignエクスプローラーとナビゲーション階層[について詳しくは、この節](../../platform/using/adobe-campaign-explorer.md#about-navigation-hierarchy)を参照してください。

ナビゲーションリストで使用されるフォルダーの種類は、**xtk:navtree**&#x200B;スキーマの文法に従ったXMLドキュメントに記述されています。

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

XMLドキュメントには、**name**&#x200B;属性と&#x200B;**namespace**&#x200B;属性を持つ&#x200B;**`<navtree>`**&#x200B;ルート要素が含まれ、ドキュメントの名前と名前空間を指定します。 名前と名前空間がドキュメント識別キーを構成します。

アプリケーションのグローバルコマンドは、ドキュメント内の&#x200B;**`<commands>`**&#x200B;要素から宣言されます。

ファイルタイプの宣言は、次の要素を含むドキュメント内で構造化されます。**`<model>`**&#x200B;と&#x200B;**`<nodemodel>`**&#x200B;が表示されます。

## グローバルコマンド{#global-commands}

グローバルコマンドを使用すると、アクションを開始できます。 このアクションは、入力フォームまたはSOAP呼び出しです。

グローバルコマンドは、メインの&#x200B;**[!UICONTROL ツール]**&#x200B;メニューからアクセスできます。

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

グローバルコマンドの説明は、次のプロパティを使用して&#x200B;**`<command>`**&#x200B;要素に入力します。

* **名前**:コマンドの内部名：名前を入力し、一意にする必要があります
* **ラベル**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **フォーム**:起動するフォーム：入力する値は、入力フォームの識別キーです(例：&quot;cus:recipient&quot;)
* **権限**:このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。使用可能な権限のリストには、**[!UICONTROL 管理/アクセス管理/ネームド権限]**&#x200B;フォルダーからアクセスできます。
* **promptLabel**:コマンドを実行する前に確認ボックスを表示します。

**`<command>`**&#x200B;要素には、**`<command>`**&#x200B;サブ要素を含めることができます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XMLドキュメントで宣言されているのと同じ順序で表示されます。

コマンド区切り文字を使用すると、コマンド間に区切りバーを表示できます。 これは、コマンドラベルに含まれる&#x200B;**&#39;-&#39;**&#x200B;値で識別されます。

**`<soapcall>`**&#x200B;タグとその入力パラメーターを任意に指定すると、実行するSOAPメソッドの呼び出しが定義されます。 SOAP APIについて詳しくは、[Campaign JSAPIのドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)を参照してください。

**`<enter>`**&#x200B;タグを使用した初期化時に、フォームコンテキストを更新できます。 このタグについて詳しくは、入力フォームのドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するグローバルコマンドの宣言：

   ```
   <command desc="Start the data import wizard" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
   ```

   キーボードショートカットは、コマンドラベルに&#x200B;**&amp;**&#x200B;が存在することで、&#39;I&#39;文字に宣言されます。

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

* SOAPメソッドの実行：

   ```
   <command name="cmd3" label="Example 3" promptLabel="Do you really want to execute the command?">
     <soapCall name="Execute" service="xtk:sql"/>
   </command>
   ```

## フォルダーの種類{#folder-type}

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

フォルダータイプの宣言は、**`<model>`**&#x200B;要素の下に入力する必要があります。 この要素を使用すると、**[!UICONTROL 新しいフォルダー]**&#x200B;を追加メニューから表示できる階層組織を定義できます。 **`<model>`**&#x200B;要素には、**`<nodemodel>`**&#x200B;要素と他の&#x200B;**`<model>`**&#x200B;要素を含める必要があります。

**name**&#x200B;および&#x200B;**label**&#x200B;属性は、要素の内部名と&#x200B;**[!UICONTROL 新しいフォルダーを追加]**&#x200B;メニューに表示されるラベルを設定します。

**`<nodemodel>`**&#x200B;要素には、次のプロパティを持つフォルダータイプの説明が含まれます。

* **名前**:内部名
* **ラベル**:「新しいフォルダーを追 **[!UICONTROL 加」メニ]** ューで、フォルダーを挿入する際のデフォルトのラベルとして使用されるラベル。
* **img**:フォルダー挿入時のデフォルトの画像。
* **hiddenCommands**:マスクするコマンドのリスト（コンマ区切り）。可能な値：&quot;adbnew&quot;、&quot;adbsave&quot;、&quot;adbcancel&quot;および&quot;adbdup&quot;
* **newFolderShortCuts**:フォルダー作成時のモデル(**`<nodemodel>`** コンマ区切り)のショートカットのリスト。
* **insertRight**、 **editRight**、 **deleteRight**:フォルダーの挿入、編集、削除の権限

**`<nodemodel>`**&#x200B;要素の下の&#x200B;**`<view>`**&#x200B;要素には、ビューに関連付けられたリストの設定が含まれます。 リストのスキーマは、**`<view>`**&#x200B;要素の&#x200B;**schema**&#x200B;属性に入力されます。

リストのレコードを編集するために、リストスキーマと同じ名前の入力フォームが暗黙的に使用されます。 **`<view>`**&#x200B;要素の&#x200B;**type**&#x200B;属性は、フォームの表示に影響します。 次のような値を選択できます。

* **listdet**:リストの下部にフォームを表示します。
* **リスト**:リストのみを表示します。フォームは、ダブルクリックするか、リストを選択するメニューの「開く」を使用して起動します。
* **フォーム**:読み取り専用フォームを表示します。
* **editForm**:編集モードでフォームを表示します。

>[!NOTE]
>
>**`<view>`**&#x200B;要素に&#x200B;**form**&#x200B;属性を入力すると、入力フォームの名前がオーバーロードされます。

リスト列のデフォルト設定は、**`<columns>`**&#x200B;要素を使用して入力します。 列が&#x200B;**xpath**&#x200B;属性を含む&#x200B;**`<node>`**&#x200B;要素で宣言され、スキーマ内で参照されるフィールドが値として使用されます。

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

### ショートカットコマンド{#shortcut-commands}

ショートカットコマンドを使用すると、リストの選択に関するアクションを開始できます。 アクションは、入力フォームまたはSOAP呼び出しです。

コマンドは、リストの&#x200B;**[!UICONTROL アクション]**&#x200B;メニューまたは関連するメニューボタンからアクセスできます。

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

コマンドの説明は、次のプロパティを持つ&#x200B;**`<command>`**&#x200B;要素に入力されます。

* **名前**:コマンドの内部名：名前は、入力および一意である必要があります。
* **ラベル**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **フォーム**:起動するフォーム：入力する値は、入力フォームの識別キーです(例：&quot;cus:recipient&quot;)と呼ばれます。
* **権限**:このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。使用可能な権限のリストには、**[!UICONTROL 管理/アクセス管理/ネームド権限]**&#x200B;フォルダーからアクセスできます。
* **promptLabel**:コマンドを実行する前に確認ボックスを表示します
* **monoSelection**:は、モノラル選択を強制します（デフォルトでは複数選択）。
* **refreshView**:コマンドの実行後にリストを強制的に再読み込みします。
* **enabledIf**:入力した式に応じて、コマンドをアクティブにします。
* **img**:リストツールバーからコマンドにアクセスできる画像を入力します。

**`<command>`**&#x200B;要素には、**`<command>`**&#x200B;サブ要素を含めることができます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XMLドキュメントで宣言されているのと同じ順序で表示されます。

コマンド区切り文字を使用すると、コマンド間に区切りバーを表示できます。 これは、コマンドラベルに含まれる&#x200B;**&#39;-&#39;**&#x200B;値で識別されます。

**`<soapcall>`**&#x200B;タグとその入力パラメーターを任意に指定すると、実行するSOAPメソッドの呼び出しが定義されます。 SOAP APIについて詳しくは、[Campaign JSAPIのドキュメント](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)を参照してください。

フォームコンテキストは、初期化時に&#x200B;**`<enter>`**&#x200B;タグを使用して更新できます。 このタグについて詳しくは、入力フォームのドキュメントを参照してください。

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

フォルダー管理操作には、次の2種類があります。

1. フォルダーはビューです。このリストには、スキーマに関連付けられているすべてのレコードが表示され、フォルダーのプロパティに入力したシステムフィルタリングが可能です。
1. フォルダーはリンクされています。リスト内のレコードは、フォルダーリンク上で暗黙的にフィルターされます。

リンクされたフォルダーの場合は、**`<nodemodel>`**&#x200B;要素の&#x200B;**folderLink**&#x200B;属性を設定する必要があります。 この属性には、データスキーマで設定されたフォルダー上のリンクの名前が含まれます。

データスキーマ内のリンクされたフォルダーの宣言の例：

```
<element default="DefaultFolder('nmsFolder', [@_folder-id])" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="define" revLabel="Recipients" target="xtk:folder" type="link"/>
```

「folder」という名前のフォルダーのリンク上の&#x200B;**`<nodemodel>`**&#x200B;の設定は次のとおりです。

```
<nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
  img="nms:folder.png" insertRight="folderInsert" label="Recipients" name="nmsFolder">
...
</nodeModel>
```
