---
product: campaign
title: LDAP を介した接続
description: LDAP を使用して Campaign にログインする方法を説明します
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 0533cd50-3aa4-4160-9152-e916e149e77f
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# LDAP を介した接続{#connecting-through-ldap}

## Campaign と LDAP の設定 {#configuring-campaign-and-ldap}

>[!NOTE]
>
>LDAP 設定は、オンプレミスインストールまたはハイブリッドインストールの場合にのみ使用できます。

LDAP の設定は、デプロイメントウィザードで実行します。 この **[!UICONTROL LDAP 統合]** オプションは、最初の設定手順で選択する必要があります。 こちらを参照してください [配置ウィザード](../../installation/using/deploying-an-instance.md#deployment-wizard).

このウィンドウでは、指定した LDAP ディレクトリを介してAdobe Campaign ユーザーの識別を設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_01.png)

* に LDAP サーバーのアドレスを指定します。 **[!UICONTROL LDAP サーバー]** フィールド。 ポート番号を追加できます。 デフォルトで使用されるポートは 389 です。
* ドロップダウンリストで、ユーザーの認証方法を選択します。

   * 暗号化されたパスワード（**md5**）

     デフォルトのモード。

   * プレーンテキストのパスワード + SSL （**TLS**）

     認証手順（パスワードを含む）全体が暗号化されます。 このモードでは、セキュアポート 636 を使用しないでください。Adobe Campaignは自動的にセキュアモードに切り替えます。

     Linux でこの認証モードを使用すると、証明書は openLDAP クライアントライブラリによって検証されます。 認証手順が暗号化されるように、有効な SSL 証明書を使用することをお勧めします。 それ以外の場合、情報はプレーンテキストになります。

     証明書は Windows でも検証されます。

   * Windows NT LAN Manager （**NTLM**）

     専用の Windows 認証。 この **[!UICONTROL 一意の識別子]** はドメイン名にのみ使用されます。

   * 分散パスワード認証（**DPA**）

     専用の Windows 認証。 この **[!UICONTROL 一意の識別子]** は、ドメイン名にのみ使用されます（domain.com）。

   * プレーンテキストのパスワード

     暗号化なし（テストフェーズでのみ使用）。

* ユーザー認証モードを選択します。 **[!UICONTROL 一意のユーザー ID を自動的に計算]** （手順を参照） [識別名の計算](#distinguished-name-calculation)）または **[!UICONTROL ディレクトリ内の一意のユーザー ID を検索]** （手順を参照） [識別子の検索](#searching-for-identifiers)）に設定します。

## 互換性 {#compatibility}

互換性のあるシステムは、選択した認証メカニズムによって異なります。 次に、オペレーティングシステムと LDAP サーバーの互換表を示します。

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

識別名（DN）識別子を計算する場合は、デプロイメントウィザードの次の手順で計算モードを設定できます。

![](assets/s_ncs_install_deployment_wiz_ldap_02.png)

* で、ディレクトリ内のユーザーの一意の識別子（識別名 – DN）を指定します **[!UICONTROL 識別名]** フィールド。

  **[!UICONTROL （ログイン）]** はAdobe Campaign演算子の識別子に置き換えられます。

  >[!CAUTION]
  >
  >この **[!UICONTROL dc]** 設定は小文字で指定する必要があります。

* オプションを選択します **[!UICONTROL ディレクトリ内の権限およびグループからユーザー権限の同期を有効にする]** これにより、LDAP ディレクトリ内のグループとユーザーの関連付け、およびAdobe Campaign内のグループとユーザーの関連付けを同期させます。

  このオプションを選択すると、 **[!UICONTROL 検索に使用するアプリケーションレベルの DN]** および **[!UICONTROL アプリケーションログインのパスワード]** が有効になっています。

  これら 2 つのフィールドに値を入力すると、Adobe Campaignは独自のログインとパスワードを使用して LDAP サーバーに接続します。 空の場合、Adobe Campaignはサーバーに匿名で接続します。

## 識別子の検索 {#searching-for-identifiers}

識別子の検索を選択した場合、デプロイメントウィザードで検索を設定できます。

* が含まれる **[!UICONTROL 検索に使用するアプリケーションレベルの DN]** および **[!UICONTROL アプリケーションログインのパスワード]** フィールドに、Adobe Campaignが識別情報の検索に接続する際に使用する識別情報とパスワードを指定します。 空の場合、Adobe Campaignはサーバーに匿名で接続します。
* を指定 **[!UICONTROL ベース識別子]** および **[!UICONTROL 検索範囲]** 検索を開始する LDAP ディレクトリのサブセットを決定するためのフィールド。

  ドロップダウンリストで必要なモードを選択します。

  ![](assets/s_ncs_install_deployment_wiz_ldap_03.png)

   1. **[!UICONTROL 再帰的（デフォルトモード）]**.

      LDAP ディレクトリは、指定したレベルから始まる完全な検索が実行されます。

   1. **[!UICONTROL ベースに限定]**.

      すべての属性が検索に含まれます。

   1. **[!UICONTROL ベースの最初のサブレベルに制限]**.

      検索は、ディレクトリのすべての属性に対して、属性の最初のレベルから実行されます。

* この **[!UICONTROL フィルター]** フィールドでは、要素を指定して検索の範囲を絞り込むことができます。

## LDAP 認証の設定 {#configuring-ldap-authorizations}

このウィンドウは、 **[!UICONTROL ディレクトリ内の権限およびグループからユーザー権限の同期を有効にする]** オプション。

![](assets/s_ncs_install_deployment_wiz_ldap_04.png)

ユーザーが属する 1 つ以上のグループと、それに対応する権限を見つけるには、いくつかのパラメーターを指定する必要があります。次に例を示します。

* この **[!UICONTROL データベース識別子]** フィールド、
* この **[!UICONTROL 検索範囲]** フィールド、

  >[!NOTE]
  >
  >DN の検索を選択した場合は、次を選択できます **[!UICONTROL DN 検索パラメーターの再利用]** 前の画面で選択した DN の値と検索範囲が引き継がれます。

* この **[!UICONTROL 権限検索フィルター]** フィールド。ログインとユーザーの識別名に基づいています。
* この **[!UICONTROL グループまたは認証名を含む属性]** ユーザーに関するフィールド、
* この **[!UICONTROL 関連付けマスク]** Adobe Campaignのグループ名とそれに関連する権限を抽出できるフィールド。 正規表現を使用して名前を検索できます。
* を選択 **[!UICONTROL 演算子がAdobe Campaignで宣言されていない場合、LDAP ディレクトリで宣言されたユーザーの接続を有効にします]** これにより、ユーザーには接続時にアクセス権が自動的に付与されます。

クリック **[!UICONTROL 保存]** インスタンスの設定を完了します。

## オペレーターの管理 {#managing-operators}

設定を確定したら、LDAP ディレクトリ経由で管理するAdobe Campaign オペレーターを定義する必要があります。

LDAP ディレクトリを使用してオペレーターを認証するには、対応するプロファイルを編集し、 **[!UICONTROL アクセスパラメーターの編集]** リンク。 「」を選択します **[!UICONTROL 認証に LDAP を使用]** オプション：その **[!UICONTROL パスワード]** このオペレーターのフィールドはグレー表示されています。

![](assets/s_ncs_install_operator_in_ldap.png)

## ユースケース {#use-cases}

この節では、ニーズに基づいて最も適切な設定を実現するのに役立つ、簡単なユースケースをいくつか示します。

1. ユーザーが LDAP ディレクトリに作成されましたが、Adobe Campaignには作成されていません。

   Adobe Campaignは、ユーザーが LDAP 認証を介してプラットフォームにアクセスするように設定できます。 Adobe CampaignAdobe Campaignでオペレーターをその場で作成できるように、LDAP ディレクトリで ID/パスワードの組み合わせの有効性を制御できる必要があります。 これを行うには、 **[!UICONTROL 演算子がAdobe Campaignで宣言されていない場合、LDAP ディレクトリで宣言されたユーザーの接続を有効にします]** オプション。 この場合、グループ同期も設定する必要があります。 **[!UICONTROL ディレクトリ内の権限およびグループからユーザー権限の同期を有効にする]** オプションを選択する必要があります。

1. ユーザーがAdobe Campaignに作成されたが、LDAP ディレクトリには作成されていない。

   Adobe Campaignにログオンすることはできません。

1. LDAP ディレクトリに、Adobe Campaignに存在しないグループがあります。

   このグループはAdobe Campaignに作成されません。 を介した照合を有効にするには、グループを作成してグループを同期する必要があります。 **[!UICONTROL ディレクトリ内の権限およびグループからユーザー権限の同期を有効にする]** オプション。

1. Adobe Campaignにグループが存在し、イベントの後に LDAP ディレクトリがアクティブになります。Adobe Campaignのユーザーグループは、LDAP グループのコンテンツに自動的に置き換えられることはありません。 同様に、グループがAdobe Campaignにのみ存在する場合、グループが LDAP で作成および同期されるまで、LDAP ユーザーはグループに追加されません。

   グループは、Adobe Campaignによるものであっても、LDAP によるものであっても、その場で作成されることはありません。 これらは、Adobe Campaignと LDAP ディレクトリの両方で個別に作成する必要があります。

   LDAP ディレクトリ内のグループの名前は、Adobe Campaign グループの名前と一致している必要があります。 関連付けマスクは、デプロイメントウィザードの最後の設定ステージであるAdobe Campaign_（.&#42;）など。
