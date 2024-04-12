---
product: campaign
title: 管理
description: 管理
feature: Monitoring
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: production-procedures
exl-id: 12a255fe-66f9-40ce-b19e-c24322c2e009
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

---

# 管理{#administration}



Adobe Campaign モジュールの自動起動（**web**, **mta**, **wfserver**&#x200B;等） が提供します **nlserver** サーバー。

Adobe Campaignをインストールすると、マシンは **nlserver** サービスは起動シーケンス中に起動します。

次のコマンドを使用して、Adobe Campaign サービスを手動で起動および停止します。

* Windows の場合：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linux の場合（root）:

   * **/etc/init.d/nlserver6 開始**
   * **/etc/init.d/nlserver6 停止**

>[!NOTE]
>
>20.1 以降では、代わりに次のコマンドを使用することをお勧めします（Linux の場合）。 **systemctl start nlserver** / **systemctl stop nlserver**

以下は、Linux でアクセス可能な通常の管理コマンドのリストです **Adobe Campaign**）:

* 開始したすべてのAdobe Campaign モジュールを表示します。 **/etc/init.d/nlserver6 pdump** または **/etc/init.d/nlserver6 の状態**

  >[!NOTE]
  >
  >の追加 **-who** のパラメーター **pdump** コマンドを使用すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
  >この **/etc/init.d/nlserver6 の状態** コマンド （「– who」パラメーターを除く）は、次の値を返します。
  >
  >    * すべてのプロセスが実行中の場合は 0 を返します。
  >    * プロセスがない場合は 1。
  >    * 2：プロセスが実行されていない場合。
  >    * エラーがある場合の別の値。
  >

* マルチインスタンスまたはモノインスタンスモジュールの開始/停止（**web**, **trackinglogd**, **syslogd**, **mta**, **wfserver**, **inmail**）:

  **nlserver 開始`<module>[@<instance>]`**

  **nlserver の停止`<module>[@<instance>][-immediate][-noconsole]`**

  を使用することもできます **nlserver の再起動`<module>[@<instance>]`** モジュールを再起動するコマンド。

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
  >* 緊急の場合は、 **-immediate** プロセスを直ちに停止するオプション （Unix コマンドと同等） **kill -9**）に設定します。
  >* の使用 **-noconsole** 起動したモジュールがコンソールに何も表示されないようにするオプション。 ログは、を介してディスクに書き込まれます。 **syslogd** モジュール。
  >* の使用 **-verbose** プロセスアクションに関する追加情報を表示するオプション。
  >
  >   例：
  >
  >   **nlserver restart web -verbose**
  >
  >   **nlserver start mta@myinstance -verbose**
  >
  >   このオプションを選択すると、ログが追加されます。 を使用せずにプロセスを再開することをお勧めします **-verbose** ログのオーバーロードを避けるために、必要な情報が見つかったら、「」オプションを選択します。

* すべてのAdobe Campaign プロセスの開始（を開始することと同じ） **nlserver6** サービス）:

  **nlserver watchdog -noconsole**

* すべてのAdobe Campaign プロセスをシャットダウンします（ **nlserver6** サービス）:

  **nlserver シャットダウン**

* をリロードします。 **nlserver web** モジュール設定（および該当する場合は web サーバー拡張機能モジュール） **serverConf.xml** および **config-`<instance>  .xml </instance>`** ファイルが編集されました。

  **nlserver config -reload**

  >[!NOTE]
  >
  >一部の設定変更は、動的には考慮されません。Adobe Campaignをシャットダウンしてから再起動する必要があります。
