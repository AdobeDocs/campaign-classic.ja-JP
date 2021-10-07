---
product: campaign
title: Web サーバー設定
description: Web サーバー設定の主なベストプラクティスの詳細を説明します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: fc0d3f16-5f62-473d-a1de-aab574eff734
source-git-commit: 32f55d02920b0104198f809b1be0a91306a4d9e4
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 37%

---

# Web サーバー設定 {#web-server-configuration}

![](../../assets/v7-only.svg)

Web サーバー (Apache/IIS) の設定に関する主なベストプラクティスを以下に示します。

* デフォルトのエラーページを変更します。

* 古い SSL のバージョンと暗号を無効にします。

   **Apache**&#x200B;で、/etc/apache2/mods-available/ssl.confを編集します。次に例を示します。

   * SSLProtocol all -SSLv2 -SSLv3 -TLSv1
   * SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SSLv3:!SSLv2:!TLSv1

   **IIS** ( ドキュメントを [参照](https://support.microsoft.com/en-us/kb/245030)) で、次の設定を実行します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL にレジストリサブキーを追加します。
   * デフォルトでネゴシエートされないプロトコル（TLS 1.2 など）をシステムが使用できるようにするには、**Protocols** キーの下にある次のレジストリキーで、DisabledByDefault 値の DWORD 値データを 0x0 に変更します。

      SCHANNEL\Protocols\TLS 1.2\Client

      SCHANNEL\Protocols\TLS 1.2\Server
   **SSL x.0 の無効化**

   SCHANNEL\Protocols\SSL 3.0\Client:DisabledByDefault:DWORD（32 ビット）値を 1 に設定

   SCHANNEL\Protocols\SSL 3.0\Server:有効：DWORD（32 ビット）値を 0 に設定

* **TRACE** メソッドを削除します。

   **Apache**&#x200B;で、/etc/apache2/conf.d/security を編集します。TraceEnable  **Off**

   **IIS** ( ドキュメントを [参照](https://www.iis.net/configreference/system.webserver/security/requestfiltering/verbs)) で、次の設定を実行します。

   * **要求フィルタリング**&#x200B;の役割サービスまたは機能がインストールされていることを確認します。
   * **要求フィルタリング**&#x200B;パネルで「HTTP 動詞」タブをクリックし、「動詞の拒否」をクリックします。アクションパネルで、開くダイアログに「TRACE」と入力します。

* バナーを削除します。

   **Apache**&#x200B;で、/etc/apache2/conf.d/security を編集します。

   * ServerSignature **Off**
   * ServerTokens **Prod**

   **IIS**&#x200B;で、次の設定を実行します。

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

   **IIS** ( ドキュメン [ト](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits)を参照 ) で、コンテンツのフィルターオプションに **maxAllowedContentLength** （許容最大コンテンツ長）を設定します。

関連トピック ： 

* [Adobe Marketing Cloudコンプライアンスの概要](https://experienceleague.adobe.com/docs/core-services/assets/Adobe-Marketing-Cloud-Privacy-and-Security-Overview.pdf) (PDF)
* [Adobe Campaign Security の概要](https://wwwimages.adobe.com/content/dam/acom/en/marketing-cloud/campaign/pdfs/54658.en.campaign.wp.adb-security.pdf) (PDF)
