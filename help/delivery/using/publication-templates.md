---
title: パブリッシュテンプレート
seo-title: パブリッシュテンプレート
description: パブリッシュテンプレート
seo-description: null
page-status-flag: never-activated
uuid: 1976f70c-b2d8-44ca-8fc3-6451fb67d18b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: content-management
discoiquuid: 279b0ae6-2578-4f1f-af59-13a1a9c80b32
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# パブリッシュテンプレート{#publication-templates}

## パブリッシュテンプレートについて {#about-publication-templates}

パブリッシュテンプレートは、パブリッシュするコンテンツの ID カードです。パブリッシュプロセスで使用する次のリソースを参照します。

* データスキーマ
* 入力フォーム
* 各出力ドキュメントの変換テンプレート

## パブリッシュテンプレートの識別 {#identification-of-a-publication-template}

パブリッシュテンプレートは、名前と名前空間で識別されます。

The identification key of a stylesheet is a string made up of the namespace and the name separated by a colon; for example: **cus:newsletter**.

>[!NOTE]
>
>実際には、スキーマ、フォーム、パブリッシュテンプレートに同じキーを使用することをお勧めします。

## パブリッシュテンプレートの作成と設定 {#creating-and-configuring-the-template}

パブリケーションテンプレートは、デフォルトでノードに保存 **[!UICONTROL Administration > Configuration > Publication templates]** されます。 To create a new template, click the **[!UICONTROL New]** button above the list of templates.

パブリッシュテンプレートを設定するには、テンプレートの名前（名前と名前空間で構成される識別キー）、テンプレートのラベル、データスキーマ、テンプレートがリンクされる入力フォームを入力します。

![](assets/d_ncs_content_model.png)

>[!NOTE]
>
>ラベルは、このパブリッシュテンプレートをベースとしてコンテンツを作成する際には常に表示されます。

「**コンテンツの生成前にステータスを確認**」オプションを選択すると、ファイル生成の条件として、コンテンツインスタンスのステータスが「検証済み」になっているかを確認します。For more on this, refer to [Publication](#publication).

変換テンプレートは出力ドキュメントごとに追加する必要があります。変換テンプレートは必要な数だけ作成できます。

The **[!UICONTROL Name of template]** field is a free label that describes the type of rendering at the output. 変換テンプレートごとに、タブのパブリッシュ設定を使用できます。

### レンダリング {#rendering}

タブで、 **[!UICONTROL Rendering]** 次を選択します。

* 出力ドキュメントの投影に使用するレンダリングのタイプ。XSLスタイルシートまたはJavaScriptテンプレート、
* 出力ドキュメントの形式：HTML、テキスト、XMLまたはRTF、
* 構成データ（使用するスタイルシートまたは JavaScript テンプレート）があるテンプレート

### パブリッシュ {#publication}

Publication involves generating the output document in the form of a file, if the type selected is **[!UICONTROL File]**.

![](assets/d_ncs_content_model2.png)

次のパブリッシュオプションを使用できます。

* The output file encoding character set can be forced via the **[!UICONTROL Encoding]** field. デフォルトでは、ラテン 1 (1252) 文字セットが使用されます。
* The **[!UICONTROL Multi-file generation]** option activates a special document publication mode. このオプションによって、出力ドキュメントの各ページの先頭にパーティションタグが入力されます。コンテンツを生成すると、入力されているパーティションタグごとにファイルが作成されます。このモードは、コンテンツブロックからミニサイトを生成するために使用されます。 for more on this, refer to [Multi-file generation](#multi-file-generation).
* The **[!UICONTROL Location]** field contains the name of the output file. ファイル名を自動生成するために、複数の変数で構成される名前にすることができます。

   変数は次の形式で入力されます。**`$(<xpath>)`。ここで、 `<xpath>` はパブリケーションテンプレートデータスキーマのフィールドのパスです。

   ファイルの名前は、日付タイプのフィールドで構成することもできます。このフィールドを正しく書式設定するには、フィールドのパスと出力フォーマットをパラメーターとして、**$date-format** 関数を使用します。

   デフォルトでは、ファイル名の構成フォーマットに「@name」フィールドと「@date」フィールドの変数を使用します。

   ```
   ct_$(@name)_$date-format(@date,'%4Y%2M%2D').htm
   ```

   生成されたファイル名は、ct_news12_20110901.htm のようになります。

   >[!NOTE]
   >
   >コンテンツの生成について詳しくは、「コンテンツインスタ [ンスの作成」を参照してくださ](../../delivery/using/using-a-content-template.md#creating-a-content-instance)い。

### 配信 {#delivery}

このタブでは、コンテンツ上で直接配信を開始するためのシナリオを選択できます。E メールのコンテンツは、出力フォーマット（HTML またはテキスト）に基づいて自動的に入力されます。

![](assets/d_ncs_content_model3.png)

>[!NOTE]
>
>For an example of delivery creation based on a content, refer to [Delivering a content instance](../../delivery/using/using-a-content-template.md#delivering-a-content-instance).

### 集約 {#aggregator}

スクリプトまたはクエリのリストからデータを集約し、コンテンツデータにより XML ドキュメントを高度なものにできます。その目的は、リンクが参照している特定の情報を補足したり、データベースから要素を追加したりすることです。

### マルチファイル生成 {#multi-file-generation}

To activate multiple file generation, select the **[!UICONTROL Multi-file generation]** option in the publication model. このオプションによって、出力ドキュメントの各ページの先頭に対して、スタイルシート内にパーティションタグを指定できます。コンテンツを生成すると、パーティションタグが出現するたびにファイルが作成されます。

パーティションタグは、次のようにスタイルシート内に組み込まれます。

**`<xsl:comment> #nl:output_replace(<name_of_file>) </xsl:comment>`** ここ **`<name_of_file>`** で、は生成するページのファイル名です。

**例：**「cus:book」スキーマを使用した複数のファイル生成

原理は、複数の章をリストするメインページを生成し、外部ページに章の詳細を表示できるようにするということです。

![](assets/d_ncs_content_chunk.png)

対応するスタイルシート（「cus:book.xsl」）は次のようになります。

```
<?xml version="1.0" encoding="ISO-8859-1" ?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output encoding="ISO-8859-1" method="html"/>

  <!-- Style sheet entry point -->
  <xsl:template match="/book">
    <html>
      <body>
        <h1><xsl:value-of select="@name"/></h1>
        <lu>
          <xsl:for-each select="chapter">
            <li><a target="_blank" href="chapter{@id}.htm"><xsl:value-of select="@name"/></a></li>  
          </xsl:for-each>
       </lu>
      </body>
    </html>
   </xsl:template>
</xsl:stylesheet>
```

章の詳細を生成するために、2 つ目のスタイルシート（「cus:chapter.xsl」）が必要です。

```
<?xml version="1.0" encoding="ISO-8859-1" ?>
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
  <xsl:output encoding="ISO-8859-1" method="html"/>

  <!-- Detail of a chapter -->
  <xsl:template match="chapter">
    <!-- Cut tag -->   
    <xsl:comment> #nl:output_replace($(path)/chapter<xsl:value-of select="@id"/>.htm)</xsl:comment>
    
    <html>
      <body>
        <h1><xsl:value-of select="@name"/></h1>
        <xsl:value-of select="page" disable-output-escaping="yes"/>
      </body>
    </html>
  </xsl:template>

  <!-- Style sheet entry point -->
  <xsl:template match="/book">
    <xsl:apply-templates/>
   </xsl:template>
</xsl:stylesheet>
```

生成するファイルに含めるページの先頭に、パーティションタグを入力します。

```
<xsl:comment> #nl:output_replace($(path)/<xsl:value-of select="@id"/>.htm)</xsl:comment>
```

The filename is constructed with the **$(path)** variable containing the publication path and **`<xsl:value-of select="@id" />`**, which matches the identifier of the chapter in the input document.

パブリッシュモデルは、「cus:book.xsl」と「cus:chapter.xsl」の 2 つのスタイルシートを使用して設定する必要があります。

The **[!UICONTROL Multi-file generation]** option must be active on the chapter transformation model:

![](assets/d_ncs_content_chunk2.png)

The **[!UICONTROL Location]** field is not used in the generation of multiple files, but you must still populate this field to avoid an error when publishing.
