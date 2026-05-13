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
TQID: https://experienceleague.adobe.com/s-FvcKmvrRP7l91MkglXI2ITjrFQYbV5Lj92k6UO7WE
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
feature_v2: id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# 管理{#administration}

Adobe Campaign モジュールの自動起動（**web**、**mta**、**wfserver**&#x200B;など） は、**nlserver** サーバーによって提供されます。

Adobe Campaignをインストールすると、ブートシーケンス中に&#x200B;**nlserver** サービスが起動するように、マシンが自動的に設定されます。

Adobe Campaign サービスを手動で起動および停止するには、次のコマンドを使用します。

* Windowsでは：

   * **net start nlserver6**
   * **net stop nlserver6**

* Linuxの場合（ルートとして）:

   * **/etc/init.d/nlserver6開始**
   * **/etc/init.d/nlserver6 stop**

>[!NOTE]
>
>20.1以降では、代わりに次のコマンドを使用することをお勧めします（Linuxの場合）: **systemctl start nlserver** / **systemctl stop nlserver**

Linuxでアクセスできる通常の管理コマンドのリストを以下に示します（**Adobe Campaign**&#x200B;として）。

* すべての開始済みAdobe Campaign モジュールを表示：**/etc/init.d/nlserver6 pdump**&#x200B;または&#x200B;**/etc/init.d/nlserver6 status**

  >[!NOTE]
  >
  >**-who** パラメーターを&#x200B;**pdump** コマンドに追加すると、現在の接続（ユーザーとプロセス）に関する情報を収集できます。\
  >**/etc/init.d/nlserver6 status** コマンド（「 – who」パラメーターなし）は、次を返します。
  >
  >    * すべてのプロセスが実行されている場合は0になります。
  >    * 1 プロセスが欠落している場合。
  >    * 2 プロセスが実行されていない場合。
  >    * エラーがある場合は、別の値を返します。
  >

* マルチインスタンスまたはモノインスタンスモジュール （**web**、**trackinglogd**、**syslogd**、**mta**、**wfserver**、**inmail**）を開始/停止します。

  **nlserver開始`<module>[@<instance>]`**

  **nlserver停止`<module>[@<instance>][-immediate][-noconsole]`**

  **nlserver restart`<module>[@<instance>]`** コマンドを使用して、モジュールを再起動することもできます。

  例：

  **nlserver開始web**

  **nlserver start mta@my_instance**

  **nlserver stop syslogd**

  **nlserver stop wfserver@my_instance**

  **nlserver stop web -immediate**

  **nlserver webを再起動**

  >[!NOTE]
  >
  >* インスタンスが指定されていない場合は、「デフォルト」インスタンスが使用されます。
  >* 緊急の場合は、**-immediate** オプションを使用して、直ちにプロセスを停止します（Unix コマンド **kill -9**&#x200B;と同等）。
  >* **-noconsole** オプションを使用して、起動したモジュールがコンソールに何も表示されないようにします。 そのログは、**syslogd** モジュールを介してディスクに書き込まれます。
  >* **-verbose** オプションを使用して、プロセスアクションに関する追加情報を表示します。
  >
  >   例：
  >
  >   **nlserver restart web -verbose**
  >
  >   **nlserver start mta@myinstance -verbose**
  >
  >   このオプションは、追加のログを追加します。 ログの過負荷を避けるために、目的の情報が見つかったら、**-verbose** オプションを使用せずにプロセスを再度開始することをお勧めします。

* すべてのAdobe Campaign プロセスを起動します（**nlserver6** サービスの起動に相当）。

  **nlserver watchdog -noconsole**

* すべてのAdobe Campaign プロセスをシャットダウンします（**nlserver6** サービスのシャットダウンに相当）。

  **nlserverのシャットダウン**

* **serverConf.xml**&#x200B;および&#x200B;**config-`<instance>  .xml </instance>`** ファイルが編集されたときに、**nlserver web** モジュール設定（および該当する場合はweb サーバー拡張モジュール）をリロードします。

  **nlserver config -reload**

  >[!NOTE]
  >
  >一部の設定変更は動的に考慮されませんが、Adobe Campaignをシャットダウンしてから再起動する必要があります。
