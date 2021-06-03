---
product: campaign
title: 管理
description: 管理
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 12a255fe-66f9-40ce-b19e-c24322c2e009
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# 管理{#administration}

Adobe Campaignモジュールの自動起動（**web**、**mta**、**wfserver**&#x200B;など） は、**nlserver**&#x200B;サーバーによって提供されます。

Adobe Campaignをインストールすると、ブートシーケンス中に&#x200B;**nlserver**&#x200B;サービスが起動するように、マシンが自動的に設定されます。

次のコマンドを使用して、Adobe Campaignサービスを手動で起動および停止します。

* Windowsの場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linuxの場合(root):

   * **/etc/init.d/nlserver6 start**
   * **/etc/init.d/nlserver6停止**

>[!NOTE]
>
>20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。**systemctl start nlserver** / **systemctl stop nlserver**

Linuxでアクセス可能な通常の管理コマンドのリストを次に示します(**Adobe Campaign**)。

* すべての開始済みAdobe Campaignモジュールを表示：**/etc/init.d/nlserver6 pdump**&#x200B;または&#x200B;**/etc/init.d/nlserver6 status**

   >[!NOTE]
   >
   >**-who**&#x200B;パラメーターを&#x200B;**pdump**&#x200B;コマンドに追加すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
   >**/etc/init.d/nlserver6 status**&#x200B;コマンド（「 —who」パラメーターを除く）は、次のように返します。
   >
   >    * すべてのプロセスが実行されている場合は0。
   >    * プロセスが見つからない場合は1。
   >    * 2を指定します。
   >    * 別の値（エラーがある場合）


* マルチインスタンスまたはモノインスタンスモジュール(**web**、**trackinglogd**、**syslogd**、**mta**、**wfserver**、**inmail**):

   **nlserverの開始`<module>[@<instance>]`**

   **nlserver停止`<module>[@<instance>][-immediate][-noconsole]`**

   **nlserver restart`<module>[@<instance>]`**&#x200B;コマンドを使用して、モジュールを再起動することもできます。

   例：

   **nlserver開始web**

   **nlserver start mta@my_instance**

   **nlserver stop syslogd**

   **nlserver stop wfserver@my_instance**

   **nlserver停止web -immediate**

   **nlserver再起動web**

   >[!NOTE]
   >
   >* インスタンスを指定しない場合は、「デフォルト」のインスタンスが使用されます。
   >* 緊急の場合は、**-immediate**&#x200B;オプションを使用して、プロセスを強制的に即時停止します（Unixコマンド&#x200B;**kill -9**&#x200B;と同じ）。
   >* **-noconsole**&#x200B;オプションを使用して、起動したモジュールがコンソールに何も表示されないようにします。 ログは&#x200B;**syslogd**&#x200B;モジュールを介してディスクに書き込まれます。
   >* **-verbose**&#x200B;オプションを使用して、プロセスアクションに関する追加情報を表示します。
   >
   >   例：
   >
   >   **nlserver restart web -verbose**
   >
   >   **nlserver start mta@myinstance -verbose**
   >
   >   このオプションでは、ログを追加します。 ログのオーバーロードを避けるために、**-verbose**&#x200B;オプションを指定せずに、再びプロセスを開始することをお勧めします。


* すべてのAdobe Campaignプロセスを起動します（**nlserver6**&#x200B;サービスを起動するのと同じ）。

   **nlserver watchdog -noconsole**

* すべてのAdobe Campaignプロセスをシャットダウンします（**nlserver6**&#x200B;サービスのシャットダウンと同じ）。

   **nlserver shutdown**

* **serverConf.xml**&#x200B;および&#x200B;**config-`<instance>  .xml </instance>`**&#x200B;ファイルが編集されたら、**nlserver web**&#x200B;モジュールの設定（および該当する場合はWebサーバー拡張モジュール）を再読み込みします。

   **nlserver config -reload**

   >[!NOTE]
   >
   >一部の設定の変更は動的には考慮されません。Adobe Campaignはシャットダウンしてから再起動する必要があります。
