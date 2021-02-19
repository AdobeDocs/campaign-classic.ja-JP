---
solution: Campaign Classic
product: campaign
title: 管理
description: 管理
audience: production
content-type: reference
topic-tags: production-procedures
translation-type: tm+mt
source-git-commit: 9c78d8f469bade41717eb854e8cec00859c1d4e3
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---


# 管理{#administration}

Adobe Campaignモジュールの自動起動（**web**、**mta**、**wfserver**&#x200B;など） は&#x200B;**nlserver**&#x200B;サーバーによって提供されます。

Adobe Campaignをインストールすると、起動シーケンス中に&#x200B;**nlserver**&#x200B;サービスの開始が起動するようにマシンが自動的に構成されます。

次のコマンドを使用して、Adobe Campaignサービスの開始を手動で行い、シャットダウンします。

* Windowsの場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linuxの場合(root):

   * **/etc/init.d/nlserver6開始**
   * **/etc/init.d/nlserver6 stop**

>[!NOTE]
>
>20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。**systemctl開始nlserver** / **systemctl stop nlserver**

Linuxでアクセス可能な通常の管理コマンドのリストを以下に示します(**Adobe Campaign**)。

* すべての開始Adobe Campaignモジュールを表示：**/etc/init.d/nlserver6 pdump**&#x200B;または&#x200B;**/etc/init.d/nlserver6 status**

   >[!NOTE]
   >
   >**-who**&#x200B;パラメーターを&#x200B;**pdump**&#x200B;コマンドに追加すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
   >**/etc/init.d/nlserver6 status**&#x200B;コマンド（「 —who」パラメーターを含まない）は、次の値を返します。
   >
   >    * すべてのプロセスが実行中の場合は0。
   >    * プロセスが見つからない場合は1。
   >    * プロセスが実行されていない場合は2。
   >    * 別の値（エラーがある場合）。


* マルチインスタンスまたはモノインスタンスモジュール(**web**、**trackinglogd**、**syslogd**、**mta**、**wfserver**、**inmail**)の開始/停止):

   **nlserver開始`<module>[@<instance>]`**

   **nlserver停止`<module>[@<instance>][-immediate][-noconsole]`**

   **nlserver restart`<module>[@<instance>]`**&#x200B;コマンドを使用して、モジュールを再起動することもできます。

   例：

   **nlserver開始Web**

   **nlserver開始mta@my_instance**

   **nlserver stop syslogd**

   **nlserver stop wfserver@my_instance**

   **nlserver停止web -immediate**

   **nlserver再起動web**

   >[!NOTE]
   >
   >* インスタンスを指定しない場合は、「デフォルト」のインスタンスが使用されます。
   >* 緊急時のイベントでは、**-immediate**&#x200B;オプションを使用して、プロセスを即時に停止します（Unixコマンド&#x200B;**kill -9**&#x200B;と同じ）。
   >* **-noconsole**&#x200B;オプションを使用して、起動したモジュールがコンソールに何も表示しないようにします。 ログは&#x200B;**syslogd**&#x200B;モジュールを介してディスクに書き込まれます。
   >* **-verbose**&#x200B;オプションを使用して、プロセスアクションに関する追加情報を表示します。

      >
      >   
      例：
      >
      >   
      **nlserver再起動web - verbose**
      >
      >   
      **nlserver開始mta@myinstance -verbose**
      >
      >   
      このオプションは、ログを追加します。 必要な情報が見つかったら、**-verbose**&#x200B;オプションを使用せずにプロセスを再び開始し、ログのオーバーロードを防ぐことをお勧めします。


* すべてのAdobe Campaignプロセスを開始アップします（**nlserver6**&#x200B;サービスの起動と同じ）。

   **nlserver watchdog - noconsole**

* すべてのAdobe Campaignプロセスをシャットダウンします（**nlserver6**&#x200B;サービスをシャットダウンするのと同じ）。

   **nlserverシャットダウン**

* **nlserver web**&#x200B;モジュール設定（および、該当するWebサーバー拡張モジュール）を、**serverConf.xml**&#x200B;と&#x200B;**config-`<instance>  .xml </instance>`**&#x200B;ファイルが編集されたら再読み込みします。

   **nlserver config -reload**

   >[!NOTE]
   >
   >設定の変更の一部は動的には考慮されません。Adobe Campaignをシャットダウンしてから再起動する必要があります。

