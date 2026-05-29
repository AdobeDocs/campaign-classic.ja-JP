---
product: campaign
title: アクセス管理
description: アクセス管理のベストプラクティスについて詳しく見る
feature: Installation, Access Management, Permissions
exl-id: af88e4e7-0ee3-48b4-9db4-7dd390d9d46a
TQID: https://experienceleague.adobe.com/dbC74X04V5SFr7fWOl1b0-Br-x-jjHFNvMSX9Y6M-JQ
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: e0eb8757-182f-49f3-94a4-1587d16f5094id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
feature_v2: []
subfeature_v2: []
source-git-commit: bb41e9407ab5853b0194bb325bbf3f17bc3ea232
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 12%

---

# アクセス管理 {#access-management}



## Web アプリ演算子

WebApp オペレーターは管理者です。 セキュリティを強化するには、次のガイドラインに従います。

* このオペレーターから右という名前の管理者を新しい管理者に置き換えます（「webapp」という名前にすることができます）。 詳しくは、[このページ](../../platform/using/access-management.md)を参照してください。

* 受信者に読み取り/書き込みアクセス権を付与するには、フォルダー（主に受信者フォルダー）にwebApp オペレーターを追加します。 詳しくは、[このページ](../../platform/using/access-management.md)を参照してください。

* マルチブランド（またはマルチジオ）インスタンスを使用する場合は、web アプリケーションへのアクセスを異なる受信者フォルダーに分割する必要がある場合があります。 それには、次の手順に従います。

   1. WebApp オペレーターの複製

   1. 重複ごとに名前を入力します。 例：webapp_brand、webapp_brand2など

   1. ブランドごとに1つのテンプレートを持つようにweb アプリケーションテンプレートを複製し、「特定のアカウントを使用」を選択してプロパティを編集してオペレーターを変更します。  詳しくは、[このページ](../../web/using/defining-web-forms-properties.md)を参照してください。

## セキュリティグループと管理者オペレーター

十分なセキュリティグループを作成して、オペレーターに必要な権限を与え、その他の権限を与えないようにします。

管理者演算子を使用しない（または共有しない）。 物理ユーザーごとに1つのオペレーターを作成します（正確な監査/ロギングを行う）。 新しい名前の管理者を管理者グループに追加します。 管理者演算子を使用しない場合は、削除せず、無効にしないでください。この演算子は、内部的に処理を実行するために使用されます。 ただし、クライアントコンソール ](../../platform/using/access-management.md)への[ アクセスを禁止し、（localhostに）セキュリティゾーンを制限できます。

管理者グループ（または管理者の名前付き権限）に演算子を追加しすぎないようにします。 これらのオペレーターは非常に強力です（すべての SQL 文の実行、サーバーでのコマンドの実行などができます）。

Adobe Campaignは、[名前付き権限](../../platform/using/access-management.md#named-rights)を通じて3つの高レベル権限を提供します。

* **管理** （管理者）：すべての名前付き権限チェックをバイパスして、すべてをアクセスできるようにし、すべてを実行できるようにします。これにより、プログラム実行（createProcess）とSQLの名前付き権限が含まれます

* **プログラム実行** （createProcess）: （サーバー上で）外部プログラムを実行できます

* **SQL**: データベースでSQL スクリプトを実行できます（セキュリティ モデルを回避できます）。 注意：複雑な計算（例えば、フィルタリング）を実行する必要がある場合は、データベース管理者にSQL関数を作成し、SQL許可リストに追加するように依頼できます。 詳しくは、[このページ](../../installation/using/scripting-coding-guidelines.md)を参照してください。

* **少数の（そして信頼できる）演算子に付与**
