---
title: 統合の設定
seo-title: 統合の設定
description: 統合の設定
seo-description: null
page-status-flag: never-activated
uuid: e2db7bdb-8630-497c-aacf-242734cc0a72
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: integrations
content-type: reference
topic-tags: adobe-experience-manager
discoiquuid: 1c20795d-748c-4f5d-b526-579b36666e8f
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 3b752b283a14bc75954fe46da5a21970c1e17fa1
workflow-type: ht
source-wordcount: '644'
ht-degree: 100%

---


# パイプラインのトラブルシューティング {#pipeline-troubleshooting}

**pipelined が失敗し、「No task corresponds to the mask pipelined@」（マスク pipelined@ に対応するタスクがありません）というエラーが表示される**

お使いのバージョンの Adobe Campaign Classic はパイプラインをサポートしていません。

1. 設定ファイル内に [!DNL pipelined] 要素が存在するかどうかを確認します。存在しない場合は、パイプラインはサポートされていません。
1. バージョン 6.11 ビルド 8705 以降にアップグレードします。

**`[``{`パイプラインが失敗し、「aurait dû commencer par  ou  (iRc=16384)」と表示される**

**NmsPipeline_Config** オプションが設定されていません。これは実際には JSON 解析エラーです。
JSON 設定を **NmsPipeline_Config** オプションで指定します。このページの「ルーティングオプション」を参照してください。

**パイプラインが失敗し、「the subject must be a valid organization or client」（件名は有効な組織またはクライアントにする必要があります）と表示される**

IMSOrgid 設定が無効です。

1. IMSOrgId が serverConf.xml で設定されていることを確認します。
1. デフォルトを上書きできる空の IMSOrgId をインスタンス設定ファイル内で探します。該当する場合は、削除します。
1. IMSOrgId が Experience Cloud 内の顧客の IMSOrgId と一致することを確認します。

**pipelined が失敗し、「invalid key」（キーが無効です）と表示される**

インスタンス設定ファイルの @authPrivateKey パラメーターが正しくありません。

1. authPrivateKey が設定されていることを確認します。
1. authPrivateKey が @ から始まり、= で終わり、およそ 4000 文字の長さであることを確認します。
1. 元のキーを探します。元のキーが、RSA 形式で、4096 ビット長であり、「-----BEGIN RSA PRIVATE KEY-----」で始まることを確認します。
   <br>必要に応じて、キーを再作成し、Adobe Analytics に登録します。[こちら](../../integrations/using/configuring-pipeline.md#oauth-client-creation)を参照してください。
1. キーが [!DNL pipelined] と同じインスタンス内でエンコードされたことを確認します。<br>必要に応じて、サンプルの JavaScript またはワークフローを使用してエンコードをやり直します。

**pipelined が失敗し、「unable to read the token during authentication」（認証時にトークンを読み取れません）と表示される**

秘密鍵の形式が無効です。

1. このページで鍵の暗号化の手順を実行します。
1. キーが同じインスタンスで暗号化されていることを確認します。
1. 設定ファイルの authPrivateKey が生成されたキーと一致することを確認します。<br>必ず OpenSSL を使用してキーペアを生成してください。例えば、PuttyGen では適切な形式が生成されません。

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
付録

**キー暗号化 JavaScript の使用方法**

秘密鍵を暗号化する JavaScript を実行します。これは、パイプライン設定に必須です。

cryptString 関数を実行する際に使用できるコード例を以下に示します。

```
/*
USAGE:
  nlserver javascript -instance:<instancename> -file -arg:"<private_key.pem file>" -file encryptKey.js
*/
 
function usage()
{
  return "USAGE:\n" +
    '  nlserver javascript -instance:<instancename> -file -arg:"<private_key.pem file>" -file encryptKey.js\n'
}
 
var fn = application.arg;
if( fn == "" )
  logError("Missing key file file\n" + usage());
 
//open the pem file
plaintext = loadFile(fn)
 
if( !plaintext.match(/^-----BEGIN RSA PRIVATE KEY-----/) )
  logError("File should be an rsa private key")
 
logInfo("Encrypted key:\n" + cryptString(plaintext, <xtkSecretKey>))
```

サーバーで、JavaScript を実行します。

```
nlserver javascript -instance:<instancename> -file -arg:"<private_key.pem file>" -file encryptKey.js
```

エンコードされたキーを出力からコンソールにコピー＆ペーストします。