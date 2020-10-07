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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 2%

---


# 設定{#configuration}

ナビゲーションリストが使用するフォルダの種類は、 **xtk:navtree** スキーマの文法に従うXMLドキュメントで記述されています。

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

XMLドキュメントには、名前空間名と名前空間を指定するための、 **`<navtree>`** name **属性と****** 属性を持つrootドキュメントが含まれています。 名前と名前空間は、ドキュメントIDキーを構成します。

アプリケーションのグローバルコマンドは、ドキュメント内で **`<commands>`** 要素から宣言されます。

ファイルタイプの宣言は、次の要素を含むドキュメントで構造化されます。 **`<model>`** と **`<nodemodel>`**。

## グローバルコマンド {#global-commands}

グローバルコマンドを使用すると、アクションを起動できます。 このアクションは、入力フォームまたはSOAP呼び出しの場合があります。

グローバルコマンドは、メインの **[!UICONTROL ツール]** メニューからアクセスできます。

コマンド設定構造は次のとおりです。

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

* **name**:コマンドの内部名：名前を入力し、一意にする必要があります
* **label**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **form**:起動するフォーム：入力する値は、入力フォームのIDキーです(例：&quot;cus:受信者&quot;)
* **rights**:このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。 使用可能な権限のリストは、 **[!UICONTROL 管理/アクセス管理/ネームド権限]** (Administration/Access Management)からアクセスできます。
* **promptLabel**:コマンドを実行する前に、確認ボックスを表示します。

要素には、サブ **`<command>`** 要素を含めることがで **`<command>`** きます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XMLドキュメントで宣言されたのと同じ順序で表示されます。

コマンドセパレーターを使用すると、コマンド間に区切りバーを表示できます。 これは、コマンドラベルに含まれ **る「 —** 」値で識別されます。

タグのオプションの存在とその入力パラメーターは、実行するSOAPメソッドの呼び出しを定義します。 **`<soapcall>`** SOAP APIについて詳しくは、 [キャンペーンJSAPIドキュメントを参照してください](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)。

初期化時に、 **`<enter>`** タグからフォームコンテキストを更新できます。 このタグに関する詳細は、入力フォームに関するドキュメントを参照してください。

**例**：

* 「xtk:import」フォームを起動するグローバルコマンドの宣言：

   ```
   <command desc="Start the data import wizard" form="xtk:import" label="&amp;Data import..." name="import" rights="import,recipientImport"/>
   ```

   キーボードショートカットが&#39;I&#39;文字で宣言されるのは、コマンドラベルに **&amp;** が含まれている場合です。

* セパレーター付きサブメニューの例：

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

## フォルダーの種類 {#folder-type}

フォルダータイプを使用すると、スキーマーのデータへのアクセスを許可できます。 フォルダーに関連付けられる表示は、リストと入力フォームで構成されます。

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

フォルダー型の宣言は、 **`<model>`** 要素の下に入力する必要があります。 この要素を使用すると、 **[!UICONTROL 追加新しいフォルダー]** メニューに表示される階層組織を定義できます。 要素には、 **`<model>`** 要素と他の **`<nodemodel>`****`<model>`** 要素を含める必要があります。

**name** と **label** の属性は、要素の内部名と **[!UICONTROL 追加、]** new folderメニューに表示されるラベルに入力されます。

この **`<nodemodel>`** 要素には、次のプロパティを持つフォルダータイプの説明が含まれます。

* **name**:内部名
* **label**:label **[!UICONTROL 新しいフォルダ]** ・メニューで使用され、フォルダの挿入時にデフォルトのラベルとして使用されます。
* **img**:フォルダ挿入時の初期設定の画像。
* **hiddenCommands**:マスクするコマンドのリスト（カンマ区切り）。 可能な値：&quot;insert&quot;、&quot;delete&quot;、&quot;update&quot;、&quot;重複&quot;。
* **newFolderShortCuts**:フォルダ作成時のモデルのショートカット(**`<nodemodel>`** カンマで区切る)のリスト。
* **insertRight**, **editRight**, **deleteRight**:フォルダの挿入、編集、削除の権限。

表示の下の **`<view>`****`<nodemodel>`** 要素には、要素に関連付けられたリストの設定が含まれています。 リストのスキーマは、要素の **スキーマ** 属性に入力され **`<view>`** ます。

リストのレコードを編集するには、リストスキーマと同じ名前の入力フォームが暗黙的に使用されます。 要素の **type属性は、フォームの表示に影響を与え****`<view>`** ます。 次のような値を選択できます。

* **listdet**:リストの下部にフォームを表示します。
* **リスト**:リストのみを表示します。 フォームは、重複をクリックするか、リストを選択するメニューの「開く」を使用して起動します。
* **form**:読み取り専用フォームを表示します。
* **editForm**:フォームを編集モードで表示します。

>[!NOTE]
>
>入力フォームの名前は、 **要素に** form **`<view>`** 属性を入力することでオーバーロードできます。

リスト列のデフォルト設定は、要素を介して入力され **`<columns>`** ます。 列が、スキーマ内で参照されるフィールドを値として持つ **`<node>`** xpath **** 属性を含む要素で宣言されている。

**例**:&quot;nms:folder&quot;スキーマーでの受信者ータイプの宣言。

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

ショートカットコマンドを使用すると、リストの選択時にアクションを起動できます。 アクションは、入力フォームまたはSOAP呼び出しの場合があります。

コマンドは、リストの **[!UICONTROL アクション]** メニューまたは関連するメニューボタンからアクセスできます。

コマンド設定構造は次のとおりです。

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

次のプロパティを使用して、 **`<command>`** 要素にコマンドの説明を入力します。

* **name**:コマンドの内部名：名前を入力し、一意にする必要があります。
* **label**:コマンドのラベル。
* **desc**:メイン画面のステータスバーに表示される説明。
* **form**:起動するフォーム：入力する値は、入力フォームのIDキーです(例：「cus:受信者」)。
* **rights**:このコマンドへのアクセスを許可するネームド権限のリスト（コンマ区切り）。 使用可能な権限のリストは、 **[!UICONTROL 管理/アクセス管理/ネームド権限]** (Administration/Access Management)からアクセスできます。
* **promptLabel**:コマンドの実行前に確認ボックスを表示する
* **monoSelection**:モノラル選択にします（デフォルトでは複数選択）。
* **refreshView**:コマンドの実行後にリストを強制的に再読み込みします。
* **enabledIf**:入力した式に応じて、コマンドをアクティブにします。
* **img**:リストツールバーからコマンドにアクセスできるように画像を入力します。

要素には、サブ **`<command>`** 要素を含めることがで **`<command>`** きます。 この場合、親要素を使用すると、これらの子要素で構成されるサブメニューを表示できます。

コマンドは、XMLドキュメントで宣言されたのと同じ順序で表示されます。

コマンドセパレーターを使用すると、コマンド間に区切りバーを表示できます。 これは、コマンドラベルに含まれ **る「 —** 」値で識別されます。

タグのオプションの存在とその入力パラメーターは、実行するSOAPメソッドの呼び出しを定義します。 **`<soapcall>`** SOAP APIについて詳しくは、 [キャンペーンJSAPIドキュメントを参照してください](https://docs.adobe.com/content/help/en/campaign-classic/technicalresources/api/index.html)。

初期化時に、 **`<enter>`** タグを使用してフォームコンテキストを更新できます。 このタグに関する詳細は、入力フォームのドキュメントを参照してください。

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

1. フォルダは表示です。リストには、スキーマのプロパティに入力されたシステムフィルタリングの可能性を含め、フォルダに関連付けられたすべてのレコードが表示されます。
1. フォルダーはリンクされています。リストー内のレコードは、フォルダーリンクで暗黙的にフィルターされます。

リンクされたフォルダーの場合、 **要素のfolderLink****`<nodemodel>`** 属性を設定する必要があります。 この属性には、データスキーマーで設定されたフォルダー上のリンクの名前が含まれます。

データスキーマー内のリンクフォルダーの宣言の例：

```
<element default="DefaultFolder('nmsFolder')" label="Folder" name="folder" revDesc="Recipients in the folder" revIntegrity="own" revLabel="Recipients" target="xtk:folder" type="link"/>
```

「folder」という名前のフォルダー **`<nodemodel>`** のリンク上でのの設定は次のとおりです。

```
<nodeModel deleteRight="folderDelete" editRight="folderEdit" folderLink="folder"
  img="nms:folder.png" insertRight="folderInsert" label="Recipients" name="nmsFolder">
...
</nodeModel>
```

