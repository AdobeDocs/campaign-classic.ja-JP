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

Adobe Campaignモジュールの自動起動 (**web**, **mta**, **wfserver**&#x200B;など ) が **nlserver** サーバー。

Adobe Campaignをインストールすると、 **nlserver** 起動シーケンス中にサービスが起動します。

次のコマンドを使用して、Adobe Campaignサービスを手動で起動および停止します。

* Windows の場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linux の場合 (root):

   * **/etc/init.d/nlserver6 start**
   * **/etc/init.d/nlserver6 停止**

>[!NOTE]
>
>20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver** / **systemctl stop nlserver**

以下は、Linux でアクセス可能な通常の管理コマンドのリストです ( **Adobe Campaign**):

* すべての開始Adobe Campaignモジュールを表示： **/etc/init.d/nlserver6 pdump** または **/etc/init.d/nlserver6 のステータス**

   >[!NOTE]
   >
   >の追加 **-who** パラメーターを **pdump** コマンドを使用すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
   >この **/etc/init.d/nlserver6 のステータス** コマンド（&quot;-who&quot;パラメータを指定しない）は、次の値を返します。
   >
   >    * すべてのプロセスが実行されている場合は 0。
   >    * プロセスが見つからない場合は 1。
   >    * 2 を返します。
   >    * 別の値（エラーがある場合）


* マルチインスタンスまたはモノラルインスタンスモジュール (**web**, **trackinglogd**, **syslogd**, **mta**, **wfserver**, **inmail**):

   **nlserver start`<module>[@<instance>]`**

   **nlserver 停止`<module>[@<instance>][-immediate][-noconsole]`**

   また、 **nlserver restart`<module>[@<instance>]`** コマンドを使用して、モジュールを再起動します。

   例：

   **nlserver 開始 web**

   **nlserver start mta@my_instance**

   **nlserver stop syslogd**

   **nlserver stop wfserver@my_instance**

   **nlserver 停止 web -immediate**

   **nlserver 再起動 web**

   >[!NOTE]
   >
   >* インスタンスを指定しない場合は、「デフォルト」インスタンスが使用されます。
   >* 緊急の場合は、 **-immediate** プロセスを即時に停止させるオプション（Unix コマンドと同じ） **kill -9**) をクリックします。
   >* 以下を使用： **-noconsole** オプションを使用して、起動したモジュールがコンソールに何も表示されないようにします。 ログは、 **syslogd** モジュール。
   >* 以下を使用： **-verbose** 「 」オプションを使用して、プロセスアクションに関する追加情報を表示できます。
      >
      >   例：
      >
      >   **nlserver 再起動 web -verbose**
      >
      >   **nlserver start mta@myinstance -verbose**
      >
      >   このオプションを選択すると、ログが追加されます。 を使用せずに、プロセスを再び開始することをお勧めします。 **-verbose** オプションを使用して、ログのオーバーロードを防ぐことができます。


* すべてのAdobe Campaignプロセスを起動します ( **nlserver6** サービス ):

   **nlserver watchdog -noconsole**

* すべてのAdobe Campaignプロセスをシャットダウンします ( **nlserver6** サービス ):

   **nlserver shutdown**

* をリロードします。 **nlserver web** モジュールの設定（および該当する場合は web サーバー拡張モジュール） **serverConf.xml** および **config-`<instance>  .xml </instance>`** ファイルが編集されました。

   **nlserver config -reload**

   >[!NOTE]
   >
   >一部の設定の変更は動的には反映されません。Adobe Campaignはシャットダウンしてから再起動する必要があります。
