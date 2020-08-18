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
source-git-commit: 5598682078a8fd3c8d9ecdca083f3a310c48f5f0
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 14%

---


# アップグレード{#upgrading}

アップグレードプロセスを開始する前に、アップグレードするAdobe Campaignのバージョンを決定して確認し、 [リリースノート](../../rn/using/latest-release.md) を参照してください。

>[!CAUTION]
>
>更新する前に、各インスタンスでデータベースのバックアップを作成することを強くお勧めします。 詳細については、「 [バックアップ](../../production/using/backup.md)」を参照してください。\
>アップグレードを実行するには、インスタンスとログにアクセスする権限と権限を持っていることを確認します。

>[!NOTE]
>
>インストー [ルガイド](../../installation/using/general-architecture.md) 、 [ビルドアップグレードの概要も参照してください](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html) 。

## Windowsの場合 {#in-windows}

新しいビルドを配信する際に新しいバージョンのAdobe Campaignを更新するには、Windowsで次の手順を適用する必要があります。

* [サービスのシャットダウン](#shut-down-services),
* [Adobe Campaign サーバーアプリケーションのアップグレード](#upgrade-the-adobe-campaign-server-application),
* [リソースの同期](#synchronize-resources),
* [サービスの再起動](#restart-services).

クライアントコンソールの更新方法については、 [この節を参照してください](../../installation/using/client-console-availability-for-windows.md)。

### サービスのシャットダウン {#shut-down-services}

すべてのファイルを新しいバージョンで置き換えるには、nlserverサービスのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）：

      **iisreset /stop**

   * Adobe Campaignサービス： **net stop nlserver6**
   >[!CAUTION]
   >
   >You also need to make sure the redirection server (webmdl) is stopped, so that the **nlsrvmod.dll** file used by IIS can be replaced with the new version.

1. Check that no tasks are active by running the **nlserver pdump** command. 次のようになります。

   ```
   C:<installation path>Adobe Campaign v7bin>nlserver pdump
   HH:MM:SS > Application Server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   No tasks
   ```

   Windowsタスクマネージャーを使用して、すべてのプロセスが停止していることを確認できます。

### Adobe Campaign サーバーアプリケーションのアップグレード {#upgrade-the-adobe-campaign-server-application}

アップグレードファイルを実行するには、次の手順を適用します。

1. **setup.exeを実行します**。

   このファイルをダウンロードするには、[ [ダウンロードセンター](https://support.neolane.net/)]リンクから[Adobe Campaignサポート]ページ(https://support.neolane.net/ **** )にアクセスします。

1. インストールモードを選択します。「 **[!UICONTROL 更新」または「修復」を選択する]**
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL 完了]**」をクリックします。

   次に、インストールプログラムが新しいファイルをコピーします。

1. 処理が完了したら「**[!UICONTROL 完了]**」をクリックします。

### リソースの同期 {#synchronize-resources}

次のコマンドラインを使用します。

**nlserver config -postupgrade -allinstances**

これにより、次の操作を実行できます。

* リソースの同期,
* スキーマの更新、
* データベースを更新します。

>[!NOTE]
>
>この操作は、(**nlserver web**)アプリケーションサーバー上でのみ1回だけ実行する必要があります。

次に、同期でエラーが発生したか、警告が発生したかを確認します。 詳しくは、「アップグレードの競合の [解決](#resolving-upgrade-conflicts)」を参照してください。

### サービスの再起動 {#restart-services}

再起動するサービスは次のとおりです。

* Web サービス（IIS）：

   **iisreset /開始**

* Adobe Campaignサービス： **net開始nlserver6**

## Linuxの場合 {#in-linux}

新しいビルドが提供されるときに新しいバージョンのAdobe Campaignを更新するには、Linuxの手順を次に示します。

* [更新されたパッケージの取得](#obtain-updated-packages)、
* [更新の実行](#perform-an-update)、
* [Webサーバーを再起動します](#reboot-the-web-server)。

クライアントコンソールの更新方法については、 [この節を参照してください](../../installation/using/client-console-availability-for-linux.md)。

>[!NOTE]
>
>Build 8757から、サードパーティのライブラリは不要になりました。

### 更新されたパッケージの取得 {#obtain-updated-packages}

Adobe Campaignの両方の更新されたパッケージを回復することによる開始:[ [ダウンロードセンター](https://support.neolane.net/)]リンクから[Adobe Campaignサポート]ページ(https://support.neolane.net/ **** )に移動します。

ファイルは **nlserver6-v7-XXX.rpmです。**

### 更新の実行 {#perform-an-update}

* RPMベースの配布(RedHat、SuSe)

   これらをインストールするには、rootとして実行します。

   ```
   $rpm -Uvh nlserver6-v7-XXXX.rpm
   ```

   XXXはファイルのバージョンです。

   rpmファイルはCentOS/Red Hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使いたくない場合は、rpmの「nodeps」オプションを使わなければならないかもしれません。

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
>完全なインストール手順については、 [この節で説明します](../../installation/using/installing-campaign-standard-packages.md)。 リソースは自動的に同期されますが、エラーが発生しないことを確認する必要があります。 詳しくは、「アップグレードの競合の [解決](#resolving-upgrade-conflicts)」を参照してください。

### Webサーバーの再起動 {#reboot-the-web-server}

新しいライブラリを適用するには、Apacheをシャットダウンする必要があります。

これを行うには、次のコマンドを実行します。

```
/etc/init.d/apache stop
```

>[!CAUTION]
>
>* スクリプトの名前は、 **apacheではなく** httpd **にすることができます**。
>* 次の応答を取得するまで、このコマンドを実行する必要があります。
   >この操作は、Apacheが新しいライブラリを適用するために必要です。

>



次に、Apacheを再起動します。

```
/etc/init.d/apache start
```

## アップグレードの競合の解決 {#resolving-upgrade-conflicts}

リソースの同期中に、 **postupgrade** コマンドを使用すると、同期でエラーが発生したか警告が発生したかを検出できます。

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

* postupgrade_ **.log`<server version number>_<time of postupgrade>`** ログファイルには、同期結果が格納されます。 It is available by default in the following directory: **`<installation directory>/var/<instance/postupgrade`**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合の解決 {#resolving-conflicts}

競合を解決するには、次の手順に従います。

1. In the Adobe Campaign tree, go to **[!UICONTROL Administration > Configuration > Package management > Edit conflicts]** .
1. リストから解決する競合を選択します。

競合を解決するには、次の3つの方法があります。

* **[!UICONTROL 解決済みとして宣言]** :前もってユーザーの介入が必要です。
* **[!UICONTROL 新しいバージョンを受け入れる]** :adobe campaignが提供するリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL 現在のバージョンを保持]** :は、更新が拒否されたことを意味します。

   >[!CAUTION]
   >
   >この解像度モードを選択すると、新しいバージョンで修正を行うメリットが得られない場合があります。

競合を手動で解決する場合は、次の手順に従います。

1. In the lower section of the window, search for the **_conflict_** string to locate the entities with conflicts. The entity installed with the new version contains the **new** argument, the entity that matches the previous version contains the **cus** argument.

   ![](assets/s_ncs_production_conflict002.png)

1. 維持しないバージョンを削除します。Delete the **_conflict_argument_** string of the entity you are keeping.

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。**[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

### ベストプラクティス{#best-practices}

更新エラーがデータベース構成にリンクされている可能性があります。 技術管理者とデータベース管理者が実行した設定が互換性があることを確認します。

例えば、Unicodeデータベースは、LATIN1データなどのストレージを許可するだけではありません。

## Warn the client consoles of the available update {#warn-the-client-consoles-of-the-available-update}

### Windowsの場合 {#in-windows-1}

On the machine where the (**nlserver web**) Adobe Campaign application server is installed, download and copy the file

**setup-client-6.XXXX.exe**

**アプリケーションの[パス]**datakitnlengjsp内

次回クライアントコンソールに接続すると、ウィンドウに、アップデートの利用可能性が通知され、アップデートのダウンロードとインストールの可能性がオファーされます。

>[!NOTE]
>
>IIS_XPGユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については [インストールガイド](../../installation/using/general-architecture.md) を参照してください。

### Linuxの場合 {#in-linux-1}

Adobe Campaignアプリケーションサーバー(**nlserver web**)がインストールされているマシン上で、次のパッケージを取得します。

**setup-client-6.XXXX.exe**

をコピーし、 **/usr/local/neolane/nl6/datakit/nl/eng/jsp**:

```
 cp setup-client-6.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
```

次回クライアントコンソールに接続すると、ウィンドウに、アップデートの利用可能性が通知され、アップデートのダウンロードとインストールの可能性がオファーされます。

>[!NOTE]
>
>Apacheユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については [インストールガイド](../../installation/using/general-architecture.md) を参照してください。

