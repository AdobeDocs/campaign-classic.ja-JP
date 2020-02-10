---
title: 接続に失敗しました
seo-title: 接続に失敗しました
description: 接続に失敗しました
seo-description: null
page-status-flag: never-activated
uuid: 5e4cf47d-9699-4b4c-9c45-064fdc17110a
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 493067fb-68f1-48b9-afaa-3127a847db83
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 90813bc2913d56136067b9f64c0e934df3f17473

---


# 接続に失敗しました{#failure-to-connect}

この理由は複数になる場合があり、状況に応じて異なります。

セキュリティゾーンの一般的な構成を確認します。

>[!NOTE]
>
>For more on configuring security zones, refer to [this section](../../installation/using/configuring-campaign-server.md#defining-security-zones).

次の情報を確認します。

1. **ネットワークチェック**

   * コンピューターからインターネットにアクセスできますか。

      インターネット上のWebサイトに接続できることを確認します（例）。 接続できない場合は、お使いのコンピューターに問題があります。 システム管理者に問い合わせてください。

   * 別のサービスを介してAdobe Campaignをホストするサーバーに接続できますか。

      SSHなどの方法でサーバーに接続します。 これが不可能な場合は、ホスト会社に問題があります。 システム管理者に問い合わせてください。

1. **Webサーバー側での確認** (IIS/apache/etc)

   * Webサーバーは応答しますか。

      Webブラウザーを使用してAdobe CampaignサーバーのアクセスURLに接続します。 **http(s)://`<urlserver>`**. 応答しない場合、Webサーバーはマシン上で停止します。 サービスを再起動するには、ホスト会社のシステム管理者に問い合わせてください。

   * Adobe Campaignが正しく統合されているか。

      次にログオンします。 **http(s)://`<urlserver>`/r/test** URL。 サーバーは、次のタイプのメッセージを返す必要があります

      ```
      <redir status='OK' date='YYYY/MM/DD HH:MM:SS' build='XXXX' host='<hostname>' localHost='<server>'/>
      ```

      この結果を取得しない場合は、統合が考慮されるWebサーバー設定をチェックインします。

1. **Adobe Campaign側での確認**

   * Adobe Campaign webモジュールは起動されていますか。

      次のURLに接続します。 **http(s)://`<URLSERVER>`/nl/jsp/logon.jsp**

      * Tomcat javaエラーが発生した場合：

         JAVA統合は正しく実行されているか。 Adobe CampaignにはSUN JDKが必要です。

         これは、次のファイルに統合されていま **`[path of application]`す。/nl6/customer.sh **

      * 空白ページを取得した場合：

         Adobe Campaign webモジュールは起動していますか。 以下を入手する必要があります。

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
>Adobe Campaignモジュールのリストを作成する際に、次のタイプの応答を取得した場合：nlserver **pdump**
>DD/MM/YYYYのAdobe Campaign Classic(7.X YY.RビルドXXX@SHA1)のHH:MM:SS/アプリケーションサーバータスクはいいえ、Adobe Campaignアプリケーション全体を再起動する必要があります。 これを行うには、次のコマンドを使用します。**nlserver watchdog -svc -noconsole **
