---
product: campaign
title: アクセス管理
description: アクセス管理のベストプラクティスの詳細を説明します
feature: Installation, Access Management, Permissions
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classicv7 にのみ適用"
exl-id: af88e4e7-0ee3-48b4-9db4-7dd390d9d46a
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 29%

---

# アクセス管理 {#access-management}



## Web アプリのオペレーター

デフォルトでは、webApp オペレーターは管理者です。セキュリティを強化するには、次のガイドラインに従います。

* このオペレーターの管理ネームド権限を新しいオペレーターに置き換えます（「webapp」という名前を使用できます）。 詳しくは、[このページ](../../platform/using/access-management.md)を参照してください。

* WebApp オペレーターをフォルダー（主に受信者フォルダー）に追加して、受信者に読み取り/書き込みアクセス権を付与します。 詳しくは、[このページ](../../platform/using/access-management.md)を参照してください。

* マルチブランド（または複数地域）インスタンスを使用する場合、Web アプリケーションのアクセスを様々な受信者フォルダーに分割する必要が生じる場合があります。 それには、次の手順に従います。

   1. WebApp オペレーターを複製

   1. 各複製の名前を入力します。 例：webapp_brand、webapp_brand2 など。

   1. Web アプリケーションテンプレートを複製して、ブランドごとに 1 つのテンプレートを作成し、プロパティを編集して、「特定のアカウントを使用」を選択してオペレーターを変更します。  詳しくは、[このページ](../../web/using/defining-web-forms-properties.md)を参照してください。

## セキュリティグループと管理オペレーター

オペレーターに十分な権限を与えて、必要な操作を行うだけでなく、必要な操作を行うだけの十分なセキュリティグループを作成します。

管理オペレーターは使用しない（または共有しない）ようにします。（正確な監査やログ記録をさせるために）物理ユーザーごとに 1 人のオペレーターを作成します。新しく名前を付けた管理者を管理グループに追加します。admin 演算子を使用しない場合は、削除せず、無効にしないでください。この演算子は内部的に処理を実行するために使用されます。 しかし、禁止できます [クライアントコンソールへのアクセス](../../platform/using/access-management.md) セキュリティゾーンを（localhost に）制限します。

管理グループの（または、管理ネームド権限がある）オペレーターの数が多くなりすぎないようにします。これらのオペレーターは非常に強力です（すべての SQL 文の実行、サーバーでのコマンドの実行などができます）。

Adobe Campaignは、 [ネームド権限](../../platform/using/access-management.md#named-rights):

* **管理** (admin)：すべての項目にアクセスし、すべての操作を実行できます。すべてのネームド権限チェックをバイパスして、PROGRAM EXECUTION(createProcess) および SQL ネームド権限が含まれます。

* **プログラムの実行** (createProcess):（サーバー上で）外部プログラムを実行できます。

* **SQL**：データベースで SQL スクリプトを実行できます（セキュリティモデルをバイパスできます）。 注意：複雑な計算（フィルタリングなど）を実行する必要がある場合は、データベース管理者に SQL 関数を作成してに追加するように依頼でき許可リストに加えるます。 詳しくは、[このページ](../../installation/using/scripting-coding-guidelines.md)を参照してください。

* **なるべく少数の（信頼できる）オペレーターにのみ付与します**
