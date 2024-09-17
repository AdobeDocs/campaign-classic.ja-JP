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
source-git-commit: 1ab08a89b17fca20e9497696417ecba580e26802
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 新しいビルド（オンプレミス）へのアップグレード{#upgrading}

アップグレードプロセスを開始する前に、アップグレード先のAdobe Campaignのバージョンを特定して確認し、[ リリースノート ](../../rn/using/latest-release.md) を参照してください。

>[!IMPORTANT]
>
>* Adobeでは、更新する前に、各インスタンスでデータベースのバックアップを作成することを強くお勧めします。 詳しくは、[この節](../../production/using/backup.md)を参照してください。
>* アップグレードを実行するには、インスタンスとログにアクセスする機能と権限があることを確認します。
>* 開始する前に、[ この節 ](../../installation/using/general-architecture.md) と [ ビルドアップグレード ](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html) の章を参照してください。
>

## Windows {#in-windows}

Windows 環境では、次の手順に従ってAdobe Campaignを新しいビルドに更新します。

* [ サービスのシャットダウン ](#shut-down-services)、
* [ アプリケーションサーバーのアップグレード ](#upgrade-the-adobe-campaign-server-application)、
* [ リソースの同期 ](#synchronize-resources)、
* [ サービスを再起動します ](#restart-services)。

クライアントコンソールの更新方法については、[ この節 ](../../installation/using/client-console-availability-for-windows.md) を参照してください。

### サービスのシャットダウン {#shut-down-services}

すべてのファイルを新しいバージョンに置き換えるには、nlserver サービスのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）：

     **iisreset /stop**

   * Adobe Campaign サービス：**net stop nlserver6**

   >[!IMPORTANT]
   >
   >また、IIS で使用する **nlsrvmod.dll** ファイルを新しいバージョンに置き換えられるように、リダイレクトサーバー（webmdl）が停止していることを確認する必要があります。

1. **nlserver pdump** コマンドを実行して、アクティブなタスクがないことを確認します。 次の問題が発生します。

   ```sql
   C:<installation path>Adobe Campaign v7bin>nlserver pdump
   HH:MM:SS > Application Server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   No tasks
   ```

   Windows タスク マネージャを使用して、すべてのプロセスが停止していることを確認できます。

### Adobe Campaign サーバーアプリケーションのアップグレード {#upgrade-the-adobe-campaign-server-application}

アップグレードファイルを実行するには、次の手順に従います。

1. **setup.exe** を実行します。

   このファイルをダウンロードするには、ユーザーの資格情報を使用して [ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) に接続します。 ソフトウェア配布について詳しくは、[ このページ ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja) を参照してください。

1. インストールモードを選択します。**[!UICONTROL 更新または修復]** を選択します。
1. **[!UICONTROL 次へ]** をクリックします。
1. 「**[!UICONTROL 終了]**」をクリックします。

   次に、インストールプログラムは新しいファイルをコピーします。

1. 操作が完了したら、「**[!UICONTROL 終了]**」をクリックします。

### リソースの同期 {#synchronize-resources}

次のコマンドラインを使用します。

**nlserver config -postupgrade -allinstances**

これにより、次の操作を実行できます。

* リソースの同期
* スキーマの更新
* データベースの更新

>[!NOTE]
>
>この操作は、1 回だけ、（**nlserver web**）アプリケーションサーバーでのみ実行してください。

次に、同期でエラーまたは警告が生成されたかどうかを確認します。 詳しくは、[ アップグレードの競合の解決 ](#resolving-upgrade-conflicts) を参照してください。

### サービスの再起動 {#restart-services}

再開するサービスは次のとおりです。

* Web サービス（IIS）：

  **iisreset /start**

* Adobe Campaign サービス：**net start nlserver6**

## Linux {#in-linux}

Linux 環境では、次の手順に従ってAdobe Campaignを新しいビルドに更新します。

* [ 更新されたパッケージをダウンロードします ](#obtain-updated-packages)、
* [ 更新の実行 ](#perform-an-update)、
* [Web サーバーを再起動します ](#reboot-the-web-server)。

[ クライアントコンソールの可用性の詳細 ](../../installation/using/client-console-availability-for-windows.md)。

### 更新されたパッケージの取得 {#obtain-updated-packages}

まず、Adobe Campaignの更新されたパッケージを両方とも復元します。ユーザー資格情報を使用して [ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html) に接続します。 ソフトウェア配布について詳しくは、[ このページ ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja) を参照してください。

ファイルは **nlserver6-v7-XXX.rpm**

>[!AVAILABILITY]
>
>v7.4.1 以降、RPM Linux パッケージ用のライブラリは Campaign に含まれなくなりました。 これらのライブラリをインストールしてください。
> 


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
>すべてのインストール手順について詳しくは、[ この節 ](../../installation/using/installing-campaign-standard-packages.md) を参照してください。 リソースは自動的に同期されますが、エラーが発生していないことを確認する必要があります。 詳しくは、[ アップグレードの競合の解決 ](#resolving-upgrade-conflicts) を参照してください。

### Web サーバーを再起動します。 {#reboot-the-web-server}

新しいライブラリを適用するには、Apache をシャットダウンする必要があります。

これを行うには、次のコマンドを実行します。

```
/etc/init.d/apache stop
```

>[!IMPORTANT]
>
>* スクリプトは **apache** ではなく **httpd** と呼ばれる場合があります。
>* 次の応答が得られるまで、このコマンドを実行する必要があります。
>
>   この操作は、Apache が新しいライブラリを適用するために必要です。

次に、Apache を再起動します。

```
/etc/init.d/apache start
```

## アップグレードの競合の解決 {#resolving-upgrade-conflicts}

リソースの同期中に、**postupgrade** コマンドを使用すると、同期でエラーまたは警告が生成されたかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果を表示する方法は 2 つあります。

* コマンドラインインターフェイスでは、エラーは 3 つの山形 **>>>** で具体化され、同期は自動的に停止します。 警告は二重の山形 **>>** で実体化され、同期が完了したら解決する必要があります。 アップグレード後に、コマンドプロンプトに概要が表示されます。 以下はその一例です。

  ```
  2013-04-09 07:48:39.749Z 00002E7A 1 info log =========Summary of the update==========
  2013-04-09 07:48:39.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
  2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
  2013-04-09 07:48:39.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
  ```

  リソースの競合に関する警告の場合は、それを解決するためにユーザーの注意が必要です。

* **postupgrade_`<server version number>_<time of postupgrade>`.log** ログファイルには、同期結果が含まれます。 このフォルダーは、デフォルトで次のディレクトリに格納されています。**`<installation directory>/var/<instance/postupgrade`** エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の解決 {#resolving-conflicts}

競合を解決するには、次の手順に従います。

1. Adobe Campaign ツリーで、**[!UICONTROL 管理/設定/パッケージ管理/競合を編集]** に移動します。
1. リストから解決する競合を選択します。

競合を解決する方法は 3 つあります。

* **[!UICONTROL 解決済みとして宣言]**：事前にユーザーの介入が必要です。
* **[!UICONTROL 新しいバージョンを承認]** :Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合にお勧めします。
* **[!UICONTROL 現在のバージョンを保持]**：更新が拒否されることを意味します。

  >[!IMPORTANT]
  >
  >この解決モードを選択した場合、新しいバージョンで修正してもメリットが得られない場合があります。

競合を手動で解決することを選択した場合は、次の手順を実行します。

1. ウィンドウの下部で、**_conflict_** 文字列を検索して、競合するエンティティを見つけます。 新しいバージョンでインストールされたエンティティには **new** 引数が含まれ、以前のバージョンに一致するエンティティには **cus** 引数が含まれます。

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 保持しているエンティティの **_conflict_argument_** 文字列を削除します。

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。 **[!UICONTROL アクション]** アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

### ベストプラクティス {#best-practices}

更新エラーは、データベース構成にリンクされている場合があります。 技術管理者とデータベース管理者が実行する設定に互換性があることを確認します。

例えば、Unicode データベースは、LATIN1 データなどの保存を許可するだけでなく、

## 利用可能な更新についてクライアントコンソールに警告する {#warn-the-client-consoles-of-the-available-update}

### Windows {#in-windows-1}

Adobe Campaign アプリケーションサーバーをインストールしているマシン（**nlserver web**）から、**setup-client-6.XXXX.exe** i n **[path of the application]/datakit/nl/eng/jsp** をダウンロードしてコピーします。

次回クライアントコンソールが接続されると、ウィンドウに更新の可用性が通知され、ユーザーは更新のダウンロードとインストールが可能になります。

>[!NOTE]
>
>IIS_XPG ユーザーにこのインストールファイルに対する適切な読み取り権限があることを確認し、詳しくは [ インストールガイド ](../../installation/using/general-architecture.md) を参照してください。

### Linux {#in-linux-1}

Adobe Campaign アプリケーションサーバー（**nlserver web**）をインストールしたマシンで、**setup-client-6.XXXX.exe** パッケージを取得してコピーし、**/usr/local/neolane/nl6/datakit/nl/eng/jsp** として保存します。

```
 cp setup-client-6.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
```

次回クライアントコンソールが接続されると、ウィンドウに更新の可用性が通知され、ユーザーは更新のダウンロードとインストールが可能になります。

>[!NOTE]
>
>Apache ユーザーにこのインストールファイルに対する適切な読み取り権限があることを確認し、詳しくは [ インストールガイド ](../../installation/using/general-architecture.md) を参照してください。
