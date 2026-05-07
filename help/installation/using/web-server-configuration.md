---
product: campaign
title: Web サーバーの設定
description: Web サーバー設定の主なベストプラクティスについて詳しく見る
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: fc0d3f16-5f62-473d-a1de-aab574eff734
source-git-commit: dba90a154e08400ae6ab6478623a50d48d72207c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 22%

---

# Web サーバーの設定 {#web-server-configuration}



Web サーバー（Apache/IIS）設定に関する主なベストプラクティスを以下に示します。

* デフォルトのエラーページを変更します。

* 古い SSL のバージョンと暗号を無効にします。

  **Apache**&#x200B;で、/etc/apache2/mods-available/ssl.confを編集します。 次に例を示します。

   * `SSLProtocol all -SSLv2 -SSLv3 -TLSv1`
   * `SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SSLv3:!SSLv2:!TLSv1`

  **IIS**&#x200B;で（[ ドキュメント ](https://support.microsoft.com/en-us/kb/245030)を参照）、次の設定を実行します。

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL にレジストリサブキーを追加します。
   * デフォルトでネゴシエーションされないプロトコル（TLS 1.2など）をシステムで使用できるようにするには、**Protocols** キーの下にある次のレジストリキーで、DisabledByDefault値のDWORD値データを0x0に変更します。

     SCHANNEL\Protocols\TLS 1.2\Client

     SCHANNEL\Protocols\TLS 1.2\Server

  **SSL x.0**&#x200B;を無効にする

  SCHANNEL\Protocols\SSL 3.0\Client: DisabledByDefault: DWORD （32 ビット）値を1に

  SCHANNEL\Protocols\SSL 3.0\Server：有効：DWORD （32 ビット）値を0に

* **TRACE** メソッドを削除します。

  **Apache**&#x200B;で、/etc/apache2/conf.d/securityで編集：TraceEnable **Off**

  **IIS**&#x200B;で（[ ドキュメント ](https://www.iis.net/configreference/system.webserver/security/requestfiltering/verbs)を参照）、次の設定を実行します。

   * **要求フィルタリング**&#x200B;の役割サービスまたは機能がインストールされていることを確認します。
   * **フィルタリングをリクエスト** ペインで、「HTTP動詞」タブをクリックし、「動詞を拒否」をクリックします。 アクションパネルで、開くダイアログにTRACEと入力します。

* バナーを削除します。

  **Apache**&#x200B;で、/etc/apache2/conf.d/securityを編集します。

   * ServerSignature **Off**
   * ServerTokens **Prod**

  **IIS**&#x200B;で、次の設定を実行します。

   * **URLScan** をインストールします。
   * **Urlscan.ini** ファイルを編集して **RemoveServerHeader=1** を設定します。

* クエリのサイズを制限して、重要なファイルがアップロードされないようにします。

  **Apache**&#x200B;で、/ ディレクトリに&#x200B;**LimitRequestBody** ディレクティブ （バイト単位のサイズ）を追加します。

  ```
  <Directory />
      Options FollowSymLinks
      AllowOverride None
      LimitRequestBody 10485760
  </Directory>
  ```

  **IIS** （[ ドキュメント ](https://www.iis.net/configreference/system.webserver/security/requestfiltering/requestlimits)を参照）で、コンテンツフィルタリングオプションで&#x200B;**maxAllowedContentLength** （許可されるコンテンツの最大長）を設定します。

関連トピック ：

* [Adobe Marketing Cloud コンプライアンスの概要](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/overview#privacy)
* [Adobe Campaignのセキュリティの概要](https://experienceleague.adobe.com/en/docs/experience-platform/landing/governance-privacy-security/overview#security)
