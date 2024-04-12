---
product: campaign
title: Web サーバーの設定
description: Web サーバー設定の主なベストプラクティスの詳細を説明します
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: fc0d3f16-5f62-473d-a1de-aab574eff734
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 25%

---

# Web サーバーの設定 {#web-server-configuration}



Web サーバー（Apache/IIS）設定に関する主なベストプラクティスの一部を以下に示します。

* デフォルトのエラーページを変更します。

* 古い SSL のバージョンと暗号を無効にします。

  **Apache の場合**/etc/apache2/mods-available/ssl.confを編集します。 次に例を示します。

   * `SSLProtocol all -SSLv2 -SSLv3 -TLSv1`
   * `SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SSLv3:!SSLv2:!TLSv1`

  **IIS の場合** （ [詳細を見る](https://support.microsoft.com/en-us/kb/245030)）、次の設定を実行します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL にレジストリサブキーを追加します。
   * 既定でネゴシエートされないプロトコル （TLS 1.2 など）をシステムが使用できるようにするには、以下のレジストリ キーで DisabledByDefault 値の DWORD 値データを 0x0 に変更します **プロトコル** キー：

     SCHANNEL\プロトコル\TLS 1.2\クライアント

     SCHANNEL\プロトコル\TLS 1.2\サーバー

  **SSL を無効にする x.0**

  SCHANNEL\Protocols\SSL 3.0\Client: DisabledByDefault: DWORD （32 ビット）値を 1 に

  SCHANNEL\Protocols\SSL 3.0\Server: Enabled: DWORD （32 ビット）値を 0 に

* **TRACE** メソッドを削除します。

  **Apache の場合**&#x200B;を/etc/apache2/conf.d/security: TraceEnable で編集します。 **オフ**

  **IIS の場合** （ [詳細を見る](https://www.iis.net/configreference/system.webserver/security/requestfiltering/verbs)）、次の設定を実行します。

   * **要求フィルタリング**&#x200B;の役割サービスまたは機能がインストールされていることを確認します。
   * が含まれる **要求のフィルター** [ HTTP 動詞 ] タブをクリックし、[ 動詞の拒否 ] をクリックします。 [ 操作 ] ウィンドウで、[ 開く ] ダイアログに「TRACE」と入力します。

* バナーを削除します。

  **Apache の場合**&#x200B;を/etc/apache2/conf.d/security：に編集します。

   * ServerSignature **Off**
   * ServerTokens **Prod**

  **IIS の場合**&#x200B;を作成し、次の設定を実行します。

   * **URLScan** をインストールします。
   * **Urlscan.ini** ファイルを編集して **RemoveServerHeader=1** を設定します。

* クエリのサイズを制限して、重要なファイルがアップロードされないようにします。

  **Apache の場合**、を追加します **LimitRequestBody** ディレクティブ （バイト単位） （/ ディレクトリ）。

  ```
  <Directory />
      Options FollowSymLinks
      AllowOverride None
      LimitRequestBody 10485760
  </Directory>
  ```

  **IIS の場合** （ [詳細を見る](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits)）、を設定します。 **maxAllowedContentLength** コンテンツフィルタリングオプションの（許可されるコンテンツの最大長）。

関連トピック ： 

* [Adobe Marketing Cloud コンプライアンスの概要](https://experienceleague.adobe.com/docs/core-services/assets/Adobe-Marketing-Cloud-Privacy-and-Security-Overview.pdf) （PDF）
* [Adobe Campaign セキュリティの概要](https://www.adobe.com/content/dam/cc/en/security/pdfs/ADB-CampaignSecurity-WP.pdf) （PDF）
