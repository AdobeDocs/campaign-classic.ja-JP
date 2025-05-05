---
product: campaign
title: Campaign へのミッドソーシングサーバーのインストール
description: この節では、Campaign でのミッドソーシングサーバーのインストールと設定について詳しく説明します
feature: Installation, Instance Settings
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 3e55d7f5-2858-4390-bba9-8fb5be0c3d98
source-git-commit: b500b2cbf68fd46bd84ddbfa71cf9431c6b60060
workflow-type: tm+mt
source-wordcount: '1061'
ht-degree: 3%

---

# ミッドソーシングサーバー{#mid-sourcing-server}



この節では、ミッドソーシングサーバーのインストールと設定、およびサードパーティがメッセージを **ミッドソーシング** モードで送信できるインスタンスのデプロイメントについて詳しく説明します。

「ミッドソーシング」アーキテクチャについては、[ ミッドソーシングデプロイメント ](../../installation/using/mid-sourcing-deployment.md) を参照してください。

ミッドソーシングサーバーのインストールは、通常の方法でサーバーをインストールする場合と同じプロセスに従います（標準設定を参照）。 これは、配信の実行に使用できる独自のデータベースを持つ独立したインスタンスです。 簡単に言えば、リモートインスタンスがミッドソーシングモードで配信を実行できるようにするための追加の設定が含まれています。

>[!CAUTION]
>
>ミッドソーシングサーバーをセットアップし、[ 同期ワークフロー ](../../workflow/using/about-technical-workflows.md) を初めて実行したら、ミッドソーシング外部アカウントの内部名を更新しないでください。

## インスタンスのインストールおよび設定手順 {#steps-for-installing-and-configuring-an-instance}

### インスタンスのインストールと設定の前提条件 {#prerequisites-for-installing-and-configuring-an-instance}

* アプリケーションサーバー上の JDK
* アプリケーションサーバー上のデータベースサーバーにアクセスします。
* ミッドソーシングサーバーへの HTTP （80）または HTTPS （443）ポートを開くように設定されたファイアウォール。

次の手順は、単一のミッドソーシングサーバーを使用した設定の詳細を示しています。 複数のサーバーを使用することもできます。 同様に、内部設定から特定のメッセージ（ワークフロー通知など）を送信することもできます。

### ミッドソーシングデプロイメント用のアプリケーションサーバーのインストールと設定 {#installing-and-configuring-the-application-server-for-mid-sourcing-deployment}

インストール手順は、スタンドアロンインスタンスの場合と同じです。 [ インストールと設定（単一マシン） ](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-) を参照してください。

ただし、次の点を適用する必要があります。

* 手順 **5** では、**mta** （配信）および **inMail** （バウンスメール）モジュールを無効にする必要があります。 ただし、**wfserver** （ワークフロー）モジュールはアクティブ状態を維持する必要があります。

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

* 手順 **6**、**9** および **10** は必要ありません。
* 手順 **12** および **13** で、接続 URL に 8080 ポートを指定する必要があります（コンソールは、web サーバーを介さずに Tomcat と直接通信するので）。 URL が `http://console.campaign.net:8080` になります。 手順 **13** で、**[!UICONTROL ミッドソーシングの問題]** パッケージとインストールするパッケージを選択します。

  ![](assets/s_ncs_install_midsourcing02.png)

  >[!CAUTION]
  >
  >技術配信のデフォルトのルーティングは、ミッドソーシング経由の電子メールルーティングに自動的に置き換えられます。

### ミッドソーシングサーバーのインストールと設定 {#installing-and-configuring-the-mid-sourcing-server}

クライアントコンソールから、（**/Administration/External accounts/** フォルダーにある **ミッドソーシングを使用したメールのルーティング** ミッドソーシングアカウントを見つけます。 **サーバーの URL**、**アカウント**、**パスワード** および **ミラーページ URL** 設定に、ミッドソーシングサーバーをホストするサーバープロバイダーから提供された情報を入力します。 接続をテストします。

>[!NOTE]
>
>**ミッドソーシングエミッタ** オプションは、2 つの **ミッドソーシング** ワークフローを作成します。 これは、デフォルトで 1 時間 20 分ごとに実行されるプロセスで、ミッドソーシングサーバーの配信情報を収集します。

## ミッドソーシングサーバーのデプロイ {#deploying-a-mid-sourcing-server}

1. アプリケーションサーバーのインストール：

   >[!CAUTION]
   >
   >ミッドソーシングサーバーをインストールし、追加のAdobe Campaign モジュールをインストールする場合は、Campaign モジュールではなく、配信モジュールを使用することをお勧めします。

   標準デプロイメントの場合と同じ手順に従い、「**[!UICONTROL ミッドソーシングプラットフォーム]**」オプションのみを選択します。

   ![](assets/s_ncs_install_midsourcing01.png)

1. ミッドソーシングモードで受信するための設定

   送信アカウントのパスワードを設定します。**/Mid ソーシング/アクセス管理/オペレーター/** フォルダーでは、**mid** オペレーターがリモートインスタンスによってミッドソーシングモードでの送信用に使用されます。 このオペレーターのパスワードを設定し、送信インスタンスの管理者に渡す必要があります。

   「**ミッドソーシングプラットフォーム**」オプションでは、送信された配信を保存するデフォルトのフォルダーと、送信を実行するデフォルトのオペレーターを作成します。

## ミッドソーシングサーバーの多重化 {#multiplexing-the-mid-sourcing-server}

>[!CAUTION]
>
>多重化は、オンプレミス環境でのみサポートされます。

ミッドソーシングインスタンスを複数の送信インスタンスで共有できます。 これらの各インスタンスは、ミッドソーシングデータベースのオペレーターに関連付ける必要があります。 中間ソーシングサーバーに 2 つ目のアカウントを作成するには、次の手順を実行します。

1. デフォルトのミッドソーシングアカウントに関連付けられるフォルダーを **[!UICONTROL ミッドソーシング/配信]** ノードに作成します（例：prod）。
1. **[!UICONTROL ミッドソーシング/配信]** ノードに、アカウントと同じ名前（例：acceptance_test）のフォルダーを作成します。

   ![](assets/mid_recette_account.png)

1. **[!UICONTROL ミッドソーシング/アクセス管理/オペレーター]** で、新しいアカウントを作成します。

   ![](assets/mid_recette_user_create.png)

1. 「**[!UICONTROL アクセス権]**」タブで、このオペレーターに **ミッドソーシング送信** グループの権限を付与します。 このアクセス権限は、**[!UICONTROL ミッドソーシング/アクセス管理/オペレーターグループ]** で使用できます。

   ![](assets/mid_recette_user_rights.png)

1. 「**[!UICONTROL 次のサブフォルダーのデータに制限]**」オプションを選択し、配信フォルダーを選択して、このオペレーターをミッドソーシング配信フォルダーに制限します。

   ![](assets/mid_recette_user_restrictions.png)

1. 次のコマンドを使用して Web モジュールを再起動します：**&#x200B; web**。

serverConf.xml ファイルのミッドソーシングサーバー設定を変更する必要があります。 次の行を「IP アドレスとの親和性の管理」セクションの既存の行の下に追加する必要があります。

```
<IPAffinity IPMask="" localDomain="" name=""/>
```

&#39;@name&#39;属性は次の規則に従う必要があります：

**&#39;marketing_account_operator_name&#39;.&#39;affinity_name&#39;.&#39;affinity_group&#39;**

「marketing_account_operator_name」は、ミッドソーシングインスタンスで宣言されたミッドソーシングアカウントの内部名に関連します。

「affinity_name」は、アフィニティに付与される任意の名前に関連します。 この名前は一意である必要があります。 許可されている文字は `[a-z]` `[A-Z]` `[0-9]` です。 目的は、パブリック IP アドレスのグループを宣言することです。

「affinity_group」は、各配信で使用されるターゲットマッピングで宣言されたサブアフィニティを関連付けます。 「。」を含む最後の部分 サブアフィニティがない場合、は無視されます。 許可されている文字は `[a-z]` `[A-Z]` `[0-9]` です。

変更を反映させるには、サーバーを停止し、再起動する必要があります。

## ミッドソーシングサーバーでのトラッキングの設定 {#configuring-tracking-on-a-mid-sourcing-server}

**ミッドソーシングサーバーの設定**

1. 「演算子」に移動し、演算子 **[!UICONTROL mid]** を選択します。
1. 「**[!UICONTROL フロントサーバー]**」タブで、トラッキングサーバー接続パラメーターを入力します。

   トラッキングインスタンスを作成するには、トラッキングサーバーの URL、トラッキングサーバーの内部アカウントのパスワード、インスタンス名、そのパスワード、関連付けられた DNS マスクを入力します。

   ![](assets/s_ncs_install_midsourcing_tracking02.png)

1. 接続パラメーターを入力したら、「**[!UICONTROL 設定を確認]**」をクリックします。
1. 必要に応じて、配信に含まれる画像の保存場所を指定します。 そのためには、ドロップダウンリストからいずれかの公開モードを選択します。

   ![](assets/s_ncs_install_midsourcing_tracking03.png)

   「**[!UICONTROL トラッキングサーバー]**」オプションを選択すると、画像は中間ソーシングサーバーにコピーされます。

**顧客プラットフォームの設定**

1. 外部ミッドソーシングルーティングアカウントに移動します。
1. 「**[!UICONTROL ミッドソーシング]**」タブで、ミッドソーシングサーバーの接続パラメーターを指定します。

   ![](assets/s_ncs_install_midsourcing_tracking06.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックして設定を確認します。
1. ミッドソーシングサーバーで参照されるトラッキングインスタンスを宣言：

   **[!UICONTROL このプラットフォームをトラッキングサーバーにアクセスするためのプロキシとして使用]** リンクをクリックします。

   トラッキングインスタンスの名前を指定し、トラッキングサーバーとの接続を確認してください。

   ![](assets/s_ncs_install_midsourcing_tracking05.png)

メッセージの配信を複数のミッドソーシングサーバーで管理する場合は、「**[!UICONTROL 代替のミッドソーシングアカウントを使用したルーティング]** オプションを選択し、異なるサーバーを指定します。

![](assets/s_ncs_install_midsourcing_tracking04.png)
