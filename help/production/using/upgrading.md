---
title: アップグレード
seo-title: アップグレード
description: アップグレード
seo-description: null
page-status-flag: never-activated
uuid: f24552d4-6bdf-411c-a1f2-b8f339c311f4
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
discoiquuid: f8e3633d-7232-44a5-842b-1a70c4f2bca2
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 1c86322fa95aee024f6c691b61a10c21a9a22eb7

---


# アップグレード{#upgrading}

アップグレードプロセスを開始する前に、アップグレード対象のAdobe Campaignのバージョンを決定し、確認して、リリースノートを参 [照してください](https://docs.campaign.adobe.com/doc/AC/en/RN.html)。

>[!CAUTION]
>
>更新する前に、各インスタンスでデータベースのバックアップを作成することを強くお勧めします。 詳しくは、「バックアップ」を参照して [ください](../../production/using/backup.md)。\
>アップグレードを実行するには、インスタンスとログにアクセスする権限と権限を持っていることを確認します。

>[!NOTE]
>
>インストールガイドとビルドア [ップグレードの概要](../../installation/using/general-architecture.md) (英語の [み](http://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html) )も参照してください。

## Windowsの場合 {#in-windows}

新しいビルドを配信する際にAdobe Campaignを新しいバージョンに更新するには、Windowsで次の手順を適用する必要があります。

* [サービスのシャットダウン](#shut-down-services),
* [Adobe Campaign サーバーアプリケーションのアップグレード](#upgrade-the-adobe-campaign-server-application),
* [リソースの同期](#synchronize-resources),
* [サービスの再起動](#restart-services).

クライアントコンソールの更新方法については、この節を参照 [してください](../../installation/using/client-console-availability-for-windows.md)。

### サービスのシャットダウン {#shut-down-services}

すべてのファイルを新しいバージョンに置き換えるには、nlserverサービスのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）：

      **iisreset /stop**

   * Adobe Campaignサービス：net **stop nlserver6**
   >[!CAUTION]
   >
   >You also need to make sure the redirection server (webmdl) is stopped, so that the **nlsrvmod.dll** file used by IIS can be replaced with the new version.

1. Check that no tasks are active by running the **nlserver pdump** command. 次の情報が表示されます。

   ```
   C:<installation path>Adobe Campaign v7bin>nlserver pdump
   HH:MM:SS > Application Server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   No tasks
   ```

   Windowsのタスクマネージャーを使用して、すべてのプロセスが停止していることを確認できます。

### Adobe Campaign サーバーアプリケーションのアップグレード {#upgrade-the-adobe-campaign-server-application}

アップグレードファイルを実行するには、次の手順を適用します。

1. **setup.exeを実行します**。

   このファイルをダウンロードするには、ダウンロードセンターリンクからAdobe Campaign Support [ページ](https://support.neolane.net/)(https://support.neolane.net/ **)にア** クセスします。

1. Select the installation mode: choose **[!UICONTROL Update or repair]**
1. クリック **[!UICONTROL Next]** .
1. クリック **[!UICONTROL Finish]** .

   次に、インストールプログラムは新しいファイルをコピーします。

1. Once the operation is complete, click **[!UICONTROL Finish]** .

### リソースの同期 {#synchronize-resources}

次のコマンドラインを使用します。

**nlserver config -postupgrade -allinstances**

これにより、次の操作を実行できます。

* リソースの同期,
* スキーマの更新、
* データベースを更新します。

>[!NOTE]
>
>この操作は、(**nlserver web**)アプリケーションサーバー上でのみ1回だけ実行します。

次に、同期にエラーまたは警告が生成されているかどうかを確認します。 詳しくは、「アップグレードの競合の解 [決」を参照してください](#resolving-upgrade-conflicts)。

### サービスの再起動 {#restart-services}

再起動するサービスは次のとおりです。

* Web サービス（IIS）：

   **iisreset /start**

* Adobe Campaignサービス： **net start nlserver6**

## Linuxの場合 {#in-linux}

新しいビルドの配信時にAdobe Campaignを新しいバージョンに更新するには、Linuxの手順を次に示します。

* [更新されたパッケージの取得](#obtain-updated-packages)、
* [更新の実行](#perform-an-update)、
* [Webサーバーを再起動します](#reboot-the-web-server)。

クライアントコンソールの更新方法については、この節を参照 [してください](../../installation/using/client-console-availability-for-linux.md)。

>[!NOTE]
>
>ビルド8757から、サードパーティのライブラリは不要になりました。

### 更新されたパッケージの取得 {#obtain-updated-packages}

最初に、Adobe Campaignの両方の更新済みパッケージを回復します。ダウンロードセンターリンクからAdobe Campaign Supportペ [ージ](https://support.neolane.net/)(https://support.neolane.net/ **)に** 移動します。

ファイル **はnlserver6-v7-XXX.rpmです。**

### 更新の実行 {#perform-an-update}

* RPMベースの配布(RedHat、SuSe)

   これらをインストールするには、rootとして実行します。

   ```
   $rpm -Uvh nlserver6-v7-XXXX.rpm
   ```

   XXXはファイルのバージョンです。

   rpmファイルは、CentOS/Red hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使いたくない場合は、rpmの&quot;nodeps&quot;オプションを使う必要があるかもしれません。

   ```
   rpm --nodeps -Uvh nlserver6-v7-XXXX-0.x86_64.rpm
   ```

* DEBベースの配布(Debian)

   これらをインストールするには、rootとして実行します。

   ```
   dpkg -i nlserver6-v7-XXXX-amd64_debX.deb
   ```

>[!NOTE]
>
>完全なインストール手順については、この節 [で説明します](../../installation/using/installing-campaign-standard-packages.md)。 リソースは自動的に同期されますが、エラーが発生していないことを確認する必要があります。 詳しくは、「アップグレードの競合の解 [決」を参照してください](#resolving-upgrade-conflicts)。

### Webサーバーの再起動 {#reboot-the-web-server}

新しいライブラリを適用するには、Apacheをシャットダウンする必要があります。

これを行うには、次のコマンドを実行します。

```
/etc/init.d/apache stop
```

>[!CAUTION]
>
>* スクリプトは、 **apacheではなく** httpdと呼ばれる場合が **あります**。
>* 次の応答を取得するまで、このコマンドを実行する必要があります。
   >この操作は、Apacheが新しいライブラリを適用するために必要です。
>



次に、Apacheを再起動します。

```
/etc/init.d/apache start
```

## アップグレードの競合の解決 {#resolving-upgrade-conflicts}

リソースの同期中に、postupgrade **** コマンドを使用して、同期にエラーが発生したか、警告が発生したかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果を表示する方法は2つあります。

* In the command-line interface, errors are materialized by a triple chevron **>>>** and synchronization is stopped automatically. Warnings are materialized by a double chevron **>>** and must be resolved once synchronization is complete. ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。以下はその一例です。

   ```
   2013-04-09 07:48:39.749Z 00002E7A 1 info log =========Summary of the update==========
   2013-04-09 07:48:39.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
   2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
   2013-04-09 07:48:39.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
   ```

   リソースの競合に関する警告は、見落とさないように注意して、解決してください。

* postupgrade_ **.logログファイルには`<server version number>_<time of postupgrade>`** 、同期結果が格納されます。 It is available by default in the following directory: **`<installation directory>/var/<instance/postupgrade`**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の解決 {#resolving-conflicts}

競合を解決するには、次の手順に従います。

1. Adobe Campaignツリーで、に進みます **[!UICONTROL Administration > Configuration > Package management > Edit conflicts]** 。
1. リストから解決する競合を選択します。

競合を解決するには、次の3つの方法があります。

* **[!UICONTROL Declare as resolved]** :は、事前にユーザーの介入が必要です。
* **[!UICONTROL Accept the new version]** :adobe Campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL Keep the current version]** :は、更新が拒否されたことを意味します。

   >[!CAUTION]
   >
   >この解像度モードを選択した場合、新しいバージョンで修正を行う必要が生じない場合があります。

競合を手動で解決する場合は、次の手順に従います。

1. In the lower section of the window, search for the **_conflict_** string to locate the entities with conflicts. The entity installed with the new version contains the **new** argument, the entity that matches the previous version contains the **cus** argument.

   ![](assets/s_ncs_production_conflict002.png)

1. 維持しないバージョンを削除します。Delete the **_conflict_argument_** string of the entity you are keeping.

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。アイコンをクリ **[!UICONTROL Actions]** ックし、を選択しま **[!UICONTROL Declare as resolved]** す。
1. 変更を保存します。これにより競合が解決します。

### ベストプラクティス{#best-practices}

更新エラーがデータベース構成にリンクされている可能性があります。 技術管理者とデータベース管理者が実行する設定が互換性があることを確認します。

例えば、Unicodeデータベースは、LATIN1データなどのストレージを許可するだけではありません。

## Warn the client consoles of the available update {#warn-the-client-consoles-of-the-available-update}

### Windowsの場合 {#in-windows-1}

On the machine where the (**nlserver web**) Adobe Campaign application server is installed, download and copy the file

**setup-client-6。** XXXX **.exe**

**アプリケ[ーションのパス]**datakitlengthjsp

次回クライアントコンソールに接続すると、ウィンドウが開き、アップデートの利用可能性がユーザーに通知され、ダウンロードおよびインストールの可能性が提供されます。

>[!NOTE]
>
>IIS_XPGユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細についてはインスト [ールガイド](../../installation/using/general-architecture.md) を参照してください。

### Linuxの場合 {#in-linux-1}

Adobe Campaignアプリケーションサーバー(**nlserver web**)がインストールされているコンピューターで、次のパッケージを取得します。

**setup-client-6。** XXXX **.exe**

それをコピーし、 **/usr/local/neolane/nl6/datakit/nl/eng/jsp**:

```
 cp setup-client-6.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
```

次回クライアントコンソールに接続すると、ウィンドウが開き、アップデートの利用可能性がユーザーに通知され、ダウンロードおよびインストールの可能性が提供されます。

>[!NOTE]
>
>Apacheユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については『インス [トールガイド](../../installation/using/general-architecture.md) 』を参照してください。

