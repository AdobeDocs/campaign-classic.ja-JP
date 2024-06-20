---
product: campaign
title: 新しいビルドへのアップグレード
description: 新しいビルドにアップグレードするための技術的な手順を説明します
feature: Monitoring, Upgrade
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4aaa6256-256a-441d-80c9-430f8e427875
source-git-commit: 1be1528d657537786c430ea9c8bdb3aad58ba20d
workflow-type: tm+mt
source-wordcount: '1154'
ht-degree: 8%

---

# 新しいビルド（オンプレミス）へのアップグレード{#upgrading}



アップグレードプロセスを開始する前に、アップグレード先のAdobe Campaignのバージョンを特定して確認し、 [リリースノート](../../rn/using/latest-release.md) .

>[!IMPORTANT]
>
>* Adobeでは、更新する前に、各インスタンスでデータベースのバックアップを作成することを強くお勧めします。 詳しくは、[この節](../../production/using/backup.md)を参照してください。
>* アップグレードを実行するには、インスタンスとログにアクセスする機能と権限があることを確認します。
>* 読み上げる [この節](../../installation/using/general-architecture.md) および [ビルドのアップグレード](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html) 開始する前に章を作成します。
>

## Windows {#in-windows}

Windows 環境では、次の手順に従ってAdobe Campaignを新しいビルドに更新します。

* [サービスのシャットダウン](#shut-down-services),
* [アプリケーションサーバーのアップグレード](#upgrade-the-adobe-campaign-server-application),
* [リソースの同期](#synchronize-resources),
* [再起動サービス](#restart-services).

クライアントコンソールの更新方法については、を参照してください。 [この節](../../installation/using/client-console-availability-for-windows.md).

### サービスのシャットダウン {#shut-down-services}

すべてのファイルを新しいバージョンに置き換えるには、nlserver サービスのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）：

     **iisreset /stop**

   * Adobe Campaign サービス： **net stop nlserver6**

   >[!IMPORTANT]
   >
   >また、リダイレクトサーバー（webmdl）が **nlsrvmod.dll** iis で使用されるファイルは、新しいバージョンに置き換えることができます。

1. を実行して、アクティブなタスクがないことを確認します。 **nlserver pdump** コマンド。 次の問題が発生します。

   ```sql
   C:<installation path>Adobe Campaign v7bin>nlserver pdump
   HH:MM:SS > Application Server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   No tasks
   ```

   Windows タスク マネージャを使用して、すべてのプロセスが停止していることを確認できます。

### Adobe Campaign サーバーアプリケーションのアップグレード {#upgrade-the-adobe-campaign-server-application}

アップグレードファイルを実行するには、次の手順に従います。

1. 実行 **setup.exe**.

   このファイルをダウンロードするには、に接続してください [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) ユーザー資格情報を使用して。 ソフトウェア配布について詳しくは、を参照してください。 [このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja).

1. インストールモードを選択します。を選択してください。 **[!UICONTROL 更新または修復]**
1. クリック **[!UICONTROL 次]** .
1. クリック **[!UICONTROL 終了]** .

   次に、インストールプログラムは新しいファイルをコピーします。

1. 操作が完了したら、 **[!UICONTROL 終了]** .

### リソースの同期 {#synchronize-resources}

次のコマンドラインを使用します。

**nlserver config -postupgrade -allinstances**

これにより、次の操作を実行できます。

* リソースの同期
* スキーマの更新
* データベースの更新

>[!NOTE]
>
>この操作は一度だけ、かつ（**nlserver web**） アプリケーションサーバー。

次に、同期でエラーまたは警告が生成されたかどうかを確認します。 詳しくは、次を参照してください [アップグレードの競合の解決](#resolving-upgrade-conflicts).

### サービスの再起動 {#restart-services}

再開するサービスは次のとおりです。

* Web サービス（IIS）：

  **iisreset /start**

* Adobe Campaign サービス： **net start nlserver6**

## Linux {#in-linux}

Linux 環境では、次の手順に従ってAdobe Campaignを新しいビルドに更新します。

* [更新されたパッケージのダウンロード](#obtain-updated-packages),
* [更新の実行](#perform-an-update),
* [Web サーバーを再起動します。](#reboot-the-web-server).

[クライアントコンソールの可用性の詳細情報](../../installation/using/client-console-availability-for-windows.md).

>[!NOTE]
>
>ビルド 8757 以降、サードパーティライブラリは必要なくなりました。

### 更新されたパッケージの取得 {#obtain-updated-packages}

まず、Adobe Campaignの更新されたパッケージを両方とも復元します。次にを接続します： [ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) ユーザー資格情報を使用して。 ソフトウェア配布について詳しくは、を参照してください。 [このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja).

ファイルは **nlserver6-v7-XXX.rpm**

### 更新の実行 {#perform-an-update}

* RPM ベースの配布（RedHat、SuSe）

  これらをインストールするには、ルートとしてを実行します。

  ```
  $rpm -Uvh nlserver6-v7-XXXX.rpm
  ```

  ここで、XXX はファイルのバージョンです。

  rpm ファイルは、CentOS/Red Hat ディストリビューションで見つけることができるパッケージに依存しています。 これらの依存関係の一部を使用しない場合は、rpm の「nodeps」オプションを使用する必要があります。

  ```
  rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
  ```

* DEB ベースの配布（Debian）

  これらをインストールするには、ルートとしてを実行します。

  ```
  dpkg -i nlserver6-v7-XXXX-amd64_debX.deb
  ```

>[!NOTE]
>
>完全なインストール手順については、を参照してください。 [この節](../../installation/using/installing-campaign-standard-packages.md). リソースは自動的に同期されますが、エラーが発生していないことを確認する必要があります。 詳しくは、次を参照してください [アップグレードの競合の解決](#resolving-upgrade-conflicts).

### Web サーバーを再起動します。 {#reboot-the-web-server}

新しいライブラリを適用するには、Apache をシャットダウンする必要があります。

これを行うには、次のコマンドを実行します。

```
/etc/init.d/apache stop
```

>[!IMPORTANT]
>
>* スクリプトは、 **httpd** の代わりに **apache**.
>* 次の応答が得られるまで、このコマンドを実行する必要があります。
>
>   この操作は、Apache が新しいライブラリを適用するために必要です。

次に、Apache を再起動します。

```
/etc/init.d/apache start
```

## アップグレードの競合の解決 {#resolving-upgrade-conflicts}

リソースの同期中、 **アップグレード後** コマンドを使用すると、同期でエラーまたは警告が生成されたかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果を表示する方法は 2 つあります。

* コマンドラインインターフェイスでは、エラーは 3 つの山形で表現されます **>>>** 同期は自動的に停止します。 警告は二重の山形で実体化されます **>>** 同期が完了したらおよびを解決する必要があります。 アップグレード後に、コマンドプロンプトに概要が表示されます。 以下はその一例です。

  ```
  2013-04-09 07:48:39.749Z 00002E7A 1 info log =========Summary of the update==========
  2013-04-09 07:48:39.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
  2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
  2013-04-09 07:48:39.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
  ```

  リソースの競合に関する警告の場合は、それを解決するためにユーザーの注意が必要です。

* この **postupgrade_`<server version number>_<time of postupgrade>`.log** ログファイルには、同期結果が含まれます。 デフォルトでは、次のディレクトリに格納されています。 **`<installation directory>/var/<instance/postupgrade`**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の解決 {#resolving-conflicts}

競合を解決するには、次の手順に従います。

1. Adobe Campaign ツリーで、に移動します。 **[!UICONTROL 管理/設定/パッケージ管理/競合を編集]** .
1. リストから解決する競合を選択します。

競合を解決する方法は 3 つあります。

* **[!UICONTROL 解決済みとして宣言]** ：事前にユーザーの介入が必要です。
* **[!UICONTROL 新しいバージョンを承認します]** :Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合にお勧めします。
* **[!UICONTROL 現在のバージョンを保持]** ：更新が拒否されたことを意味します。

  >[!IMPORTANT]
  >
  >この解決モードを選択した場合、新しいバージョンで修正してもメリットが得られない場合があります。

競合を手動で解決することを選択した場合は、次の手順を実行します。

1. ウィンドウの下部で、 **_矛盾_** 競合するエンティティを検索する文字列。 新しいバージョンでインストールされるエンティティには、 **新規** 以前のバージョンと一致するエンティティを持つ引数 **cus** 引数。

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 を削除 **_conflict_argument_** 保持するエンティティの文字列。

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。 「」をクリックします **[!UICONTROL アクション]** アイコンと選択 **[!UICONTROL 解決済みとして宣言]** .
1. 変更を保存します。これにより競合が解決します。

### ベストプラクティス {#best-practices}

更新エラーは、データベース構成にリンクされている場合があります。 技術管理者とデータベース管理者が実行する設定に互換性があることを確認します。

例えば、Unicode データベースは、LATIN1 データなどの保存を許可するだけでなく、

## 利用可能な更新についてクライアントコンソールに警告する {#warn-the-client-consoles-of-the-available-update}

### Windows {#in-windows-1}

Adobe Campaign アプリケーションサーバーがインストールされているマシン上（**nlserver web**）、ファイルをダウンロードしてコピーします。  **setup-client-6.XXXX.exe** いいえ **[アプリケーションのパス]/datakit/nl/eng/jsp**.

次回クライアントコンソールが接続されると、ウィンドウに更新の可用性が通知され、ユーザーは更新のダウンロードとインストールが可能になります。

>[!NOTE]
>
>IIS_XPG ユーザーにこのインストールファイルに対する適切な読み取り権限があることを確認し、を参照してください。 [インストールガイド](../../installation/using/general-architecture.md) を参照してください。

### Linux {#in-linux-1}

Adobe Campaign アプリケーションサーバー（**nlserver web**）がインストールされています。を取得します  **setup-client-6.XXXX.exe** パッケージ化してコピー、として保存 **/usr/local/neolane/nl6/datakit/nl/eng/jsp**:

```
 cp setup-client-6.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
```

次回クライアントコンソールが接続されると、ウィンドウに更新の可用性が通知され、ユーザーは更新のダウンロードとインストールが可能になります。

>[!NOTE]
>
>Apache ユーザーにこのインストールファイルに対する適切な読み取り権限があることを確認し、を参照してください。 [インストールガイド](../../installation/using/general-architecture.md) を参照してください。
