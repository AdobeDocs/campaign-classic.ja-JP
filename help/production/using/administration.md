---
title: 管理
seo-title: 管理
description: 管理
seo-description: null
page-status-flag: never-activated
uuid: 376efec1-1647-43b4-b72f-2603214c7cc6
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: production-procedures
discoiquuid: 860be8be-f28c-4836-b4fb-e91c6a4616c6
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 3801665574d0cdc9c0caf46fb2f0eede38f1b2cc

---


# 管理{#administration}

Adobe Campaignモジュール(Web **、** mta **、** wfserver ****&#x200B;など)の自動起動は **nlserver** 。

Adobe Campaignをインストールすると、起動シーケンス中に **nlserver** サービスが起動するようにコンピューターが自動的に設定されます。

Adobe Campaignサービスを手動で起動および停止するには、次のコマンドを使用します。

* Windowsの場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linux(root)の場合：

   * **/etc/init.d/nlserver6 start**
   * **/etc/init.d/nlserver6 stop**

>[!NOTE]
>
>20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）。 **systemctl start nlserver** / **systemctl stop nlserver**

Linux( **Adobe Campaign**)でアクセス可能な通常の管理コマンドを以下に示します。

* すべての開始済みAdobe Campaignモジュールを表示： **/etc/init.d/nlserver6 pdump** or **/etc/init.d/nlserver6 status**

   >[!NOTE]
   >
   >pdumpコマンドに **-whoパラメ** ーターを追 **加すると** 、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
   >/etc/init.d/ **nlserver6 statusコマンド** （「 —who」パラメーターを含まない）は、次の値を返します。
   >
   >    * すべてのプロセスが実行されている場合は0。
   >    * プロセスが見つからない場合は1。
   >    * プロセスが実行されていない場合は2。
   >    * 別の値（エラーが発生した場合）。


* マルチインスタンスまたはモノインスタンスモジュール(**web,****trackingd,** syslogd **,** syslogd **,** mta, **wfserver, intermail** name, mail **** instance)の開始/停止

   **nlserverの起動`<module>[@<instance>]`**

   **nlserver停止`<module>[@<instance>][-immediate][-noconsole]`**

   また、 **nlserver restartコマンドを使用して、モジュー`<module>[@<instance>]`**ルを再起動することもできます。

   例：

   **nlserver webの起動**

   **nlserver start mta@my_instance**

   **nlserver停止syslogd**

   **nlserver stop wfserver@my_instance**

   **nlserver Stop Web -immediate**

   **nlserver再起動Web**

   >[!NOTE]
   > 
   >    * インスタンスを指定しない場合は、「デフォルト」インスタンスが使用されます。
   >    * 緊急の場合は、 **-immediate** オプションを使用して、プロセスを強制的に即時停止します(Unixコマンド **kill -9**&#x200B;と同じ)。
   >    * 起動したモジュ **ールがコンソールに何も表示されないようにするには、** -noconsoleオプションを使用します。 ログは、 **syslogdモジュールを介してディスクに書き込ま** れます。
   >    * プロセスアクシ **** ョンに関する追加情報を表示するには、-verboseオプションを使用します。
      >    
      >      
      例：
      >    
      >      
      **nlserver再起動web - verbose**
      >    
      >      
      **nlserver start mta@myinstance - verbose**
      >    
      >      
      このオプションは、ログを追加します。 必要な情報が見つかったら、 **-verboseオプションを使用せずにプロセスを再び開始して** 、ログのオーバーロードを防ぐことをお勧めします。


* すべてのAdobe Campaignプロセスを起動します( **nlserver6** サービスの起動と同じ)。

   **nlserver watchdog - noconsole**

* すべてのAdobe Campaignプロセスを停止します( **nlserver6** サービスの停止と同じ)。

   **nlserverシャットダウン**

* serverConf.xml **ファイルと** config **— ファイルを編集したら、nlserver web** モジュール設定（および該当する場合はWebサーバー拡張モジュール）を再読み込 **`<instance>  .xml </instance>`**みします。

   **nlserver config -reload**

   >[!NOTE]
   >
   >一部の設定変更は動的には考慮されません。Adobe Campaignをシャットダウンしてから再起動する必要があります。

