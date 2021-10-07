---
product: campaign
title: LDAP を介した接続
description: 'LDAP を使用して Campaign にログインする方法を説明します '
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 0533cd50-3aa4-4160-9152-e916e149e77f
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 2%

---

# LDAP を介した接続{#connecting-through-ldap}

![](../../assets/v7-only.svg)

## Campaign と LDAP の設定 {#configuring-campaign-and-ldap}

>[!NOTE]
>
>LDAP 設定は、オンプレミスインストールまたはハイブリッドインストールでのみ可能です。

LDAP 設定は、デプロイウィザードで実行されます。 最初の設定手順で、**[!UICONTROL LDAP 統合]** オプションを選択する必要があります。 [ デプロイウィザード ](../../installation/using/deploying-an-instance.md#deployment-wizard) を参照してください。

ウィンドウでは、指定した LDAP ディレクトリを介したAdobe Campaignユーザーの ID を設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_01.png)

* **[!UICONTROL 「LDAP server]**」フィールドに LDAP サーバーのアドレスを指定します。 ポート番号を追加できます。 デフォルトでは、使用されるポートは 389 です。
* ドロップダウンリストで、ユーザーの認証方法を選択します。

   * 暗号化されたパスワード (**md5**)

      デフォルトモード。

   * プレーンテキストのパスワード+ SSL (**TLS**)

      認証手順全体（パスワードを含む）が暗号化されます。 セキュアポート 636 は、次のモードでは使用できません。Adobe Campaignは自動的にセキュアモードに切り替わります。

      この認証モードを使用すると、Linux では、証明書は openLDAP クライアントライブラリによって検証されます。 認証手順が暗号化されるように、有効な SSL 証明書を使用することをお勧めします。 それ以外の場合は、情報はプレーンテキストで表示されます。

      証明書は Windows でも検証されます。

   * Windows NT LAN Manager (**NTLM**)

      独自の Windows 認証。 **[!UICONTROL 一意の識別子]** はドメイン名にのみ使用されます。

   * 分散パスワード認証 (**DPA**)

      独自の Windows 認証。 **[!UICONTROL 一意の識別子]** は、ドメイン名 (domain.com) にのみ使用されます。

   * プレーンテキストのパスワード

      暗号化は使用しない（テストフェーズでのみ使用）。

* ユーザー認証モードを選択します。**[!UICONTROL 一意のユーザー識別子]** を自動的に計算する（手順 [ 識別名の計算 ](#distinguished-name-calculation) を参照）か、**[!UICONTROL ディレクトリ内で一意のユーザー識別子を検索します（手順 [ 識別子の検索 ](#searching-for-identifiers) を参照）。]**

## 互換性 {#compatibility}

互換性のあるシステムは、選択した認証メカニズムによって異なります。 次に、オペレーティングシステムと LDAP サーバーの互換性マトリックスを示します。

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
   <td> NTLM および DPA<br /> </td> 
   <td> </td> 
   <td> Windows<br /> </td> 
  </tr> 
  <tr> 
   <td> プレーンテキスト <br /> </td> 
   <td> Windows、Linux<br /> </td> 
   <td> Windows、Linux<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 識別名の計算 {#distinguished-name-calculation}

識別名 (DN) 識別子を計算する場合は、デプロイウィザードの次の手順で計算モードを設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_02.png)

* **[!UICONTROL 識別名]** フィールドで、ディレクトリ（識別名 — DN）内のユーザーの一意の識別子を指定します。

   **[!UICONTROL （ログイン）]** は、Adobe Campaignオペレーターの ID に置き換えられます。

   >[!CAUTION]
   >
   >**[!UICONTROL dc]** の設定は小文字にする必要があります。

* LDAP ディレクトリのグループとユーザーの関連付けと、Adobe Campaignのグループとユーザーの関連付けを同期するには、「**[!UICONTROL Enable synchronization of user rights from authorizations and groups in the directory]**」オプションを選択します。

   このオプションを選択すると、検索 ]**に使用する**[!UICONTROL  アプリケーションレベル DN と **[!UICONTROL アプリケーションログイン]** のパスワードが有効になります。

   これら 2 つのフィールドに値を入力すると、Adobe Campaignは独自のログインとパスワードを使用して LDAP サーバーに接続します。 空の場合、Adobe Campaignは匿名でサーバーに接続します。

## 識別子の検索 {#searching-for-identifiers}

識別子を検索する場合は、デプロイウィザードで検索を設定できます。

* 「**[!UICONTROL アプリケーションレベル DN で、]** の検索と **[!UICONTROL のパスワード]**」フィールドに、Adobe Campaignが識別子を検索する際に使用する識別子とパスワードを入力します。 空の場合、Adobe Campaignは匿名でサーバーに接続します。
* **[!UICONTROL 基本識別子]** と **[!UICONTROL 検索範囲]** フィールドを指定して、検索を開始する LDAP ディレクトリのサブセットを決定します。

   ドロップダウンリストで必要なモードを選択します。

   ![](assets/s_ncs_install_deployment_wiz_ldap_03.png)

   1. **[!UICONTROL 繰り返し（デフォルトモード）]**。

      LDAP ディレクトリは、特定のレベルから始まり、完全に検索されます。

   1. **[!UICONTROL ベースに限定]**.

      すべての属性が検索に含まれます。

   1. **[!UICONTROL 基本の最初のサブレベルに制限されます]**。

      検索は、ディレクトリのすべての属性に対して実行され、属性の最初のレベルから開始されます。

* 「**[!UICONTROL フィルター]**」フィールドを使用して、検索範囲を絞り込むための要素を指定できます。

## LDAP 認証の設定 {#configuring-ldap-authorizations}

このウィンドウは、「]**ディレクトリ内の権限およびグループのユーザー権限の同期を有効にする」オプションを選択すると表示されます。**[!UICONTROL 

![](assets/s_ncs_install_deployment_wiz_ldap_04.png)

ユーザーが属するグループまたはグループと、それに対応する権限を検索するには、次のように、複数のパラメーターを指定する必要があります。

* **[!UICONTROL データベース識別子]** フィールド
* **[!UICONTROL 検索範囲]** フィールド

   >[!NOTE]
   >
   >DN の検索を選択した場合は、「**[!UICONTROL DN 検索パラメーター]** を再利用して、前の画面から DN と検索範囲の選択した値を引き継ぐことができます。

* **[!UICONTROL 権限検索フィルター]** フィールド。ログイン名とユーザーの識別名に基づきます。
* ユーザーに関するグループまたは認証名 ]**フィールドを含む**[!UICONTROL  属性
* **[!UICONTROL 関連付けマスク]** フィールド。Adobe Campaignでのグループ名とそれに関連する権限を抽出できます。 正規表現を使用して、名前を検索できます。
* 「**[!UICONTROL Adobe Campaign]** でオペレーターが宣言されていない場合、LDAP ディレクトリで宣言されたユーザーの接続を有効にする」を選択して、接続時にユーザーにアクセス権が自動的に付与されるようにします。

「**[!UICONTROL 保存]**」をクリックして、インスタンスの設定を終了します。

## オペレーターの管理 {#managing-operators}

設定を確認したら、LDAP ディレクトリを介して管理するAdobe Campaignオペレーターを定義する必要があります。

LDAP ディレクトリを使用してオペレーターを認証するには、対応するプロファイルを編集し、「**[!UICONTROL アクセスパラメーターを編集]**」リンクをクリックします。 「**[!UICONTROL 認証に LDAP を使用]**」オプションを選択します。**[!UICONTROL Password]** フィールドは、この演算子では灰色表示になっています。

![](assets/s_ncs_install_operator_in_ldap.png)

## 使用例 {#use-cases}

この節では、ニーズに基づいて最も適切な設定を達成するのに役立つ、簡単な使用例をいくつか示します。

1. ユーザーが LDAP ディレクトリに作成されたが、Adobe Campaignには作成されなかった。

   Adobe Campaign のプラットフォームにアクセスするユーザーを、LDAP で認証することができます。Adobe Campaignでオペレーターをオンザフライで作成できるように、Adobe Campaignは、LDAP ディレクトリ内の ID とパスワードの組み合わせの有効性を制御できる必要があります。 これをおこなうには、「**[!UICONTROL Adobe Campaign]** で演算子が宣言されていない場合は、LDAP ディレクトリで宣言されたユーザーの接続を有効にする」オプションをオンにします。 この場合、グループの同期も設定する必要があります。**[!UICONTROL ディレクトリ]** で、認証およびグループからのユーザー権限の同期を有効にするオプションを選択する必要があります。

1. ユーザーはAdobe Campaignに作成されましたが、LDAP ディレクトリには作成されていません。

   Adobe Campaignにログオンできなくなります。

1. LDAP ディレクトリに、Adobe Campaignに存在しないグループがあります。

   このグループは、Adobe Campaignでは作成されません。 **[!UICONTROL 「]** ディレクトリ内の認証とグループからのユーザー権限の同期を有効にする」オプションを使用してマッチアップを有効にするには、グループを作成し、グループを同期する必要があります。

1. グループはAdobe Campaignに存在し、イベントの後に LDAP ディレクトリがアクティブ化されます。Adobe Campaignのユーザーグループは、LDAP グループの内容に自動的に置き換えられません。 同様に、グループがAdobe Campaignにのみ存在する場合は、LDAP でグループが作成および同期されるまで、LDAP ユーザーを追加できません。

   グループは、Adobe Campaignでも LDAP でも、その場で作成されることはありません。 これらは、Adobe Campaignと LDAP ディレクトリの両方で、個別に作成する必要があります。

   LDAP ディレクトリ内のグループの名前は、Adobe Campaignグループの名前と一致する必要があります。 関連付けマスクは、デプロイウィザードの最後の設定段階で定義します。Adobe Campaign_(.*) と呼ばれます。
