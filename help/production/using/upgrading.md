---
product: campaign
title: 新しいビルドへのアップグレード
description: 新しいビルドにアップグレードするための技術的な手順を説明します
audience: production
content-type: reference
topic-tags: updating-adobe-campaign
exl-id: 4aaa6256-256a-441d-80c9-430f8e427875
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 15%

---

# 新しいビルドへのアップグレード（オンプレミス）{#upgrading}

アップグレードプロセスを開始する前に、アップグレード先のAdobe Campaignのバージョンを特定して確認し、[リリースノート](../../rn/using/latest-release.md)を参照してください。

>[!IMPORTANT]
>
>* Adobeでは、更新する前に各インスタンスでデータベースのバックアップを作成することを強くお勧めします。 詳しくは、[こちらの節](../../production/using/backup.md)を参照してください。
>* アップグレードを実行するには、インスタンスとログにアクセスする権限と権限があることを確認してください。
>* [この節](../../installation/using/general-architecture.md)と[ビルドのアップグレード](https://helpx.adobe.com/jp/campaign/kb/acc-build-upgrade.html)の章を読んでから、始めてください。

>



## Windows {#in-windows}

Windows環境でAdobe Campaignを新しいビルドに更新するには、次の手順に従います。

* [サービスのシャットダウン](#shut-down-services),
* [アプリケーションサーバーのアップグレード](#upgrade-the-adobe-campaign-server-application),
* [リソースの同期](#synchronize-resources),
* [サービスの再起動](#restart-services).

クライアントコンソールの更新方法については、[この節](../../installation/using/client-console-availability-for-windows.md)を参照してください。

### サービスのシャットダウン {#shut-down-services}

すべてのファイルを新しいバージョンで置き換えるには、nlserverサービスのすべてのインスタンスをシャットダウンする必要があります。

1. 以下のサービスをシャットダウンします。

   * Web サービス（IIS）：

      **iisreset /stop**

   * Adobe Campaignサービス：**net stop nlserver6**
   >[!IMPORTANT]
   >
   >また、IISで使用される&#x200B;**nlsrvmod.dll**&#x200B;ファイルを新しいバージョンに置き換えるには、リダイレクションサーバー(webmdl)が停止していることを確認する必要があります。

1. **nlserver pdump**&#x200B;コマンドを実行して、アクティブなタスクがないことを確認します。 次のようになります。

   ```
   C:<installation path>Adobe Campaign v7bin>nlserver pdump
   HH:MM:SS > Application Server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
   No tasks
   ```

   Windowsタスクマネージャーを使用して、すべてのプロセスが停止していることを確認できます。

### Adobe Campaign サーバーアプリケーションのアップグレード {#upgrade-the-adobe-campaign-server-application}

アップグレードファイルを実行するには、次の手順に従います。

1. **setup.exe**&#x200B;を実行します。

   このファイルをダウンロードするには、ユーザーの資格情報を使用して[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)に接続します。 ソフトウェアの配布について詳しくは、[このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=ja)を参照してください。

1. インストールモードを選択します。**[!UICONTROL 更新または修復]**&#x200B;を選択します。
1. 「**[!UICONTROL 次へ]**」をクリックします。
1. 「**[!UICONTROL 終了]**」をクリックします。

   次に、新しいファイルがコピーされます。

1. 処理が完了したら「**[!UICONTROL 完了]**」をクリックします。

### リソースの同期 {#synchronize-resources}

次のコマンドラインを使用します。

**nlserver config -postupgrade -allinstances**

これにより、次の操作を実行できます。

* リソースの同期
* スキーマの更新
* データベースの更新

>[!NOTE]
>
>この操作は、(**nlserver web**)アプリケーションサーバー上でのみ1回だけ実行する必要があります。

次に、同期でエラーまたは警告が生成されたかどうかを確認します。 詳しくは、[アップグレードの競合の解決](#resolving-upgrade-conflicts)を参照してください。

### サービスの再起動 {#restart-services}

再起動するサービスは次のとおりです。

* Web サービス（IIS）：

   **iisreset /start**

* Adobe Campaignサービス：**net start nlserver6**

## Linux {#in-linux}

Linux環境でAdobe Campaignを新しいビルドに更新するには、次の手順に従います。

* [更新されたパッケージをダウンロードします](#obtain-updated-packages)。
* [更新を実行します](#perform-an-update)。
* [Webサーバーを再起動します](#reboot-the-web-server)。

[クライアントコンソールの可用性の詳細を説明します](../../installation/using/client-console-availability-for-windows.md)。

>[!NOTE]
>
>ビルド8757以降、サードパーティライブラリは不要になりました。

### 更新されたパッケージを取得します{#obtain-updated-packages}

最初に、Adobe Campaignの更新済みパッケージの両方を回復します。ユーザーの資格情報を使用して、[ソフトウェア配布ポータル](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html)に接続します。 ソフトウェアの配布について詳しくは、[このページ](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html?lang=en)を参照してください。

ファイルは&#x200B;**nlserver6-v7-XXX.rpm**&#x200B;です。

### 更新{#perform-an-update}を実行します

* RPMベースの配布(RedHat、SuSe)

   これらをインストールするには、rootとして実行します。

   ```
   $rpm -Uvh nlserver6-v7-XXXX.rpm
   ```

   XXXはファイルのバージョンです。

   rpmファイルは、CentOS/Red Hatディストリビューションで見つけられるパッケージに依存しています。 これらの依存関係の一部を使用したくない場合は、rpmの「nodeps」オプションを使用する必要がある場合があります。

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
>完全なインストール手順については、[この節](../../installation/using/installing-campaign-standard-packages.md)で詳しく説明しています。 リソースは自動的に同期されますが、エラーが発生していないことを確認する必要があります。 詳しくは、[アップグレードの競合の解決](#resolving-upgrade-conflicts)を参照してください。

### Webサーバー{#reboot-the-web-server}を再起動します。

新しいライブラリを適用するには、Apacheをシャットダウンする必要があります。

これをおこなうには、次のコマンドを実行します。

```
/etc/init.d/apache stop
```

>[!IMPORTANT]
>
>* スクリプトは、**apache**&#x200B;ではなく、**httpd**&#x200B;と呼ばれる場合があります。
>* 次の応答が返されるまで、このコマンドを実行する必要があります。

   >
   >   
   この操作は、Apacheが新しいライブラリを適用するために必要です。


次に、Apacheを再起動します。

```
/etc/init.d/apache start
```

## アップグレードの競合を解決{#resolving-upgrade-conflicts}

リソースの同期中に、**postupgrade**&#x200B;コマンドを使用して、同期でエラーが発生したか警告が発生したかを検出できます。

### 同期結果を表示します。{#view-the-synchronization-result}

同期結果を表示する方法は2つあります。

* コマンドラインインターフェイスでは、エラーは三重山形記号&#x200B;**>>**&#x200B;で実現され、同期は自動的に停止されます。 警告は二重山括弧&#x200B;**>**&#x200B;で示され、同期が完了したら解決する必要があります。 ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。以下はその一例です。

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

### 競合の解決{#resolving-conflicts}

競合を解決するには、次の手順に従います。

1. Adobe Campaignツリーで、 **[!UICONTROL 管理/設定/パッケージ管理/競合を編集]**&#x200B;に移動します。
1. リストから解決する競合を選択します。

競合を解決する方法は3つあります。

* **[!UICONTROL 解決済みとして宣言]** :事前にユーザーの操作が必要です。
* **[!UICONTROL 新しいバージョンを受け入れる]** :Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL 現在のバージョンを保持]** :は、更新が拒否されたことを示します。

   >[!IMPORTANT]
   >
   >この解像度モードを選択すると、新しいバージョンで修正できない場合があります。

競合を手動で解決する場合は、次の手順に従います。

1. ウィンドウの下部のセクションで、**_conflict_**&#x200B;文字列を検索し、競合するエンティティを探します。 新しいバージョンでインストールされたエンティティには&#x200B;**new**&#x200B;引数が含まれ、以前のバージョンに一致するエンティティには&#x200B;**cus**&#x200B;引数が含まれます。

   ![](assets/s_ncs_production_conflict002.png)

1. 維持しないバージョンを削除します。保持するエンティティの&#x200B;**_conflict_argument_**&#x200B;文字列を削除します。

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。**[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

### ベストプラクティス{#best-practices}

更新エラーは、データベース設定にリンクされている可能性があります。 技術管理者とデータベース管理者が実行した設定に互換性があることを確認します。

例えば、Unicodeデータベースは、LATIN1データなどのストレージを許可するだけではありません。

## 使用可能な更新{#warn-the-client-consoles-of-the-available-update}をクライアントコンソールに警告する

### Windows {#in-windows-1}

Adobe Campaignアプリケーションサーバーがインストールされているマシン(**nlserver web**)で、**setup-client-6.XXXX.exe** in **[アプリケーションのパス]/datakit/nl/eng/jsp**&#x200B;をダウンロードしてコピーします。

次回クライアントコンソールを接続すると、更新が使用可能であることをユーザーに通知するウィンドウが表示され、更新をダウンロードしてインストールできるようになります。

>[!NOTE]
>
>IIS_XPGユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については、[インストールガイド](../../installation/using/general-architecture.md)を参照してください。

### Linux {#in-linux-1}

Adobe Campaignアプリケーションサーバー(**nlserver web**)がインストールされているマシンで、**setup-client-6.XXXX.exe**&#x200B;パッケージを取得し、**/usr/local/neolane/nl6/datakit/nl/eng/jsp**&#x200B;として保存してコピーします。

```
 cp setup-client-6.XXXX.exe /usr/local/neolane/nl6/datakit/nl/eng/jsp
```

次回クライアントコンソールを接続すると、更新が使用可能であることをユーザーに通知するウィンドウが表示され、更新をダウンロードしてインストールできるようになります。

>[!NOTE]
>
>Apacheユーザーがこのインストールファイルに対する適切な読み取り権限を持っていることを確認し、詳細については、[インストールガイド](../../installation/using/general-architecture.md)を参照してください。
