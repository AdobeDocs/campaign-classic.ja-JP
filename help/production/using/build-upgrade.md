---
product: campaign
title: ビルドのアップグレードを開始
description: 新しいビルドにアップグレードするための主な手順を説明します
feature: Monitoring, Upgrade
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: c5a9c99a-4078-45d8-847b-6df9047a2fe2
TQID: https://experienceleague.adobe.com/XC0Q-35cYPjVHM-h2GNE570DqM8vxjSicu4vxnqYuSo
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2:
  - id: b82389f8-9b5e-4083-8e3b-3cef299fb8b9
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
subfeature_v2:
  - id: cfc95e9b-b035-4403-a6a9-b27a8a053a37
  - id: e3988c18-3cfa-4f16-b812-ac2d2b1056fa
  - id: e5e477db-ebc7-4368-ab0f-4d8fc2aed405
  - id: e656c701-3899-4db3-989c-de0980ddfffa
  - id: eff19c99-440a-4318-b319-444edc4d8d8f
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 2422
ht-degree: 38%

---

# ビルドアップグレードの実行{#performing-a-build-upgrade}



このセクションでは、アップグレードプロセスと、競合を特定して解決する手順について詳しく説明します。

ビルドのアップグレードは慎重に実行する必要があり、その影響は事前に完全に考慮する必要があり、手順は高レベルの規律で完了する必要があります。 アップグレードを成功させるには、以下に説明する手順を実行するのはエキスパートユーザーのみであることを確認してください。 また、アップグレードを開始する前に、[Adobe カスタマーケア &#x200B;](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)にお問い合わせいただくことを強くお勧めします。

次の前提条件が必要です。

* Campaign のアーキテクチャに関する理解
* システムおよびサーバーサイドの知識
* 管理者としての権限とアクセス許可

詳細については、次の節を参照してください。[Adobe Campaignの更新](../../production/using/upgrading.md)、[新しいバージョンへの移行](../../migration/using/about-migration.md)。

ホスト型およびハイブリッド型のインスタンスの場合は、Adobe Technical Operations チームにビルドのアップグレードをリクエストする必要があります。 詳しくは、このページの下部にある「よくある質問」セクションを参照してください。 [&#x200B; ビルドのアップグレードに関するFAQ](../../platform/using/faq-build-upgrade.md)も参照してください。

## アップグレードの準備

![](assets/do-not-localize/icon_planification.png)

ビルドのアップグレードを開始する前に、以下の説明に従って完全な準備を実行する必要があります。
システムをアップグレードする準備ができたら、ビルドのアップグレードに&#x200B;**少なくとも** 2時間かかります。

ビルドのアップグレードをおこなうには、以下のリソースが必要です。

* Adobe アーキテクト – データベース構造を理解する（すぐに使用できるスキーマと、追加された追加のスキーマ、キャンペーン設計、および特定の順序で開始してテストする必要があるクリティカルパス機能）。
* プロジェクトマネージャー – ビルドアップグレードに様々なインスタンス（実稼動、ステージング、テスト）およびその他のサードパーティサーバーとアプリケーション（データベース、SFTP サイト、メッセージングサービスプロバイダー）が含まれる場合、すべてのテストを調整するプロジェクトマネージャーを持つことはベストプラクティスと見なされます。
* Adobe Campaign管理者 – 管理者は、セキュリティ、フォルダーレイアウト、レポート、インポート\エクスポートの要件など、サーバーの構成を把握しています。 管理者がいない状況でビルドのアップグレードを実行しないでください。
* Adobe Campaign オペレーター（マーケティングユーザー） – アップグレードの成功は、ユーザーが日常業務を正常に実行できるかどうかにかかっています。 このため、アップグレードされたサーバーのテストには、必ず毎日1つ以上のオペレーターを含めてください。

### プランニング

ビルドのアップグレードを計画する際に重要なポイントを紹介します。

1. アップグレードには、少なくとも 2 時間確保しておく。
1. アドビおよびお客様側担当者の連絡先詳細を配布しておく。
1. ホステッド インスタンスの場合：Adobeとカスタマー担当者がアップグレードの時間と実行する担当者を調整します。
1. オンプレミスのインスタンスの場合：お客様側担当者がすべてのプロセスを管理します。カスタマイズされたワークフローや配信ロジックのテスト時にサポートが必要な場合は、コンサルティングサービスを依頼してください。
1. アップグレードするAdobe Campaignのバージョンを決定して確認します。[Adobe Campaign Classic リリースノート &#x200B;](../../rn/using/rn-overview.md)を参照してください。
1. アップグレードの実行可能ファイルがあることを確認します。

### キーパーソン

ビルドアップグレードプロセスには、次のメンバーが関与する必要があります。

* Adobe アーキテクト：ホスト型またはハイブリッド型アーキテクチャの場合、アーキテクトはAdobe Campaign Client Careと連携する必要があります。

* プロジェクトマネージャー：
   * オンプレミスでのインストールの場合：お客様の内部プロジェクトリーダーがアップグレードをリードし、ライフサイクルテストを管理します。

   * ホスト型インストールの場合：ホスティングチームは、Adobe Campaign クライアントケアチームとお客様と連携して、すべてのインスタンスのアップグレードタイムラインを調整します。

* Adobe Campaign管理者：
   * オンプレミス インストールの場合：管理者はアップグレードを実行します。

   * ホスト型インストールの場合：ホスティングチームがアップグレードを実行します。

* Adobe Campaign operator\marketing user: オペレーターは、開発、テストおよび実稼動インスタンスでテストを実行します。

### ビルドのアップグレードの準備

ビルドのアップグレードを開始する前に、オンプレミスのお客様は次の準備を行う必要があります。

1. アップグレード前にすべての開発作業がエクスポート（パッケージとしてエクスポート）可能であることを確認する。

1. 移行元の環境と移行先の環境のすべてのインスタンスについてデータベースの完全バックアップを作成する。

1. 最新バージョンの[&#x200B; サーバー設定ファイル &#x200B;](../../installation/using/the-server-configuration-file.md)を入手します。

1. [最新ビルドをダウンロード &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)。 [詳細情報](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)。

ビルドのアップグレードを開始する前に、すべての[便利なコマンドライン &#x200B;](../../installation/using/command-lines.md)を把握する必要もあります。

* **nlserver pdump**：実行中のプロセスのリストを表示します
* **nlserver pdump -who**：アクティブなクライアントセッションのリストを表示します
* **nlserver monitor -missing**：不足しているプロパティのリストを表示します
* **nlserver start process@instance-name**: プロセスを開始します
* **nlserver stop process@instance-name**: プロセスを停止します
* **nlserver restart process@instance-name**: プロセスを再起動します
* **nlserver shutdown**：すべてのCampaign プロセスを停止します
* **nlserver watchdog -svc**：ウォッチドッグを開始します（UNIX のみ）

## アップグレードの実行

![](assets/do-not-localize/icon_process.png)

以下の手順は、**オンプレミス**&#x200B;のお客様のみが実行できます。 ホステッド顧客の場合は、ホスティングチームが対応します。 Adobe Campaignを新しいビルドにアップデートするには、以下で詳細な手順を説明します。

### 環境の複製

ここでは、Adobe Campaign の環境を複製する方法を説明します。これにより、移行元の環境が移行先の環境に復元され、同一の作業環境が 2 つになります。

これを行うには、次の手順に従います。

1. 移行元となる環境に含まれているすべてのインスタンス上にあるデータベースのコピーを作成します。

1. 作成したコピーを、移行先となる環境のすべてのインスタンス上に復元します。

1. 起動前に、ターゲット環境で&#x200B;**nms:freezeInstance.js**&#x200B;焼灼化スクリプトを実行します。 これにより、ログ、トラッキング、配信、キャンペーンワークフローなど、外部とやり取りするすべてのプロセスが停止します。

   ```
   nlserverjavacsriptnms:freezeInstance.js–instance:<dev> -arg:run
   ```

1. 次のように、焼灼率を確認します。

   * IDが&#x200B;**0**&#x200B;に設定されている配信部分のみが配信部分であることを確認してください。

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

すべてのファイルを新しいバージョンに置き換えるには、nlserverserviceのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス （IIS）: **iisreset /stop**
   * Adobe Campaign サービス：**net stop nlserver6**

   >[!NOTE]
   >
   >IISで使用されているnlsrvmod.dll ファイルを新しいバージョンに置き換えられるように、リダイレクトサーバー（webmdl）が停止していることを確認します。
   >

1. **nlserver pdump** コマンドを実行して、アクティブなタスクがないことを検証します。 タスクがない場合、出力は次のようになります。

   ```
   C:\<installation path>\bin>nlserverpdump HH:MM:SS > Application Server for Adobe Campaign version x.x (build xxx) dated xx/xx/xxxx No tasks
   ```

1. すべてのプロセスが停止したことを確認するには、Windows タスク マネージャーを確認します。

### Adobe Campaign Server アプリケーションのアップグレード

1. **Setup.exe** ファイルを実行します。 このファイルをダウンロードする必要がある場合は、[&#x200B; ダウンロードセンター](https://experience.adobe.com/jp/downloads/content/software-distribution/en/campaign.html)にアクセスしてください。

1. インストールモードを選択：**更新**&#x200B;または&#x200B;**修復**。

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
   >この操作は、nlserverweb アプリケーションサーバー上で1回だけ実行する必要があります。
   >

   1つのデータベースのみを同期するには、次のコマンドを実行します。

   ```
   nlserver config -postupgrade -instance: <instance_name>
   ```

1. 同期によってエラーまたは警告が発生したかどうかを確認します。

### サービスの再起動

以下のサービスを再起動する必要があります。

* Web サービス （IIS）: **issreset /start**
* Adobe Campaign サービス：**net start nlserver6**

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

Campaign インスタンスでトランザクションメッセージ（Message Center）が有効になっている場合、アップグレードするには、次の追加手順を実行する必要があります。

1. Message Center の本番サーバーを、選択したバージョンに更新します。
1. ポストアップグレードスクリプトを実行します。
1. テストを実行して E メールが Message Center の本番用インスタンスを通じて正常に受信されることを確認します。
1. クライアントをアップグレードし、キャッシュをクリアします。
1. パッケージをエクスポートします。
   * クライアントパッケージのエクスポートツールを使用したパッケージのエクスポート
   * スキーマパッケージのインポート
   * クライアントの切断と再接続
   * データベースを更新
   * 切断して再接続
   * Admin パッケージのインポート
   * コンテンツパッケージの読み込み
   * コンテンツ管理パッケージのインポート
   * 切断して再接続
   * ワークフローの迅速なサニティーチェックの実行

1. Message Center テンプレートをパブリッシュして、サーバーと Message Center インスタンス間のインターフェイスが機能していることを確認します。
1. テストを実行して、Message Center実稼動インスタンスを通じてメールが正常に受信されていることを確認します。
1. 本番環境でワークフローのテストを実行して、配信が受信されることを確認します。

#### ミッドソーシング

ミッドソーシング環境のコンテキストでは、アップグレードするために次の追加手順を実行する必要があります。

1. ミッドソーシングサーバーのアップグレードを調整するには、[Adobe カスタマーケア &#x200B;](https://helpx.adobe.com/jp/enterprise/using/support-for-experience-cloud.html)にお問い合わせください。
1. テストリンクを実行して、バージョンが更新されたことを検証します。 例：

   ```
   http://[InsertServerURL]/r/test
   ```

>[!NOTE]
>
>ミッドソーシングサーバーは、マーケティングサーバーと常に同じバージョン（またはそれ以上の最新バージョン）を実行する必要があります。
>

## 紛争の場合

### 競合の特定

同期結果を確認する必要があります。 この手順は、オンプレミスのお客様のみが実行します。 ホステッド顧客の場合は、ホスティングチームが対応します。 同期結果の表示方法は 2 つあります。

コマンドラインインターフェイスでは、エラーは3つの山形「>>>」によって具現化され、同期は自動的に停止されます。 警告はダブルシェブロン「>>」によって実体化され、同期が完了したら解決する必要があります。 アップグレード後の最後に、コマンド プロンプトに概要が表示されます。 以下はその一例です。

```
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log =========Summary of the update==========
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
YYYY-MM-DD HH:MM:SS.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView‘ and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
```

警告がリソースの競合に関係する場合、それを解決するにはユーザーの注意が必要です。

**postupgrade_ServerVersionNumber_TimeOfPostupgrade.log** ファイルに同期結果が含まれています。 デフォルトでは、次のディレクトリで使用できます：**installationDirectory/var/`<instance-name>`/postupgrade**。 エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の分析

**競合はどのように見つかりますか？**

競合は、問題のサーバー上のpostupgrade.log内またはCampaign クライアントインターフェイス内で見つけることができます（管理/設定/パッケージ管理/競合の編集）。

識別子「stockOverview」およびタイプ「nms:webApp」を持つドキュメントは、新しいバージョンと競合しています。

競合が見つかった場合は、以下の条件に該当するかを確認します。

* お客様が変更またはカスタマイズしたオブジェクトか
* 本番環境で変更したオブジェクトか

これらの条件のいずれも当てはまらない場合、これは偽陽性です。 どちらにも該当する場合は、実際に競合が存在します。

**お客様がオブジェクトを変更しましたか？**

1. 競合しているオブジェクトを特定します。
1. お客様にオブジェクトを変更したかどうかを問い合わせます。
1. オブジェクトに異常がないかを確認します。
1. オブジェクトのコードに最終変更日が設定されているかを確認します。
1. 競合のXML コードで「_conflict」属性を調べます。 カスタマイズされた形跡がないかを確認します。

**新しいビルドでオブジェクトが変更されましたか？**

1. 「普通の容疑者はいるか？」 組み込みweb アプリケーションまたはレポート（例：「deliveryValidation」、「deliveryOverview」、「budget」）。
1. 変更ログを見て更新がないかを調べます。
1. Adobe Campaignの専門家に聞く。
1. コードに対して「差分表示」を実行します。

### 競合の解決

競合を解決するには、次の手順に従います。

1. Adobe Campaign エクスプローラーで&#x200B;**管理／設定／パッケージ管理／競合を編集**&#x200B;に移動します。

1. リストから解決する競合を選択します。
競合を解決するには、次の3つのオプションがあります。**新しいバージョンを承認**、**現在のバージョンを保持**、**コードを結合（および解決済みとして宣言）**、**競合を無視（推奨されません）**。

**新しいバージョンはいつ承認できますか？**

* 標準機能が必要な場合
* カスタマイズしていない場合（カスタマイズした内容はすべて削除されます）

**現在のバージョンはいつ保持できますか？**

* カスタマイズしている場合
* 結合を実行したくない場合
* アップグレードが原因で競合しているオブジェクトを修正する必要がない場合

**結合を実行するタイミング？**

* 結合できるのはフォーム、レポート、Web アプリケーションのみです。
* 小規模な結合であればコードの知識がなくても実行できる場合があります。
* 複雑な結合は適切なスキルと能力を持った人が実行する必要があります。
* [結合の実行](#perform-a-merge)を参照してください。

**競合を無視した場合はどうなりますか？**

* 競合した状態が続きます。
* オブジェクトはアップグレードされません。
* バージョンの互換性が失われたり、バグ修正を適用しても改善されなかったりといった長期的な影響が生じます。

>[!IMPORTANT]
>競合は解決することを強くお勧めします。
>

### 結合の実行{#perform-a-merge}

結合には様々なタイプがあります。

1. 容易な結合：カスタム要素と新規要素は小さく無関係で、コーディングは必要ありません。
1. 変更なし：新しいバージョンを受け入れる、最終更新日のみ変更する、コメント、タブ、スペースまたは新しい行のみ。 （例：意図しない保存）。
1. 軽微な変更：1行のみ変更されました。 （例：xpathToLoad）。
1. 複雑な結合：コーディングが必要な場合。 開発スキルが必要です。 [複合結合](#complex-merges)を参照してください。

#### 結合方法

1. 元のバージョン、新しいバージョン、カスタムバージョンの3つのバージョンをすべて取得します。
1. 元のバージョンと新しいバージョンの間に「差分」を実行します。
1. 変更を抽出します。
1. 変更がない場合、現在のバージョンを維持して競合を解決します。

#### コードの場所

1. ビルトインコードは、datakit フォルダーのXML ファイルに保存されます。 競合するオブジェクトに一致するXML ファイルを検索します。 例：installationDirectory\datakit\nms\fra\form\recipient.xml
1. 元のバージョンを取得します。[&#x200B; ダウンロードセンター](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)またはアップグレードされていない製品の別のインストールを使用します。
1. 新しいバージョンを取得します。[&#x200B; ダウンロードセンター](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)またはお客様がインストールしたファイルを使用します。
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
1. 非回帰を確認します。

手動で競合を解決する場合の手順は以下のとおりです。

1. ウィンドウの下部で&#x200B;**_conflict_string_**&#x200B;を検索して、競合のあるエンティティを見つけます。 新しいバージョンでインストールされたエンティティは新しい引数を持ちます。古いバージョンと一致するエンティティはカスタム引数を持ちます。
1. 保持しないバージョンを削除します。 保持しているエンティティの&#x200B;**_conflict_argument_**&#x200B;文字列を削除します。
1. 解決した競合に移動します。 **アクション**&#x200B;アイコンをクリックし、「**解決済みとして宣言**」を選択します。
1. 変更を保存します。これにより競合が解決します。

#### 高度な結合{#complex-merges}

1. 変更の内容を理解する：変更をリバースエンジニアリングし、変更ログを調べ、Adobe Campaignの専門家にフォローアップします。
1. 変更の処理方法を決定します。
1. カスタマイズの内容を理解する：変更のリバースエンジニアリング

以下は高度な結合を実行する際の手順です。

1. 変更セットからコードのビットをコピー
1. カスタマイズしたバージョンにペースト
1. カスタマイズの非回帰のテスト
1. 変更の機能をテストします
1. ユーザー同意テストの実行
1. テスト環境で実行します。


>[!IMPORTANT]
>複雑な結合を実行するには、開発スキルが必要です。
>

**関連トピック**

* [ビルドのアップグレードに関する FAQ](../../platform/using/faq-build-upgrade.md)
* [Campaign Classic リリースノート](../../rn/using/rn-overview.md)
* [Campaign Classic のヘルプとサポートのオプション](../../support.md)
* [Campaign年間アップグレードプログラム](../../rn/using/rn-overview.md)
