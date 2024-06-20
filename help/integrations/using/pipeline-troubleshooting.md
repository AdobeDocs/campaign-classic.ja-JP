---
product: campaign
title: パイプラインのトラブルシューティング
description: パイプラインのトラブルシューティング
feature: Triggers
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
audience: integrations
content-type: reference
exl-id: 76645a6f-9536-49d6-b12a-fdd6113d31fa
source-git-commit: 8de62db2499449fc9966b6464862748e2514a774
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 100%

---

# パイプラインのトラブルシューティング {#pipeline-troubleshooting}



**パイプライン化されたプロセスが失敗し、「No task corresponds to the mask pipelined@&lt; instance >」（&lt;インスタンス> でパイプライン化されたマスクに対応するタスクがありません）というエラーが表示される**

お使いのバージョンの Adobe Campaign Classic はパイプラインをサポートしていません。

1. 設定ファイル内に [!DNL pipelined] 要素が存在するかどうかを確認します。存在しない場合は、パイプラインはサポートされていません。
1. Campaign 20.3 / [!DNL Gold Standard] 11 以降へのアップグレード。

**`[` `{`パイプライン化されたプロセスが失敗し、「aurait dû commencer par ou (iRc=16384)」と表示される**

**NmsPipeline_Config** オプションが設定されていません。これは実際には JSON 解析エラーです。
JSON 設定を **NmsPipeline_Config** オプションで指定します。このページの「ルーティングオプション」を参照してください。

**パイプライン化されたプロセスが失敗し、「the subject must be a valid organization or client」（件名は有効な組織またはクライアントにする必要があります）と表示される**

組織 ID の設定が無効です。

1. 組織 ID（ImsOrgId）が serverConf.xml で設定されていることを確認します。
1. インスタンス設定ファイルの空の組織 ID がデフォルトの組織 ID を上書きできるかどうかを確認します。該当する場合は、削除します。
1. 組織 ID が正しいことを確認します。組織 ID を見つけるには、[このページ](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=ja){_blank}を参照してください。

**パイプライン化されたプロセスが失敗し、「invalid key」（キーが無効です）と表示される**

インスタンス設定ファイルの @authPrivateKey パラメーターが正しくありません。

1. authPrivateKey が設定されていることを確認します。
1. authPrivateKey が @ から始まり、= で終わり、およそ 4000 文字の長さであることを確認します。
1. 元のキーを探して、それが RSA 形式で、長さが 4096 ビット、`-----BEGIN RSA PRIVATE KEY-----` で始まることを確認します。
   <br>必要に応じて、キーを再作成し、Adobe Analytics に登録します。
1. キーが [!DNL pipelined] と同じインスタンス内でエンコードされたことを確認します。<br>必要に応じて、サンプルの JavaScript またはワークフローを使用してエンコードをやり直します。

**パイプライン化されたプロセスが失敗し、「unable to read the token during authentication」（認証時にトークンを読み取れません）と表示される**

秘密鍵の形式が無効です。

1. このページで鍵の暗号化の手順を実行します。
1. キーが同じインスタンスで暗号化されていることを確認します。
1. 設定ファイルの authPrivateKey が生成されたキーと一致することを確認します。<br>必ず OpenSSL を使用してキーペアを生成してください。例えば、PuttyGen では適切な形式が生成されません。

**pipelined が失敗し、「アクセストークンを取得できません」と表示される**

ログは次のようになります。

```
2021-05-31T08:42:18.124Z        66462   66501   1       error   log     Listener: JWT Token is empty. (iRc=16384)
2021-05-31T08:42:18.210Z        66462   66501   1       error   log     Unknown authentication mode: 'Bearer realm="Adobe Analytics"'. (iRc=-55)
2021-05-31T08:42:18.210Z        66462   66501   1       error   log     BAS-010007 Function not implemented (iRc=-55)
2021-05-31T08:42:48.582Z        66462   66501   1       warning log     Connection seems to have been lost. Attempting to reconnect.
2021-05-31T08:43:09.156Z        66462   66501   1       error   log     INT-150012 The HTTP query returned a 'Forbidden' type error (403) (iRc=-53)
2021-05-31T08:43:09.160Z        66462   66501   1       error   log     Error while authenticating: '{"error":"This client: df73c224e5-triggers-test is no longer allowed to get access token."}' (iRc=16384)
```

このエラーメッセージは、従来の Omniture ベースの OAuth を使用して認証が設定されていることを意味します。認証をアップグレードするには、[Adobe Experience Cloud Triggers の Adobe I/O の設定](../../integrations/using/about-triggers.md#implement)を参照してください。

**トリガーが取得されない**

[!DNL pipelined] プロセスが実行中で、トリガーが取得されない場合は、次の手順に従います。

1. トリガーが Analytics でアクティブで、イベントを生成していることを確認します。
1. [!DNL pipelined] プロセスが実行中であることを確認します。
1. [!DNL pipelined] ログでエラーを探します。
1. [!DNL pipelined] ステータスページでエラーを探します。trigger-discarted、trigger-failures は 0 でなければなりません。
1. トリガー名が **[!UICONTROL NmsPipeline_Config]** オプションで設定されていることを確認します。疑わしい点がある場合は、ワイルドカードオプションを使用します。
1. Analytics がアクティブなトリガーを持ち、イベントを生成していることを確認します。設定が Analytics でおこなわれてから、設定が有効になるまでに数時間の遅延が生じる可能性があります。

**イベントが顧客にリンクされていない**

一部のイベントが顧客にリンクされていない場合は、次の手順に従います。

1. 紐付けワークフローが実行中であることを確認します（該当する場合）。
1. イベントに顧客 ID が含まれていることを確認します。
1. 顧客 ID を使用して顧客テーブルに対するクエリを作成します。
1. 顧客インポートの頻度を確認します。新規顧客は、ワークフローで Adobe Campaign にインポートされます。

**イベント処理の遅延**

Analytics のタイムスタンプが、Campaign でのイベントの作成日時よりはるかに古い場合。

一般に、トリガーでマーケティングキャンペーンが起動されるまでに 15～90 分かかることがあります。これは、データ収集の実装、パイプラインでの読み込み、定義済みトリガーのカスタム設定、Adobe Campaign 内のワークフローによって異なります。

1. [!DNL pipelined] プロセスが実行されているかどうかを確認します。
1. 再試行の原因となる可能性のあるエラーを pipelined.log で探します。該当する場合は、エラーを修正します。
1. [!DNL pipelined] ステータスページでキューのサイズを確認します。キューのサイズが大きい場合は、JS のパフォーマンスを向上させます。
1. ボリュームに伴って遅延が増加するようなので、メッセージを少なくして Analytics にトリガーを設定します。

**レガシー認証から Adobe IO 認証へのステージインスタンスのアップグレード**

ステージインスタンスで統合認証を変更しても、実稼動インスタンスの設定には影響しません。ステージインスタンスをアップグレードし、認証を Adobe IO に更新して、ステージインスタンスでトリガーをテストできます。

実稼動インスタンスは引き続きレガシー認証を使用し、この変更による影響は受けません。
