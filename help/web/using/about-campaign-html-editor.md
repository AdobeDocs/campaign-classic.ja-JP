---
title: Campaign の HTML エディターについて
seo-title: Campaign の HTML エディターについて
description: Campaign の HTML エディターについて
seo-description: null
page-status-flag: never-activated
uuid: 1b1d392d-4f19-4092-b57d-02051a242675
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: web
content-type: reference
topic-tags: editing-html-content
discoiquuid: 1ffe9f58-7258-4794-a314-524065f8a33b
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: c9c9d5f96856ce9e19571bad032d2bf04eaa60bd

---


# Campaign の HTML エディターについて{#about-campaign-html-editor}

**デジタルコンテンツエディター（DCE）**&#x200B;は、HTML コンテンツエディターです。DCE を使用すると、Adobe Campaign 内で HTML 形式のテンプレートやコンテンツを容易に作成したり修正したりできます

DCE を使用すると、ページ要素を挿入および書式設定したり、HTML ページの要素にデータベースフィールドを関連付けたりできます。Web アプリケーション用のページを作成する場合や、アクティブになっているテンプレートに基づいて配信を作成する場合には、デフォルトで DCE を使用できます。

>[!NOTE]
>
>DCE で実行できるのは、この節で説明する操作のみです。
>
>サーバー側 JavaScript コードを追加したい場合は、パーソナライゼーションブロックに追加することをお勧めします。パーソナライゼーションブロックの作成と変更について詳しくは、[このページ](../../delivery/using/personalization-blocks.md)を参照してください。

>[!CAUTION]
>
>プライバシー保護のために、すべての外部リソースに対して HTTPS を使用することをお勧めします。

## コンテンツエディターの一般的な操作 {#content-editor-general-operation}

ここでは、Web アプリケーションのフレームワーク内および配信のコンテキストで、DCE で編集したコンテンツを編集およびアップロードする主な手順について説明します。

一般的な操作を次に示します。

![](assets/dce_schema.png)

シンプルな Web アプリケーションを作成する手順を次に示します。

* Web アプリケーションを作成します（詳しくは、[ランディングページの作成](../../web/using/creating-a-landing-page.md)を参照）。
* 既存のコンテンツを選択するか、標準テンプレートからのコンテンツを作成します（詳しくは、[テンプレート管理](../../web/using/template-management.md)を参照）。
* コンテンツを編集および設定します（詳しくは、[コンテンツの編集](../../web/using/editing-content.md)を参照）。
* Web アプリケーションをパブリッシュします（詳しくは、[コンテンツのパブリッシュ](../../web/using/creating-a-landing-page.md#step-3---publishing-content)および[このページ](../../web/using/publishing-a-web-form.md#managing-web-forms-delivery-and-tracking)を参照）。

>[!NOTE]
>
>Web アプリケーションのフレームワーク内での DCE の実装の完全な例について詳しくは、[ランディングページの作成](../../web/using/creating-a-landing-page.md)を参照してください。

E メール配信を作成する手順は、次のとおりです。

* DCE がアクティブな E メールタイプのテンプレートから配信を作成します。
* 既存のコンテンツを選択するか、標準テンプレートからコンテンツを作成します。
* オンラインコンテンツを編集および設定します。
* 配信を送信します（詳しくは、[この節](../../delivery/using/communication-channels.md)を参照）。

>[!NOTE]
>
>E メール配信のフレームワーク内での DCE の実装の完全な例について詳しくは、[この使用例](../../web/using/use-case--creating-an-email-delivery.md)を参照してください。

