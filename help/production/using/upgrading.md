---
solution: Campaign Classic
product: campaign
title: 新しいビルドへのアップグレード
description: 新しいビルドにアップグレードする技術的な手順を説明します。
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
translation-type: tm+mt
source-git-commit: 33debcd6e399d2780277644103a620d46c22022e
workflow-type: tm+mt
source-wordcount: '1193'
ht-degree: 14%

---


# 新しいビルド（オンプレミス）にアップグレードする{#upgrading}

アップグレードプロセスを開始する前に、アップグレード対象のAdobe Campaignのバージョンを決定して確認し、[リリースノート](../../rn/using/latest-release.md)を参照してください。

>[!IMPORTANT]
>
>更新する前に、各インスタンスでデータベースのバックアップを作成することを強くお勧めします。 詳しくは、[バックアップ](../../production/using/backup.md)を参照してください。\
>アップグレードを実行するには、インスタンスとログにアクセスする権限と権限を持っていることを確認します。

>[!NOTE]
>
>[インストールガイド](../../installation/using/general-architecture.md)と[ビルドアップグレード](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html)の手引きも参照してください。

## Windows {#in-windows}

新しいビルドを配信する際に新しいバージョンのAdobe Campaignを更新するには、Windowsで次の手順を適用する必要があります。

* [サービスのシャットダウン](#shut-down-services),
* [Adobe Campaign サーバーアプリケーションのアップグレード](#upgrade-the-adobe-campaign-server-application),
* [リソースの同期](#synchronize-resources),
* [サービスの再起動](#restart-services).

クライアントコンソールの更新方法については、[このセクション](../../installation/using/client-console-availability-for-windows.md)を参照してください。

### サービスのシャットダウン {#shut-down-services}

すべてのファイルを新しいバージョンで置き換えるには、nlserverサービスのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）：

      **iisreset /stop**

   * Adobe Campaignサービス：**nlserver6** net stop nlserver6

   >[!IMPORTANT]
   >
   >また、IISで使用される&#x200B;**nlsrvmod.dll**&#x200B;ファイルを新しいバージョンに置き換えるために、リダイレクトサーバー(webmdl)が停止していることを確認する必要があります。

1. **nlserver pdump**&#x200B;コマンドを実行して、タスクがアクティブでないことを確認します。 次のようになります。

   ```
   C:<installation path>Adobe Campaign v7bin>nlserver pdump
   HH:MM:SS > Application Server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   No tasks
   ```

   Windowsタスクマネージャーを使用して、すべてのプロセスが停止していることを確認できます。

### Adobe Campaign サーバーアプリケーションのアップグレード {#upgrade-the-adobe-campaign-server-application}

アップグレードファイルを実行するには、次の手順を適用します。

1. **setup.exe**&#x200B;を実行します。

   このファイルをダウンロードするには、ユーザーの資格情報を使用して[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/jp/campaign.html)に接続します。 ソフトウェアの配布についての詳細は、[このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=en)を参照してください。

1. インストールモードを選択します。**[!UICONTROL 更新または修復]**&#x200B;を選択
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL 終了]**」をクリックします。

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

次に、同期でエラーが発生したか、警告が発生したかを確認します。 この点について詳しくは、[アップグレードの競合の解決](#resolving-upgrade-conflicts)を参照してください。

### サービスの再起動 {#restart-services}

再起動するサービスは次のとおりです。

* Web サービス（IIS）：

   **iisreset /開始**

* Adobe Campaignサービス：**net開始nlserver6**

## Linux {#in-linux}

新しいビルドが提供されるときに新しいバージョンのAdobe Campaignを更新するには、Linuxの手順を次に示します。

* [更新されたパッケージの取得](#obtain-updated-packages)、
* [更新の実行](#perform-an-update)、
* [Webサーバーを再起動します](#reboot-the-web-server)。

クライアントコンソールの更新方法については、[このセクション](../../installation/using/client-console-availability-for-linux.md)を参照してください。

>[!NOTE]
>
>Build 8757から、サードパーティのライブラリは不要になりました。

### 更新されたパッケージを入手{#obtain-updated-packages}

Adobe Campaignの両方の更新されたパッケージを回復することによる開始:ユーザーの資格情報を使用して、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)に接続します。 ソフトウェアの配布についての詳細は、[このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=en)を参照してください。

ファイルは&#x200B;**nlserver6-v7-XXX.rpm**&#x200B;です。

### 更新を実行{#perform-an-update}

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
>完全なインストール手順については、[このセクション](../../installation/using/installing-campaign-standard-packages.md)で詳しく説明します。 リソースは自動的に同期されますが、エラーが発生しないことを確認する必要があります。 この点について詳しくは、[アップグレードの競合の解決](#resolving-upgrade-conflicts)を参照してください。

### Webサーバーを再起動します{#reboot-the-web-server}

新しいライブラリを適用するには、Apacheをシャットダウンする必要があります。

これを行うには、次のコマンドを実行します。

```
/etc/init.d/apache stop
```

>[!IMPORTANT]
>
>* スクリプトの名前は、**apache**&#x200B;の代わりに&#x200B;**httpd**&#x200B;にすることができます。
>* 次の応答を取得するまで、このコマンドを実行する必要があります。
>
>   この操作は、Apacheが新しいライブラリを適用するために必要です。


次に、Apacheを再起動します。

```
/etc/init.d/apache start
```

## アップグレードの競合を解決{#resolving-upgrade-conflicts}

リソースの同期中に、**postupgrade**&#x200B;コマンドを使用して、同期にエラーが発生したか警告が発生したかを検出できます。

### 同期結果の表示{#view-the-synchronization-result}

同期結果を表示する方法は2つあります。

* コマンドラインインターフェイスでは、エラーはトリプルシェブロン&#x200B;**>>**&#x200B;によって実現され、同期は自動的に停止します。 警告は、重複の山形&#x200B;**>**&#x200B;によって実現され、同期が完了したら解決する必要があります。 ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。以下はその一例です。

   ```
   2013-04-09 07:48:39.749Z 00002E7A 1 info log =========Summary of the update==========
   2013-04-09 07:48:39.749Z 00002E7A 1 info log <instance name> instance, 6 warning(s) and 0 error(s) during the update.
   2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.749Z 00002E7A 1 warning log The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.750Z 00002E7A 1 warning log The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
   2013-04-09 07:48:39.750Z 00002E7A 1 warning log Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
   ```

   リソースの競合に関する警告は、見落とさないように注意して、解決してください。

* **postupgrade_`<server version number>_<time of postupgrade>`.log**&#x200B;ログファイルには、同期結果が格納されます。 デフォルトでは、次のディレクトリで使用できます。**`<installation directory>/var/<instance/postupgrade`**. エラーと警告はそれぞれエラーと警告の属性で明示されます。

### 競合を解決{#resolving-conflicts}

競合を解決するには、次の手順に従います。

1. Adobe Campaignツリーで、**[!UICONTROL Administration/Configuration/Package management/Edit conflicts]**&#x200B;に移動します。
1. リストから解決する競合を選択します。

競合を解決するには、次の3つの方法があります。

* **[!UICONTROL 解決済みとして宣言]** :前もってユーザーの介入が必要です。
* **[!UICONTROL 新しいバージョンを承認する]** :Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL 現在のバージョンを保持]** :は、更新が拒否されたことを意味します。

   >[!IMPORTANT]
   >
   >この解像度モードを選択すると、新しいバージョンで修正を行うメリットが得られない場合があります。

競合を手動で解決する場合は、次の手順に従います。

1. ウィンドウの下のセクションで、**_conflict_**&#x200B;文字列を探して、競合のあるエンティティを探します。 新しいバージョンと共にインストールされるエンティティには、**new**&#x200B;引数が含まれ、前のバージョンと一致するエンティティには、**cus**&#x200B;引数が含まれます。

   ![](assets/s_ncs_production_conflict002.png)

1. 維持しないバージョンを削除します。保持するエンティティの&#x200B;**_conflict_argument_**&#x200B;文字列を削除します。

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。**[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

### ベストプラクティス{#best-practices}

更新エラーがデータベース構成にリンクされている可能性があります。 技術管理者とデータベース管理者が実行した設定が互換性があることを確認します。

例えば、Unicodeデータベースは、LATIN1データなどのストレージを許可するだけではありません。

## クライアントコンソールに利用可能な更新を警告する{#warn-the-client-consoles-of-the-available-update}

### Windows {#in-windows-1}

(**nlserver web**)Adobe Campaignアプリケーションサーバーがインストールされているマシン上で、ファイルをダウンロードしてコピーします

**setup-client-6.XXXX.exe**

**[アプリケーション]**datakitnlengjspのパス

次回クライアントコンソールに接続すると、ウィンドウに、アップデートの利用可能性が通知され、アップデートのダウンロードとインストールの可能性がオファーされます。

>[!NOTE]
>
>IIS_XPGユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については[インストールガイド](../../installation/using/general-architecture.md)を参照してください。

### Linux {#in-linux-1}

Adobe Campaignアプリケーションサーバー(**nlserver web**)がインストールされているマシン上で、次のパッケージを取得します。

**setup-client-6.XXXX.exe**

それをコピーして、**/usr/local/neolane/nl6/datakit/nl/eng/jsp**&#x200B;として保存します。

```
 cp setup-client-6.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
```

次回クライアントコンソールに接続すると、ウィンドウに、アップデートの利用可能性が通知され、アップデートのダウンロードとインストールの可能性がオファーされます。

>[!NOTE]
>
>Apacheユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については[インストールガイド](../../installation/using/general-architecture.md)を参照してください。

