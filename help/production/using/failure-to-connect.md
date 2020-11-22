---
solution: Campaign Classic
product: campaign
title: 接続の失敗
description: 接続の失敗
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---


# 接続の失敗{#failure-to-connect}

この理由は複数あり、様々なコンテキストに応じて異なります。

セキュリティゾーンの一般的な構成を確認します。

>[!NOTE]
>
>For more on configuring security zones, refer to [this section](../../installation/using/configuring-campaign-server.md#defining-security-zones).

次の情報を確認します。

1. **ネットワークの確認**

   * コンピューターからインターネットにアクセスできますか。

      インターネット上のWebサイトに接続できることを確認します（例）。 接続できない場合は、コンピューターに問題があります。 システム管理者に問い合わせてください。

   * 別のサービスを介してサーバーホスティングAdobe Campaignに接続できますか。

      SSHまたは他の方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者に問い合わせてください。

1. **Webサーバー側でのチェック** (IIS/apache/etc)

   * Webサーバーは応答しますか。

      Webブラウザーを使用してAdobe CampaignサーバーのアクセスURLに接続します。 **http(s)://`<urlserver>`**. 応答しない場合、Webサーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。

   * Adobe Campaignは正しく統合されているか。

      次の場所にログオンします。 **http(s):// `<urlserver>`/r/test** URL。 サーバーは、次の種類のメッセージを返す必要があります

      ```
      <redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='<hostname>' localHost='<server>'/>
      ```

      この結果を取得しない場合は、統合が考慮されるウェブサーバ設定をチェックインします。

1. **Adobe Campaign側のチェック**

   * Adobe CampaignWebモジュールが起動しているか。

      次のURLに接続します。 **http(s)://`<URLSERVER>`/nl/jsp/logon.jsp**

      * Tomcat Javaエラーが発生した場合：

         JAVA統合は正しく実行されているか。 Adobe CampaignにはSUN JDKが必要です。

         これは、次のファイルに統合されてい **`[path of application]`ます。/nl6/customer.sh**

      * 空白のページを取得した場合：

         Adobe CampaignWebモジュールは起動しているか。 以下を入手する必要があります。

         ```
         nlserver pdump
         HH:MM:SS > Application server for Adobe Campaign Classic (7.X YY.R build XXX@SHA1) of DD/MM/YYYY
         [...]
         web@default (27515) - 55.2 Mb
         [...]
         ```

      * そうでない場合は、次のコマンドを使用して再起動します。

         ```
         nlserver start web
         ```
>[!NOTE]
>
>Adobe Campaignモジュールのリスト時に次のタイプの応答を取得する場合： **nlserver pdump**
>HH:MM:SS > Application server forAdobe Campaign Classic(7.X YY.R build XXX@SHA1) of DD/MM/YYYYAdobe Campaign全体を再起動する必要があります。タスクはいりません。 これを行うには、次のコマンドを使用します。**nlserver watchod -svc -noconsole **
