---
product: campaign
title: データパッケージの使用
description: データパッケージの使用
feature: Data Management, Package Export/Import
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: platform
content-type: reference
topic-tags: administration-basics
exl-id: d3369b63-a29b-43b7-b2ad-d36d4f46c82e
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: ht
source-wordcount: '2544'
ht-degree: 100%

---

# データパッケージの使用{#working-with-data-packages}



## データパッケージについて {#about-data-packages}

Adobe Campaign では、パッケージシステムを通じて、プラットフォーム設定とデータをエクスポートまたはインポートできます。パッケージには、様々な種類の設定や要素を含めることができ、フィルターされている場合とそうでない場合があります。

データパッケージを使用すると、XML 形式のファイル経由で Adobe Campaign データベース内のエンティティを表示できます。パッケージに含まれる 1 つのエンティティは、それに該当するすべてのデータによって表現されます。

**データパッケージ**&#x200B;の原則とは、データの設定をエクスポートして別の Adobe Campaign システム内に組み込むことです。この[節](#data-package-best-practices)では、一貫したデータパッケージのセットを維持する方法を説明します。

### パッケージの種類 {#types-of-packages}

エクスポート可能なパッケージとしては、ユーザーパッケージ、プラットフォームパッケージ、管理パッケージの 3 種類があります。

* **ユーザーパッケージ**：エクスポートするエンティティのリストを選択できます。このタイプのパッケージでは、依存関係の管理とエラーの検証がおこなわれます。
* **プラットフォームパッケージ**：スキーマ、JavaScript コードなど、すべての付加的な技術リソース（非標準）が含まれています。

  ![](assets/ncs_datapackage_package_platform.png)

* **管理パッケージ**：テンプレート、ライブラリなど、すべての付加的なテンプレートやビジネスオブジェクト（非標準）が含まれています。

  ![](assets/ncs_datapackage_package_admin.png)

>[!CAUTION]
>
>**プラットフォーム**&#x200B;タイプと&#x200B;**管理**&#x200B;タイプのパッケージには、事前に定義された、エクスポートするエンティティのリストが含まれます。個々のエンティティは、作成したパッケージに含まれる事前定義のリソースを削除するためのフィルター条件にリンクされています。

## データ構造 {#data-structure}

1 つのデータパッケージは、**xrk:navtree** データスキーマの文法に準拠した 1 個の構造化 XML ドキュメントによって記述されます。

データパッケージの例：

```
<package>
  <entities schema="nms:recipient">
    <recipient email="john.smith@adobe.com" lastName="Smith" firstName="John">      
      <folder _operation="none" name="nmsRootFolder"/>      
      <company _operation="none" name="Adobe"/>
    </recipient>
  </entities>
  <entities schema="sfa:company">
    <company name="Adobe">
      location city="London" zipCode="W11 2BQ"/>
    </company>
  </entities>
</package>
```

XML ドキュメントの先頭と末尾には必ず **`<package>`** 要素を記述します。それに続くすべての **`<entities>`** 要素によって、データがドキュメントタイプ別に配置されます。

1 つの **`<entities>`** 要素には、その要素の **schema** 属性で指定されたデータスキーマの形式に基づくパッケージのデータが含まれます。

パッケージ内のデータには、例えば自動生成キー（**autopk** オプション）のような、ベース間の互換性がない内部キーが含まれていてはなりません。

この例では、&quot;folder&quot; リンクと &quot;company&quot; リンクが、宛先テーブル内のいわゆる &quot;ハイレベル&quot; キーで次のように置き換えられています。

```
<recipient>
  <folder _operation="none" name="nmsRootFolder"/>
  <company _operation="none" name="Adobe"/>
</recipient>
```

**`operation`** 属性の値が &quot;none&quot; であることが、紐付けリンクの定義であることを意味します。

データパッケージの作成は、任意のテキストエディターを使って手作業でおこなうことができます。ただし、XML ドキュメントの構造は常に &quot;xtk:navtree&quot; データスキーマに準拠している必要があります。Adobe Campaign コンソールには、データパッケージのエクスポートとインポートを実行できるモジュールがあります。

## パッケージのエクスポート {#exporting-packages}

### パッケージのエクスポートについて {#about-package-export}

パッケージは次の 3 つの方法でエクスポートできます。

* **[!UICONTROL パッケージエクスポートアシスタント]**&#x200B;を使用して、単一のパッケージにオブジェクトセットをエクスポートできます。詳しくは、[パッケージへの一連のオブジェクトのエクスポート](#exporting-a-set-of-objects-in-a-package)を参照してください。
* **単一のオブジェクト**&#x200B;を右クリックして、**[!UICONTROL アクション／パッケージにエクスポート]**&#x200B;を選択して、パッケージにエクスポートできます。
* **パッケージ定義**&#x200B;を使用して、パッケージ構造を作成し、オブジェクトを追加した後、パッケージにエクスポートできます。詳しくは、 [パッケージ定義の管理](#managing-package-definitions)を参照してください。

パッケージをエクスポートしたら、そのパッケージと追加したすべてのエンティティを別の Campaign インスタンスにインポートできます。

### パッケージに含まれる一連のオブジェクトのエクスポート {#exporting-a-set-of-objects-in-a-package}

Adobe Campaign クライアントコンソールの&#x200B;**[!UICONTROL ツール／詳細設定／パッケージをエクスポート]**&#x200B;メニューを選択すると、パッケージエクスポートアシスタントにアクセスできます。

![](assets/ncs_datapackage_typepackage.png)

アシスタントでは、これら 3 種類のパッケージを以下に示す手順で扱います。

1. エクスポートの対象とするエンティティのリストをドキュメントタイプ別に表示します。

   ![](assets/ncs_datapackage_export2.png)

   >[!CAUTION]
   >
   >エクスポートの対象が&#x200B;**[!UICONTROL オファーカテゴリ]**、**[!UICONTROL オファー環境]**、**[!UICONTROL プログラム]**&#x200B;または&#x200B;**[!UICONTROL プラン]**&#x200B;タイプのフォルダーである場合は、**xtk:folder** を絶対に選択しないでください。選択するとデータの一部が失われることがあります。フォルダーに対応するエンティティ（オファーカテゴリには **nms:offerCategory**、オファー環境には **nms:offerEnv**、プログラムには **nms:program**、プランには **nms:plan**）を選択します。

   リスト管理機能により、エクスポートの対象として設定に含めるエンティティを追加および削除できます。新しいエンティティを追加するには「**[!UICONTROL 追加]**」をクリックします。

   「**[!UICONTROL 詳細]**」ボタンをクリックすると、選択されている設定内容を編集できます。

   >[!NOTE]
   >
   >エンティティのエクスポート処理の流れは、依存関係メカニズムによってコントロールされます。詳しくは、[依存関係の管理](#managing-dependencies)を参照してください。

1. エンティティ設定画面で、抽出するドキュメントのタイプに関するフィルタークエリを定義します。

   ここでは、データ抽出用のフィルタリング節を設定する必要があります。

   ![](assets/ncs_datapackage_export4.png)

   >[!NOTE]
   >
   >Query Editor については、[この節](../../platform/using/about-queries-in-campaign.md)を参照してください。

1. 「**[!UICONTROL 次へ]**」をクリックし、抽出処理時にデータの順序を決める並べ替え基準の列を選択します。

   ![](assets/ncs_datapackage_export5.png)

1. エクスポートを実行する前に、抽出するデータのプレビューを確認します。

   ![](assets/ncs_datapackage_export6.png)

1. パッケージエクスポートアシスタントの最終ページで、エクスポートを開始します。「**[!UICONTROL ファイル]**」フィールドで指定されたファイルにデータが格納されます。

   ![](assets/ncs_datapackage_export7.png)

### 依存関係の管理 {#managing-dependencies}

Adobe Campaign のエクスポートメカニズムでは、エクスポートされる様々な要素間のリンクをトラッキングできます。

このメカニズムは次の 2 つのルールに基づいて機能します。

* リンクの整合性タイプ **own** または **owncopy** を使ってリンクされたオブジェクトは、エクスポート対象オブジェクトと同じパッケージに含めてエクスポートされます。
* リンクの整合性タイプ **neutral** または **define** を使ってリンク（定義リンク）されたオブジェクトは、別途エクスポートする必要があります。

>[!NOTE]
>
>スキーマ要素に関連付けられる整合性タイプの定義については、[この節](../../configuration/using/database-mapping.md#links--relation-between-tables)を参照してください。

#### キャンペーンのエクスポート {#exporting-a-campaign}

キャンペーンをエクスポートする方法の例を以下に示します。エクスポートするマーケティングキャンペーンには、「MyWorkflow」フォルダー（ノード：管理／プロダクション／テクニカルワークフロー／キャンペーンプロセス／MyWorkflow）内のタスク（ラベル：「MyTask」）およびワークフロー（ラベル：「CampaignWorkflow」）が含まれます。

タスクとワークフローはキャンペーンと同じパッケージ内にエクスポートされます。これは、対応するスキーマが &quot;own&quot; 整合性タイプのリンクで結びつけられているからです。

パッケージの内容：

```
<?xml version='1.0'?>
<package author="Administrator (admin)" buildNumber="7974" buildVersion="7.1" img=""
label="" name="" namespace="" vendor="">
 <desc></desc>
 <version buildDate="2013-01-09 10:30:18.954Z"/>
 <entities schema="nms:operation">
  <operation duration="432000" end="2013-01-14" internalName="OP1" label="MyCampaign"
  modelName="opEmpty" start="2013-01-09">
   <controlGroup>
    <where filteringSchema=""/>
   </controlGroup>
   <seedList>
    <where filteringSchema="nms:seedMember"></where>
    <seedMember internalName="SDM1"></seedMember>
   </seedList>
   <parameter useAsset="1" useBudget="1" useControlGroup="1" useDeliveryOutline="1"
   useDocument="1" useFCPValidation="0" useSeedMember="1" useTask="1"
   useValidation="1" useWorkflow="1"></parameter>
   <fcpSeed>
    <where filteringSchema="nms:seedMember"></where>
   </fcpSeed>
   <owner _operation="none" name="admin" type="0"/>
   <program _operation="none" name="nmsOperations"/>
   <task end="2013-01-17 10:07:51.000Z" label="MyTask" name="TSK2" start="2013-01-16 10:07:51.000Z"
   status="1">
    <owner _operation="none" name="admin" type="0"/>
    <operation _operation="none" internalName="OP1"/>
    <folder _operation="none" name="nmsTask"/>
   </task>
   <workflow internalName="WKF12" label="CampaignWorkflow" modelName="newOpEmpty"
   order="8982" scenario-cs="Notification of the workflow supervisor (notifySupervisor)"
   schema="nms:recipient">
    <scenario internalName="notifySupervisor"/>
    <desc></desc>
    <folder _operation="none" name="Folder4"/>
    <operation _operation="none" internalName="OP1"/>
   </workflow>
  </operation>
 </entities>
</package>   
```

パッケージのタイプに対する所属関係は、スキーマ内では **@pkgAdmin および @pkgPlatform** 属性によって定義されています。どちらの属性にも、パッケージへの所属条件を定義する XTK 式が指定されます。

```
<element name="offerEnv" img="nms:offerEnv.png" 
template="xtk:folder" pkgAdmin="@id != 0">
```

最後に、**@pkgStatus** 属性は、これらの要素または属性に関するエクスポートルールの定義に使われます。この属性の値に応じて、該当する要素または属性はエクスポートされるパッケージに含まれます。この属性に指定できる値は次の 3 種類です。

* **never**：そのフィールドやリンクをエクスポートしない
* **always**：そのフィールドを必ずエクスポートする
* **preCreate**：リンクされたエンティティの作成を許可する

>[!NOTE]
>
>**preCreate** 値は、リンクタイプのイベントに対してのみ使用できます。この値を指定すると、エクスポートされるパッケージ内のまだロードされていないエンティティを参照するリンクを作成することが認められます。

## パッケージ定義の管理 {#managing-package-definitions}

パッケージ定義では、パッケージ構造を作成し、エンティティを追加してから、単一のパッケージにエクスポートできます。その後、このパッケージと追加されたすべてのエンティティを他の Campaign インスタンスにインポートできます。

**関連トピック：**

* [パッケージ定義の作成](#creating-a-package-definition)
* [パッケージ定義へのエンティティの追加](#adding-entities-to-a-package-definition)
* [パッケージ定義の生成に関する設定](#configuring-package-definitions-generation)
* [パッケージ定義からのパッケージのエクスポート](#exporting-packages-from-a-package-definition)

### パッケージ定義の作成 {#creating-a-package-definition}

パッケージ定義には、**[!UICONTROL 管理／設定／パッケージ管理／パッケージ定義]**&#x200B;メニューからアクセスできます。

パッケージ定義を作成するには、「**[!UICONTROL 新規]**」ボタンをクリックし、パッケージ定義の一般情報を入力します。

![](assets/packagedefinition_create.png)

その後、パッケージ定義にエンティティを追加し、XML ファイルパッケージにエクスポートします。

**関連トピック：**

* [パッケージ定義へのエンティティの追加](#adding-entities-to-a-package-definition)
* [パッケージ定義の生成に関する設定](#configuring-package-definitions-generation)
* [パッケージ定義からのパッケージのエクスポート](#exporting-packages-from-a-package-definition)

### パッケージ定義へのエンティティの追加 {#adding-entities-to-a-package-definition}

「**[!UICONTROL コンテンツ]**」タブで「**[!UICONTROL 追加]**」ボタンをクリックし、パッケージとしてエクスポートするエンティティを選択します。エンティティを選択する際のベストプラクティスについては、[この節](#exporting-a-set-of-objects-in-a-package)を参照してください。

![](assets/packagedefinition_addentities.png)

エンティティは、インスタンス内の場所から直接パッケージ定義に追加できます。これをおこなうには、以下の手順に従います。

1. 目的のエンティティを右クリックして、**[!UICONTROL アクション／パッケージにエクスポート]**&#x200B;を選択します。

   ![](assets/packagedefinition_singleentity.png)

1. **[!UICONTROL パッケージ定義に追加]**&#x200B;を選択し、エンティティを追加するパッケージ定義を選択します。

   ![](assets/packagedefinition_packageselection.png)

1. エンティティをパッケージ定義に追加すると、そのエンティティがパッケージとしてエクスポートされます（[この節](#exporting-packages-from-a-package-definition)を参照）。

   ![](assets/packagedefinition_entityadded.png)

### パッケージ定義の生成の設定 {#configuring-package-definitions-generation}

パッケージの生成は、パッケージ定義の「**[!UICONTROL コンテンツ]**」タブで設定できます。設定をおこなうには、「**[!UICONTROL 生成パラメーター]**」リンクをクリックします。

![](assets/packagedefinition_generationparameters.png)

* **[!UICONTROL 定義を含める]**：パッケージ定義で現在使用されている定義を含めます。
* **[!UICONTROL インストールスクリプトを含める]**：パッケージのインポート時に実行する JavaScript スクリプトを追加できます。選択すると、パッケージ定義画面に「**[!UICONTROL スクリプト]**」タブが表示されます。
* **[!UICONTROL デフォルト値を含める]**：すべてのエンティティ属性の値をパッケージに追加します。

  このオプションは、エクスポート内容が長くなりすぎないように、デフォルトでは選択されません。つまり、デフォルト値（スキーマで別途定義されていない場合の、空の文字列、「0」、「false」）を持つエンティティ属性はパッケージに追加されず、エクスポートもおこなわれません。

  >[!CAUTION]
  >
  >このオプションの選択を解除すると、ローカルのバージョンとインポートされたバージョンが結合されます。
  >
  >パッケージのインポート先のインスタンスに、パッケージと同じエンティティ（同じ外部 ID など）が含まれている場合は、そのエンティティの属性は更新されません。元のインスタンスにデフォルト値を持つ属性がある場合、それらがパッケージに含まれないので、こうしたことが起こります。
  >
  >この場合は「**[!UICONTROL デフォルト値を含める]**」オプションを選択すると、元のインスタンスからすべての属性がパッケージにエクスポートされるので、複数のバージョンが結合されることはありません。

### パッケージ定義からのパッケージのエクスポート {#exporting-packages-from-a-package-definition}

パッケージ定義からパッケージをエクスポートするには、以下の手順に従います。

1. エクスポートするパッケージ定義を選択し、「**[!UICONTROL アクション]**」ボタンをクリックし、「**[!UICONTROL パッケージをエクスポート]**」を選択します。
1. エクスポートするパッケージに対応した XML ファイルがデフォルトで選択されます。パッケージ定義の名前空間と名前に基づいて名前が付けられます。
1. パッケージ名と場所を定義したら、「**[!UICONTROL 開始]**」ボタンをクリックしてエクスポートを開始します。

   ![](assets/packagedefinition_packageexport.png)

## パッケージのインポート {#importing-packages}

Adobe Campaign クライアントコンソールのメインメニューで&#x200B;**[!UICONTROL ツール／詳細設定／パッケージをインポート]**&#x200B;を選択すると、パッケージインポートアシスタントにアクセスできます。

ライセンス条項に応じて、（例えば、別の Adobe Campaign インスタンスから）既にエクスポートしたパッケージをインポートするか、[組み込みパッケージ](../../installation/using/installing-campaign-standard-packages.md)をインポートすることができます。

![](assets/ncs_datapackage_import.png)

### ファイルからのパッケージのインストール {#installing-a-package-from-a-file}

既存のデータパッケージをインポートするには、パッケージの XML ファイルを選択し、「**[!UICONTROL 開く]**」をクリックします。

![](assets/ncs_datapackage_import_1.png)

インポートされるパッケージの内容が、エディターの中央部セクションに表示されます。

「**[!UICONTROL 次へ]**」、「**[!UICONTROL 開始]**」の順にクリックすると、インポートが開始されます。

![](assets/ncs_datapackage_import_2.png)

### ビルトインパッケージのインストール {#installing-a-standard-package}

標準パッケージは、Adobe Campaign の設定時にインストールされるビルトインパッケージです。権限とデプロイメントモデルに応じて、新しいオプションやアドオンを入手する場合や、新しいオファーにアップグレードする場合に、新しい標準パッケージをインポートできます。

インストールできるパッケージを確認するには、ライセンス契約を参照してください。

ビルトインパッケージについて詳しくは、[こちら](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

## データパッケージのベストプラクティス {#data-package-best-practices}

この節では、プロジェクトの全期間にわたって一貫した方法でデータパッケージを編成する方法について説明します。

パッケージには、様々な種類の設定や要素を含めることができ、フィルターされている場合とそうでない場合があります。一部の要素が見つからない場合や、要素またはパッケージが正しい順序で読み込まれない場合は、プラットフォームの設定が破損する可能性があります。

また、複数のユーザーが多数の機能を持つ同じプラットフォームで作業をおこなう場合、パッケージ仕様フォルダーがすぐに複雑化する可能性があります。

必須ではありませんが、この節では、Adobe Campaign で大規模プロジェクトのパッケージを整理して使用するのに役立つソリューションを提供します。

主な制約を次に示します。
* パッケージを整理し、変更内容と変更日時を追跡する
* 設定が更新された場合、更新に直接リンクされていない要素の破損リスクを最小限に抑える

>[!NOTE]
>
>パッケージを自動的にエクスポートするワークフローの設定について詳しくは、[このページ](https://helpx.adobe.com/jp/campaign/kb/export-packages-automatically.html)を参照してください。

### レコメンデーション {#data-package-recommendations}

必ず、同じバージョンのプラットフォーム内でインポートします。同じビルドを持つ 2 つのインスタンス間にパッケージをデプロイしていることを確認する必要があります。ビルドが異なる場合は、インポートを強制的に実行せず、最初にプラットフォームを必ず更新してください。

>[!IMPORTANT]
>
>異なるバージョン間のインポートは、アドビではサポートされていません。
<!--This is not allowed. Importing from 6.02 to 6.1, for example, is prohibited. If you do so, R&D won’t be able to help you resolve any issues you encounter.-->

スキーマとデータベースの構造に注意してください。スキーマを含むパッケージのインポートの後にスキーマの生成が必要です。

### 解決策 {#data-package-solution}

#### パッケージの種類 {#package-types}

まず、様々なタイプのパッケージを定義します。次の 4 つのタイプのみが使用されます。

**エンティティ**
* スキーマ、フォーム、フォルダー、配信テンプレートなど、Adobe Campaign 内のすべての「xtk」および「nms」固有の要素が含まれます。
* エンティティは、「admin」要素と「platform」要素の両方として見なすことができます。
* Campaign インスタンスにアップロードする際に、パッケージに複数のエンティティを含めないでください。

<!--Nothing “works” alone. An entity package does not have a specific role or objective.-->

新しいインスタンスに設定をデプロイする必要がある場合は、すべてのエンティティパッケージをインポートできます。

**機能**

このパッケージタイプには、以下が当てはまります。
* クライアントの要件や仕様に対応する。
* 1 つまたは複数の機能が含まれる。
* 他のパッケージを使用せずに機能を実行できるように、すべての依存関係を含める必要がある。

**キャンペーン**

このパッケージは必須ではありません。キャンペーンが機能として見なされる場合でも、すべてのキャンペーンに対して特定のタイプを作成すると便利です。

**アップデート**

設定が完了すると、1 つの機能を別の環境にエクスポートすることができます。例えば、開発環境からテスト環境にパッケージをエクスポートすることができます。このテストでは、欠陥が明らかになります。まず、開発環境で欠陥を修正する必要があります。次に、パッチをテストプラットフォームに適用する必要があります。

1 つ目の解決策は、機能全体を再度エクスポートすることです。ただし、リスク（不要な要素の更新）を回避するには、修正のみを含むパッケージを使用した方が安全です。

そのため、機能のエンティティタイプを 1 つだけ含む「アップデート」パッケージを作成することをお勧めします。

更新は修正になるだけでなく、エンティティ、機能、キャンペーンパッケージの新しい要素にもなります。パッケージ全体をデプロイしないようにするには、アップデートパッケージをエクスポートします。

### 命名規則 {#data-package-naming}

タイプが定義されたら、命名規則を指定する必要があります。Adobe Campaign では、パッケージ仕様のサブフォルダーを作成できません。パッケージ名を整理する最適な方法は、番号を使用することです。番号は、パッケージ名のプレフィックスとして使用します。次の規則を使用できます。

* エンティティ：1 ～ 99
* 機能：100 ～ 199
* キャンペーン：200 ～ 299
* アップデート：5000 ～ 5999

### パッケージ {#data-packages}

>[!NOTE]
>
>正しいパッケージ数を定義するためのルールを設定することをお勧めします。

#### エンティティパッケージの順序 {#entity-packages-order}

インポートを円滑におこなうために、エンティティパッケージはインポートされる順に並べる必要があります。次に例を示します。
* 001 – スキーマ
* 002 – フォーム
* 003 – 画像
* その他

>[!NOTE]
>
>フォームは、スキーマの更新後にのみインポートする必要があります。

#### パッケージ 200 {#package-200}

特定のキャンペーンに対しては、パッケージ番号「200」を使用しないでください。この番号は、すべてのキャンペーンに関する情報を更新する際に使用されます。

#### アップデートパッケージ {#update-package}

最後に、アップデートパッケージの番号について説明します。アップデートパッケージには、プレフィックスが「5」のパッケージ番号（エンティティ、機能またはキャンペーン）が割り当てられます。次に例を示します。
* 5001 で 1 つのスキーマを更新
* 5200 ですべてのキャンペーンを更新
* 5101 で 101 機能を更新

容易に再利用できるようにするために、アップデートパッケージには、特定のエンティティを 1 つだけ含める必要があります。分割するには、新しい番号（1 からの開始）を追加します。これらのパッケージに固有の順序規則はありません。例えば、101 機能（ソーシャルアプリケーション）があると仮定します。
* これには、Web アプリと外部アカウントが含まれます。
   * パッケージのラベルは「101 - ソーシャルアプリケーション（socialApplication）」です。
* Web アプリに欠陥があります。
   * Web アプリを修正します。
   * 「5101 - 1 - ソーシャルアプリケーションの Web アプリ（socialApplication_webApp）」という名前の修正パッケージを作成する必要があります。
* ソーシャル機能用に新しい外部アカウントを追加する必要があります。
   * 外部アカウントを作成します。
   * 新しいパッケージは「5101 - 2 - ソーシャルアプリケーションの外部アカウント（socialApplication_extAccount）」です。
   * 同時に、101 パッケージが更新され、外部アカウントに追加されますが、デプロイされません。
     ![](assets/ncs_datapackage_best-practices-1.png)

#### パッケージドキュメント {#package-documentation}

パッケージを更新する場合、変更内容や理由（「新しいスキーマを追加」、「欠陥を修正」など）の詳細を説明するために、必ず説明フィールドにコメントを入れてください。

![](assets/ncs_datapackage_best-practices-2.png)

また、コメントの日付も指定する必要があります。アップデートパッケージに関するコメントは常に「親」（「5」プレフィックスを含まないパッケージ）に報告してください。

>[!IMPORTANT]
>
>説明フィールドには、2,000 文字まで入力できます。
