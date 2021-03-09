---
solution: Campaign Classic
product: campaign
title: アクセス管理
description: アクセス管理のベストプラクティスの詳細を表示します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: f03554302c77a39a3ad68d47417ed930f43302b7
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 37%

---


# アクセス管理 {#access-management}

## WebAppの演算子

デフォルトでは、webApp オペレーターは管理者です。セキュリティを向上させるには、次のガイドラインに従います。

* この演算子から「right」という名前の管理者を新しい管理者に置き換えます（「webapp」という名前を付けることができます）。 詳しくは、[このページ](../../platform/using/access-management.md)を参照してください。

* フォルダー(主に受信者フォルダー)内のwebApp演算子追加。受信者に読み取り/書き込みアクセス権を付与します。 詳しくは、[こちらのページ](../../platform/using/access-management.md)を参照してください。

* マルチブランド（または複数の地域）のインスタンスを使用する場合は、Webアプリケーションのアクセスを様々な受信者フォルダーに分割する必要があります。 それには、次の手順に従います。

   1. webApp演算子の重複

   1. 各重複の名前を入力します。 次に例を示します。webapp_brand、webapp_brand2など

   1. Webアプリケーションテンプレートを重複し、ブランドごとに1つのテンプレートを作成します。また、「Use a specific account」を選択して、プロパティを編集し、演算子を変更します。  詳しくは、[こちらのページ](../../web/using/defining-web-forms-properties.md)を参照してください。

## セキュリティグループと管理者演算子

十分なセキュリティグループを作成して、オペレータが必要な操作を行えるだけの権限を与え、それ以上の権限は与えません。

管理オペレーターは使用しない（または共有しない）ようにします。（正確な監査やログ記録をさせるために）物理ユーザーごとに 1 人のオペレーターを作成します。新しく名前を付けた管理者を管理グループに追加します。admin演算子を使用しない場合は、削除せずに無効にしないでください。この演算子は、処理を実行する際に内部的に使用されます。 ただし、クライアントコンソール](../../platform/using/access-management.md)への[アクセスを禁止し、そのセキュリティゾーンを（localhostに）制限することはできます。

管理グループの（または、管理ネームド権限がある）オペレーターの数が多くなりすぎないようにします。これらのオペレーターは非常に強力です（すべての SQL 文の実行、サーバーでのコマンドの実行などができます）。

Adobe Campaignは、[ネームド権限](../../platform/using/access-management.md#named-rights)を通じて3つの高レベルの権限を提供します。

* **管理** （管理者）:すべての項目にアクセスを与え、すべての項目に対して何もかものを実行できるようにし、名前付きの権利チェックを省略し、プログラムEXECUTION (createProcess)やSQLネームド権限を含める

* **プログラムの実行** (createProcess):外部プログラムの実行を許可する（サーバー上で）

* **SQL**:データベースでSQLスクリプトを実行できます（セキュリティモデルを回避できます）。複雑な演算（フィルタリングなど）を実行する必要がある場合、データベース管理者に対して、SQL 関数を作成し、許可リストに登録するよう依頼できます。詳しくは、[こちらのページ](../../installation/using/scripting-coding-guidelines.md)を参照してください。

* **なるべく少数の（信頼できる）オペレーターにのみ付与します**
