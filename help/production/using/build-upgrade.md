---
product: campaign
title: ビルドのアップグレードの概要
description: 新しいビルドにアップグレードするための主な手順を説明します
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: c5a9c99a-4078-45d8-847b-6df9047a2fe2
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '2353'
ht-degree: 53%

---

# ビルドアップグレードの実行{#performing-a-build-upgrade}

![](../../assets/v7-only.svg)

この節では、アップグレードプロセスに関する詳細な手順と、競合を特定して解決する手順について説明します。

ビルドのアップグレードは慎重におこなう必要があります。必ず事前にアップグレードが及ぼす影響を検討し、作業は高度なスキルを備えた人が実行するようにしてください。アップグレードを正常に完了するために、後述の手順を実行する人はエキスパートユーザーに限定してください。また、アップグレードを開始する前に [Adobe カスタマーサポート](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に連絡することを強くお勧めします。

アップグレードの前提条件は以下のとおりです。

* Campaign のアーキテクチャに関する理解
* システムおよびサーバーサイドの知識
* 管理者としての権限とアクセス許可

詳しくは、次の節を参照してください。[Adobe Campaign](../../production/using/upgrading.md)、[ 新しいバージョンへの移行 ](../../migration/using/about-migration.md) を更新しています。

ホストされているインスタンスおよびハイブリッドインスタンスの場合、アドビのテクニカルオペレーションチームにビルドのアップグレードをリクエストする必要があります。詳しくは、このページの下にあるよくある質問の節を参照してください。また、[ ビルドアップグレードの FAQ](../../platform/using/faq-build-upgrade.md) も参照してください。

## アップグレードの準備

![](assets/do-not-localize/icon_planification.png)

ビルドのアップグレードを開始する前に、以下に示すように完全な準備を行う必要があります。
システムをアップグレードする準備が整ったら、ビルドのアップグレードには少なくとも **** 2 時間かかります。

ビルドのアップグレードをおこなうには、以下のリソースが必要です。

* Adobeアーキテクト — データベース構造（標準スキーマと追加された追加のスキーマ、キャンペーンデザイン、特定の順序で開始およびテストする必要のある重要なパス機能）を理解します。
* プロジェクトマネージャー — ビルドのアップグレードに様々なインスタンス（実稼動、ステージング、テスト）や、その他のサードパーティのサーバーおよびアプリケーション（データベース、SFTP サイト、メッセージングサービスプロバイダー）が含まれる場合、ベストプラクティスと見なされます。
* Adobe Campaign 管理者：管理者はセキュリティ、フォルダーの配置、レポート、インポートおよびエクスポートの要件をはじめとするサーバーの設定を把握しています。管理者がいない状況でビルドのアップグレードを実行しないでください。
* Adobe Campaignのオペレーター（マーケティングユーザー） — アップグレードを成功させるには、ユーザーの日々のタスクを正常に実行できるかどうかが必要です。このため、アップグレードしたサーバーのテストには、必ず日常のオペレーターを 1 人以上含めてください。

### 計画

ビルドのアップグレードを計画する際に重要なポイントを紹介します。

1. アップグレードには、少なくとも 2 時間確保しておく。
1. アドビおよびお客様側担当者の連絡先詳細を配布しておく。
1. ホストされたインスタンスの場合：Adobeとお客様のスタッフが、アップグレードの時間と実行者を調整します。
1. オンプレミスのインスタンスの場合：お客様側担当者がすべてのプロセスを管理します。カスタマイズされたワークフローや配信ロジックのテスト時にサポートが必要な場合は、コンサルティングサービスを依頼してください。
1. アップグレード先のAdobe Campaignのバージョンを特定して確認します。[Adobe Campaign Classicのリリースノート ](../../rn/using/rn-overview.md) を参照してください。
1. アップグレードの実行可能ファイルがあることを確認します。

### 主要人物

ビルドのアップグレードプロセスには、以下の担当者が関与する必要があります。

* Adobeアーキテクト：ホストアーキテクチャまたはハイブリッドアーキテクチャの場合、アーキテクトはAdobe Campaign ClientCare と連携する必要があります。

* プロジェクトマネージャー：
   * オンプレミスインストールの場合：お客様の社内プロジェクトリーダーがアップグレードをリードし、ライフサイクルテストを管理します。

   * ホストインストールの場合：ホスティングチームは、Adobe Campaign Client Care チームおよびお客様と連携し、すべてのインスタンスについてアップグレードのタイムラインを調整します。

* Adobe Campaign 管理者：:
   * オンプレミスインストールの場合：管理者がアップグレードを実行します。

   * ホストインストールの場合：ホスティングチームがアップグレードを実行します。

* Adobe Campaign operator\marketing user:オペレーターは、開発用、テスト用、および本番用の各インスタンスに対してテストを実行します。

### ビルドのアップグレードの準備

ビルドのアップグレードを開始する前に、オンプレミス版のお客様は次の準備を行う必要があります。

1. アップグレード前にすべての開発作業がエクスポート（パッケージとしてエクスポート）可能であることを確認する。

1. 移行元の環境と移行先の環境のすべてのインスタンスについてデータベースの完全バックアップを作成する。

1. [ サーバー構成ファイル ](../../installation/using/the-server-configuration-file.md) の最新バージョンを入手します。

1. [最新ビルドをダウンロードします](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html?lang=ja)。[詳細情報](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)。

また、ビルドのアップグレードを開始する前に、[ 便利なコマンドライン ](../../installation/using/command-lines.md) をすべて把握しておく必要があります。

* **nlserver pdump**：実行中のプロセスのリストを表示します
* **nlserver pdump -who**：アクティブなクライアントセッションのリストを表示します
* **nlserver monitor -missing**：不足しているプロパティのリストを表示します
* **nlserver start process@instanceName**:プロセスを開始
* **nlserver stop process@instanceName**:プロセスを停止
* **nlserver restart process@instanceName**:プロセスを再起動
* **nlserver shutdown**:すべての Campaign プロセスを停止
* **nlserver watchdog -svc**：ウォッチドッグを開始します（UNIX のみ）

## アップグレードの実行

![](assets/do-not-localize/icon_process.png)

以下の手順は、オンプレミスの **のお客様のみが実行します。**&#x200B;ホスト版のお客様については、ホスティングチームがこの作業を実行します。Adobe Campaignを新しいビルドに更新する手順については、以下で詳しく説明します。

### 環境の複製

ここでは、Adobe Campaign の環境を複製する方法を説明します。これにより、移行元の環境が移行先の環境に復元され、同一の作業環境が 2 つになります。

これは、次の手順に従って行います。

1. 移行元となる環境に含まれているすべてのインスタンス上にあるデータベースのコピーを作成します。

1. 作成したコピーを、移行先となる環境のすべてのインスタンス上に復元します。

1. 起動前に、ターゲット環境で **nms:freezeInstance.js** 焼灼スクリプトを実行します。 これにより、外部とやり取りするすべてのプロセスが停止します。ログ、トラッキング、配信、キャンペーンワークフローなど

   ```
   nlserverjavacsriptnms:freezeInstance.js–instance:<dev> -arg:run
   ```

1. 次のように、注意点を確認します。

   * ID が **0** に設定されているのが配信部分のみであることを確認します。

      ```
      SELECT * FROM neolane.nmsdeliverypart;
      ```

   * 配信ステータスが正しく更新されていることを確認します。

      ```
      SELECT iSate, count(*) FROM neolane.nmsdeliveryGroup By iProd;
      ```

   * ワークフローのステータスが正しく更新されていることを確認します。

      ```
      SELECT iState, count (*) FROM neolane.xtkworkflowGROUP BY iState;
      SELECT iStatus, count (*) FROM neolane.xtkworkflowGROUP BY iStatus;
      ```

### サービスのシャットダウン

すべてのファイルを新しいバージョンで置き換えるために、nlserverservice のすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス (IIS):**iisreset /stop**
   * Adobe Campaignサービス：**net stop nlserver6**

   >[!NOTE]
   >
   >IIS で使用されている nlsrvmod.dll ファイルを新しいバージョンで置き換えることができるように、リダイレクションサーバー（webmdl）が停止したことを確認してください。

1. **nlserver pdump** コマンドを実行してアクティブなタスクがないことを確認します。タスクがない場合、出力は次のようになります。

   ```
   C:\<installation path>\bin>nlserverpdump HH:MM:SS > Application Server for Adobe Campaign version x.x (build xxx) dated xx/xx/xxxx No tasks
   ```

1. Windows タスクマネージャーで、すべてのプロセスが停止したことを確認します。

### Adobe Campaign Server アプリケーションのアップグレード

1. **Setup.exe** ファイルを実行します。 このファイルをダウンロードする必要がある場合は、[ ダウンロードセンター ](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html) にアクセスします。

1. インストールモードを選択します。**更新** または **修復**。

1. 「**次へ**」をクリックします。

1. 「**完了**」をクリックすると、インストールプログラムによって新しいファイルがコピーされます。

1. 処理が完了したら「**完了**」をクリックします。

### リソースの同期

1. コマンドラインを開きます。

1. **nlserver config -postupgrade -allinstances** を実行して以下の作業をおこないます。

   * リソースの同期
   * スキーマの更新
   * データベースの更新

   >[!NOTE]
   >
   >この操作は、nlserverweb アプリケーションサーバー上で 1 回だけ実行する必要があります。

   1 つのデータベースのみを同期するには、次のコマンドを実行します。

   ```
   nlserver config -postupgrade -instance: <instance_name>
   ```

1. 同期によってエラーや警告が発生したかどうかを確認します。

### サービスの再起動

以下のサービスを再起動する必要があります。

* Web サービス (IIS):**issreset /start**
* Adobe Campaignサービス：**net start nlserver6**

### クライアントコンソールの更新

クライアントコンソールは、サーバーインスタンスと同じビルドになっている必要があります。

Adobe Campaign アプリケーションサーバーがインストールされているマシン（nlserverweb）で、以下のファイルをダウンロードしてインストールします。

```
Setup-client-7.xxxx.exe in [path of the application]\datakit\nl\en\jsp
```

次回クライアントコンソールに接続したときに、ウィンドウが開いて新しい更新が利用可能なことを知らせるメッセージが表示され、その更新をダウンロードしてインストールするよう促されます。

### 特定の追加タスク

一部の設定では、新しいビルドに更新するために特定の追加タスクが必要です。

#### トランザクションメッセージ

トランザクションメッセージ (Message Center) が Campaign インスタンスで有効になっている場合、次の追加手順を実行してアップグレードする必要があります。

1. Message Center の本番サーバーを、選択したバージョンに更新します。
1. ポストアップグレードスクリプトを実行します。
1. テストを実行して E メールが Message Center の本番用インスタンスを通じて正常に受信されることを確認します。
1. クライアントをアップグレードし、キャッシュをクリアします。
1. パッケージのエクスポート:
   * クライアントパッケージの書き出しツールを使用したパッケージの書き出し
   * スキーマパッケージのインポート
   * クライアントの切断と再接続
   * データベースの更新
   * 接続を解除し、再接続します
   * 管理パッケージのインポート
   * コンテンツパッケージの読み込み
   * コンテンツ管理パッケージの読み込み
   * 接続を解除し、再接続します
   * ワークフローの迅速なサニティチェックの実行

1. Message Center テンプレートをパブリッシュして、サーバーと Message Center インスタンス間のインターフェイスが機能していることを確認します。
1. テストを実行して、E メールが Message Center の実稼動インスタンスを通じて正常に受信されることを確認します。
1. 本番環境でワークフローのテストを実行して、配信が受信されることを確認します。

#### ミッドソーシング

ミッドソーシング環境のコンテキストで、次の追加手順を実行してアップグレードする必要があります。

1. [Adobeカスタマーケア ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) に連絡して、ミッドソーシングサーバーのアップグレードを調整してください。
1. テストリンクを実行して、バージョンが更新されたことを検証します。 例：

   ```
   http://[InsertServerURL]/r/test
   ```

>[!NOTE]
>
>ミッドソーシングサーバーは、常にマーケティングサーバーと同じバージョン（またはより新しいバージョン）を実行する必要があります。

## 競合の場合

### 競合の特定

同期の結果を確認する必要があります。 ここで紹介する手順はオンプレミス版のお客様のみを対象にしています。ホスト版のお客様については、ホスティングチームがこの作業を実行します。同期結果の表示方法は 2 つあります。

コマンドラインインターフェイスでは、エラーは三重山形記号「>>>」で実現され、同期は自動的に停止されます。 警告は二重山括弧「>>」で示され、同期が完了したら解決する必要があります。 ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。以下はその一例です。

```
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log =========Summary of the update==========
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView‘ and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
```

リソースの競合に関する警告は、見落とさないように注意して、解決してください。

**postupgrade_ServerVersionNumber_TimeOfPostupgrade.log** ファイルには、同期結果が含まれます。 デフォルトでは、次のディレクトリで使用できます。**installationDirectory/var/instanceName/postupgrade**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の分析

**競合を見つける方法**

競合は、対象のサーバーの postupgrade.log または Campaign クライアントインターフェイス（管理/設定/パッケージ管理/競合を編集）で見つかります。

The document with identifier ‘stockOverview’ and type ‘nms:webApp’ is in conflict with the new version.

競合が見つかった場合は、以下の条件に該当するかを確認します。

* お客様が変更またはカスタマイズしたオブジェクトか
* 本番環境で変更したオブジェクトか

どちらにも該当しない場合は、誤検出です。どちらにも該当する場合は、実際に競合が存在します。

**お客様が変更したオブジェクトかどうかの確認**

1. 競合しているオブジェクトを特定します。
1. お客様にオブジェクトを変更したかどうかを問い合わせます。
1. オブジェクトに異常がないかを確認します。
1. オブジェクトのコードに最終変更日が設定されているかを確認します。
1. 競合の XML コードに「_conflict」属性がないかを調べます。カスタマイズされた形跡がないかを確認します。

**新しいビルドで変更されたオブジェクトかどうかの確認**

1. 「常習犯」の仕業かもしれません。組み込みの Web アプリケーションまたはレポート ( 例：「deliveryValidation」、「deliveryOverview」、「budget」)。
1. 変更ログを見て更新がないかを調べます。
1. Adobe Campaignの専門家に聞いて。
1. コードに対して「差分表示」を実行します。

### 競合の解決

競合を解決するには、次の手順に従います。

1. Adobe Campaign エクスプローラーで&#x200B;**管理／設定／パッケージ管理／競合を編集**&#x200B;に移動します。

1. リストから解決する競合を選択します。競合を解決する方法は 3 つあります。**新しいバージョンを受け入れる**、**現在のバージョンを保持する**、**コードを結合し（解決済みとして宣言）**、**競合を無視（非推奨）**。

**新しいバージョンを承認できるケース**

* 標準機能が必要な場合
* カスタマイズしていない場合（カスタマイズした内容はすべて削除されます）

**現在のバージョンを維持できるケース**

* カスタマイズしている場合
* 結合を実行したくない場合
* アップグレードが原因で競合しているオブジェクトを修正する必要がない場合

**結合を実行するケース**

* 結合できるのはフォーム、レポート、Web アプリケーションのみです。
* 小規模な結合であればコードの知識がなくても実行できる場合があります。
* 複雑な結合は適切なスキルと能力を持った人が実行する必要があります。
* [ 結合の実行 ](#perform-a-merge) を参照してください。

**競合を放置した場合**

* 競合した状態が続きます。
* オブジェクトはアップグレードされません。
* バージョンの互換性が失われたり、バグ修正を適用しても改善されなかったりといった長期的な影響が生じます。

>[!IMPORTANT]
>競合は解決することを強くお勧めします。

### 結合の実行{#perform-a-merge}

結合には様々なタイプがあります。

1. 簡単な結合：カスタム要素と新しい要素は小さく、関連性がなく、コーディングは不要です。
1. 変更なし：新しいバージョンを承認します。最終更新日のみ変更され、コメント、タブ、スペース、新規行のみ反映されます（例：意図しない保存）。
1. 軽微な変更：1 行のみ変更されます（例：xpathToLoad）。
1. 高度な結合：コーディングが必要な場合です。開発に関するスキルが必要です。[ 複雑な結合 ](#complex-merges) を参照してください。

#### 結合方法

1. 3 つのバージョンをすべて入手する：元のバージョン、新しいバージョンおよびカスタムバージョン。
1. 元のバージョンと新しいバージョンの間で「差分」を実行します。
1. 変更を抽出します。
1. 変更がない場合、現在のバージョンを維持して競合を解決します。

#### コードの場所

1. 組み込みコードは、データキットフォルダー内の XML ファイルに格納されます。 競合しているオブジェクトに対応する XML ファイルを探します。例：installationDirectory\datakit\nms\fra\form\recipient.xml
1. 元のバージョンを取得：[ ダウンロードセンター ](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html) または製品のアップグレードされていない別のインストールを通じて。
1. 新しいバージョンの取得：[ ダウンロードセンター ](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html) またはお客様のインストール済みファイルを通じて。
1. カスタムバージョンの取得：Campaign クライアント内からオブジェクトのソースコードを取得します。

### 差分表示の実行方法

1. テキストエディターまたは結合エディター（Notepad ++、AraxisMerge、WinMerge など）をインストールします。
1. エディターで元のファイルと新しいファイルを開きます。
1. 差分表示（2 つのファイルの比較）を実行します。
1. 差分を特定します。

### 結合方法

1. カスタムバージョンから着手します。
1. 変更を適用します。
1. 解決済みとして宣言して、競合を解決します。
1. 非回帰性を確認します。

手動で競合を解決する場合の手順は以下のとおりです。

1. ウィンドウの下部のセクションで **_conflict_string_** を検索し、競合するエンティティを探します。 新しいバージョンでインストールされたエンティティは新しい引数を持ちます。古いバージョンと一致するエンティティはカスタム引数を持ちます。
1. 維持しないバージョンを削除します。保持するエンティティの **_conflict_argument_** 文字列を削除します。
1. 解決した競合に移動します。**アクション**&#x200B;アイコンをクリックし、「**解決済みとして宣言**」を選択します。
1. 変更を保存します。これにより競合が解決します。

#### 高度な結合{#complex-merges}

1. 変更の内容を理解します。変更をリバースエンジニアリングし、変更ログを調べ、Adobe Campaignの専門家にフォローアップします。
1. 変更をどのように処理するかを決定します。
1. カスタマイズの機能を理解します。変更をリバースエンジニアリングする

以下は高度な結合を実行する際の手順です。

1. 変更セットからコードのビットをコピーする
1. カスタマイズしたバージョンに貼り付けます。
1. カスタマイズの非回帰性のテスト
1. 変更の機能のテスト
1. ユーザー受け入れテストの実行
1. テスト環境で実行します。


>[!IMPORTANT]
>複雑な結合を実行するには、開発スキルが必要です。

**関連トピック**

* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign Classic リリースノート](../../rn/using/rn-overview.md)
* [Campaign Classic のヘルプとサポートのオプション](../../support.md)
* [[!DNL Gold Standard] プログラム](../../rn/using/gs-overview.md)
