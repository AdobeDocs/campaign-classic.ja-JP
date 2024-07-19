---
product: campaign
title: ビルドアップグレードの概要
description: 新しいビルドにアップグレードするための主な手順を説明します
feature: Monitoring, Upgrade
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: c5a9c99a-4078-45d8-847b-6df9047a2fe2
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 36%

---

# ビルドアップグレードの実行{#performing-a-build-upgrade}



この節では、アップグレードプロセスと、競合を特定して解決する手順について詳しく説明します。

ビルドのアップグレードは慎重に行う必要があります。その影響は事前に十分に考慮する必要があり、手順は高いレベルの規律で完了する必要があります。 アップグレードを正常に行うには、以下に説明する手順を実行するのはエキスパートユーザーのみにしてください。 また、アップグレードを開始する前に、[Adobeサポート ](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html) に連絡することを強くお勧めします。

次の前提条件が必要です。

* Campaign のアーキテクチャに関する理解
* システムおよびサーバーサイドの知識
* 管理者としての権限とアクセス許可

詳しくは、[Adobe Campaignの更新 ](../../production/using/upgrading.md)、[ 新しいバージョンへの移行 ](../../migration/using/about-migration.md) の節を参照してください。

ホストインスタンスとハイブリッドインスタンスの場合、Adobeテクニカルオペレーションチームにビルドのアップグレードをリクエストする必要があります。 詳しくは、このページの下部にあるよくある質問の節を参照してください。 また、[ ビルドアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md) も参照してください。

## アップグレードの準備

![](assets/do-not-localize/icon_planification.png)

ビルドアップグレードを開始する前に、以下に説明するように完全な準備を行う必要があります。
システムをアップグレードする準備が整ったら、ビルドアップグレードには **少なくとも** 2 時間かかります。

ビルドのアップグレードをおこなうには、以下のリソースが必要です。

* Adobeアーキテクト – データベース構造（標準提供のスキーマと追加のスキーマ、キャンペーン設計、特定の順序で開始およびテストする必要があるクリティカルパス機能）を理解します。
* プロジェクトマネージャー – ビルドアップグレードに多数の異なるインスタンス（実稼動、ステージング、テスト）やその他のサードパーティのサーバーおよびアプリケーション（データベース、SFTP サイト、メッセージングサービスプロバイダー）が関与する場合、すべてのテストを調整するプロジェクトマネージャーを使用することがベストプラクティスと見なされます。
* Adobe Campaign管理者 – 管理者は、セキュリティ、フォルダーレイアウト、レポートおよびインポート/エクスポートの要件など、サーバーの設定を把握しています（ただし、これに限定されません）。 管理者がいない状況でビルドのアップグレードを実行しないでください。
* Adobe Campaign オペレーター（マーケティングユーザー） – アップグレードを成功させるには、ユーザーが日々のタスクを正常に実行できるかどうかが決まります。 このため、アップグレードされたサーバーのテストには、常に毎日 1 人以上のオペレーターを含めてください。

### 計画

ビルドのアップグレードを計画する際に重要なポイントを紹介します。

1. アップグレードには、少なくとも 2 時間確保しておく。
1. アドビおよびお客様側担当者の連絡先詳細を配布しておく。
1. ホステッド環境のインスタンスの場合：Adobeとお客様のスタッフが、アップグレードの時間と実行者を調整します。
1. オンプレミスのインスタンスの場合：お客様側担当者がすべてのプロセスを管理します。カスタマイズされたワークフローや配信ロジックのテスト時にサポートが必要な場合は、コンサルティングサービスを依頼してください。
1. アップグレード先のAdobe Campaignのバージョンを特定して確認します。[Adobe Campaign Classic リリースノート ](../../rn/using/rn-overview.md) を参照してください。
1. アップグレードの実行可能ファイルがあることを確認します。

### 主要人物

ビルドアップグレードプロセスには、次のユーザーが必要です。

* Adobeアーキテクト：ホストアーキテクチャまたはハイブリッドアーキテクチャの場合、アーキテクトはAdobe Campaign クライアントケアと連携する必要があります。

* プロジェクトマネージャー：
   * オンプレミスインストールの場合：お客様の社内プロジェクトリーダーがアップグレードを主導し、ライフサイクルテストを管理します。

   * ホステッド環境でのインストールの場合：ホスティングチームは、Adobe Campaign Client Care チームおよびお客様と協力して、すべてのインスタンスのアップグレードタイムラインを調整します。

* Adobe Campaign管理者：
   * オンプレミスインストールの場合：管理者がアップグレードを実行します。

   * ホスト環境インストールの場合：ホスティングチームがアップグレードを実行します。

* Adobe Campaign オペレーター\マーケティングユーザー：開発、テスト、実稼動の各インスタンスでテストを実行します。

### ビルドアップグレードの準備

ビルドのアップグレードを開始する前に、オンプレミスのお客様は次の準備を行う必要があります。

1. アップグレード前にすべての開発作業がエクスポート（パッケージとしてエクスポート）可能であることを確認する。

1. 移行元の環境と移行先の環境のすべてのインスタンスについてデータベースの完全バックアップを作成する。

1. [ サーバー設定ファイル ](../../installation/using/the-server-configuration-file.md) の最新バージョンを取得します。

1. [ 最新ビルドをダウンロードします ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)。 [詳細情報](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)。

また、ビルドアップグレードを開始する前に、[ 役に立つコマンドライン ](../../installation/using/command-lines.md) をすべて理解しておく必要があります。

* **nlserver pdump**：実行中のプロセスのリストを表示します
* **nlserver pdump -who**：アクティブなクライアントセッションのリストを表示します
* **nlserver monitor -missing**：不足しているプロパティのリストを表示します
* **nlserver start process@instance-name**: プロセスを開始します
* **nlserver stop process@instance-name**: プロセスを停止します
* **nlserver restart process@instance-name**: プロセスを再起動します
* **nlserver シャットダウン**：すべての Campaign プロセスを停止します
* **nlserver watchdog -svc**：ウォッチドッグを開始します（UNIX のみ）

## アップグレードの実行

![](assets/do-not-localize/icon_process.png)

以下の手順は、（オンプレミス **のお客様のみが実行** ます。 ホスト環境のお客様の場合は、ホスティングチームが対応します。 Adobe Campaignを新しいビルドに更新する手順について詳しくは、以下で説明します。

### 環境を複製

ここでは、Adobe Campaign の環境を複製する方法を説明します。これにより、移行元の環境が移行先の環境に復元され、同一の作業環境が 2 つになります。

これを行うには、次の手順に従います。

1. 移行元となる環境に含まれているすべてのインスタンス上にあるデータベースのコピーを作成します。

1. 作成したコピーを、移行先となる環境のすべてのインスタンス上に復元します。

1. 起動する前に、ターゲット環境で **nms:freezeInstance.js** 焼灼スクリプトを実行します。 これにより、ログ、トラッキング、配信、キャンペーンワークフローなど、外部とやり取りするすべてのプロセスが停止します。

   ```
   nlserverjavacsriptnms:freezeInstance.js–instance:<dev> -arg:run
   ```

1. 次の手順に従って、焼灼を確認します。

   * ID が **0** に設定されている配信部分が唯一であることを確認します。

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

すべてのファイルを新しいバージョンに置き換えるには、nlserverservice のすべてのインスタンスがシャットダウンされている必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）: **iisreset /stop**
   * Adobe Campaign サービス：**net stop nlserver6**

   >[!NOTE]
   >
   >IIS で使用される nlsrvmod.dll ファイルを新しいバージョンに置き換えられるように、リダイレクトサーバー（webmdl）が停止されていることを確認します。
   >

1. **nlserver pdump** コマンドを実行して、アクティブなタスクがないことを検証します。 タスクがない場合の出力は次のようになります。

   ```
   C:\<installation path>\bin>nlserverpdump HH:MM:SS > Application Server for Adobe Campaign version x.x (build xxx) dated xx/xx/xxxx No tasks
   ```

1. Windows タスクマネージャーで、すべてのプロセスが停止したことを確認します。

### Adobe Campaign Server アプリケーションのアップグレード

1. **Setup.exe** ファイルを実行します。 このファイルをダウンロードする必要がある場合は、[ ダウンロードセンター ](https://experience.adobe.com/jp/downloads/content/software-distribution/en/campaign.html) にアクセスしてください。

1. インストール モードとして **更新** または **修復** を選択します。

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
   >この操作は、nlserverweb アプリケーションサーバーで 1 回だけ実行してください。
   >

   1 つのデータベースのみを同期するには、次のコマンドを実行します。

   ```
   nlserver config -postupgrade -instance: <instance_name>
   ```

1. 同期でエラーまたは警告が発生したかどうかを確認します。

### サービスの再起動

以下のサービスを再起動する必要があります。

* Web サービス （IIS）: **issreset /start**
* Adobe Campaign サービス：**net start nlserver6**

### クライアントコンソールの更新

クライアントコンソールは、サーバーインスタンスと同じビルド上にある必要があります。

Adobe Campaign アプリケーションサーバーがインストールされているマシン（nlserverweb）で、以下のファイルをダウンロードしてインストールします。

```
Setup-client-7.xxxx.exe in [path of the application]\datakit\nl\en\jsp
```

次回クライアントコンソールに接続したときに、ウィンドウが開いて新しい更新が利用可能なことを知らせるメッセージが表示され、その更新をダウンロードしてインストールするよう促されます。

### 特定の追加タスク

一部の設定では、新しいビルドに更新するために、特定の追加タスクが必要です。

#### トランザクションメッセージ

トランザクションメッセージ（Message Center）が Campaign インスタンスで有効になっている場合は、アップグレードするために次の追加手順を実行する必要があります。

1. Message Center の本番サーバーを、選択したバージョンに更新します。
1. ポストアップグレードスクリプトを実行します。
1. テストを実行して E メールが Message Center の本番用インスタンスを通じて正常に受信されることを確認します。
1. クライアントをアップグレードし、キャッシュをクリアします。
1. パッケージをエクスポートします。
   * クライアントパッケージのエクスポートツールを使用したパッケージのエクスポート
   * スキーマパッケージをインポート
   * クライアントの切断と再接続
   * データベースの更新
   * 切断して再接続します
   * 管理パッケージのインポート
   * コンテンツパッケージをインポート
   * コンテンツ管理パッケージの読み込み
   * 切断して再接続します
   * ワークフローの健全性を簡単にチェック

1. Message Center テンプレートをパブリッシュして、サーバーと Message Center インスタンス間のインターフェイスが機能していることを確認します。
1. テストを実行し、Message Center の実稼動インスタンスを介してメールが正常に受信されることを確認します。
1. 本番環境でワークフローのテストを実行して、配信が受信されることを確認します。

#### ミッドソーシング

ミッドソーシング環境のコンテキストでは、アップグレードするための次の追加手順を実行する必要があります。

1. ミッドソーシングサーバーのアップグレードの調整については、{0](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)Adobeカスタマーケア } にお問い合わせください。[
1. テストリンクを実行して、バージョンが更新されていることを確認します。 例：

   ```
   http://[InsertServerURL]/r/test
   ```

>[!NOTE]
>
>ミッドソーシングサーバーは、常にマーケティングサーバーと同じバージョン（または新しいバージョン）を実行する必要があります。
>

## 競合の場合

### 競合の特定

同期結果を確認する必要があります。 この手順は、オンプレミスのお客様のみが実行します。 ホスト環境のお客様の場合は、ホスティングチームが対応します。 同期結果の表示方法は 2 つあります。

コマンドラインインターフェイスでは、エラーは 3 つの山形「>>>」で実体化され、同期は自動的に停止します。 警告は、2 つの山形記号「>>」によって実体化され、同期が完了したら解決する必要があります。 アップグレード後に、コマンドプロンプトに概要が表示されます。 以下はその一例です。

```
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log =========Summary of the update==========
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView‘ and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
```

リソースの競合に関する警告の場合は、それを解決するためにユーザーの注意が必要です。

**postupgrade_ServerVersionNumber_TimeOfPostupgrade.log** ファイルには、同期結果が含まれます。 デフォルトでは、**installationDirectory/var/`<instance-name>`/postupgrade** ディレクトリで使用できます。 エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の分析

**競合はどのように見つかりましたか？**

競合は、対象となるサーバーの postupgrade.log 内、または Campaign クライアントインターフェイス（管理/設定/パッケージ管理/競合を編集）内で見つかります。

The document with identifier ‘stockOverview’ and type ‘nms:webApp’ is in conflict with the new version.

競合が見つかった場合は、以下の条件に該当するかを確認します。

* お客様が変更またはカスタマイズしたオブジェクトか
* 本番環境で変更したオブジェクトか

これらの条件がどちらも適用されない場合、これは偽陽性です。 どちらにも該当する場合は、実際に競合が存在します。

**オブジェクトは顧客によって変更されていますか？**

1. 競合しているオブジェクトを特定します。
1. お客様にオブジェクトを変更したかどうかを問い合わせます。
1. オブジェクトに異常がないかを確認します。
1. オブジェクトのコードに最終変更日が設定されているかを確認します。
1. 「_conflict」属性の競合から XML コードを調べます。 カスタマイズされた形跡がないかを確認します。

**オブジェクトは新しいビルドで変更されましたか？**

1. 何か「普通の容疑者？」 ビルトインの web アプリケーションまたはレポート（例：「deliveryValidation」、「deliveryOverview」、「budget」）。
1. 変更ログを見て更新がないかを調べます。
1. Adobe Campaignの専門家に質問してください。
1. コードに対して「差分表示」を実行します。

### 競合の解決

競合を解決するには、次の手順に従います。

1. Adobe Campaign エクスプローラーで&#x200B;**管理／設定／パッケージ管理／競合を編集**&#x200B;に移動します。

1. リストで解決する競合を選択します。
競合を解決するオプションは 3 つあります。**新しいバージョンを承認する**、**現在のバージョンを保持する**、**コードを結合（および解決済みとして宣言）**、**競合を無視（推奨しません）** です。

**新しいバージョンを受け入れることはできますか？**

* 標準機能が必要な場合
* カスタマイズしていない場合（カスタマイズした内容はすべて削除されます）

**最新バージョンを保持できるのはいつですか？**

* カスタマイズしている場合
* 結合を実行したくない場合
* アップグレードが原因で競合しているオブジェクトを修正する必要がない場合

**結合を実行するタイミング**

* 結合できるのはフォーム、レポート、Web アプリケーションのみです。
* 小規模な結合であればコードの知識がなくても実行できる場合があります。
* 複雑な結合は適切なスキルと能力を持った人が実行する必要があります。
* [ 結合の実行 ](#perform-a-merge) を参照してください。

**競合を無視するとどうなりますか？**

* 競合した状態が続きます。
* オブジェクトはアップグレードされません。
* バージョンの互換性が失われたり、バグ修正を適用しても改善されなかったりといった長期的な影響が生じます。

>[!IMPORTANT]
>競合は解決することを強くお勧めします。
>

### 結合の実行{#perform-a-merge}

結合には様々なタイプがあります。

1. 簡単に結合：カスタム要素と新しい要素は小さく、無関係で、コーディングは必要ありません。
1. 変更なし：新しいバージョンを受け入れる、最終更新日のみ変更する、コメント、タブ、スペース、または新しい行のみ変更する。 （例：意図しない保存）。
1. 些細な変更：変更された行は 1 行だけです。 （例：xpathToLoad）。
1. 複雑な結合：コーディングが必要な場合。 開発スキルが必要です。 [ 複雑な結合 ](#complex-merges) を参照してください。

#### 結合方法

1. 元のバージョン、新しいバージョン、カスタムバージョンの 3 つのバージョンをすべて取得します。
1. 元のバージョンと新しいバージョンの「差分」を実行します。
1. 変更を抽出します。
1. 変更がない場合、現在のバージョンを維持して競合を解決します。

#### コードの場所

1. 組み込みコードは、データキットフォルダーの XML ファイルに保存されます。 競合するオブジェクトに一致する XML ファイルを検索します。 例：installationDirectory\datakit\nms\fra\form\recipient.xml
1. [ ダウンロードセンター ](https://experience.adobe.com/#/downloads/content/software-distribution/ja/campaign.html) またはアップグレードされていない別の製品インストールから、元のバージョンを取得します。
1. [ ダウンロードセンター ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) またはお客様のインストール済みファイルから、新しいバージョンを取得します。
1. カスタムバージョンの取得：Campaign クライアント内からオブジェクトのソースコードを取得します。

### 差分表示の実行方法

1. テキストエディターまたは結合エディター（Notepad ++、AraxisMerge、WinMerge など）をインストールします。
1. エディターで元のファイルと新しいファイルを開きます。
1. 差分表示（2 つのファイルの比較）を実行します。
1. 差分を特定します。

### 結合方法

1. カスタムバージョンから着手します。
1. 変更を適用します。
1. 競合を解決済みと宣言して解決します。
1. 非回帰をチェックします。

手動で競合を解決する場合の手順は以下のとおりです。

1. ウィンドウの下部で、**_conflict_string_** を検索して、競合するエンティティを見つけます。 新しいバージョンでインストールされたエンティティは新しい引数を持ちます。古いバージョンと一致するエンティティはカスタム引数を持ちます。
1. 保持しないバージョンを削除します。 保持しているエンティティの **_conflict_argument_** 文字列を削除します。
1. 解決した競合に移動します。 **アクション**&#x200B;アイコンをクリックし、「**解決済みとして宣言**」を選択します。
1. 変更を保存します。これにより競合が解決します。

#### 高度な結合{#complex-merges}

1. 変更内容を理解する：変更内容をリバースエンジニアリングし、変更内容ログを確認して、Adobe Campaignのエキスパートによるフォローアップを行います。
1. 変更の処理方法を決定します。
1. カスタマイズの機能を理解する：変更のリバースエンジニアリング

以下は高度な結合を実行する際の手順です。

1. 変更セットからコードをコピーします
1. カスタマイズしたバージョンに貼り付け
1. カスタマイズの非回帰のテスト
1. 変更機能のテスト
1. ユーザー受け入れテストの実行
1. テスト環境で実行します。


>[!IMPORTANT]
>複雑な融合を行うには開発力が必要です。
>

**関連トピック**

* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign Classic リリースノート](../../rn/using/rn-overview.md)
* [Campaign Classic のヘルプとサポートのオプション](../../support.md)
* [Campaign 年次アップグレードプログラム](../../rn/using/rn-overview.md)
