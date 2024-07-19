---
product: campaign
title: Web サーバーの設定
description: Web サーバー設定の主なベストプラクティスの詳細を説明します
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: fc0d3f16-5f62-473d-a1de-aab574eff734
source-git-commit: dba90a154e08400ae6ab6478623a50d48d72207c
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 25%

---

# Web サーバーの設定 {#web-server-configuration}



Web サーバー（Apache/IIS）設定に関する主なベストプラクティスの一部を以下に示します。

* デフォルトのエラーページを変更します。

* 古い SSL のバージョンと暗号を無効にします。

  **Apache の場合**、/etc/apache2/mods-available/ssl.confを編集します。 次に例を示します。

   * `SSLProtocol all -SSLv2 -SSLv3 -TLSv1`
   * `SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SSLv3:!SSLv2:!TLSv1`

  **IIS の場合** （[ ドキュメント ](https://support.microsoft.com/en-us/kb/245030) を参照）、次の設定を実行します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL にレジストリサブキーを追加します。
   * 既定でネゴシエートされないプロトコル （TLS 1.2 など）をシステムが使用できるようにするには、**Protocols** キーの下にある次のレジストリ キーで、DisabledByDefault 値の DWORD 値データを 0x0 に変更します。

     SCHANNEL\プロトコル\TLS 1.2\クライアント

     SCHANNEL\プロトコル\TLS 1.2\サーバー

  **SSL を無効にする x.0**

  SCHANNEL\Protocols\SSL 3.0\Client: DisabledByDefault: DWORD （32 ビット）値を 1 に

  SCHANNEL\Protocols\SSL 3.0\Server: Enabled: DWORD （32 ビット）値を 0 に

* **TRACE** メソッドを削除します。

  **Apache の場合**、/etc/apache2/conf.d/security: TraceEnable **Off** で編集します。

  **IIS の場合** （[ ドキュメント ](https://www.iis.net/configreference/system.webserver/security/requestfiltering/verbs) を参照）、次の設定を実行します。

   * **要求フィルタリング**&#x200B;の役割サービスまたは機能がインストールされていることを確認します。
   * **要求フィルター** ウィンドウで、[ HTTP 動詞 ] タブをクリックし、[ 動詞の拒否 ] をクリックします。 [ 操作 ] ウィンドウで、[ 開く ] ダイアログに「TRACE」と入力します。

* バナーを削除します。

  **Apache の場合**、/etc/apache2/conf.d/security を編集します。

   * ServerSignature **Off**
   * ServerTokens **Prod**

  **IIS の場合**、次の設定を実行します。

   * **URLScan** をインストールします。
   * **Urlscan.ini** ファイルを編集して **RemoveServerHeader=1** を設定します。

* クエリのサイズを制限して、重要なファイルがアップロードされないようにします。

  **Apache の場合**、/ディレクトリに **LimitRequestBody** ディレクティブ（バイト単位のサイズ）を追加します。

  ```
  <Directory />
      Options FollowSymLinks
      AllowOverride None
      LimitRequestBody 10485760
  </Directory>
  ```

  **IIS** （[ ドキュメント ](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits) を参照）で、コンテンツフィルタリングオプションの **maxAllowedContentLength** （許可されるコンテンツの最大長）を設定します。

関連トピック ： 

* [Adobe Marketing Cloud コンプライアンスの概要 ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/overview#privacy)
* [Adobe Campaignのセキュリティの概要 ](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/overview#security)
