---
product: campaign
title: 管理
description: 管理
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 12a255fe-66f9-40ce-b19e-c24322c2e009
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# 管理{#administration}

![](../../assets/v7-only.svg)

Adobe Campaignモジュールの自動起動（**web**、**mta**、**wfserver** など） は **nlserver** サーバーによって提供されます。

Adobe Campaignをインストールすると、ブートシーケンス中に **nlserver** サービスが起動するように、マシンが自動的に設定されます。

次のコマンドを使用して、Adobe Campaignサービスを手動で起動および停止します。

* Windows の場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linux の場合 (root):

   * **/etc/init.d/nlserver6 start**
   * **/etc/init.d/nlserver6 の停止**

>[!NOTE]
>
>20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。**systemctl start nlserver** / **systemctl stop nlserver**

Linux でアクセス可能な通常の管理コマンドのリストを次に示します (**Adobe Campaign**)。

* すべての開始済みAdobe Campaignモジュールを表示：**/etc/init.d/nlserver6 pdump** または **/etc/init.d/nlserver6 status**

   >[!NOTE]
   >
   >**-who** パラメーターを **pdump** コマンドに追加すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
   >**/etc/init.d/nlserver6 status** コマンド（「 —who」パラメーターを除く）は次のように返します。
   >
   >    * すべてのプロセスが実行されている場合は 0。
   >    * プロセスが見つからない場合は 1。
   >    * 2 プロセスが実行されていない場合。
   >    * 別の値（エラーがある場合）


* マルチインスタンスまたはモノインスタンスモジュール (**web**、**trackinglogd**、**syslogd**、**mta**、**wfserver**、**inmail**):

   **nlserver の開始`<module>[@<instance>]`**

   **nlserver 停止`<module>[@<instance>][-immediate][-noconsole]`**

   **nlserver restart`<module>[@<instance>]`** コマンドを使用して、モジュールを再起動することもできます。

   例：

   **nlserver 開始 web**

   **nlserver start mta@my_instance**

   **nlserver stop syslogd**

   **nlserver stop wfserver@my_instance**

   **nlserver 停止 web -immediate**

   **nlserver 再起動 web**

   >[!NOTE]
   >
   >* インスタンスを指定しない場合は、「デフォルト」のインスタンスが使用されます。
   >* 緊急の場合は、**-immediate** オプションを使用して、プロセスを強制的に即時停止します（Unix コマンド **kill -9** と同じ）。
   >* **-noconsole** オプションを使用して、起動したモジュールがコンソールに何も表示されないようにします。 ログは、**syslogd** モジュールを介してディスクに書き込まれます。
   >* **-verbose** オプションを使用して、プロセスアクションに関する追加情報を表示します。

      >
      >   例：
      >
      >   **nlserver restart web - verbose**
      >
      >   **nlserver start mta@myinstance -verbose**
      >
      >   このオプションを選択すると、ログが追加されます。 ログのオーバーロードを避けるため、必要な情報が見つかったら **-verbose** オプションを指定せずに、プロセスを再び開始することをお勧めします。


* すべてのAdobe Campaignプロセスを起動します（**nlserver6** サービスを起動するのと同じ）。

   **nlserver watchdog -noconsole**

* すべてのAdobe Campaignプロセスをシャットダウンします（**nlserver6** サービスのシャットダウンと同じ）。

   **nlserver shutdown**

* **serverConf.xml** および **config-`<instance>  .xml </instance>`** ファイルが編集されたら、**nlserver web** モジュールの設定（および該当する場合は Web サーバー拡張モジュール）を再読み込みします。

   **nlserver config -reload**

   >[!NOTE]
   >
   >一部の設定変更は動的には考慮されません。Adobe Campaignをシャットダウンしてから再起動する必要があります。
