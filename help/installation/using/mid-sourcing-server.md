---
product: campaign
title: Campaign へのミッドソーシングサーバーのインストール
description: この節では、Campaign でのミッドソーシングサーバーのインストールと設定について詳しく説明します
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 3e55d7f5-2858-4390-bba9-8fb5be0c3d98
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 3%

---

# ミッドソーシングサーバー{#mid-sourcing-server}



この節では、ミッドソーシングサーバーのインストールと設定、およびサードパーティがメッセージを送信できるインスタンスのデプロイメントについて詳しく説明します **ミッドソーシング** モード。

「ミッドソーシング」アーキテクチャについては、次を参照してください。 [ミッドソーシングデプロイメント](../../installation/using/mid-sourcing-deployment.md).

ミッドソーシングサーバーのインストールは、通常の方法でサーバーをインストールする場合と同じプロセスに従います（標準設定を参照）。 これは、配信の実行に使用できる独自のデータベースを持つ独立したインスタンスです。 簡単に言えば、リモートインスタンスがミッドソーシングモードで配信を実行できるようにするための追加の設定が含まれています。

>[!CAUTION]
>
>ミッドソーシングサーバーをセットアップして、 [ワークフローを同期](../../workflow/using/about-technical-workflows.md) を初めて実行する場合は、ミッドソーシング外部アカウントの内部名を更新しないでください。

## インスタンスのインストールおよび設定手順 {#steps-for-installing-and-configuring-an-instance}

### インスタンスのインストールと設定の前提条件 {#prerequisites-for-installing-and-configuring-an-instance}

* アプリケーションサーバー上の JDK
* アプリケーションサーバー上のデータベースサーバーにアクセスします。
* ミッドソーシングサーバーへの HTTP （80）または HTTPS （443）ポートを開くように設定されたファイアウォール。

次の手順は、単一のミッドソーシングサーバーを使用した設定の詳細を示しています。 複数のサーバーを使用することもできます。 同様に、内部設定から特定のメッセージ（ワークフロー通知など）を送信することもできます。

### ミッドソーシングデプロイメント用のアプリケーションサーバーのインストールと設定 {#installing-and-configuring-the-application-server-for-mid-sourcing-deployment}

インストール手順は、スタンドアロンインスタンスの場合と同じです。 こちらを参照してください [インストールと設定（単一マシン）](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-).

ただし、次の点を適用する必要があります。

* ステップ時 **5**&#x200B;を無効にする必要があります **mta** （配信）と **inMail** （バウンスメール）モジュール この **wfserver** （ワークフロー）モジュールは、アクティブな状態を維持する必要があります。

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

  詳しくは、[この節](../../installation/using/configuring-campaign-server.md#enabling-processes)を参照してください。

* 手順 **6**, **9** および **10** 必要ありません。
* 手順の実行中 **12** および **13**（コンソールは Web サーバー経由ではなく Tomcat と直接通信するので）接続 URL に 8080 ポートを示す必要があります。 URL はになります `http://console.campaign.net:8080`. ステップ中 **13**&#x200B;を選択し、 **[!UICONTROL ミッドソーシングに関する問題]** パッケージと、インストールするパッケージ。

  ![](assets/s_ncs_install_midsourcing02.png)

  >[!CAUTION]
  >
  >技術配信のデフォルトのルーティングは、ミッドソーシング経由の電子メールルーティングに自動的に置き換えられます。

### ミッドソーシングサーバーのインストールと設定 {#installing-and-configuring-the-mid-sourcing-server}

クライアントコンソールから、を見つけます。 **ミッドソーシングを使用したメールルーティング** ミッドソーシングアカウント（ **/Administration/External accounts/** フォルダー）に保存します。 を入力 **サーバーの URL**, **アカウント**, **password** および **ミラーページ URL** ミッドソーシングサーバーをホストするサーバープロバイダーから提供される情報を使用した設定。 接続をテストします。

>[!NOTE]
>
>この **ミッドソーシングエミッタ** オプションが 2 つ作成します **ミッドソーシング** ワークフロー。 これは、デフォルトで 1 時間 20 分ごとに実行されるプロセスで、ミッドソーシングサーバーの配信情報を収集します。

## ミッドソーシングサーバーのデプロイ {#deploying-a-mid-sourcing-server}

1. アプリケーションサーバーのインストール：

   >[!CAUTION]
   >
   >ミッドソーシングサーバーをインストールし、追加のAdobe Campaign モジュールをインストールする場合は、Campaign モジュールではなく、配信モジュールを使用することをお勧めします。

   標準デプロイメントの場合と同じ手順に従い、を選択するだけです **[!UICONTROL ミッドソーシングプラットフォーム]** オプション。

   ![](assets/s_ncs_install_midsourcing01.png)

1. ミッドソーシングモードで受信するための設定

   送信アカウントのパスワードを次のように設定します。 **/ミッドソーシング/アクセス管理/オペレーター/** フォルダー、 **mid** 演算子は、リモートインスタンスでミッドソーシングモードでの送信に使用されます。 このオペレーターのパスワードを設定し、送信インスタンスの管理者に渡す必要があります。

   この **ミッドソーシングプラットフォーム** このオプションは、送信された配信を保存するデフォルトのフォルダーと、送信を実行するデフォルトのオペレーターを作成します。

## ミッドソーシングサーバーの多重化 {#multiplexing-the-mid-sourcing-server}

>[!CAUTION]
>
>多重化は、オンプレミス環境でのみサポートされます。

ミッドソーシングインスタンスを複数の送信インスタンスで共有できます。 これらの各インスタンスは、ミッドソーシングデータベースのオペレーターに関連付ける必要があります。 中間ソーシングサーバーに 2 つ目のアカウントを作成するには、次の手順を実行します。

1. にフォルダーを作成します。 **[!UICONTROL ミッドソーシング /配信]** デフォルトの中間ソーシングアカウントに関連付けられるノード （例：prod）。
1. にフォルダーを作成します。 **[!UICONTROL ミッドソーシング /配信]** アカウントと同じ名前のノード（例：acceptance_test）。

   ![](assets/mid_recette_account.png)

1. 対象： **[!UICONTROL ミッドソーシング/アクセス管理/オペレーター]**&#x200B;新しいアカウントを作成します。

   ![](assets/mid_recette_user_create.png)

1. が含まれる **[!UICONTROL アクセス権]** タブで、このオペレーターにの権限を付与します **ミッドソーシング送信** グループ。 このアクセス権限は、次の場所で使用できます **[!UICONTROL ミッドソーシング/ アクセス管理/ オペレーターグループ]**.

   ![](assets/mid_recette_user_rights.png)

1. 「」を選択します **[!UICONTROL のサブフォルダー内のデータに制限]** 「」オプションと「配信」フォルダーを選択して、このオペレーターをミッドソーシング配信フォルダーに制限します。

   ![](assets/mid_recette_user_restrictions.png)

1. 次のコマンドを使用して、Web モジュールを再起動します。 **nlserver restart web**.

serverConf.xml ファイルのミッドソーシングサーバー設定を変更する必要があります。 次の行を「IP アドレスとの親和性の管理」セクションの既存の行の下に追加する必要があります。

```
<IPAffinity IPMask="" localDomain="" name=""/>
```

&#39;@name&#39;属性は次の規則に従う必要があります：

**&#39;marketing_account_operator_name&#39;.&#39;affinity_name&#39;.&#39;affinity_group&#39;**

「marketing_account_operator_name」は、ミッドソーシングインスタンスで宣言されたミッドソーシングアカウントの内部名に関連します。

「affinity_name」は、アフィニティに付与される任意の名前に関連します。 この名前は一意である必要があります。 許可される文字は次のとおりです `[a-z]``[A-Z]``[0-9]`. 目的は、パブリック IP アドレスのグループを宣言することです。

「affinity_group」は、各配信で使用されるターゲットマッピングで宣言されたサブアフィニティを関連付けます。 「。」を含む最後の部分 サブアフィニティがない場合、は無視されます。 許可される文字は次のとおりです `[a-z]``[A-Z]``[0-9]`.

変更を反映させるには、サーバーを停止し、再起動する必要があります。

## ミッドソーシングサーバーでのトラッキングの設定 {#configuring-tracking-on-a-mid-sourcing-server}

**ミッドソーシングサーバーの設定**

1. 「演算子」に移動し、演算子を選択します **[!UICONTROL mid]**.
1. が含まれる **[!UICONTROL フロントサーバー]** タブで、トラッキングサーバー接続パラメーターを入力します。

   トラッキングインスタンスを作成するには、トラッキングサーバーの URL、トラッキングサーバーの内部アカウントのパスワード、インスタンス名、そのパスワード、関連付けられた DNS マスクを入力します。

   ![](assets/s_ncs_install_midsourcing_tracking02.png)

1. 接続パラメーターを入力したら、 **[!UICONTROL 設定を確認します]**.
1. 必要に応じて、配信に含まれる画像の保存場所を指定します。 そのためには、ドロップダウンリストからいずれかの公開モードを選択します。

   ![](assets/s_ncs_install_midsourcing_tracking03.png)

   を選択した場合 **[!UICONTROL トラッキングサーバー]** オプションを選択した場合、画像はミッドソーシングサーバーにコピーされます。

**顧客プラットフォームの設定**

1. 外部ミッドソーシングルーティングアカウントに移動します。
1. 「**[!UICONTROL ミッドソーシング]**」タブで、ミッドソーシングサーバーの接続パラメーターを指定します。

   ![](assets/s_ncs_install_midsourcing_tracking06.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックして設定を確認します。
1. ミッドソーシングサーバーで参照されるトラッキングインスタンスを宣言：

   リンクをクリック **[!UICONTROL このプラットフォームをトラッキングサーバーにアクセスするためのプロキシとして使用]**,

   トラッキングインスタンスの名前を指定し、トラッキングサーバーとの接続を確認してください。

   ![](assets/s_ncs_install_midsourcing_tracking05.png)

メッセージの配信を複数のミッドソーシングサーバーで管理する場合は、このオプションを選択します **[!UICONTROL 代替ミッドソーシングアカウントによるルーティング]** そして、異なるサーバーを指定します。

![](assets/s_ncs_install_midsourcing_tracking04.png)
