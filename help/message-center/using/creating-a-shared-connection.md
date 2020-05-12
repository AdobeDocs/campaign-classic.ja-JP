---
title: 共有接続の作成
seo-title: 共有接続の作成
description: 共有接続の作成
seo-description: null
page-status-flag: never-activated
uuid: 30d6d23b-72c6-4454-8d6b-a10102f89262
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: instance-configuration
discoiquuid: 7f471ac1-cd6a-4371-977e-52d60ce8d968
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: f4ecdab4c17a6ba8deb3b98079f57bb7a9adf4a0
workflow-type: tm+mt
source-wordcount: '1051'
ht-degree: 100%

---


# 共有接続の作成{#creating-a-shared-connection}

>[!IMPORTANT]
>
>* コントロールインスタンスまたは実行インスタンスで [Message Center テクニカルワークフロー](../../message-center/using/technical-workflows.md)によって使用されるスキーマで作成されたスキーマ拡張は、Adobe Campaign トランザクションメッセージモジュールによって使用される別のインスタンスに複製する必要があります。
>* コントロールインスタンスおよび実行インスタンスは、異なるマシンにインストールする必要があります。同じ Campaign インスタンスを共有できなくなります。
>



## コントロールインスタンス {#control-instance}

分割アーキテクチャを使用している場合、コントロールインスタンスにリンクする実行インスタンスを指定し、両者を接続する必要があります。トランザクションメッセージテンプレートは実行インスタンスにデプロイされます。コントロールインスタンスと実行インスタンス間の接続は、**[!UICONTROL 実行インスタンス]**&#x200B;タイプの外部アカウントを設定することで作成します。外部アカウントは実行インスタンスの数だけ作成する必要があります。

>[!NOTE]
>
>実行インスタンスを複数のコントロールインスタンスで使用する場合、フォルダーおよびオペレーターごとにデータを分けることができます。詳しくは、[複数のコントロールインスタンスの使用](#using-several-control-instances)を参照してください。

実行インスタンスタイプの外部アカウントを作成するには、次の手順に従います。

1. **[!UICONTROL 管理／プラットフォーム／外部アカウント]**&#x200B;フォルダーに移動します。
1. Adobe Campaign にデフォルトで用意されている、実行インスタンスタイプの外部アカウントのうちの 1 つを選択し、右クリックして「**[!UICONTROL 複製]**」を選択します。

   ![](assets/messagecenter_create_extaccount_001.png)

1. 必要に応じて、ラベルを変更します。

   ![](assets/messagecenter_create_extaccount_002.png)

1. 「**[!UICONTROL 有効]**」オプションを選択し、外部アカウントを運用可能にします。

   ![](assets/messagecenter_create_extaccount_003.png)

1. 実行インスタンスがインストールされているサーバーのアドレスを指定します。

   ![](assets/messagecenter_create_extaccount_004.png)

1. アカウントにはオペレーターフォルダーで定義されている Message Center エージェントを指定します。デフォルトで Adobe Campaign に指定されているアカウントは **[!UICONTROL mc]** です。

   ![](assets/messagecenter_create_extaccount_005.png)

1. オペレーターフォルダーで定義されたアカウントのパスワードを入力します。

   >[!NOTE]
   >
   >インスタンスにログオンするたびにパスワードを入力しなくても済むように、実行インスタンス内でコントロールインスタンスの IP アドレスを指定することができます。詳しくは、[実行インスタンス](#execution-instance)を参照してください。

1. 実行インスタンスで使用する復元方法を指定します。

   復元するデータは、実行インスタンスによりコントロールインスタンスへと転送され、トランザクションメッセージとイベントアーカイブに追加されます。

   ![](assets/messagecenter_create_extaccount_007.png)

   データ収集は、HTTP/HTTPS アクセスを使用する Web サービス経由または Federated Data Access（FDA） モジュール経由のいずれかでおこなわれます。

   >[!NOTE]
   >
   >FDA over HTTP を使用する場合、Postgres データベースを使用する実行インスタンスのみがサポートされます。MSSQL または Oracle データベースはサポートされていません。

   コントロールインスタンスから実行インスタンスのデータベースへ直接接続できる場合には、後者の接続方法を推奨します。直接接続できない場合は、Web サービス経由の接続を選択します。FDA アカウントには、コントロールインスタンス上に作成した個々の実行インスタンスのデータベースに接続する場合と同じアカウントを指定します。

   ![](assets/messagecenter_create_extaccount_008.png)

   Federated Data Access（FDA） について詳しくは、[外部データベースへのアクセス](../../platform/using/about-fda.md)を参照してください。

1. 「**[!UICONTROL 接続をテスト]**」をクリックし、コントロールインスタンスと実行インスタンスがリンクされたことを確認します。

   ![](assets/messagecenter_create_extaccount_006.png)

1. 各実行インスタンスには識別子を関連付ける必要があります。各実行インスタンスへの識別子の割り当ては、デプロイウィザードを使用して手動でおこなうか（[実行インスタンスの識別](../../message-center/using/identifying-execution-instances.md)を参照してください）、コントロールインスタンスから「**接続を初期化**」ボタンをクリックして自動でおこなうことができます。

   ![](assets/messagecenter_create_extaccount_006bis.png)

## 実行インスタンス {#execution-instance}

パスワードの入力なしでコントロールインスタンスから実行インスタンスに接続できるようにするには、**Message Center** の「アクセス権」セクションでコントロールインスタンスの IP アドレスを入力します。ただし、デフォルトでは空のパスワードを使用することは禁止されています。

空のパスワードを使用するには、実行インスタンスに移動し、イベントを配信する情報システムの IP アドレスに限定したセキュリティゾーンを定義します。このセキュリティゾーンは、空のパスワードと `<identifier> / <password>` タイプの接続を許可している必要があります。詳しくは、[この節](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。

>[!NOTE]
>
>実行インスタンスを複数のコントロールインスタンスで使用する場合、フォルダーおよびオペレーターごとにデータを分けることができます。詳しくは、[複数のコントロールインスタンスの使用](#using-several-control-instances)を参照してください。

1. 実行インスタンスのオペレーターフォルダーに移動します（**[!UICONTROL 管理／アクセス管理／オペレーター]**）。
1. **Message Center** エージェントを選択します。

   ![](assets/messagecenter_operator_001.png)

1. 「**[!UICONTROL 編集]**」タブを選択し、「**[!UICONTROL アクセス権]**」をクリックし、「**[!UICONTROL アクセスパラメーターを編集...]**」リンクをクリックします。

   ![](assets/messagecenter_operator_002.png)

1. **[!UICONTROL アクセス設定]**&#x200B;ウィンドウで、「**[!UICONTROL 信頼済み IP マスクを追加]**」リンクをクリックし、コントロールインスタンスの IP アドレスを追加します。

   ![](assets/messagecenter_operator_003.png)

## 複数のコントロールインスタンスの使用 {#using-several-control-instances}

1 つの実行クラスターは複数のコントロールインスタンスで共有することができます。このタイプのアーキテクチャでは次の設定が必要です。

ここで、2 つのブランドを管理する会社の例を見てみましょう。ブランドにはそれぞれ専用のコントロールインスタンス、**コントロール 1** および&#x200B;**コントロール 2** を使用します。実行インスタンスも 2 つ使用します。それぞれのコントロールインスタンスには、異なる Message Center オペレーターを入力する必要があります。**コントロール 1** インスタンスには **mc1** オペレーター、**コントロール 2** インスタンスには **mc2** オペレーターを入力します。

すべての実行インスタンスのツリーにて、オペレーターにつきフォルダーを 1 つずつ作成し（**フォルダー 1** と&#x200B;**フォルダー 2**）、各オペレーターのフォルダーに対するお互いのデータアクセスを制限します。

### コントロールインスタンスの設定 {#configuring-control-instances}

1. **コントロール 1** コントロールインスタンス内では、各実行インスタンスにつき 1 つの外部アカウントを作成し、それぞれの外部アカウントに **mc1** オペレーターを入力します。その後は、すべての実行インスタンス上に **mc1** オペレーターが作成されるようになります（[実行インスタスの設定](#configuring-execution-instances)を参照してください）。

   ![](assets/messagecenter_multi_control_1.png)

1. **コントロール 2** コントロールインスタンス内では、各実行インスタンスにつき 2 つの外部アカウントを作成し、それぞれの外部アカウントに **mc2** オペレーターを入力します。その後は、すべての実行インスタンス上に **mc2** オペレーターが作成されるようになります（[実行インスタンスの設定](#configuring-execution-instances)を参照してください）。

   ![](assets/messagecenter_multi_control_2.png)

   >[!NOTE]
   >
   >コントロールインスタンスの設定について詳しくは、[コントロールインスタンス](#control-instance)を参照してください。

### 実行インスタンスの設定 {#configuring-execution-instances}

複数のコントロールインスタンスを使用するには、この設定をすべての実行インスタンスで実行する必要があります。

1. **[!UICONTROL 管理／プロダクション／Message Center]** ノードにて、各オペレーターにつき 1 つのフォルダーを作成します。ここでは、**フォルダー 1** および&#x200B;**フォルダー 2** とします。フォルダーやビューの作成について詳しくは、[プラットフォーム](../../platform/using/access-management.md#folders-and-views)を参照してください。

   ![](assets/messagecenter_multi_control_3.png)

1. デフォルトで用意されている Message Center のオペレーター（**mc**）を複製して、**mc1** と **mc2** オペレーターを作成します。オペレーターの作成について詳しくは、[この節](../../platform/using/access-management.md#operators)を参照してください。

   ![](assets/messagecenter_multi_control_4.png)

   >[!NOTE]
   >
   >**mc1** と **mc2** オペレーターには、**[!UICONTROL Message Center の実行]**&#x200B;権限を与える必要があり、Adobe Campaign クライアントコンソールへのアクセス権は与えてはなりません。オペレーターは、必ずセキュリティゾーンにリンクされていなければなりません。詳しくは、[この節](../../installation/using/configuring-campaign-server.md#defining-security-zones)を参照してください。

1. 各オペレーターで、「**[!UICONTROL 次のサブフォルダー内の情報に制限]**」ボックスをオンにし、該当フォルダー（**mc1** オペレーターは&#x200B;**フォルダー 1**、**mc2** オペレーターは&#x200B;**フォルダー 2**）を選択します。

   ![](assets/messagecenter_multi_control_5.png)

1. 各オペレーターには、各自のフォルダーへの読み取り／書き込みの権限を与えます。これをおこなうには、フォルダーを右クリックして「**[!UICONTROL プロパティ]**」を選択します。次に「**[!UICONTROL セキュリティ]**」タブを選択し、該当オペレーター（**フォルダー 1** では **mc1**、**フォルダー 2** では **mc2**）を追加します。**[!UICONTROL 「データを読み取る」／「データを書き込み」]**&#x200B;ボックスの両方が選択されていることを確認します。

   ![](assets/messagecenter_multi_control_6.png)

