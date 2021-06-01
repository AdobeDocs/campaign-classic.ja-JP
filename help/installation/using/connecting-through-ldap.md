---
product: campaign
title: LDAP を介した接続
description: 'LDAPを使用してCampaignにログインする方法を説明します。 '
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 0533cd50-3aa4-4160-9152-e916e149e77f
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 2%

---

# LDAP を介した接続{#connecting-through-ldap}

## キャンペーンとLDAPの設定{#configuring-campaign-and-ldap}

>[!NOTE]
>
>LDAP設定は、オンプレミスインストールまたはハイブリッドインストールでのみ可能です。

LDAP設定は、デプロイウィザードで実行されます。 最初の設定手順で、**[!UICONTROL LDAP integration]**&#x200B;オプションを選択する必要があります。 [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard)を参照してください。

ウィンドウでは、指定したLDAPディレクトリを介したAdobe CampaignユーザーのIDを設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_01.png)

* **[!UICONTROL LDAP server]**&#x200B;フィールドにLDAPサーバーのアドレスを指定します。 ポート番号を追加できます。 デフォルトでは、使用されるポートは389です。
* ドロップダウンリストで、ユーザーの認証方法を選択します。

   * 暗号化されたパスワード(**md5**)

      デフォルトモード。

   * プレーンテキストのパスワード+ SSL (**TLS**)

      認証手順全体（パスワードを含む）が暗号化されます。 セキュアポート636は、このモードでは使用できません。Adobe Campaignは自動的にセキュアモードに切り替わります。

      この認証モードを使用すると、Linuxでは、証明書はopenLDAPクライアントライブラリによって検証されます。 認証手順が暗号化されるように、有効なSSL証明書を使用することをお勧めします。 そうしないと、情報はプレーンテキストになります。

      証明書はWindowsでも検証されます。

   * Windows NT LAN Manager (**NTLM**)

      独自のWindows認証。 **[!UICONTROL 一意の識別子]**&#x200B;はドメイン名にのみ使用されます。

   * 分散パスワード認証(**DPA**)

      独自のWindows認証。 **[!UICONTROL 一意の識別子]**&#x200B;は、ドメイン名(domain.com)にのみ使用されます。

   * プレーンテキストのパスワード

      暗号化なし（テストフェーズでのみ使用）。

* ユーザー認証モードを選択します。**[!UICONTROL 一意のユーザー識別子]**&#x200B;を自動的に計算する（手順[識別名の計算](#distinguished-name-calculation)を参照）か、**[!UICONTROL ディレクトリ内で一意のユーザー識別子を検索します（手順[識別子の検索](#searching-for-identifiers)を参照）。]**

## 互換性 {#compatibility}

互換性のあるシステムは、選択した認証メカニズムによって異なります。 次に、オペレーティングシステムとLDAPサーバーの互換性マトリックスを示します。

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
   <td> プレーンテキスト<br /> </td> 
   <td> Windows、Linux<br /> </td> 
   <td> Windows、Linux<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 識別名の計算{#distinguished-name-calculation}

識別名(DN)識別子を計算する場合は、デプロイウィザードの次の手順で計算モードを設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_02.png)

* **[!UICONTROL 識別名]**&#x200B;フィールドに、ディレクトリ内のユーザーの一意の識別子（識別名 — DN）を指定します。

   **[!UICONTROL （ログイン）]** は、Adobe CampaignオペレーターのIDに置き換えられます。

   >[!CAUTION]
   >
   >**[!UICONTROL dc]**&#x200B;の設定は小文字にする必要があります。

* LDAPディレクトリ内のグループとユーザーの関連付け、およびAdobe Campaign内のグループとユーザーの関連付けを同期するには、「**[!UICONTROL Enable synchronization of user rights from authorizations and groups in the directory]**」オプションを選択します。

   このオプションを選択すると、検索&#x200B;]**に使用する**[!UICONTROL &#x200B;アプリケーションレベルDNと、アプリケーションログイン&#x200B;]**の**[!UICONTROL &#x200B;パスワードが有効になります。

   これら2つのフィールドに値を入力すると、Adobe Campaignは独自のログインとパスワードを使用してLDAPサーバーに接続します。 空の場合、Adobe Campaignは匿名でサーバーに接続します。

## 識別子{#searching-for-identifiers}の検索

識別子の検索を選択した場合、デプロイウィザードで検索を設定できます。

* 検索&#x200B;]**および**[!UICONTROL &#x200B;アプリケーションログイン&#x200B;]**フィールドの検索に使用する**[!UICONTROL &#x200B;アプリケーションレベルDNに、Adobe Campaignが識別子を検索するために接続する識別子とパスワードを指定します。 空の場合、Adobe Campaignは匿名でサーバーに接続します。
* 検索を開始するLDAPディレクトリのサブセットを決定するために、**[!UICONTROL 基本識別子]**&#x200B;および&#x200B;**[!UICONTROL 検索範囲]**&#x200B;フィールドを指定します。

   ドロップダウンリストで必要なモードを選択します。

   ![](assets/s_ncs_install_deployment_wiz_ldap_03.png)

   1. **[!UICONTROL 繰り返し（デフォルトモード）]**。

      LDAPディレクトリは、指定されたレベルから始まり、完全に検索されます。

   1. **[!UICONTROL ベースに限定]**.

      すべての属性が検索に含まれます。

   1. **[!UICONTROL ベース]**&#x200B;の最初のサブレベルに制限されます。

      検索は、ディレクトリのすべての属性に対して、属性の第1レベルから開始して実行されます。

* 「**[!UICONTROL フィルター]**」フィールドを使用して、検索範囲を絞り込むための要素を指定できます。

## LDAP認証の設定{#configuring-ldap-authorizations}

このウィンドウは、「]**ディレクトリ内の権限およびグループのユーザー権限の同期を有効にする」オプションを選択すると表示されます。**[!UICONTROL 

![](assets/s_ncs_install_deployment_wiz_ldap_04.png)

ユーザーが属するグループまたはグループと、対応する権限を検索するために、複数のパラメーターを指定する必要があります。例：

* **[!UICONTROL データベース識別子]**&#x200B;フィールド
* **[!UICONTROL 検索範囲]**&#x200B;フィールド

   >[!NOTE]
   >
   >DNの検索を選択した場合は、「**[!UICONTROL DN検索パラメーター]**&#x200B;を再利用して、前の画面からDNと検索範囲の選択した値を引き継ぐ」を選択できます。

* **[!UICONTROL 権限検索フィルター]**&#x200B;フィールド（ログイン名とユーザーの識別名に基づく）
* ユーザーに関するグループまたは認証名&#x200B;]**フィールドを含む**[!UICONTROL &#x200B;属性
* **[!UICONTROL 関連付けマスク]**&#x200B;フィールド。Adobe Campaignでのグループ名とそれに関連する権限を抽出できます。 正規表現を使用して、名前を検索できます。
* オペレーターがAdobe Campaign ]**で宣言されていない場合は、「**[!UICONTROL  LDAPディレクトリで宣言されたユーザーの接続を有効にする」を選択し、接続時にユーザーにアクセス権が自動的に付与されるようにします。

「**[!UICONTROL 保存]**」をクリックして、インスタンスの設定を終了します。

## オペレーターの管理{#managing-operators}

設定を確認したら、LDAPディレクトリを使用して、管理するAdobe Campaignオペレーターを定義する必要があります。

LDAPディレクトリを使用してオペレーターを認証するには、対応するプロファイルを編集し、「**[!UICONTROL アクセスパラメーター]**&#x200B;を編集」リンクをクリックします。 「**[!UICONTROL 認証にLDAPを使用]**」オプションを選択します。**[!UICONTROL パスワード]**&#x200B;フィールドは、この演算子では灰色表示になっています。

![](assets/s_ncs_install_operator_in_ldap.png)

## ユースケース {#use-cases}

この節では、ニーズに基づいて最も適切な設定を実現するのに役立つ、簡単な使用例をいくつか示します。

1. ユーザーがLDAPディレクトリに作成されたが、Adobe Campaignには作成されていない。

   Adobe Campaign のプラットフォームにアクセスするユーザーを、LDAP で認証することができます。Adobe CampaignでオペレーターをオンザフライでAdobe Campaignで作成できるように、LDAPディレクトリ内のIDとパスワードの組み合わせの有効性を制御できる必要があります。 これをおこなうには、「Adobe Campaign ]**で演算子が宣言されていない場合、LDAPディレクトリで宣言されたユーザーの接続を有効にする」オプションをオンにします。**[!UICONTROL &#x200B;この場合、グループの同期も設定する必要があります。**[!UICONTROL ディレクトリ]**&#x200B;のオプションで、認証およびグループからのユーザー権限の同期を有効にする必要があります。

1. ユーザーがAdobe Campaignに作成されたが、LDAPディレクトリには作成されていない。

   Adobe Campaignにログオンできなくなります。

1. LDAPディレクトリに、Adobe Campaignに存在しないグループがあります。

   このグループはAdobe Campaignでは作成されません。 **[!UICONTROL 「]**&#x200B;ディレクトリ内の認証とグループからのユーザー権限の同期を有効にする」オプションを使用して一致を有効にするには、グループを作成し、グループを同期する必要があります。

1. グループはAdobe Campaignに存在し、イベントの後にLDAPディレクトリがアクティブ化されます。Adobe Campaignのユーザーグループは、LDAPグループのコンテンツに自動的に置き換えられません。 同様に、Adobe Campaignにのみグループが存在する場合、LDAPでグループが作成および同期されるまで、LDAPユーザーを追加できません。

   グループは、Adobe CampaignでもLDAPでも、その場で作成されることはありません。 これらは、Adobe CampaignとLDAPディレクトリの両方で、個別に作成する必要があります。

   LDAPディレクトリ内のグループの名前は、Adobe Campaignグループの名前と一致する必要があります。 関連付けマスクは、デプロイウィザードの最後の設定段階で定義されます。Adobe Campaign_(.*)を使用します。
