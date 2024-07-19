---
product: campaign
title: 管理
description: 管理
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 12a255fe-66f9-40ce-b19e-c24322c2e009
source-git-commit: b7dedddc080d1ea8db700fabc9ee03238b3706cc
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---

# 管理{#administration}

Adobe Campaign モジュール（**web**、**mta**、**wfserver** など）の自動起動 は、**nlserver** サーバーによって提供されます。

Adobe Campaignをインストールすると、ブートシーケンス中に **nlserver** サービスが起動するように、マシンが自動的に設定されます。

次のコマンドを使用して、Adobe Campaign サービスを手動で起動および停止します。

* Windows の場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linux の場合（root）:

   * **/etc/init.d/nlserver6 開始**
   * **/etc/init.d/nlserver6 停止**

>[!NOTE]
>
>20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver** / **systemctl stop nlserver**

Linux で（**0}Adobe Campaign} として）アクセスできる通常の管理コマンドのリストを次に示します。**

* 起動されたすべてのAdobe Campaign モジュールを表示します：**/etc/init.d/nlserver6 pdump** または **/etc/init.d/nlserver6 status**

  >[!NOTE]
  >
  >**pdump** コマンドに **-who** パラメーターを追加すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
  >**/etc/init.d/nlserver6 status** コマンド（「– who」パラメーターを除く）は、次の値を返します。
  >
  >    * すべてのプロセスが実行中の場合は 0 を返します。
  >    * プロセスがない場合は 1。
  >    * 2：プロセスが実行されていない場合。
  >    * エラーがある場合の別の値。
  >

* マルチインスタンスまたはモノインスタンスモジュール（**web**、**trackinglogd**、**syslogd**、**mta**、**wfserver**、**inmail**）の起動または停止：

  **nlserver start`<module>[@<instance>]`**

  **nlserver stop`<module>[@<instance>][-immediate][-noconsole]`**

  **nlserver restart`<module>[@<instance>]`** コマンドを使用して、モジュールを再起動することもできます。

  例：

  **nlserver start web**

  **nlserver start mta@my_instance**

  **nlserver stop syslogd**

  **nlserver stop wfserver@my_instance**

  **nlserver stop web -immediate**

  **nlserver restart web**

  >[!NOTE]
  >
  >* インスタンスを指定しない場合は、「default」インスタンスが使用されます。
  >* 緊急事態が発生した場合は、**-immediate** オプションを使用して、プロセスを直ちに停止します（Unix コマンド **kill -9** と同等）。
  >* **-noconsole** オプションを使用して、起動したモジュールにコンソールに何も表示されないようにします。 ログは、**syslogd** モジュールを介してディスクに書き込まれます。
  >* **-verbose** オプションを使用すると、プロセスアクションに関する追加情報を表示できます。
  >
  >   例：
  >
  >   **nlserver restart web -verbose**
  >
  >   **nlserver start mta@myinstance -verbose**
  >
  >   このオプションを選択すると、ログが追加されます。 ログの過負荷を避けるために、必要な情報が見つかったら、**-verbose** オプションを使用せずにプロセスを再開することをお勧めします。

* すべてのAdobe Campaign プロセスを開始します（**nlserver6** サービスを開始する場合と同じ）。

  **nlserver watchdog -noconsole**

* すべてのAdobe Campaign プロセスをシャットダウンします（**nlserver6** サービスをシャットダウンするのと同じ）。

  **nlserver のシャットダウン**

* **serverConf.xml** および **config-`<instance>  .xml </instance>`** ファイルが編集されたら、**nlserver web** モジュール設定（および該当する場合は web サーバー拡張モジュール）を再読み込みします。

  **nlserver config -reload**

  >[!NOTE]
  >
  >一部の設定変更は、動的には考慮されません。Adobe Campaignをシャットダウンしてから再起動する必要があります。
