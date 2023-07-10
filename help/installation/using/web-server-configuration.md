---
product: campaign
title: Web サーバー設定
description: Web サーバー設定の主なベストプラクティスの詳細を説明します
badge-v7-only: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7 only"
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: fc0d3f16-5f62-473d-a1de-aab574eff734
source-git-commit: 8debcd3d8fb883b3316cf75187a86bebf15a1d31
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 38%

---

# Web サーバー設定 {#web-server-configuration}



Web サーバー (Apache/IIS) の設定に関する主なベストプラクティスを以下にいくつか示します。

* デフォルトのエラーページを変更します。

* 古い SSL のバージョンと暗号を無効にします。

  **Apache 上**、/etc/apache2/mods-available/ssl.confを編集します。 次に例を示します。

   * SSLProtocol all -SSLv2 -SSLv3 -TLSv1
   * SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SSLv3:!SSLv2:!TLSv1

  **IIS の場合** ( [ドキュメント](https://support.microsoft.com/en-us/kb/245030)) で、次の設定を実行します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL にレジストリサブキーを追加します。
   * デフォルトでネゴシエートされないプロトコル（TLS 1.2 など）をシステムが使用できるようにするには、次のレジストリキーで、DisabledByDefault 値の DWORD 値データを 0x0 に変更します。 **プロトコル** キー：

     SCHANNEL\Protocols\TLS 1.2\Client

     SCHANNEL\Protocols\TLS 1.2\Server

  **SSL x.0 を無効にします。**

  SCHANNEL\Protocols\SSL 3.0\Client:DisabledByDefault:DWORD（32 ビット）値を 1 に設定

  SCHANNEL\Protocols\SSL 3.0\Server:有効：DWORD（32 ビット）値を 0 に設定

* **TRACE** メソッドを削除します。

  **Apache 上**、 /etc/apache2/conf.d/security で編集します。TraceEnable **オフ**

  **IIS の場合** ( [ドキュメント](https://www.iis.net/configreference/system.webserver/security/requestfiltering/verbs)) で、次の設定を実行します。

   * **要求フィルタリング**&#x200B;の役割サービスまたは機能がインストールされていることを確認します。
   * **要求フィルタリング**&#x200B;パネルで「HTTP 動詞」タブをクリックし、「動詞の拒否」をクリックします。アクションパネルで、開くダイアログに「TRACE」と入力します。

* バナーを削除します。

  **Apache 上**、 /etc/apache2/conf.d/security を編集します。

   * ServerSignature **Off**
   * ServerTokens **Prod**

  **IIS の場合**、次の設定を実行します。

   * **URLScan** をインストールします。
   * **Urlscan.ini** ファイルを編集して **RemoveServerHeader=1** を設定します。

* クエリのサイズを制限して、重要なファイルがアップロードされないようにします。

  **** Apache で、**LimitRequestBody** ディレクティブ（サイズはバイト単位で指定）を / ディレクトリに追加します。

  ```
  <Directory />
      Options FollowSymLinks
      AllowOverride None
      LimitRequestBody 10485760
  </Directory>
  ```

  **IIS の場合** ( [ドキュメント](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits))、 **maxAllowedContentLength** （許可されるコンテンツの最大長）を使用できます。

関連トピック ： 

* [Adobe Marketing Cloud Compliance の概要](https://experienceleague.adobe.com/docs/core-services/assets/Adobe-Marketing-Cloud-Privacy-and-Security-Overview.pdf) (PDF)
* [Adobe Campaign Security の概要](https://www.adobe.com/content/dam/cc/en/security/pdfs/ADB-CampaignSecurity-WP.pdf) (PDF)
