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
translation-type: tm+mt
source-git-commit: 39d6da007d69f81da959660b24b56ba2558a97ba
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 2%

---


# パイプラインのトラブルシューティング {#pipeline-troubleshooting}

**パイプラインは、「マスクのパイプライン@に対応するタスクがありません」というエラーが表示されて失敗します。**

お使いのバージョンのAdobe CampaignClassicはパイプラインをサポートしていません。

1. 設定ファイルにパイプライン要素が存在するかどうかを確認します。 サポートされていない場合は、サポートされていないことを意味します。
1. バージョン6.11ビルド8705以降にアップグレードします。

**パイプラインは、&quot;aurait doencer par &#39;[&#39; ou &#39;{&#39; (iRc=16384)&quot;で失敗します。**

NmsPipeline_Config **** オプションが設定されていません。 これは実際にはJSON解析エラーです。
JSON設定をオプションNmsPipeline_Config **に設定します**。 このページの「ルーティングオプション」を参照してください。

**パイプラインが失敗し、「件名は有効な組織またはクライアントである必要があります」と表示される**

IMSOrgid構成が無効です。

1. IMSOrgIdがserverConf.xmlに設定されていることを確認します。
1. インスタンス設定ファイル内で、デフォルトを上書きできる空のIMSOrgIdを探します。 該当する場合は、削除します。
1. IMSOrgIdがExperience Cloud内の顧客のIMSOrgIdと一致することを確認します。

**パイプラインは「無効なキー」で失敗します**

インスタンス構成ファイルの@authPrivateKeyパラメーターが正しくありません。

1. authPrivateKeyが設定されていることを確認します。
1. authPrivateKeyを確認します。 @、=で終わる開始、およそ4000文字の長さ。
1. 元のキーを探して、次のものであることを確認します。 RSA形式では、4096ビット長で —BEGIN RSA PRIVATE KEY — を持つ開始。
   <br> 必要に応じて、キーを再作成し、AdobeAnalyticsに登録します。 この[節](../../integrations/using/configuring-pipeline.md#oauth-client-creation)を参照してください。
1. キーがパイプラインと同じインスタンス内でエンコードされたことを確認します。 <br>必要に応じて、サンプルのJavaScriptまたはワークフローを使用してエンコードをやり直します。

**「認証中にトークンを読み取れません」という内容のパイプラインでの失敗**

秘密鍵の形式が無効です。

1. このページで鍵の暗号化の手順を実行します。
1. キーが同じインスタンスで暗号化されていることを確認します。
1. 設定ファイルのauthPrivateKeyが生成されたキーと一致することを確認します。 <br>必ずOpenSSLを使用してキーペアを生成してください。 例えば、PuttyGenは適切なフォーマットを生成しません。

**トリガーは取得されません**

パイプラインプロセスが実行中で、トリガーが取得されない場合：

1. トリガーがAnalyticsでアクティブで、イベントを生成していることを確認します。
1. パイプラインプロセスが実行中であることを確認します。
1. パイプラインログでエラーを探します。
1. パイプライン状態ページでエラーを探します。 trigger-discarted、trigger-failuresは0でなければなりません。
1. トリガー名がNmsPipeline_Config **** オプションで設定されていることを確認します。 疑わしい点がある場合は、ワイルドカードオプションを使用します。
1. Analyticsがアクティブなトリガーを持ち、イベントを生成していることを確認します。 設定がAnalyticsで行われてから数時間後に、設定が有効になるまでに遅延が生じる可能性があります。

**イベントが顧客にリンクされていない**

一部のイベントが顧客にリンクされていない場合：

1. 調整ワークフローが実行中であることを確認します（該当する場合）。
1. イベントに顧客IDが含まれていることを確認します。
1. 顧客IDを使用して顧客テーブルにクエリを作成します。
1. 顧客インポートの頻度を確認します。 新規顧客は、ワークフローを使用してAdobe Campaignにインポートされます。

**イベント処理の遅延**

Analyticsのタイムスタンプが、キャンペーンでのイベントの作成日よりずっと古い場合。

一般的に、トリガーは、マーケティングキャンペーンを起動するのに15 ～ 90分かかる場合があります。 これは、データ収集の実装、パイプラインへの読み込み、定義されたトリガーのカスタム設定、Adobe Campaign内のワークフローによって異なります。

1. パイプラインプロセスが実行中かどうかを確認します。
1. 再試行の原因となる可能性のあるエラーは、pipelined.logで探します。 該当する場合は、エラーを修正します。
1. キューサイズのパイプライン状態ページを確認します。 キューのサイズが大きい場合は、JSのパフォーマンスを向上させます。
1. 遅延はボリュームに伴って増加するようなので、メッセージを少なくして、Analyticsでトリガーを設定します。
付録

**鍵暗号化JavaScriptの使用方法**

JavaScriptを実行して秘密鍵を暗号化します。 パイプライン設定に必要です。

cryptString関数を実行する際に使用できるコードの例を以下に示します。

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

サーバーで、JavaScriptを実行します。

```
nlserver javascript -instance:<instancename> -file -arg:"<private_key.pem file>" -file encryptKey.js
```

エンコードされたキーを出力からコンソールにコピー&amp;ペーストします。