---
product: campaign
title: Campaign でのミッドソーシングサーバーのインストール
description: この節では、Campaign でのミッドソーシングサーバーのインストールと設定について説明します
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 3e55d7f5-2858-4390-bba9-8fb5be0c3d98
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 1%

---

# ミッドソーシングサーバー{#mid-sourcing-server}

![](../../assets/v7-only.svg)

この節では、ミッドソーシングサーバーのインストールと設定、およびサードパーティが **ミッドソーシング** モードでメッセージを送信できるようにするインスタンスのデプロイメントについて説明します。

「ミッドソーシング」アーキテクチャは、[ ミッドソーシングデプロイメント ](../../installation/using/mid-sourcing-deployment.md) で説明しています。

ミッドソーシングサーバーのインストール手順は、通常の方法でサーバーをインストールする場合と同じです（標準設定を参照）。 独自のデータベースを持つ独立したインスタンスで、配信の実行に使用できます。 簡単に言えば、ミッドソーシングモードでリモートインスタンスを通じて配信を実行できるようにする追加の設定が含まれています。

>[!CAUTION]
>
>ミッドソーシングサーバーが設定され、[ 同期ワークフロー ](../../workflow/using/about-technical-workflows.md) が初めて実行されたら、必ずミッドソーシング外部アカウントの内部名を更新しないでください。

## インスタンスのインストールと設定の手順 {#steps-for-installing-and-configuring-an-instance}

### インスタンスのインストールと設定の前提条件 {#prerequisites-for-installing-and-configuring-an-instance}

* アプリケーションサーバーの JDK。
* アプリケーションサーバー上のデータベースサーバーにアクセスする。
* ミッドソーシングサーバーに対して HTTP(80) または HTTPS(443) ポートを開くように設定されたファイアウォール。

以下の手順では、単一のミッドソーシングサーバーを使用した設定について詳しく説明します。 複数のサーバーを使用することもできます。 同様に、内部設定から特定のメッセージ（例えば、ワークフロー通知）を送信することもできます。

### ミッドソーシングデプロイメント用のアプリケーションサーバーのインストールと設定 {#installing-and-configuring-the-application-server-for-mid-sourcing-deployment}

インストール手順は、スタンドアロンインスタンスの手順と同じです。 [ インストールと設定（シングルマシン）](../../installation/using/standalone-deployment.md#installing-and-configuring--single-machine-) を参照してください。

ただし、次の条件を満たす必要があります。

* 手順 **5** で、**mta** （配信）および **inMail** （バウンスメール）モジュールを無効にする必要があります。 ただし、**wfserver** （ワークフロー）モジュールはアクティブのままにする必要があります。

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

* 手順 **6**、**9**、**10** は不要です。
* 手順 **12** と **13** の間に、接続 URL の 8080 ポートを示す必要があります（コンソールは Web サーバーを介せずに Tomcat と直接通信するため）。 URL は [http://console.campaign.net:8080](http://console.campaign.net) になります。 手順 **13** の間に、**[!UICONTROL Issue to Mid-sourcing]** パッケージおよびインストールするパッケージを選択します。

   ![](assets/s_ncs_install_midsourcing02.png)

   >[!CAUTION]
   >
   >技術的な配信のデフォルトのルーティングは、ミッドソーシング経由の E メールルーティングに自動的に置き換えられます。

### ミッドソーシングサーバーのインストールと設定 {#installing-and-configuring-the-mid-sourcing-server}

クライアントコンソールで、ミッドソーシング **ミッドソーシングアカウント（**/Administration/External accounts/**フォルダー内）を使用した** E メールルーティングを探します。 サーバー **、** アカウント **、** パスワード **、** ミラーページの URL **の URL に、ミッドソーシングサーバーをホストするサーバープロバイダーから提供された情報を入力します。**&#x200B;接続をテストします。

>[!NOTE]
>
>**mid-sourcingEmitter** オプションは、2 つの **ミッドソーシング** ワークフローを作成します。 これは、デフォルトで 1 時間 20 分おきに実行され、ミッドソーシングサーバー上の配信情報を収集するプロセスです。

## ミッドソーシングサーバーのデプロイ {#deploying-a-mid-sourcing-server}

1. アプリケーションサーバーのインストール：

   >[!CAUTION]
   >
   >ミッドソーシングサーバーをインストールし、追加のAdobe Campaignモジュールをインストールする場合は、Campaign モジュールではなく、配信モジュールを使用することをお勧めします。

   標準のデプロイメントと同じ手順に従い、「**[!UICONTROL ミッドソーシングプラットフォーム]**」オプションのみを選択します。

   ![](assets/s_ncs_install_midsourcing01.png)

1. ミッドソーシングモードでの受信の設定

   送信アカウントのパスワードを設定します。**/Mid-sourcing/Access Management/Operators/** フォルダーでは、**mid** 演算子が、ミッドソーシングモードでの送信にリモートインスタンスで使用されます。 このオペレーターのパスワードを設定し、送信インスタンスの管理者に渡す必要があります。

   「**ミッドソーシングプラットフォーム**」オプションは、送信された配信と送信を実行するデフォルトのオペレーターを保存するためのデフォルトのフォルダーを作成します。

## ミッドソーシングサーバーの多重化 {#multiplexing-the-mid-sourcing-server}

>[!CAUTION]
>
>多重化は、オンプレミス環境でのみサポートされます。

ミッドソーシングインスタンスを複数の送信インスタンスで共有できます。 これらの各インスタンスは、ミッドソーシングデータベースの演算子と関連付ける必要があります。 ミッドソーシングサーバーで 2 番目のアカウントを作成するには：

1. **[!UICONTROL ミッドソーシング/配信]** ノードに、デフォルトのミッドソーシングアカウントに関連付けるフォルダーを作成します ( 例：prod) を使用します。
1. **[!UICONTROL ミッドソーシング/配信]** ノードに、アカウントと同じ名前のフォルダーを作成します ( 例：accepting_test) を返します。

   ![](assets/mid_recette_account.png)

1. **[!UICONTROL ミッドソーシング/アクセス管理/オペレーター]** で、新しいアカウントを作成します。

   ![](assets/mid_recette_user_create.png)

1. 「**[!UICONTROL アクセス権]**」タブで、このオペレーターに「**ミッドソーシング送信**」グループの権限を付与します。 このアクセス権は、**[!UICONTROL ミッドソーシング/アクセス管理/オペレーターグループ]** で使用できます。

   ![](assets/mid_recette_user_rights.png)

1. 「**** のサブフォルダー内のデータに制限」オプションを選択し、配信フォルダーを選択して、このオペレーターをミッドソーシング配信フォルダーに制限します。

   ![](assets/mid_recette_user_restrictions.png)

1. 次のコマンドを使用して、Web モジュールを再起動します。**nlserver web** を再起動します。

serverConf.xml ファイルのミッドソーシングサーバーの設定を変更する必要があります。 既存の行の下の「IP アドレスを使用したアフィニティの管理」セクションに、次の行を追加する必要があります。

```
<IPAffinity IPMask="" localDomain="" name=""/>
```

「@name」属性は、次のルールに従う必要があります。

**&#39;marketing_account_operator_name&#39;.&#39;affinity_name&#39;.&#39;affinity_group&#39;**

「marketing_account_operator_name」は、ミッドソーシングインスタンスで宣言されたミッドソーシングアカウントの内部名に関連します。

&#39;affinity_name&#39;は、アフィニティに与えられた任意の名前に関連します。 この名前は一意である必要があります。 許可されている文字は `[a-z]``[A-Z]``[0-9]` です。 目的は、パブリック IP アドレスのグループを宣言することです。

「affinity_group」は、各配信で使用されるターゲットマッピングで宣言されたサブアフィニティを関連付けます。 「。」を含む最後の部分 サブアフィニティがない場合は無視されます。 許可されている文字は `[a-z]``[A-Z]``[0-9]` です。

変更を反映するには、サーバーを停止してから再起動する必要があります。

## ミッドソーシングサーバーでのトラッキングの設定 {#configuring-tracking-on-a-mid-sourcing-server}

**ミッドソーシングサーバーの設定**

1. 「operators」に移動し、演算子 **[!UICONTROL mid]** を選択します。
1. 「**[!UICONTROL Frontal servers]**」タブで、トラッキングサーバーの接続パラメーターを入力します。

   トラッキングインスタンスを作成するには、トラッキングサーバーの URL、トラッキングサーバーの内部アカウントのパスワード、インスタンスの名前、パスワード、およびそれに関連付けられた DNS マスクを入力します。

   ![](assets/s_ncs_install_midsourcing_tracking02.png)

1. 接続パラメーターを入力したら、「**[!UICONTROL 設定を確認]**」をクリックします。
1. 必要に応じて、配信に含まれる画像の保存場所を指定します。 それには、ドロップダウンリストからパブリッシュモードの 1 つを選択します。

   ![](assets/s_ncs_install_midsourcing_tracking03.png)

   「**[!UICONTROL トラッキングサーバー]**」オプションを選択した場合、画像はミッドソーシングサーバーにコピーされます。

**顧客プラットフォームの設定**

1. 外部ミッドソーシングルーティングアカウントに移動します。
1. 「**[!UICONTROL ミッドソーシング]**」タブで、ミッドソーシングサーバー接続のパラメーターを指定します。

   ![](assets/s_ncs_install_midsourcing_tracking06.png)

1. 「**[!UICONTROL 接続をテスト]**」をクリックして設定を確認します。
1. ミッドソーシングサーバーで参照されるトラッキングインスタンスを宣言します。

   リンク **[!UICONTROL Use this platform as a proxy をクリックして、トラッキングサーバー]** にアクセスします。

   トラッキングインスタンスの名前を指定し、トラッキングサーバーとの接続を確認します。

   ![](assets/s_ncs_install_midsourcing_tracking05.png)

メッセージの配信を複数のミッドソーシングサーバーで管理する場合は、「**[!UICONTROL Routing with alternating mid-sourcing accounts]**」オプションを選択し、異なるサーバーを指定します。

![](assets/s_ncs_install_midsourcing_tracking04.png)
