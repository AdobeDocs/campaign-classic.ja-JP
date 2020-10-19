---
title: LDAP を介した接続
description: 'LDAPを使用してキャンペーンにログインする方法を学びます '
page-status-flag: never-activated
uuid: 13a426bc-7c34-49e5-ac8e-26d830845f28
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: additional-configurations
discoiquuid: 1563db7c-ccb6-46b3-9299-67ec0aedaca0
translation-type: tm+mt
source-git-commit: b447e316bed8e0e87d608679c147e6bd7b0815eb
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 1%

---


# LDAP を介した接続{#connecting-through-ldap}

## キャンペーンとLDAPの設定 {#configuring-campaign-and-ldap}

>[!NOTE]
>
>LDAP設定は、オンプレミスまたはハイブリッドインストールでのみ可能です。

LDAP設定は、デプロイメントウィザードで実行されます。 最初の設定手順で **[!UICONTROL LDAP統合]** ・オプションを選択する必要があります。 「 [配置ウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard)」を参照してください。

このウィンドウでは、指定したLDAPディレクトリを介してAdobe CampaignユーザーのIDを設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_01.png)

* 「 **[!UICONTROL LDAP server]** 」フィールドにLDAPサーバーのアドレスを指定します。 ポート番号を追加できます。 デフォルトでは、使用されるポートは389です。
* ドロップダウンリストで、ユーザーの認証方法を選択します。

   * Encrypted password (**md5**)

      デフォルトモード

   * テキスト形式のパスワード+ SSL(**TLS**)

      認証手順（パスワードを含む）全体が暗号化されます。 次のモードでは、セキュアポート636を使用しないでください。Adobe Campaignは自動的にセキュアモードに切り替わります。

      この認証モードを使用する場合、Linuxでは、証明書はopenLDAPクライアントライブラリによって検証されます。 認証手順が暗号化されるように、有効なSSL証明書を使用することをお勧めします。 それ以外の場合は、情報はプレーンテキストで表示されます。

      証明書はWindowsでも検証されます。

   * Windows NT LAN Manager (**NTLM**)

      独自仕様のWindows認証。 [ **[!UICONTROL 一意の識別子]** ]は、ドメイン名にのみ使用されます。

   * 分散パスワード認証(**DPA**)

      独自仕様のWindows認証。 「 **[!UICONTROL 一意の識別子]** 」は、ドメイン名(domain.com)にのみ使用されます。

   * プレーンテキストのパスワード

      暗号化しない（テストフェーズでのみ使用）。

* ユーザー認証モードを選択します。 **[!UICONTROL 一意のユーザー識別子を自動的に計算する]** (手順 [の識別名の計算を参照)か、ディレクトリ内の一意のユーザー識別子を](#distinguished-name-calculation)検索します(手順 **[!UICONTROL 識別子の検索を参照]**[](#searching-for-identifiers))。

## 互換性 {#compatibility}

互換性のあるシステムは、選択した認証メカニズムに応じて異なります。 次に、オペレーティングシステムとLDAPサーバーの互換表を示します。

<table> 
 <thead> 
  <tr> 
   <th> </th> 
   <th> OpenLDAP<br /> </th> 
   <th> Active Directory<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> md5<br /> </td> 
   <td> Windows、Linux<br /> </td> 
   <td> Linux<br /> </td> 
  </tr> 
  <tr> 
   <td> TLS<br /> </td> 
   <td> Linux<br /> </td> 
   <td> Windows、Linux<br /> </td> 
  </tr> 
  <tr> 
   <td> NTLMおよびDPA<br /> </td> 
   <td> </td> 
   <td> Windows<br /> </td> 
  </tr> 
  <tr> 
   <td> plain text<br /> </td> 
   <td> Windows、Linux<br /> </td> 
   <td> Windows、Linux<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 識別名の計算 {#distinguished-name-calculation}

識別名(DN)識別子を計算する場合は、デプロイメントウィザードの次の手順で計算モードを設定します。

![](assets/s_ncs_install_deployment_wiz_ldap_02.png)

* 「 **[!UICONTROL 識別名]** 」フィールドで、ディレクトリ（識別名 — DN）内のユーザーの一意の識別子を指定します。

   **[!UICONTROL (login)]** は、Adobe Campaign演算子の識別子に置き換えられます。

   >[!CAUTION]
   >
   >dc **** 設定は小文字にする必要があります。

* LDAPディレクトリ内のグループとユーザーの関連付けと、Adobe Campaign内のグループとユーザーの関連付けを同期するには、 **** 「ディレクトリ内の承認とグループからのユーザー権限の同期を有効にする」オプションを選択します。

   このオプションを選択すると、アプリケーションログインの検索 **[!UICONTROL と]** パスワードに使用されるアプリケーションレベルDNが有効になります **** 。

   これらの2つのフィールドに値を入力すると、Adobe Campaignは独自のログインとパスワードを使用してLDAPサーバーに接続します。 空の場合、Adobe Campaignは匿名でサーバーに接続します。

## 識別子の検索 {#searching-for-identifiers}

識別子を検索する場合は、デプロイメントウィザードで検索を設定できます。

* アプリのログインフィールドの検索 **[!UICONTROL と]****** パスワードに使用するアプリケーションレベルDNで、Adobe Campaignが識別子を検索する際に使用する識別子とパスワードを指定します。 空の場合、Adobe Campaignは匿名でサーバーに接続します。
* 「 **[!UICONTROL Base identifier]** 」フィールドと「 **[!UICONTROL Search scope]** 」フィールドを指定して、検索の開始元となるLDAPディレクトリのサブセットを特定します。

   ドロップダウンリストで、必要なモードを選択します。

   ![](assets/s_ncs_install_deployment_wiz_ldap_03.png)

   1. **[!UICONTROL Recursive（デフォルトモード）]**。

      LDAPディレクトリは、特定のレベルから始まり、完全に検索されます。

   1. **[!UICONTROL ベースに限定]**.

      すべての属性が検索に含まれます。

   1. **[!UICONTROL ベースの最初のサブレベルに制限します]**。

      ディレクトリのすべての属性に対して、属性の最初のレベルから検索が実行されます。

* 「 **[!UICONTROL フィルタ]** 」フィールドを使用すると、検索の範囲を絞り込むための要素を指定できます。

## LDAP承認の設定 {#configuring-ldap-authorizations}

このウィンドウは、「Enable synchronization of user rights from authorizations and groups in the directory **** 」オプションを選択した場合に表示されます。

![](assets/s_ncs_install_deployment_wiz_ldap_04.png)

ユーザーが属するグループやグループ、およびそれに対応する権限を検索するには、次のようにいくつかのパラメーターを指定する必要があります。

* 「 **[!UICONTROL Database identifier]** 」フィールド、
* [ **[!UICONTROL 検索範囲]** ]フィールド、

   >[!NOTE]
   >
   >DNの検索を選択した場合は、前の画面でDNおよび検索範囲に対して選択した値を伝達するために **** 、「DN検索パラメーターを再利用」を選択できます。

* ログインとユーザーの識別名に基づく **[!UICONTROL 権限検索フィルタ]** 、
* ユーザーに関するグループまたは認証名 **** 、
* adobe campaign内でのグループ名とその関連付けられた権限を抽出できる **[!UICONTROL 「関連付けマスク]** 」フィールド。 正規式を使用して名前を検索できます。
* Adobe Campaignで演算子が宣言されていない場合にLDAPディレクトリで宣言されたユーザーの接続を **[!UICONTROL 有効にするを選択して]** 、接続時にユーザーにアクセス権が自動的に付与されるようにします。

「 **[!UICONTROL 保存]** 」をクリックして、インスタンスの設定を終了します。

## 演算子の管理 {#managing-operators}

設定を確認したら、LDAPディレクトリを介して管理するAdobe Campaign演算子を定義する必要があります。

LDAPディレクトリを使用して演算子を認証するには、対応するプロファイルを編集し、「 **[!UICONTROL Edit the access parameters]** 」リンクをクリックします。 「 **[!UICONTROL Use LDAP for authentication]** 」オプションを選択します。この演算子の「 **[!UICONTROL パスワード]** 」フィールドは灰色表示になっています。

![](assets/s_ncs_install_operator_in_ldap.png)

## 使用例 {#use-cases}

この節では、ニーズに基づいて最も適切な設定を達成するのに役立つ、簡単な使用例をいくつか示します。

1. LDAPディレクトリにユーザーが作成されましたが、Adobe Campaignには作成されません。

   Adobe Campaignは、ユーザーがLDAP認証を介してプラットフォームにアクセスするように設定できます。 Adobe CampaignがLDAPディレクトリ内のIDとパスワードの組み合わせの有効性を制御できる必要があります。これにより、Adobe Campaign内でオンザフライで演算子を作成できます。 To do this, check the **[!UICONTROL Enable the connection of users declared in the LDAP directory if the operator is not declared in Adobe Campaign]** option. この場合、グループ同期も設定する必要があります。「 **[!UICONTROL Enable synchronization of user rights from authorizations and groups in the directory]** 」オプションを選択する必要があります。

1. ユーザーがAdobe Campaignで作成されましたが、LDAPディレクトリにはありません。

   Adobe Campaignにログオンできません。

1. LDAPディレクトリ内に、Adobe Campaignに存在しないグループがあります。

   このグループはAdobe Campaignに作成されません。 「Enable synchronization of user rights from authorizations and groups in the directory **** 」オプションを使用して、グループを作成し、グループを同期して、一致を有効にする必要があります。

1. Adobe Campaignにグループが存在し、イベント後にLDAPディレクトリがアクティブ化される。adobe campaign内のユーザーグループは、LDAPグループのコンテンツに自動的に置き換えられません。 同様に、グループがAdobe Campaign内にのみ存在する場合、LDAPでグループが作成および同期されるまで、LDAPユーザーを追加できません。

   Adobe Campaign別でもLDAP別でも、グループはその場で作成されることはありません。 これらは、Adobe CampaignとLDAPディレクトリの両方で個別に作成する必要があります。

   LDAPディレクトリ内のグループの名前は、Adobe Campaignグループの名前と一致する必要があります。 関連付けマスクは、配置ウィザードの最後の設定段階で定義します。Adobe Campaign_(.*)を使用します。

