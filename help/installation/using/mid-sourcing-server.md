---
title: Adobe Campaign Classicでのミッドソーシングサーバのインストール
description: この節では、Adobe Campaign Classicのミッドソーシングサーバのインストールと設定について説明します。
page-status-flag: never-activated
uuid: 9b891a64-d75e-44d2-8de2-17334e1b8dca
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: additional-configurations
discoiquuid: 34ee3d99-4ffb-4279-b994-5ab7abc7cf06
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b9577d190f26e21f116d99d48fdf2bca84585d50
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 0%

---


# ミッドソーシングサーバー{#mid-sourcing-server}

この節では、ミッドソーシングサーバーのインストールと設定、およびサードパーティが **ミッドソーシング** モードでメッセージを送信できるようにするインスタンスのデプロイについて説明します。

「ミッドソーシング」アーキテクチャは、 [ミッドソーシングの導入時に表示されます](../../installation/using/mid-sourcing-deployment.md)。

ミッドソーシングサーバのインストールは、通常の方法でサーバをインストールする場合と同じプロセスに従います（標準設定を参照）。 独自のデータベースを持つ独立したインスタンスで、配信の実行に使用できます。 簡単に言うと、リモートインスタンスがミッドソーシングモードで配信を実行できるようにするための追加の設定が含まれています。

## インスタンスのインストールおよび設定手順 {#steps-for-installing-and-configuring-an-instance}

### インスタンスのインストールおよび設定に必要な前提条件 {#prerequisites-for-installing-and-configuring-an-instance}

* アプリケーションサーバーのJDK。
* アプリケーションサーバー上のデータベースサーバーにアクセスします。
* ミッドソーシングサーバーへのHTTP(80)またはHTTPS(443)ポートを開くように構成されたファイアウォール。

次の手順では、1台のミッドソーシングサーバーを使用した設定について説明します。 複数のサーバーを使用することもできます。 同様に、内部設定から特定のメッセージ（ワークフロー通知など）を送信することもできます。

### ミッドソーシングデプロイメント用のアプリケーションサーバーのインストールと設定 {#installing-and-configuring-the-application-server-for-mid-sourcing-deployment}

インストール手順は、スタンドアロンインスタンスの場合と同じです。 『 [インストールと設定（シングルマシン）』を参照してください](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-)。

ただし、次の条件を適用する必要があります。

* 手順 **5**&#x200B;で、 **mta** (配信)モジュールとinMail **** （バウンスメール）モジュールを無効にする必要があります。 ただし、 **wfserver** (workflow)モジュールは、アクティブな状態を維持する必要があります。

   ```
   <?xml version='1.0'?>
   <serverconf>  
     <shared>    
       <!-- add lang="eng" to dataStore to force English for the instance -->    
       <dataStore hosts="console.campaign.net*">      
         <mapping logical="*" physical="default"/>    
       </dataStore>  </shared>  
       <mta autoStart="false"/>  
       <wfserver autoStart="true"/>  
       <inMail autoStart="false"/>  
       <sms autoStart="false"/>  
       <listProtect autoStart="false"/>
   </serverconf>
   ```

   For more on this, refer to [Enabling processes](../../installation/using/campaign-server-configuration.md#enabling-processes).

* 手順 **6**、 **9** 、10は必要ありません **** 。
* 手順12 **と13** の間に ****、接続URLの8080ポートを指定する必要があります（コンソールはWebサーバーを経由せずにTomcatと直接通信するため）。 URLはhttp://console.campaign.net:8080になり [ます](http://console.campaign.net)。 手順13 **で**、ミッドソーシングに向けた **[!UICONTROL 問題]** パッケージと、インストールする問題を選択します。

   ![](assets/s_ncs_install_midsourcing02.png)

   >[!CAUTION]
   >
   >技術配信のデフォルトのルーティングは、自動的にミッドソーシングを介した電子メールルーティングに置き換えられます。

### ミッドソーシングサーバーのインストールと設定 {#installing-and-configuring-the-mid-sourcing-server}

クライアントコンソールで、ミッドソーシング **ミッドソーシングアカウントを使用して** 電子メールルーティングを探します( **/Administration/外部アカウント/** フォルダー内)。 ミッドソーシングサーバーの **URL、**&#x200B;アカウント **、パスワード**、 ******** ミラーページURLの設定に、サーバーサーバーをホストするサーバープロバイダーが提供する情報を入力します。 接続をテストします。

>[!NOTE]
>
>mid-sourcingEmitter **(** mid-sourcingEmitter **)オプションは2つの** ミッドソーシングワークフローを作成します。 これは、デフォルトで1時間20分おきに実行され、ミッドソーシングサーバー上の配信情報を収集するプロセスです。

## ミッドソーシングサーバーの展開 {#deploying-a-mid-sourcing-server}

1. アプリケーションサーバーのインストール：

   >[!CAUTION]
   >
   >ミッドソーシングサーバーをインストールし、追加のAdobe Campaignモジュールをインストールする場合は、キャンペーンモジュールではなく配信モジュールを使用することをお勧めします。

   標準のデプロイメントと同じ手順で、 **[!UICONTROL ミッドソーシングプラットフォーム]** (Platform Platform)オプションのみを選択します。

   ![](assets/s_ncs_install_midsourcing01.png)

1. ミッドソーシングモードで受信するための設定

   送信アカウントのパスワードの設定：/ **ミッドソーシング/Access Management/Operators/** フォルダー内で、 **mid** 演算子は、ミッドソーシングモードで送信するリモートインスタンスで使用されます。 この演算子のパスワードを設定し、送信インスタンスの管理者に渡す必要があります。

   「 **ミッドソーシングプラットフォーム** 」オプションは、送信された配信と送信を実行するデフォルトの演算子を保存するためのデフォルトのフォルダーを作成します。

## ミッドソーシングサーバの多重化 {#multiplexing-the-mid-sourcing-server}

>[!CAUTION]
>
>多重化は、オンプレミスの環境に対してのみサポートされます。

1つのミッドソーシングインスタンスを複数の送信インスタンスで共有できます。 これらの各インスタンスは、ミッドソーシングデータベース内の演算子と関連付ける必要があります。 ミッドソーシングサーバー上に2番目のアカウントを作成するには：

1. デフォルトの配信アカウントに関連付けるミッドソーシングー **** /ミッドソーシングーノードにーを作成します(例：prod)。
1. アカウントと同じ名前で、 **[!UICONTROL ミッドソーシング/配信]** ・ノードにフォルダを作成します(例：acception_test)。

   ![](assets/mid_recette_account.png)

1. [ **[!UICONTROL ミッドソーシング] > [アクセス管理] > [演算子]**]で、新しいアカウントを作成します。

   ![](assets/mid_recette_user_create.png)

1. 「 **[!UICONTROL アクセス権]** 」タブで、この操作者に **ミッドソーシング送信グループの権限を与えます** 。 このアクセス権は、 **[!UICONTROL ミッドソーシング/アクセス管理/演算子グループから利用できます]**。

   ![](assets/mid_recette_user_rights.png)

1. 「 **[!UICONTROL Restrict to data in the sub-folders of]** 」オプションを選択し、「配信」配信を選択して、この演算子を「ミッドソーシングフォルダ」フォルダに制限します。

   ![](assets/mid_recette_user_restrictions.png)

1. 次のコマンドを使用して、Webモジュールを再起動します。 **nlserver web**.

ミッドソーシングサーバーの設定は、serverConf.xmlファイルで変更する必要があります。 既存の行の下の「IPアドレスを持つアフィニティの管理」セクションに次の行を追加する必要があります。

```
<IPAffinity IPMask="" localDomain="" name=""/>
```

&#39;@name&#39;属性は、次のルールを適用する必要があります。

**&#39;marketing_account_operator_name&#39;.&#39;アフィニティ名&#39;.&#39;アフィニティグループ&#39;**

&#39;marketing_account_operator_name&#39;は、ミッドソーシングインスタンスで宣言されたミッドソーシングアカウントの内部名に関連付けられます。

&#39;アフィニティ名&#39;は、アフィニティに与えられた任意の名前に関連します。 この名前は一意にする必要があります。 認証された文字は `[a-z]``[A-Z]``[0-9]`です。 目的は、パブリックIPアドレスのグループを宣言することです。

&#39;アフィニティグループ&#39;は、各配信で使用されるターゲットマッピングで宣言されたサブアフィニティを関連付けます。 「。」を含む最後の部分 は、下位アフィニティがない場合は無視されます。 認証された文字は `[a-z]``[A-Z]``[0-9]`です。

変更を考慮するには、サーバーを停止してから再起動する必要があります。

## ミッドソーシングサーバーでの追跡の設定 {#configuring-tracking-on-a-mid-sourcing-server}

**ミッドソーシングサーバーの設定**

1. 「operators」に移動し、演算子 **[!UICONTROL midを選択します]**。
1. 「 **[!UICONTROL フロントサーバー]** 」タブで、トラッキングサーバー接続パラメーターを入力します。

   トラッキングインスタンスを作成するには、トラッキングサーバーのURL、トラッキングサーバー内部アカウントのパスワード、インスタンスの名前、パスワード、およびそれに関連付けられたDNSマスクを入力します。

   ![](assets/s_ncs_install_midsourcing_tracking02.png)

1. 接続パラメーターを入力したら、「 **[!UICONTROL 設定を]**&#x200B;確認」をクリックします。
1. 必要に応じて、配信に含まれる画像を保存する場所を指定します。 これを行うには、ドロップダウンリストからいずれかのパブリケーションモードを選択します。

   ![](assets/s_ncs_install_midsourcing_tracking03.png)

   「 **[!UICONTROL トラッキングサーバ」オプションを選択すると]** 、画像がミッドソーシングサーバにコピーされます。

**顧客プラットフォームの設定**

1. 外部ミッドソーシングルーティングアカウントに移動します。
1. 「 **[!UICONTROL ミッドソーシング]** 」タブで、ミッドソーシングサーバーの接続パラメーターを指定します。

   ![](assets/s_ncs_install_midsourcing_tracking06.png)

1. 「接続を **[!UICONTROL テストする]**」をクリックして設定を確認します。
1. ミッドソーシングサーバーで参照されるトラッキングインスタンスを宣言します。

   Click the link **[!UICONTROL Use this platform as a proxy to access the tracking servers]**,

   トラッキングインスタンスの名前を指定し、トラッキングサーバーとの接続を確認します。

   ![](assets/s_ncs_install_midsourcing_tracking05.png)

メッセージの配信を複数のミッドソーシングサーバーで管理する場合は、ミッドソーシングアカウントが1つおきになるオプション **[!UICONTROL ルーティングを選択し]** 、別のサーバーを指定します。

![](assets/s_ncs_install_midsourcing_tracking04.png)

