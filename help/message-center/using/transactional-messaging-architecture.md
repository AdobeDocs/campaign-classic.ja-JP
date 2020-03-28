---
title: Adobe Campaign Classic トランザクションメッセージのアーキテクチャ
description: ここでは、Adobe Campaign Classic トランザクションメッセージのアーキテクチャについて説明します。
page-status-flag: never-activated
uuid: a8fe7a37-6df7-49f4-838f-97a72e4a38f3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: introduction
discoiquuid: a910d5fe-cef4-47d8-b3bc-0055ef0d1afd
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 25ae29490f8b4c58dad499669f5bccff43de8b7a

---


# トランザクションメッセージのアーキテクチャ{#transactional-messaging-architecture}

## 実行およびコントロールインスタンスについて {#about-execution-and-control-instances}

Adobe Campaign のトランザクションメッセージ機能（Message Center とも呼ばれます）は、スケーラビリティをサポートし、365 日 24 時間サービスを提供するように設計されています。Message Center は、以下のいくつかのインスタンスで構成されています。

* 1 つのコントロールインスタンス：メッセージテンプレートを作成します。
* 1 つまたは複数の実行インスタンス：イベントを受け取り、メッセージを配信します。

これらの機能を使用するために、Adobe Campaign のユーザーはコントロールインスタンスにログオンし、トランザクションメッセージテンプレートの作成、シードリストを使用したメッセージプレビューの生成、レポートの表示、実行インスタンスの監視をおこないます。

実行インスタンスは、イベントを受け取り、イベントをトランザクションメッセージテンプレートにリンクし、パーソナライズしたメッセージをそれぞれの受信者に送信します。

![](assets/messagecenter_diagram.png)

## 複数のコントロールインスタンスのサポート {#supporting-several-control-instances}

>[!CAUTION]
>
>複数のコントロールインスタンスでの実行クラスターの共有は、オンプレミス環境でのみサポートされます。

1 つの実行クラスターを複数のコントロールインスタンスで共有することができます。例えば、複数の専門店舗を管理している場合、ブランドごとにそれぞれ 1 つずつコントロールセンターを設定し、すべてのコントロールセンターを同じ実行クラスターにリンクすることができます。

![](assets/messagecenter_diagram_2.png)

>[!NOTE]
>
>必要な設定について詳しくは、[複数のコントロールインスタンスの使用](../../message-center/using/creating-a-shared-connection.md#using-several-control-instances)を参照してください。

## インスタンスのインストール {#installing-instances}

トランザクションメッセージパッケージをインストールする際の注意事項がいくつかあります。本番環境で使用する前に、テスト環境で動作させることをお勧めします。また、互換性のある Adobe Campaign のライセンスが必要です。詳しくは、アドビのアカウント担当者にお問い合わせください。

>[!CAUTION]
>
>コントロールインスタンスおよび実行インスタンスは、異なるマシンにインストールする必要があります。同じ Campaign インスタンスを共有できなくなります。

複数のチャネルを使用する場合は、トランザクションメッセージパッケージをインストールする前に関連パッケージをインストールして設定する必要があります。[配信チャネルの追加](#adding-a-delivery-channel)を参照してください。

* コントロールインスタンスをインストールするには、「**[!UICONTROL トランザクションメッセージコントロール]**」モジュールを選択します。

   ![](assets/messagecenter_install_controlinstance_001.png)

* 実行インスタンスをインストールするには、「**[!UICONTROL トランザクションメッセージ実行]**」モジュールを選択します。

   ![](assets/messagecenter_install_executioninstance_001.png)

## 配信チャネルの追加 {#adding-a-delivery-channel}

配信チャネル（モバイルチャネル、モバイルアプリチャネルなど）の追加は、トランザクションメッセージパッケージのインストール前におこなう必要があります。E メールチャネルのトランザクションメッセージプロジェクトを開始し、プロジェクトの最中に新規でチャネルを追加することにした場合は、次の手順に従います。

1. パッケージインポートウィザードを使用し、追加したいチャネル、例えば&#x200B;**モバイルチャネル**&#x200B;をインストールします（**[!UICONTROL ツール／詳細設定／パッケージをインポート／Adobe Campaign パッケージ]**）。
1. ファイルをインポートし（**[!UICONTROL ツール／詳細設定／パッケージをインポート／ファイル]**）、**datakitnms **`[Your language]`**packagemessageCenter.xml** ファイルを選択します。
1. 「**[!UICONTROL インポートするデータの XML コンテンツ]**」には、追加したチャネルに対応する配信テンプレートのみを残します。例えば、**モバイルチャネル**&#x200B;を追加した場合には、**[!UICONTROL モバイルトランザクションメッセージ]**（smsTriggerMessage）に対応する **entities** 要素のみを残します。**モバイルアプリチャネル**&#x200B;を追加した場合は、**iOS トランザクションメッセージ**（iosTriggerMessage）と **Android トランザクションメッセージ**（androidTriggerMessage）のみを残します。

   ![](assets/messagecenter_install_channel.png)

## トランザクションメッセージおよびインバウンドインタラクション {#transactional-messages-and-inbound-interaction}

トランザクションメッセージでは、インバウンドインタラクションモジュールと組み合わせることで、その受信者専用のマーケティングオファーをメッセージに挿入することができます。

>[!NOTE]
>
>インタラクションモジュールについて詳しくは、[インタラクション](../../interaction/using/interaction-and-offer-management.md)を参照してください。

トランザクションメッセージをインタラクションと一緒に使用するには、以下の設定をおこなう必要があります。

* コントロールインスタンス上に&#x200B;**インタラクション**&#x200B;パッケージをインストールし、オファーカタログを設定します。

   >[!CAUTION]
   >
   >オファーは実行インスタンス上に複製しないでください。

* オファーのパーソナライズには、受信者にリンクされた識別子がイベントに含まれている必要があります。この識別子の値は **@externalId** 属性に記載されている必要があります。**インタラクション**&#x200B;は、プライマリキーで受信者を識別するようデフォルトで設定されています。

   ```
   <rtEvent type="order_confirmation" email="john.doe@adobe.com" externalId="1242"> 
   ```

   例えば E メールアドレスなど、指定したフィールドによる識別がおこなわれるよう、**インタラクション**&#x200B;を設定することもできます。

   ```
   <rtEvent type="order_confirmation" email="john.doe@adobe.com" externalId="john.doe@yahoo.com"> 
   ```

E メールキャンペーン用に作成するのと同様に、配信テンプレートを作成します。

* オファーをトランザクションメッセージテンプレートに追加します。
* プレビューを確認して、配達確認を送信し、テンプレートをパブリッシュします。

また、オファースペースで、単一モードを有効にする必要があります。詳しくは、[この節](../../interaction/using/creating-offer-spaces.md)を参照してください。

## トランザクションメッセージおよびプッシュ通知 {#transactional-messaging-and-push-notifications}

トランザクションメッセージでは、モバイルアプリチャネルモジュールと組み合わせることで、通知を介してモバイルデバイスにトランザクションメッセージをプッシュすることができます。

>[!NOTE]
>
>モバイルアプリチャネルについて詳しくは、[この節](../../delivery/using/about-mobile-app-channel.md)を参照してください。

トランザクションメッセージモジュールをモバイルアプリチャネルと一緒に使用するには、以下の設定をおこなう必要があります。

1. **モバイルアプリチャネル**&#x200B;パッケージをコントロールインスタンスと実行インスタンス上にインストールします。
1. **モバイルアプリチャネル**&#x200B;タイプの Adobe Campaign サービスおよびサービスに含まれるモバイルアプリを実行インスタンスに複製します。

イベントには次の要素が含まれる必要があります。

* モバイルデバイス ID（Android では **registrationId**、iOS では **deviceToken**）。この ID が、通知を送信する宛先の「アドレス」を表します。
* モバイルアプリケーションへのリンクまたは統合キー（**uuid**）。アプリケーション固有の接続情報を復元することができます。
* 通知が送信されるチャネル（**wishedChannel**）：iOS は 41、Android は 42 です
* パーソナライズに役立つすべてのデータ。

以下は、この情報を含むイベントの例です。

```
<SOAP-ENV:Envelope xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/">
   <SOAP-ENV:Body>
     <urn:PushEvent>
         <urn:sessiontoken>mc/</urn:sessiontoken>
         <urn:domEvent>

              <rtEvent wishedChannel="41" type="DELIVERY" registrationToken="2cefnefzef758398493srefzefkzq483974">
                <mobileApp _operation=”none” uuid="com.adobe.NeoMiles"/>
                <ctx>
                    <deliveryTime>1:30 PM</deliveryTime>
                    <url>http://www.adobe.com</url>
                </ctx>
              </rtEvent>

         </urn:domEvent>
     </urn:PushEvent>           
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

>[!NOTE]
>
>メッセージテンプレートの作成に変更はありません。

## トランザクションメッセージと LINE {#transactional-messaging-and-line}

LINE チャネルとトランザクションメッセージを組み合わせると、コンシューマー向けモバイルデバイスにインストールされた LINE アプリでリアルタイムメッセージを送信できます。これは、LINE ユーザーがブランドのページを追加したときに歓迎メッセージを送信するために使用されます。

トランザクションメッセージモジュールを LINE と共に使用するには、**マーケティング**&#x200B;インスタンスと&#x200B;**実行**&#x200B;インスタンスの設定で次の要素が必要になります。

* **[!UICONTROL LINE コネクト]**&#x200B;パッケージを両方のインスタンスにインストールします。
* **[!UICONTROL トランザクションメッセージコントロール]**&#x200B;パッケージをマーケティングインスタンスに、**[!UICONTROL トランザクションメッセージ実行]**&#x200B;パッケージを実行インスタンスに、それぞれインストールします。
* 両方のインスタンスで LINE の&#x200B;**外部アカウント**&#x200B;と&#x200B;**サービス**&#x200B;を作成します。このとき、同じ名前を使用してこれらが同期されるようにします。LINE の外部アカウントとサービスの作成方法について詳しくは、[この節](../../delivery/using/line-channel.md#creating-a-line-account-and-an-external-account-)を参照してください。

次に、**[!UICONTROL エクスプローラー]**&#x200B;から、**[!UICONTROL プラットフォーム]**／**[!UICONTROL 外部アカウント]**&#x200B;を選択して、それぞれのインスタンスで異なる外部アカウントを設定する必要があります。

1. **実行**&#x200B;インスタンスでは、**[!UICONTROL 外部データベース]**&#x200B;外部アカウントを次の設定で作成します。

   ![](assets/line_config_mc.png)

   * **[!UICONTROL ラベル]**&#x200B;および&#x200B;**[!UICONTROL 内部名]**：必要に応じて外部アカウントに名前を付けます。
   * **[!UICONTROL タイプ]**：「**[!UICONTROL 外部データベース]**」を選択します。
   * 「**[!UICONTROL 有効]**」ボックスをオンにする必要があります。
   **[!UICONTROL 接続]**&#x200B;カテゴリで、以下の設定をおこないます。

   * **[!UICONTROL タイプ]**：データベースサーバー（例：PostgresSQL）を選択します。
   * **[!UICONTROL サーバー]**：データベースサーバーの URL を入力します。
   * **[!UICONTROL アカウント]**：データベースアカウントを入力します。

      >[!NOTE]
      >
      >データベースユーザーは、FDA 接続に関するテーブル（XtkOption、NmsVisitor、NmsVisitorSub、NmsService、NmsBroadLogRtEvent、NmsBroadLogBatchEvent、NmsTrackingLogRtEvent、NmsTrackingLogBatchEvent、NmsRtEvent、NmsBatchEvent、NmsBroadLogMsg、NmsTrackingUrl、NmsDelivery、NmsWebTrackingLogXtkFolder）の読み取り権限を持っている必要があります。

   * **[!UICONTROL パスワード]**：データベースアカウントのパスワードを入力します。
   * **[!UICONTROL データベース]**：実行インスタンスのデータベース名を入力します。
   * 「**[!UICONTROL リモートデータベースへの HTTP リレーアカウントのターゲット]**」 ボックスをオンにする必要があります。


1. **マーケティング**&#x200B;インスタンスでは、**[!UICONTROL 外部データベース]**&#x200B;アカウントを次の設定で作成します。

   ![](assets/line_config_mc_1.png)

   * **[!UICONTROL ラベル]**&#x200B;および&#x200B;**[!UICONTROL 内部名]**：必要に応じて外部アカウントに名前を付けます。
   * **[!UICONTROL タイプ]**：「**[!UICONTROL 外部データベース]**」を選択します。
   * 「有効」ボックスをオンにする必要があります。
   **[!UICONTROL 接続]**&#x200B;カテゴリで、以下の設定をおこないます。

   * **[!UICONTROL タイプ]**：「**[!UICONTROL リモートデータベースへの HTTP リレー]**」を選択します。
   * **[!UICONTROL サーバー]**：キャンペーンのサーバー URL（実行インスタンスのもの）を入力します。
   * **[!UICONTROL アカウント]**：実行インスタンスへのアクセスに使用するアカウントを入力します。
   * **[!UICONTROL パスワード]**：実行インスタンスへのアクセスに使用するアカウントのパスワードを入力します。
   * **[!UICONTROL データソース]**：**[!UICONTROL nms:extAccount:ID]** という構文で、実行インスタンスの外部データベースアカウントを入力します。


1. **マーケティング**&#x200B;インスタンスで、して、データ同期ワークフローを作成するための&#x200B;**[!UICONTROL 実行インスタンス]**&#x200B;外部アカウントを次の設定で作成します。

   ![](assets/line_config_mc_2.png)

   * **[!UICONTROL ラベル]**&#x200B;および&#x200B;**[!UICONTROL 内部名]**：必要に応じて外部アカウントに名前を付けます。
   * **[!UICONTROL タイプ]**：**[!UICONTROL 実行インスタンス]**&#x200B;を選択します。
   * 「有効」ボックスをオンにする必要があります。
   **[!UICONTROL 接続]**&#x200B;カテゴリで、以下の設定をおこないます。

   * **[!UICONTROL URL]**：実行インスタンスの URL を入力します。
   * **[!UICONTROL アカウント]**：実行インスタンスへのアクセスに使用するアカウントを入力します。
   * **[!UICONTROL パスワード]**：実行インスタンスへのアクセスに使用するアカウントのパスワードを入力します。
   **[!UICONTROL アカウント接続方法]**&#x200B;カテゴリで、以下の設定をおこないます。

   * **[!UICONTROL 方法]**：「**[!UICONTROL Federated Data Access（FDA）]**」を選択します。
   * **[!UICONTROL FDA アカウント]**：ドロップダウンからお使いの FDA アカウントを選択します。
   * 「**[!UICONTROL アーカイブワークフローを作成]**」ボタンをクリックします。
   * 「**[!UICONTROL データ同期ワークフローを作成]**」ボタンをクリックして、LINE データ同期ワークフローを作成します。



1. これで、トランザクションメッセージの作成を開始できる状態になりました。詳しくは、この[ページ](../../message-center/using/introduction.md)を参照してください。
