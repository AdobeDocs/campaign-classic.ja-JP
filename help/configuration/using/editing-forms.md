---
product: campaign
title: フォームの編集
description: フォームの編集
audience: configuration
content-type: reference
topic-tags: input-forms
exl-id: 24604dc9-f675-4e37-a848-f1911be84f3e
source-git-commit: f4b9ac3300094a527b5ec1b932d204f0e8e5ee86
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 5%

---


# フォームの編集{#editing-forms}

![](../../assets/common.svg)

## 概要

マーケターやオペレーターは、入力フォームを使用して、レコードの作成、変更、プレビューをおこないます。 Formsは、情報を視覚的に表現します。

入力フォームを作成および変更できます。

* デフォルトで配信されるファクトリ入力フォームを変更できます。 ファクトリの入力フォームは、ファクトリデータスキーマに基づいています。
* 定義したデータスキーマに基づいて、カスタムの入力フォームを作成できます。

Formsは `xtk:form` タイプ。 入力フォームの構造は、 `xtk:form` スキーマ。 このスキーマを表示するには、 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL データスキーマ]** を選択します。 詳細を表示 [フォーム構造](form-structure.md).

入力フォームにアクセスするには、 **[!UICONTROL 管理] > [!UICONTROL 設定] > [!UICONTROL 入力フォーム]** メニューから、次の操作を実行します。

![](assets/d_ncs_integration_form_arbo.png)

フォームをデザインするには、XML エディターで XML コンテンツを編集します。

![](assets/d_ncs_integration_form_edit.png)

[詳細情報](form-structure.md#formatting)。

フォームをプレビューするには、 **[!UICONTROL プレビュー]** タブ：

![](assets/d_ncs_integration_form_preview.png)

## フォームタイプ

様々なタイプの入力フォームを作成できます。 フォームの種類によって、ユーザーによるフォームのナビゲーション方法が決まります。

* コンソール画面

   これはデフォルトのフォームタイプです。 フォームは単一のページで構成されます。

   ![](assets/console_screen_form.png)

* コンテンツ管理

   このフォームタイプをコンテンツ管理に使用します。 参照 [使用例](../../delivery/using/use-case--creating-content-management.md).

   ![](../../delivery/using/assets/d_ncs_content_form13.png)

* ウィザード

   このフォームは、特定のシーケンスで並べられた複数のフローティングスクリーンで構成されます。 ユーザーは画面間を移動します。 [詳細情報](form-structure.md#wizards)。

* アイコンボックス

   このフォームは複数のページで構成されます。 フォームに移動するには、フォームの左側でアイコンを選択します。

   ![](assets/iconbox_form_preview.png)

* ノートブック

   このフォームは複数のページで構成されます。 フォームに移動するには、フォーム上部のタブを選択します。

   ![](assets/notebook_form_preview.png)

* 縦長ペイン

   このフォームは、ナビゲーションツリーを表示します。

* 横長ペイン

   このフォームは、項目のリストを表示します。

## コンテナ

フォームでは、次のような様々な目的でコンテナを使用できます。

* フォーム内のコンテンツを整理する
* 入力フィールドへのアクセスを定義
* 他のフォーム内でのフォームのネスト

[詳細情報](form-structure.md#containers)。

### コンテンツを整理

コンテナを使用してフォーム内のコンテンツを整理する：

* フィールドを複数のセクションにグループ化できます。
* 複数ページのフォームにページを追加できます。

コンテナを挿入するには、 `<container>` 要素。 [詳細情報](form-structure.md#containers)。

#### グループフィールド

コンテナを使用して、入力フィールドを整理されたセクションにグループ化します。

フォームにセクションを挿入するには、次の要素を使用します。 `<container type="frame">`. （オプション）セクションタイトルを追加するには、 `label` 属性。

構文： `<container type="frame" label="`*section_title*`"> […] </container>`

この例では、コンテナによって **作成** セクション ( **[!UICONTROL 作成者]** および **[!UICONTROL 名前]** 入力フィールド：

```xml
<form _cs="Coupons (nms)" entitySchema="xtk:form" img="xtk:form.png" label="Coupons"
      name="coupon" namespace="nms" type="default" xtkschema="xtk:form">
  <input xpath="@code"/>
  <input xpath="@type"/>
  <container label="Creation" type="frame">
    <input xpath="createdBy"/>
    <input xpath="createdBy/@name"/>
  </container>
</form>
```

![](assets/console_screen_form.png)

#### 複数ページのフォームにページを追加

複数ページフォームの場合は、コンテナを使用してフォームページを作成します。

この例では、 **一般** および **詳細** フォームのページ：

```xml
<container img="ncm:book.png" label="General">
[…]
</container>
<container img="ncm:detail.png" label="Details">
[…]
</container>
```

### フィールドへのアクセスを定義

コンテナを使用して、表示内容を定義し、フィールドへのアクセスを定義します。 フィールドのグループのオン/オフを切り替えることができます。

### フォームのネスト

コンテナを使用して、他のフォーム内にフォームをネストします。 [詳細情報](#add-pages-to-multipage-forms)。

## 画像への参照

画像を検索するには、「 」を選択します。 **[!UICONTROL 管理]** > **[!UICONTROL 設定]** > **[!UICONTROL 画像]** を選択します。

画像をフォーム内の要素（アイコンなど）に関連付けるには、画像への参照を追加します。 以下を使用： `img` 属性 ( 例： `<container>` 要素。

構文: `img="`*`namespace`*`:`*`filename`*`.`*`extension`*`"`

この例では、 `book.png` および `detail.png` 画像 `ncm` 名前空間：

```xml
<container img="ncm:book.png" label="General">
[…]
</container>
<container img="ncm:detail.png" label="Details">
[…]
</container>
```

これらの画像は、ユーザーがクリックして複数ページフォームを移動するアイコンに使用されます。

![](assets/nested_forms_preview.png)
