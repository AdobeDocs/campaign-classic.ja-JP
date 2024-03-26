---
product: campaign
title: ビルドのアップグレードの基本を学ぶ
description: 新しいビルドにアップグレードするための主な手順を説明します
feature: Monitoring, Upgrade
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: c5a9c99a-4078-45d8-847b-6df9047a2fe2
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '2330'
ht-degree: 36%

---

# ビルドアップグレードの実行{#performing-a-build-upgrade}



この節では、アップグレードプロセスに関する詳細な手順と、競合を識別および解決する手順について説明します。

ビルドのアップグレードは慎重に実行する必要があり、その影響を事前に十分に考慮し、手順は高いレベルの規律で完了する必要があります。 アップグレードを成功させるには、以下の手順を実行するのはエキスパートユーザーのみにしてください。 また、と連絡を取ることを強くお勧めします [Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) アップグレードを開始する前に、

次の前提条件が必要です。

* Campaign のアーキテクチャに関する理解
* システムおよびサーバーサイドの知識
* 管理者としての権限とアクセス許可

詳しくは、次の節を参照してください。 [Adobe Campaignの更新](../../production/using/upgrading.md), [新しいバージョンへの移行](../../migration/using/about-migration.md).

ホストインスタンスおよびハイブリッドインスタンスの場合、ビルドのアップグレードをAdobeの技術運用チームにリクエストする必要があります。 詳しくは、このページの下部にあるよくある質問の節を参照してください。 また、 [ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md).

## アップグレードの準備

![](assets/do-not-localize/icon_planification.png)

ビルドのアップグレードを開始する前に、以下に示すように、完全な準備を行う必要があります。
システムをアップグレードする準備が整うと、ビルドのアップグレードが行われます。 **少なくとも** 2 時間。

ビルドのアップグレードをおこなうには、以下のリソースが必要です。

* Adobeアーキテクト — データベース構造（標準のスキーマと追加された追加のスキーマ、キャンペーンデザイン、および特定の順序で開始およびテストする必要のある重要なパス機能）を理解します。
* プロジェクトマネージャー — ビルドのアップグレードに様々なインスタンス（実稼動、ステージング、テスト）や他のサードパーティのサーバーおよびアプリケーション（データベース、SFTP サイト、メッセージングサービスプロバイダー）が含まれる場合、ベストプラクティスと見なされます。
* Adobe Campaign管理者 — 管理者は、セキュリティ、フォルダーのレイアウト、レポート、読み込み/書き出しの要件など、サーバーの設定について把握しています。 管理者がいない状況でビルドのアップグレードを実行しないでください。
* Adobe Campaignのオペレーター（マーケティングユーザー） — 正常にアップグレードするには、ユーザーが日々のタスクを正常に実行できるかどうかが重要です。 このため、アップグレードしたサーバーのテストには、必ず毎日少なくとも 1 人のオペレーターを含めてください。

### 計画

ビルドのアップグレードを計画する際に重要なポイントを紹介します。

1. アップグレードには、少なくとも 2 時間確保しておく。
1. アドビおよびお客様側担当者の連絡先詳細を配布しておく。
1. ホストインスタンスの場合：Adobeと顧客スタッフが、アップグレードの時間と実行者を調整します。
1. オンプレミスのインスタンスの場合：お客様側担当者がすべてのプロセスを管理します。カスタマイズされたワークフローや配信ロジックのテスト時にサポートが必要な場合は、コンサルティングサービスを依頼してください。
1. アップグレード先のAdobe Campaignのバージョンを決定して確認します。 [Adobe Campaign Classicリリースノート](../../rn/using/rn-overview.md).
1. アップグレードの実行可能ファイルがあることを確認します。

### 主要担当者

ビルドのアップグレードプロセスには、以下の担当者が関与している必要があります。

* Adobeアーキテクト：ホストアーキテクチャまたはハイブリッドアーキテクチャの場合、アーキテクトはAdobe Campaign Client Care と連携する必要があります。

* プロジェクトマネージャー：
   * オンプレミスでのインストールの場合：お客様の内部プロジェクトリーダーがアップグレードをリードし、ライフサイクルテストを管理します。

   * ホストインストールの場合：ホスティングチームがAdobe Campaign Client Care チームおよびお客様と連携し、すべてのインスタンスについてアップグレードのスケジュールを調整します。

* Adobe Campaign Administrator:
   * オンプレミスインストールの場合：管理者がアップグレードを実行します。

   * ホスト版の場合：ホスティングチームがアップグレードを実行します。

* Adobe Campaign operator\marketing user: operator が開発用、テスト用、本番用の各インスタンスのテストを実行します。

### ビルドのアップグレードを準備する

ビルドのアップグレードを開始する前に、オンプレミス版のお客様は次の準備を行う必要があります。

1. アップグレード前にすべての開発作業がエクスポート（パッケージとしてエクスポート）可能であることを確認する。

1. 移行元の環境と移行先の環境のすべてのインスタンスについてデータベースの完全バックアップを作成する。

1. の最新バージョンを取得する [サーバー設定ファイル](../../installation/using/the-server-configuration-file.md).

1. [最新ビルドをダウンロード](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html). [詳細情報](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)。

また、 [便利なコマンドライン](../../installation/using/command-lines.md) ビルドのアップグレードを開始する前に、以下を実行します。

* **nlserver pdump**：実行中のプロセスのリストを表示します
* **nlserver pdump -who**：アクティブなクライアントセッションのリストを表示します
* **nlserver monitor -missing**：不足しているプロパティのリストを表示します
* **nlserver start process@instance-name**：プロセスを開始します
* **nlserver stop process@instance-name**：プロセスを停止します。
* **nlserver restart process@instance-name**：プロセスを再開します。
* **nlserver shutdown**：すべての Campaign プロセスを停止します。
* **nlserver watchdog -svc**：ウォッチドッグを開始します（UNIX のみ）

## アップグレードの実行

![](assets/do-not-localize/icon_process.png)

以下の手順は、次の場合にのみ実行されます。 **オンプレミス** 顧客。 ホスト型のお客様の場合は、ホスティングチームが対応します。 Adobe Campaignを新しいビルドに更新するには、詳細な手順を以下に示します。

### 環境を複製

ここでは、Adobe Campaign の環境を複製する方法を説明します。これにより、移行元の環境が移行先の環境に復元され、同一の作業環境が 2 つになります。

これを行うには、次の手順に従います。

1. 移行元となる環境に含まれているすべてのインスタンス上にあるデータベースのコピーを作成します。

1. 作成したコピーを、移行先となる環境のすべてのインスタンス上に復元します。

1. を実行します。 **nms:freezeInstance.js** 起動前のターゲット環境の警告スクリプト。 これにより、ログ、トラッキング、配信、キャンペーンワークフローなど、外部とやり取りするすべてのプロセスが停止します。

   ```
   nlserverjavacsriptnms:freezeInstance.js–instance:<dev> -arg:run
   ```

1. 次のように、注意点を確認します。

   * ID がに設定されているのが唯一の配信部分であることを確認します。 **0**:

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

すべてのファイルを新しいバージョンで置き換えるには、nlserverservice のすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス (IIS): **iisreset /stop**
   * Adobe Campaignサービス： **net stop nlserver6**

   >[!NOTE]
   >
   >IIS で使用される nlsrvmod.dll ファイルを新しいバージョンに置き換えられるように、リダイレクションサーバー (webmdl) が停止していることを確認します。
   >

1. を実行して、アクティブなタスクがないことを検証します。 **nlserver pdump** コマンドを使用します。 タスクがない場合、出力は次のようになります。

   ```
   C:\<installation path>\bin>nlserverpdump HH:MM:SS > Application Server for Adobe Campaign version x.x (build xxx) dated xx/xx/xxxx No tasks
   ```

1. Windows のタスクマネージャで、すべてのプロセスが停止していることを確認します。

### Adobe Campaign Server アプリケーションのアップグレード

1. を実行します。 **Setup.exe** ファイル。 このファイルをダウンロードする必要がある場合は、 [ダウンロードセンター](https://experience.adobe.com/jp/downloads/content/software-distribution/en/campaign.html).

1. インストールモードを選択します。 **更新** または **修復**.

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
   >

   1 つのデータベースのみを同期するには、次のコマンドを実行します。

   ```
   nlserver config -postupgrade -instance: <instance_name>
   ```

1. 同期でエラーや警告が発生したかどうかを確認します。

### サービスの再起動

以下のサービスを再起動する必要があります。

* Web サービス (IIS): **issreset /start**
* Adobe Campaignサービス： **net start nlserver6**

### クライアントコンソールの更新

クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

Adobe Campaign アプリケーションサーバーがインストールされているマシン（nlserverweb）で、以下のファイルをダウンロードしてインストールします。

```
Setup-client-7.xxxx.exe in [path of the application]\datakit\nl\en\jsp
```

次回クライアントコンソールに接続したときに、ウィンドウが開いて新しい更新が利用可能なことを知らせるメッセージが表示され、その更新をダウンロードしてインストールするよう促されます。

### 特定の追加タスク

一部の設定では、新しいビルドに更新するために特定の追加タスクが必要です。

#### トランザクションメッセージ

トランザクションメッセージ (Message Center) が Campaign インスタンスで有効になっている場合、アップグレードするには、次の追加手順を実行する必要があります。

1. Message Center の本番サーバーを、選択したバージョンに更新します。
1. ポストアップグレードスクリプトを実行します。
1. テストを実行して E メールが Message Center の本番用インスタンスを通じて正常に受信されることを確認します。
1. クライアントをアップグレードし、キャッシュをクリアします。
1. パッケージをエクスポートします。
   * クライアントパッケージの書き出しツールを使用してパッケージを書き出す
   * スキーマパッケージをインポート
   * クライアントを切断して再接続します。
   * データベースを更新
   * 接続を解除して再接続します。
   * 管理パッケージをインポート
   * コンテンツパッケージを読み込む
   * コンテンツ管理パッケージを読み込む
   * 接続を解除して再接続します。
   * ワークフローのクイックサニティチェックの実行

1. Message Center テンプレートをパブリッシュして、サーバーと Message Center インスタンス間のインターフェイスが機能していることを確認します。
1. テストを実行して、E メールが Message Center の実稼働インスタンスを通じて正常に受信されたことを確認します。
1. 本番環境でワークフローのテストを実行して、配信が受信されることを確認します。

#### ミッドソーシング

ミッドソーシング環境の場合、アップグレードするには、次の追加手順を実行する必要があります。

1. 連絡先 [Adobeカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) をクリックして、ミッドソーシングサーバーのアップグレードを調整します。
1. テストリンクを実行して、バージョンが更新されていることを検証します。 例：

   ```
   http://[InsertServerURL]/r/test
   ```

>[!NOTE]
>
>ミッドソーシングサーバーは、マーケティングサーバーと同じバージョン（またはそれ以降）を常に実行する必要があります。
>

## 競合の場合

### 競合の特定

同期結果を確認する必要があります。 この手順はオンプレミスのお客様のみが実行します。 ホスト型のお客様の場合は、ホスティングチームが対応します。 同期結果の表示方法は 2 つあります。

コマンドラインインターフェイスでは、エラーは 3 つの山形記号「>>>」で実現され、同期は自動的に停止します。 警告は二重山形記号「>>」で具体化され、同期が完了したら解決する必要があります。 アップグレード後の最後に、コマンドプロンプトに概要が表示されます。 以下はその一例です。

```
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log =========Summary of the update==========
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView‘ and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
```

リソースの競合に関する警告が発生した場合は、解決にユーザーの注意が必要です。

The **postupgrade_ServerVersionNumber_TimeOfPostupgrade.log** ファイルには同期結果が含まれます。 デフォルトでは、次のディレクトリで使用できます。 **installationDirectory/var/`<instance-name>`/postupgrade**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合を分析

**競合の検出方法**

競合は、該当するサーバーの postupgrade.log または Campaign クライアントインターフェイス（管理/設定/パッケージ管理/競合を編集）で見つけることができます。

The document with identifier ‘stockOverview’ and type ‘nms:webApp’ is in conflict with the new version.

競合が見つかった場合は、以下の条件に該当するかを確認します。

* お客様が変更またはカスタマイズしたオブジェクトか
* 本番環境で変更したオブジェクトか

どちらの条件も当てはまらない場合、これは偽陽性です。 どちらにも該当する場合は、実際に競合が存在します。

**顧客がオブジェクトを変更したか。**

1. 競合しているオブジェクトを特定します。
1. お客様にオブジェクトを変更したかどうかを問い合わせます。
1. オブジェクトに異常がないかを確認します。
1. オブジェクトのコードに最終変更日が設定されているかを確認します。
1. 競合から XML コードを調べ、&quot;_conflict&quot;属性を調べます。 カスタマイズされた形跡がないかを確認します。

**新しいビルドでオブジェクトが変更されたか。**

1. 「いつもの容疑者は？」 組み込みの Web アプリケーションまたはレポート（例：「deliveryValidation」、「deliveryOverview」、「budget」）。
1. 変更ログを見て更新がないかを調べます。
1. Adobe Campaignの専門家に聞いてみてください。
1. コードに対して「差分表示」を実行します。

### 競合の解決

競合を解決するには、次の手順に従います。

1. Adobe Campaign エクスプローラーで&#x200B;**管理／設定／パッケージ管理／競合を編集**&#x200B;に移動します。

1. リストで解決する競合を選択します。
競合を解決する方法は 3 つあります。 **新しいバージョンを承認**, **現在のバージョンを保持**, **コードを結合する（および解決済みとして宣言する）**, **競合を無視（非推奨）**.

**新しいバージョンを受け入れられるのはいつですか？**

* 標準機能が必要な場合
* カスタマイズしていない場合（カスタマイズした内容はすべて削除されます）

**現在のバージョンを維持できるのはいつですか？**

* カスタマイズしている場合
* 結合を実行したくない場合
* アップグレードが原因で競合しているオブジェクトを修正する必要がない場合

**結合を実行するタイミング**

* 結合できるのはフォーム、レポート、Web アプリケーションのみです。
* 小規模な結合であればコードの知識がなくても実行できる場合があります。
* 複雑な結合は適切なスキルと能力を持った人が実行する必要があります。
* 詳しくは、 [結合の実行](#perform-a-merge).

**競合を無視した場合はどうなりますか？**

* 競合した状態が続きます。
* オブジェクトはアップグレードされません。
* バージョンの互換性が失われたり、バグ修正を適用しても改善されなかったりといった長期的な影響が生じます。

>[!IMPORTANT]
>競合は解決することを強くお勧めします。
>

### 結合の実行{#perform-a-merge}

結合には様々なタイプがあります。

1. 簡単な結合：カスタム要素と新しい要素は小さく、無関係で、コーディングは不要です。
1. 変更なし：新しいバージョンを受け入れ、最終更新日のみ変更し、コメント、タブ、スペースまたは改行のみを受け入れます。 （例：意図しない保存）。
1. 些細な変更：1 行だけが変更されました。 （例：xpathToLoad）。
1. 複雑な結合：コーディングが必要な場合。 開発スキルが必要です。 詳しくは、 [複雑な結合](#complex-merges).

#### 結合方法

1. 3 つのバージョン（元のバージョン、新しいバージョン、カスタムバージョン）をすべて取得します。
1. 元のバージョンと新しいバージョンの間で「差分」を実行します。
1. 変更を抽出します。
1. 変更がない場合、現在のバージョンを維持して競合を解決します。

#### コードの場所

1. 組み込みコードは、datakit フォルダー内の XML ファイルに保存されます。 競合するオブジェクトに一致する XML ファイルを検索します。 例： installationDirectory\datakit\nms\fra\form\recipient.xml
1. 元のバージョンの取得：を使用 [ダウンロードセンター](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html) または製品のアップグレードされていない別のインストール。
1. 新しいバージョンの取得：経由で [ダウンロードセンター](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) またはお客様がインストールしたファイル。
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

1. ウィンドウの下部のセクションで、を検索します。 **_conflict_string_** 競合するエンティティを検索します。 新しいバージョンでインストールされたエンティティは新しい引数を持ちます。古いバージョンと一致するエンティティはカスタム引数を持ちます。
1. 保持しないバージョンを削除します。 を削除します。 **_conflict_argument_** 保持するエンティティの文字列。
1. 解決した競合に移動します。 **アクション**&#x200B;アイコンをクリックし、「**解決済みとして宣言**」を選択します。
1. 変更を保存します。これにより競合が解決します。

#### 高度な結合{#complex-merges}

1. 変更の内容を理解します。変更のリバースエンジニアリング、変更ログの調査、Adobe Campaignの専門家へのフォローアップを行います。
1. 変更の処理を決定します。
1. カスタマイズの内容を理解する：変更をリバースエンジニアリングします。

以下は高度な結合を実行する際の手順です。

1. 変更セットからコードのビットをコピーする
1. カスタマイズしたバージョンに貼り付けます。
1. カスタマイズの不回帰性のテスト
1. 変更の機能のテスト
1. ユーザー受け入れテストの実行
1. テスト環境で実行します。


>[!IMPORTANT]
>複雑な結合を実行するには、開発スキルが必要です。
>

**関連トピック**

* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign Classic リリースノート](../../rn/using/rn-overview.md)
* [Campaign Classic のヘルプとサポートのオプション](../../support.md)
* [Campaign の年別アップグレードプログラム](../../rn/using/rn-overview.md)
