---
product: campaign
title: LDAP を介した接続
description: LDAP を使用して Campaign にログインする方法を説明します。
feature: Installation, Instance Settings
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 0533cd50-3aa4-4160-9152-e916e149e77f
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 4%

---

# LDAP を介した接続{#connecting-through-ldap}

## Campaign と LDAP の設定 {#configuring-campaign-and-ldap}

>[!NOTE]
>
>LDAP 設定は、オンプレミスインストールまたはハイブリッドインストールでのみ使用できます。

LDAP 設定は、デプロイウィザードで実行されます。 The **[!UICONTROL LDAP の統合]** 最初の設定手順で、オプションを選択する必要があります。 参照： [デプロイウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).

ウィンドウでは、指定した LDAP ディレクトリを介したAdobe Campaignユーザーの ID を設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_01.png)

* LDAP サーバーのアドレスを **[!UICONTROL LDAP サーバー]** フィールドに入力します。 ポート番号を追加できます。 デフォルトでは、使用されるポートは 389 です。
* ドロップダウンリストで、ユーザーの認証方法を選択します。

   * 暗号化されたパスワード (**md5**)

     デフォルトモード。

   * プレーンテキストのパスワード+ SSL (**TLS**)

     認証手順全体（パスワードを含む）が暗号化されます。 セキュアポート 636 は、このモードでは使用できません。Adobe Campaignは、セキュアモードに自動的に切り替わります。

     この認証モードを使用する場合、Linux では、証明書は openLDAP クライアントライブラリによって検証されます。 認証手順が暗号化されるように、有効な SSL 証明書を使用することをお勧めします。 それ以外の場合、情報はプレーンテキストで表示されます。

     証明書は、Windows でも検証されます。

   * Windows NT LAN Manager (**NTLM**)

     独自の Windows 認証。 The **[!UICONTROL 一意の識別子]** は、ドメイン名にのみ使用されます。

   * 分散パスワード認証 (**DPA**)

     独自の Windows 認証。 The **[!UICONTROL 一意の識別子]** は、ドメイン名 (domain.com) にのみ使用されます。

   * プレーンテキストのパスワード

     暗号化なし（テストフェーズでのみ使用）

* ユーザー認証モードを選択します。 **[!UICONTROL 一意のユーザー識別子を自動的に計算]** （手順を参照） [識別名の計算](#distinguished-name-calculation)) または **[!UICONTROL ディレクトリ内の一意のユーザー ID を検索します。]** （手順を参照） [識別子の検索](#searching-for-identifiers)) をクリックします。

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
   <td> プレーンテキスト<br /> </td> 
   <td> Windows、Linux<br /> </td> 
   <td> Windows、Linux<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 識別名の計算 {#distinguished-name-calculation}

識別名 (DN) 識別子を計算する場合は、デプロイウィザードの次の手順で計算モードを設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_02.png)

* ユーザーの一意の識別子を、 **[!UICONTROL 識別名]** フィールドに入力します。

  **[!UICONTROL （ログイン）]** はAdobe Campaign演算子の ID に置き換えられます。

  >[!CAUTION]
  >
  >The **[!UICONTROL dc]** の設定は小文字にする必要があります。

* 「 」オプションを選択します。 **[!UICONTROL ディレクトリ内の認証およびグループからのユーザー権限の同期を有効にします]** LDAP ディレクトリ内のグループとユーザーの関連付けと、Adobe Campaign内のグループとユーザーの関連付けを同期するため。

  このオプションを選択すると、 **[!UICONTROL 検索に使用するアプリケーションレベル DN]** および **[!UICONTROL アプリケーションログインのパスワード]** が有効になっている。

  これら 2 つのフィールドに値を入力すると、Adobe Campaignは独自のログインとパスワードを使用して LDAP サーバーに接続します。 空の場合は、Adobe Campaignは匿名でサーバーに接続します。

## 識別子の検索 {#searching-for-identifiers}

識別子の検索を選択した場合、デプロイウィザードで検索を設定できます。

* Adobe Analytics の **[!UICONTROL 検索に使用するアプリケーションレベル DN]** および **[!UICONTROL アプリケーションログインのパスワード]** フィールドには、Adobe Campaignが識別子を検索する際に使用する識別子とパスワードを入力します。 空の場合は、Adobe Campaignは匿名でサーバーに接続します。
* 次を指定します。 **[!UICONTROL ベース識別子]** および **[!UICONTROL 検索範囲]** 検索を開始する LDAP ディレクトリのサブセットを決定するためのフィールド。

  ドロップダウンリストで必要なモードを選択します。

  ![](assets/s_ncs_install_deployment_wiz_ldap_03.png)

   1. **[!UICONTROL 再帰（デフォルトのモード）]**.

      LDAP ディレクトリは、指定されたレベルから始まり、完全に検索されます。

   1. **[!UICONTROL ベースに限定]**.

      すべての属性が検索に含まれます。

   1. **[!UICONTROL ベースの最初のサブレベルに制限]**.

      検索は、ディレクトリのすべての属性に対して実行され、属性の第 1 レベルから開始されます。

* The **[!UICONTROL フィルター]** 「 」フィールドでは、検索範囲を絞り込むための要素を指定できます。

## LDAP 認証の設定 {#configuring-ldap-authorizations}

このウィンドウは、 **[!UICONTROL ディレクトリ内の認証およびグループからのユーザー権限の同期を有効にします]** オプション。

![](assets/s_ncs_install_deployment_wiz_ldap_04.png)

ユーザーが属するグループまたはグループと、それに対応する権限を検索するには、複数のパラメーターを指定する必要があります。例：

* の **[!UICONTROL データベース識別子]** フィールド、
* の **[!UICONTROL 検索範囲]** フィールド、

  >[!NOTE]
  >
  >DN の検索を選択した場合は、「 **[!UICONTROL DN 検索パラメーターの再利用]** 前の画面から、DN と検索範囲の選択した値を引き継ぐため。

* の **[!UICONTROL 権限検索フィルター]** フィールド（ログインとユーザーの識別名に基づく）
* の **[!UICONTROL グループまたは認証名を含む属性]** ユーザーのフィールド
* の **[!UICONTROL 関連付けマスク]** Adobe Campaign内のグループ名とそれに関連する権限を抽出できるフィールド。 正規表現を使用して、名前を検索できます。
* 選択 **[!UICONTROL オペレーターがAdobe Campaignで宣言されていない場合に、LDAP ディレクトリで宣言されたユーザーの接続を有効にする]** 接続時にユーザーにアクセス権が自動的に付与されるようにします。

クリック **[!UICONTROL 保存]** をクリックして、インスタンスの設定を完了します。

## オペレーターの管理 {#managing-operators}

設定を確認したら、LDAP ディレクトリを使用して、管理するAdobe Campaignオペレーターを定義する必要があります。

LDAP ディレクトリを使用してオペレーターを認証するには、対応するプロファイルを編集し、 **[!UICONTROL アクセスパラメーターの編集]** リンク。 を選択します。 **[!UICONTROL 認証に LDAP を使用]** option: **[!UICONTROL パスワード]** この演算子のフィールドは灰色表示になっています。

![](assets/s_ncs_install_operator_in_ldap.png)

## ユースケース {#use-cases}

この節では、ニーズに応じて最も適切な設定をおこなうのに役立つ、簡単な使用例をいくつか示します。

1. ユーザーが LDAP ディレクトリに作成されたが、Adobe Campaignには作成されていない。

   Adobe Campaign のプラットフォームにアクセスするユーザーを、LDAP で認証することができます。Adobe Campaignでオペレーターをその場でAdobe Campaignで作成できるように、LDAP ディレクトリ内の ID とパスワードの組み合わせの有効性を制御できる必要があります。 これをおこなうには、 **[!UICONTROL オペレーターがAdobe Campaignで宣言されていない場合に、LDAP ディレクトリで宣言されたユーザーの接続を有効にする]** オプション。 この場合、グループの同期も設定する必要があります。 **[!UICONTROL ディレクトリ内の認証およびグループからのユーザー権限の同期を有効にします]** オプションを選択する必要があります。

1. ユーザーがAdobe Campaignに作成されましたが、LDAP ディレクトリには作成されていません。

   Adobe Campaignにログオンできなくなります。

1. LDAP ディレクトリ内に、Adobe Campaignに存在しないグループがあります。

   このグループはAdobe Campaignでは作成されません。 グループを作成し、グループを同期して、 **[!UICONTROL ディレクトリ内の認証およびグループからのユーザー権限の同期を有効にします]** オプション。

1. グループはAdobe Campaignに存在し、イベントの後に LDAP ディレクトリがアクティブ化されます。 Adobe Campaignのユーザーグループは、LDAP グループのコンテンツに自動的に置き換えられません。 同様に、グループがAdobe Campaignにのみ存在する場合は、LDAP でグループが作成されて同期されるまで、LDAP ユーザーを追加できません。

   グループは、Adobe Campaignでも LDAP でも、その場では作成されません。 これらは、Adobe Campaignと LDAP ディレクトリの両方で、個別に作成する必要があります。

   LDAP ディレクトリ内のグループの名前は、Adobe Campaignグループの名前と一致する必要があります。 関連付けマスクは、デプロイメントウィザードの最後の設定段階で定義されます。 Adobe Campaign_(.&#42;) など ) です。
