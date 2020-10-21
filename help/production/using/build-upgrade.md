---
title: ビルドのアップグレードを開始する
description: 新しいビルドにアップグレードするための主な手順
page-status-flag: never-activated
uuid: f24552d4-6bdf-411c-a1f2-b8f339c311f4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
discoiquuid: f8e3633d-7232-44a5-842b-1a70c4f2bca2
translation-type: tm+mt
source-git-commit: 8ec525f400c29b986eadd888d29f1579860871c6
workflow-type: tm+mt
source-wordcount: '2366'
ht-degree: 52%

---


# ビルドアップグレードの実行{#performing-a-build-upgrade}

このセクションでは、アップグレードプロセスの詳細なチュートリアルと、競合を識別して解決する手順を説明します。

ビルドのアップグレードは慎重におこなう必要があります。必ず事前にアップグレードが及ぼす影響を検討し、作業は高度なスキルを備えた人が実行するようにしてください。アップグレードを正常に完了するために、後述の手順を実行する人はエキスパートユーザーに限定してください。また、アップグレードを開始する前に [Adobe カスタマーサポート](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)に連絡することを強くお勧めします。

アップグレードの前提条件は以下のとおりです。

* Campaign のアーキテクチャに関する理解
* システムおよびサーバーサイドの知識
* 管理者としての権限とアクセス許可

詳しくは、次の節を参照してください。 [Adobe Campaignの更新](../../production/using/upgrading.md)、新しいバージョン [への移行](../../migration/using/about-migration.md)。

ホストされているインスタンスおよびハイブリッドインスタンスの場合、アドビのテクニカルオペレーションチームにビルドのアップグレードをリクエストする必要があります。詳しくは、このページの下にあるよくある質問の節を参照してください。Also consult the [build upgrade FAQ](../../platform/using/faq-build-upgrade.md).

## アップグレードの準備

![](assets/do-not-localize/icon_planification.png)

ビルドアップグレードを開始する前に、以下の説明に従って完全な準備を行う必要があります。
システムをアップグレードする準備が整ったら、ビルドのアップグレードに **は** 2時間以上かかります。

ビルドのアップグレードをおこなうには、以下のリソースが必要です。

* adobeアーキテクト — データベース構造(標準搭載のスキーマ、追加されたその他のスキーマ、キャンペーン設計、および特定の順序で開始およびテストする必要のある重要なパス機能)を理解します。
* プロジェクトマネージャー — ビルドのアップグレードに多数の異なるインスタンス（実稼働、ステージング、テスト）や、他のサードパーティのサーバーおよびアプリケーション(データベース、SFTPサイト、メッセージングサービスプロバイダー)が含まれる場合、ベストプラクティスと見なされます。
* Adobe Campaign 管理者：管理者はセキュリティ、フォルダーの配置、レポート、インポートおよびエクスポートの要件をはじめとするサーバーの設定を把握しています。管理者がいない状況でビルドのアップグレードを実行しないでください。
* adobe campaignオペレーター（マーケティングユーザー） — アップグレードを成功させるには、ユーザーが日次タスクを正常に実行できるかどうかに依存します。このため、必ず、アップグレードしたサーバーのテストに日別演算子を少なくとも1つ含めてください。

### 計画

ビルドのアップグレードを計画する際に重要なポイントを紹介します。

1. アップグレードには、少なくとも 2 時間確保しておく。
1. アドビおよびお客様側担当者の連絡先詳細を配布しておく。
1. ホストインスタンスの場合：Adobeとお客様のスタッフは、アップグレードの時間と実行者を調整します。
1. オンプレミスのインスタンスの場合：お客様側担当者がすべてのプロセスを管理します。カスタマイズされたワークフローや配信ロジックのテスト時にサポートが必要な場合は、コンサルティングサービスを依頼してください。
1. Determine and confirm which version of Adobe Campaign you want to upgrade to - consult the [Adobe Campaign Classic release notes](../../rn/using/rn-overview.md).
1. アップグレードの実行可能ファイルがあることを確認します。

### 主要人物

ビルドのアップグレードプロセスには、次の担当者が関与する必要があります。

* Adobeアーキテクト：ホストアーキテクチャまたはハイブリッドアーキテクチャの場合、アーキテクトはAdobe CampaignのClientCareと連携する必要があります。

* プロジェクトマネージャー：
   * オンプレミスインストールの場合：お客様の社内プロジェクトリーダーは、アップグレードをリードし、ライフサイクルテストを管理します。

   * ホストインストールの場合：ホスティングチームは、Adobe CampaignのClientCareチームおよびお客様と提携して、すべてのインスタンスのアップグレードの日程を調整します。

* Adobe Campaign 管理者：:
   * オンプレミスインストールの場合：管理者がアップグレードを実行します。

   * ホストインストールの場合：ホスティングチームがアップグレードを実行します。

* Adobe Campaign演算子\マーケティングユーザー：演算子は、開発、テストおよび実稼働のインスタンスに対してテストを実行します。

### ビルドのアップグレードの準備

ビルドアップグレードを開始する前に、オンプレミスのお客様は次の準備を行う必要があります。

1. アップグレード前にすべての開発作業がエクスポート（パッケージとしてエクスポート）可能であることを確認する。

1. 移行元の環境と移行先の環境のすべてのインスタンスについてデータベースの完全バックアップを作成する。

1. サー [バー設定ファイルの最新バージョンを取得します](../../installation/using/the-server-configuration-file.md)。

1. 最新のビルドをダウンロードします。 [ダウンロードセンターの詳細を表示します](https://docs.adobe.com/content/help/ja-JP/experience-cloud/software-distribution/home.html)。

You also need to know all the [useful command lines](../../installation/using/command-lines.md) before starting a build upgrade:

* **nlserver pdump**：実行中のプロセスのリストを表示します
* **nlserver pdump -who**：アクティブなクライアントセッションのリストを表示します
* **nlserver monitor -missing**：不足しているプロパティのリストを表示します
* **nlserver開始process@instanceName**:プロセスの開始
* **nlserver stop process@instanceName**:プロセスの停止
* **nlserver restart process@instanceName**:プロセスを再開する
* **nlserver shutdown**:すべてのキャンペーンプロセスを停止します。
* **nlserver watchdog -svc**：ウォッチドッグを開始します（UNIX のみ）

## アップグレードの実行

![](assets/do-not-localize/icon_process.png)

以下の手順は、 **オンプレミスのお客様のみが実行し** ます。 ホスト版のお客様については、ホスティングチームがこの作業を実行します。Adobe Campaignを新しいビルドに更新するには、詳細な手順を以下に説明します。

### 環境の重複

ここでは、Adobe Campaign の環境を複製する方法を説明します。これにより、移行元の環境が移行先の環境に復元され、同一の作業環境が 2 つになります。

これをおこなうには、以下の手順に従います。

1. 移行元となる環境に含まれているすべてのインスタンス上にあるデータベースのコピーを作成します。

1. 作成したコピーを、移行先となる環境のすべてのインスタンス上に復元します。

1. 起動する前に、 **nms:freezeInstance.js** 焼灼スクリプトをターゲット環境で実行します。 これにより、外部との対話をすべてのプロセスが停止します。ログ、トラッキング、配信、キャンペーンワークフローなど

   ```
   nlserverjavacsriptnms:freezeInstance.js–instance:<dev> -arg:run
   ```

1. 次に示すように、注意を確認します。

   * Check that the only delivery part is the one which ID is set to **0**:

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

   * Webサービス(IIS): **iisreset / stop**
   * Adobe Campaignサービス： **net stop nlserver6**

   >[!NOTE]
   >
   >IIS で使用されている nlsrvmod.dll ファイルを新しいバージョンで置き換えることができるように、リダイレクションサーバー（webmdl）が停止したことを確認してください。

1. **nlserver pdump** コマンドを実行してアクティブなタスクがないことを確認します。タスクがない場合、出力は次のようになります。

   ```
   C:\<installation path>\bin>nlserverpdump HH:MM:SS > Application Server for Adobe Campaign version x.x (build xxx) dated xx/xx/xxxx No tasks
   ```

1. Windowsタスクマネージャーで、すべてのプロセスが停止したことを確認します。

### Adobe Campaignサーバーアプリケーションのアップグレード

1. Setup **.exe** ファイルを実行します。 このファイルをダウンロードする必要がある場合は、ダウンロードセンター [にアクセスします](https://docs.adobe.com/content/help/ja-JP/experience-cloud/software-distribution/home.html)。

1. インストールモードを選択します。 **更新** または **修復**。

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
   >この操作は、nlserverwebアプリケーションサーバー上でのみ実行する必要があります。

   1つのデータベースのみを同期するには、次のコマンドを実行します。

   ```
   nlserver config -postupgrade -instance: <instance_name>
   ```

1. 同期でエラーまたは警告が生成されたかどうかを確認します。

### サービスの再起動

以下のサービスを再起動する必要があります。

* Webサービス(IIS): **issreset /開始**
* Adobe Campaignサービス： **net開始nlserver6**

### クライアントコンソールの更新

Adobe Campaign アプリケーションサーバーがインストールされているマシン（nlserverweb）で、以下のファイルをダウンロードしてインストールします。


    ```
    Setup-client-7.xxxx.exe in [path of the application]\datakit\nl\en\jsp
    ```

次回クライアントコンソールに接続したときに、ウィンドウが開いて新しい更新が利用可能なことを知らせるメッセージが表示され、その更新をダウンロードしてインストールするよう促されます。

### 特定の追加タスク

一部の設定では、新しいビルドに更新するために特定の追加タスクが必要です。

#### トランザクションメッセージング

キャンペーンインスタンスでトランザクションメッセージング(Message Center)が有効になっている場合、次の追加手順を実行してアップグレードする必要があります。

1. Message Center の本番サーバーを、選択したバージョンに更新します。
1. ポストアップグレードスクリプトを実行します。
1. テストを実行して E メールが Message Center の本番用インスタンスを通じて正常に受信されることを確認します。
1. クライアントをアップグレードし、キャッシュをクリアします。
1. パッケージをエクスポートします。
   * クライアントパッケージエクスポートツールを使用したパッケージのエクスポート
   * スキーマパッケージの読み込み
   * クライアントの切断と再接続
   * データベースの更新
   * 切断して再接続
   * 管理パッケージのインポート
   * コンテンツパッケージの読み込み
   * コンテンツ管理パッケージの読み込み
   * 切断して再接続
   * ワークフローのサニティチェックを簡単に実行する

1. Message Center テンプレートをパブリッシュして、サーバーと Message Center インスタンス間のインターフェイスが機能していることを確認します。
1. テストを実行して、Message Center実稼働インスタンスを通じて電子メールが正常に受信されたことを確認します。
1. 本番環境でワークフローのテストを実行して、配信が受信されることを確認します。

#### ミッドソーシング

ミッドソーシング環境のコンテキストで、次の追加手順を実行してアップグレードする必要があります。

1. Contact [Adobe Customer Care](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) to coordinate the upgrade of the Mid-Sourcing server.
1. テストリンクを実行して、バージョンが更新されたことを検証します。 例：

   ```
   http://[InsertServerURL]/r/test
   ```

>[!NOTE]
>
>ミッドソーシングサーバーは、常に、マーケティングサーバーと同じバージョン（または最新のバージョン）を実行する必要があります。


## 競合が発生した場合

### 競合を識別

同期結果を確認する必要があります。 ここで紹介する手順はオンプレミス版のお客様のみを対象にしています。ホスト版のお客様については、ホスティングチームがこの作業を実行します。同期結果の表示方法は 2 つあります。

コマンドラインインターフェイスでは、エラーはトリプルシェブロン&#39;>>&#39;によって実現され、同期は自動的に停止します。 警告は、重複の山形「>>」によって実現され、同期が完了したら解決する必要があります。 ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。以下はその一例です。

```
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log =========Summary of the update==========
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView‘ and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
```

リソースの競合に関する警告は、見落とさないように注意して、解決してください。

postupgrade_ServerVersionNumber_TimeOfPostupgrade.log **** ファイルには、同期結果が格納されます。 デフォルトでは、次のディレクトリで使用できます。 **installationDirectory/var/instanceName/postupgrade**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合を分析する

**競合を見つける方法**

競合は、該当するキャンペーンのpostupgrade.log内、またはサーバークライアントインターフェイス内（管理/設定/パッケージ管理/競合を編集）で見つかります。

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

1. 「常習犯」の仕業かもしれません。組み込みのWebアプリケーションまたはレポート(例：&#39;deliveryValidation&#39;、&#39;deliveryOverview&#39;、&#39;budget&#39;)。
1. 変更ログを見て更新がないかを調べます。
1. Adobe Campaignの専門家に聞いて。
1. コードに対して「差分表示」を実行します。

### 競合の解決

競合を解決するには、次の手順に従います。

1. Adobe Campaign エクスプローラーで&#x200B;**管理／設定／パッケージ管理／競合を編集**&#x200B;に移動します。

1. リストから解決する競合を選択します。競合を解決するには、次の3つの方法があります。 **新しいバージョンを受け入れ**、 **現在のバージョンを保持**、コードを **結合（解決と宣言）、競合を**&#x200B;無視（推奨しません） ****。

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
* 結合の [実行を参照してください](#perform-a-merge)。

**競合を放置した場合**

* 競合した状態が続きます。
* オブジェクトはアップグレードされません。
* バージョンの互換性が失われたり、バグ修正を適用しても改善されなかったりといった長期的な影響が生じます。

>[!CAUTION]
>競合は解決することを強くお勧めします。


### 結合の実行{#perform-a-merge}

結合には様々なタイプがあります。

1. 簡単な結合：カスタム要素と新規要素は小さく、無関係で、コーディングは必要ありません。
1. 変更なし：新しいバージョンを承認します。最終更新日のみ変更され、コメント、タブ、スペース、新規行のみ反映されます（例：意図しない保存）。
1. 軽微な変更：1 行のみ変更されます（例：xpathToLoad）。
1. 高度な結合：コーディングが必要な場合です。開発に関するスキルが必要です。複雑な結合を参照して [ください](#complex-merges)。

#### 結合方法

1. 3つのバージョンをすべて入手する：元のバージョン、新しいバージョン、およびカスタムバージョン。
1. 元のバージョンと新しいバージョンの間で「相違」を実行します。
1. 変更を抽出します。
1. 変更がない場合、現在のバージョンを維持して競合を解決します。

#### コードの場所

1. 組み込みコードは、データキットフォルダー内のXMLファイルに保存されます。 競合しているオブジェクトに対応する XML ファイルを探します。例：installationDirectory\datakit\nms\fra\form\recipient.xml
1. 元のバージョンを取得します。ダウンロ [ードセンター](https://docs.adobe.com/content/help/ja-JP/experience-cloud/software-distribution/home.html) 、または製品のアップグレードされていない他のインストールを使用します。
1. 新しいバージョンを取得します。[ [ダウンロードセンター](https://docs.adobe.com/content/help/ja-JP/experience-cloud/software-distribution/home.html) ]またはお客様のインストール済みファイルを使用します。
1. カスタムバージョンの取得：Campaign クライアント内からオブジェクトのソースコードを取得します。

### 差分表示の実行方法

1. テキストエディターまたは結合エディター（Notepad ++、AraxisMerge、WinMerge など）をインストールします。
1. エディターで元のファイルと新しいファイルを開きます。
1. 差分表示（2 つのファイルの比較）を実行します。
1. 差分を特定します。

### 結合方法

1. カスタムバージョンから着手します。
1. 変更を適用します。
1. 解決したと宣言して競合を解決します。
1. 回帰しないかどうかを確認します。

手動で競合を解決する場合の手順は以下のとおりです。

1. In the lower section of the window, search for the **_conflict_string_** to locate the entities with conflicts. 新しいバージョンでインストールされたエンティティは新しい引数を持ちます。古いバージョンと一致するエンティティはカスタム引数を持ちます。
1. 維持しないバージョンを削除します。Delete the **_conflict_argument_** string of the entity you are keeping.
1. 解決した競合に移動します。**アクション**&#x200B;アイコンをクリックし、「**解決済みとして宣言**」を選択します。
1. 変更を保存します。これにより競合が解決します。

#### 高度な結合{#complex-merges}

1. 変更の効果を理解する：変更をリバースエンジニアリングし、変更ログを調べ、Adobe Campaignの専門家にフォローアップします。
1. 変更の処理を決定します。
1. カスタマイズの機能を理解します。変更をリバースエンジニアリングする

以下は高度な結合を実行する際の手順です。

1. 変更セットからコードのビットをコピー
1. カスタマイズしたバージョンに貼り付けます。
1. カスタマイズの非回帰性のテスト
1. 変更の機能のテスト
1. ユーザー受け入れテストの実行
1. テスト環境で実行します。


>[!CAUTION]
>複雑な結合を実行するには、開発スキルが必要です。


**関連トピック**

* [ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign Classic リリースノート](../../rn/using/rn-overview.md)
* [Campaign Classicのヘルプとサポートのオプション](https://helpx.adobe.com/campaign/kb/ac-support.html#acc-support-req)
* [ゴールドスタンダードプログラム](https://helpx.adobe.com/jp/campaign/kb/gold-standard.html)