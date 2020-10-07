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
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 2%

---


# 管理{#administration}

Adobe Campaignモジュール(**web**、 **mta**、 **wfserver**&#x200B;など)の自動起動 は、 **nlserver** serverによって提供されます。

インストールAdobe Campaignは、ブートシーケンス中に **nlserver** service開始が起動するようにマシンを自動的に構成します。

次のコマンドを使用して、Adobe Campaignサービスの開始を手動で行い、シャットダウンします。

* Windowsの場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linuxの場合(root):

   * **/etc/init.d/nlserver6開始**
   * **/etc/init.d/nlserver6 stop**

>[!NOTE]
>
>20.1からは、（Linuxの場合は）次のコマンドを使用することをお勧めします。 **systemctl開始nlserver** / **systemctl stop nlserver**

Linuxでアクセス可能な通常の管理コマンドのリストを以下に示します( **Adobe Campaign**)。

* すべての開始Adobe Campaignモジュールを表示： **/etc/init.d/nlserver6 pdump** or **/etc/init.d/nlserver6 status**

   >[!NOTE]
   >
   >**pdump** コマンドに —who **** パラメーターを追加すると、現在の接続（ユーザーおよびプロセス）に関する情報を収集できます。\
   >/etc/init.d/nlserver6の **status** コマンド（「 —who」パラメーターを含まない）は、次の値を返します。
   >
   >    * すべてのプロセスが実行中の場合は0。
   >    * プロセスが見つからない場合は1。
   >    * プロセスが実行されていない場合は2。
   >    * 別の値（エラーがある場合）。


* マルチインスタンスまたはモノインスタンスモジュール(**web**、trackinglogd **、syslogd**、mta、 **mta、wserver、** server、inmail、serverserver、inmail、ininstance ************ module)の開始/停止

   **nlserver開始`<module>[@<instance>]`**

   **nlserver停止`<module>[@<instance>][-immediate][-noconsole]`**

   また、 **nlserver restartコマンドを使用して、モジュールを再起動するこ`<module>[@<instance>]`** ともできます。

   例：

   **nlserver開始Web**

   **nlserver開始mta@my_instance**

   **nlserver stop syslogd**

   **nlserver stop wfserver@my_instance**

   **nlserver停止web -immediate**

   **nlserver再起動web**

   >[!NOTE]
   > 
   >    * インスタンスを指定しない場合は、「デフォルト」のインスタンスが使用されます。
   >    * 緊急時のイベントでは、 **-immediate** (即時 **)オプションを使用して、プロセスを強制的に即時停止します(Unixコマンド** kill -9と同じ)。
   >    * 起動したモジュールがコンソールに何も表示しないようにするには、 **-noconsole** (-noconsole)オプションを使用します。 ログは、 **syslogd** モジュールを介してディスクに書き込まれます。
   >    * プロセスアクションに関する追加情報を表示するには、 **-verbose** オプションを使用します。

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
      このオプションは、ログを追加します。 必要な情報が見つかったら、 **-verbose** （詳細）オプションを指定せずにプロセスを再開し、ログのオーバーロードを防ぐことをお勧めします。


* すべてのAdobe Campaignプロセスの開始( **nlserver6** サービスの起動と同じ):

   **nlserver watchdog - noconsole**

* すべてのAdobe Campaignプロセスをシャットダウンします( **nlserver6** サービスのシャットダウンと同じ)。

   **nlserverシャットダウン**

* serverConf.xml **ファイルと** config- **ファイルが編集されたら、nlserver web****`<instance>  .xml </instance>`** モジュール設定（および、該当する場合はWebサーバー拡張モジュール）を再読み込みします。

   **nlserver config -reload**

   >[!NOTE]
   >
   >設定の変更の一部は動的には考慮されません。Adobe Campaignをシャットダウンしてから再起動する必要があります。

