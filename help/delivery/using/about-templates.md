---
title: テンプレートについて
seo-title: テンプレートについて
description: テンプレートについて
seo-description: null
page-status-flag: never-activated
uuid: 13b5ad3a-aded-43b8-ae4d-c23aa7bc17bd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: using-delivery-templates
discoiquuid: 22e289d0-c33c-4daa-a893-b292e523f30b
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 7dbc876fae0bde78e3088ee1ab986cd09e9bcc38

---


# テンプレートについて{#about-templates}

配信設定は、再利用できるように配信テンプレートに保存できます。テンプレートには配信の完全な設定を保存したり、部分的な設定のみ保存したりできます。

配信テンプレートは、この章で説明するように、手動で実行したり、イベント（所定の時刻や、サーバーへのファイル到着時など）に応じて実行したりできます。配信テンプレートは、ツリー内のノード **[!UICONTROL Resources > Templates > Delivery templates]** を介して設定できます。

![](assets/s_user_template_list.png)

テンプレートには次の 2 つのタイプがあります。

1. Adobe Campaign のネイティブ配信テンプレート

   ネイティブテンプレートは絶対にシステムから削除しないでください。各種の配信チャネルで使用する必要最小限の設定内容がネイティブテンプレートに含まれています。ただし、特定の機能を制限する目的や、ユーザーに独自のデフォルト設定（トラッキングの有効化、送信者 E メールアドレスなど）を提供する目的のために Adobe Campaign 管理者が変更を加えることは可能です。テンプレートのリスト上では、ネイティブシナリオは太字で表示されます。変更する場合は、コピーを作成する必要があります。

1. 事前定義済みの配信テンプレート

   Adobe Campaign 管理者は、新しい配信テンプレートを作成できます。作成した配信テンプレートは、オペレーター（適切なアクセス権を持っている場合）が再利用することも、サーバープロセスを使用して自動的に再利用することもできます。例えば、E メール配信テンプレートを設定しておくと、ユーザーがそのテンプレートを使用して配信を作成する際は、単にテキストまたは HTML コンテンツを入力して配信するだけで済みます。その他の選択項目は、管理者によって既に設定されています。

>[!NOTE]
>
>使用できるテンプレートの種類は、ユーザー自身が持つアクセス権、ユーザーのインスタンス設定およびコンテキストによって異なります。例えば、情報サービスを作成する際に、確認メッセージ用の配信テンプレートをリンクするとします。その場合にアクセスできるテンプレートは、ターゲットマッピングが購読マッピングであるテンプレートのみです。詳しくは、「ターゲットマッピングの選択」 [および「サービスと購読につ](../../delivery/using/selecting-a-target-mapping.md) いて」を参照してください [](../../delivery/using/about-services-and-subscriptions.md)。
