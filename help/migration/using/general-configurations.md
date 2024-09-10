---
product: campaign
title: 一般設定
description: 一般設定
feature: Upgrade
audience: migration
content-type: reference
topic-tags: configuration
hide: true
hidefromtoc: true
exl-id: 7aad0e49-8d9c-40c7-9d6a-42fee0ae5870
source-git-commit: 7906e9fee164d731659bbb9f96394faca5961240
workflow-type: tm+mt
source-wordcount: '2612'
ht-degree: 4%

---

# 一般設定{#general-configurations}

この節では、v5.11 または v6.02 から移行する際に、Adobe Campaign v7 で実行される設定について詳しく説明します。

さらに、次の点に注意してください。

* v5.11 から移行する場合は、[ この節 ](../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11) で説明した設定も完了する必要があります。
* v6.02 から移行する場合は、[ この節 ](../../migration/using/configuring-your-platform.md#specific-configurations-in-v6-02) で説明されている設定も完了する必要があります。

## タイムゾーン {#time-zones}

### マルチタイムゾーンモード {#multi-time-zone-mode}

v6.02 では、「マルチタイムゾーン」モードは PostgreSQL データベースエンジンでのみ使用できます。 どのようなタイプのデータベースエンジンを使用しても提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。

TIMESTAMP WITH TIMEZONE モードを使用するには、postupgrade コマンドラインに **-userTimestamptz:1** オプションも追加する必要があります。

>[!IMPORTANT]
>
>互換性のないデータベース エンジンで **-usetimestamptz:1** パラメーターを使用すると、データベースが破損するため、データベースのバックアップを復元し、上記のコマンドを再実行する必要があります。

>[!NOTE]
>
>移行後にコンソール（**[!UICONTROL 管理/プラットフォーム/オプション/WdbcTimeZone]** ノード）を通じてタイムゾーンを変更できます。
>
>タイムゾーン管理について詳しくは、[ この節 ](../../installation/using/time-zone-management.md) を参照してください。

### Oracle {#oracle}

アップグレード後に **ORA 01805** エラーが発生した場合は、アプリケーション・サーバーとデータベース・サーバー間のOracleのタイムゾーン・ファイルが同期されていないことを意味します。 これらを再同期するには、次の手順に従います。

1. 使用されているタイムゾーンファイルを特定するには、次のコマンドを実行します。

   ```
   select * from v$timezone_file
   ```

   タイムゾーンファイルは通常、**ORACLE_HOME/oracore/zoneinfo/** フォルダーにあります。

1. タイムゾーンファイルが両方のサーバーで同じであることを確認します。

詳細については、[https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004](https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004) を参照してください。

クライアントとサーバーの間でタイムゾーンの不一致が発生した場合も、遅延が発生する可能性があります。 そのため、クライアントサイドとサーバーサイドで同じバージョンのOracleライブラリを使用することをお勧めします。両方のタイムゾーンが同じである必要があります。

両側が同じタイムゾーン上にあるかどうかを確認するには：

1. 次のコマンドを実行して、クライアント側のタイムゾーンファイルのバージョンを確認します。

   ```
   genezi -v
   ```

   genezi は **$genezi_HOME/bin** リポジトリにあるバイナリです。ORACLEの場合は、次のようになります。

1. 次のコマンドを実行して、サーバー側のタイムゾーンファイルのバージョンを確認します。

   ```
   select * from v$timezone_file
   ```

1. クライアント側でタイム・ゾーン・ファイルを変更するには、**ORA_TZFILE** 環境変数を使用します。

## セキュリティ {#security}

### セキュリティゾーン {#security-zones}

>[!IMPORTANT]
>
>セキュリティ上の理由から、Adobe Campaign プラットフォームにはデフォルトでアクセスできなくなりました。セキュリティゾーンを設定する必要があるので、オペレーターの IP アドレスを収集します。

Adobe Campaign v7 には、「セキュリティゾーン **という概念が含ま** ています。 インスタンスにログオンするには、各ユーザーをゾーンに関連付ける必要があります。また、ユーザーの IP アドレスは、セキュリティゾーンで定義されたアドレスまたはアドレスの範囲に含まれている必要があります。 セキュリティゾーンの設定は、Adobe Campaign サーバーの設定ファイルで行うことができます。 ユーザーが関連付けられているセキュリティゾーンは、コンソール（**[!UICONTROL 管理/アクセス管理/オペレーター]**）で定義する必要があります。

**移行前に**、移行後にアクティブ化するセキュリティ ゾーンの定義についてネットワーク管理者に問い合わせてください。

**アップグレード後** （サーバーの再起動前）に、セキュリティゾーンを設定する必要があります。

セキュリティゾーンの設定は [ この節 ](../../installation/using/security-zones.md) にあります。

### ユーザーパスワード {#user-passwords}

v7 では、**internal** および **admin** オペレーター接続はパスワードで保護する必要があります。 これらのアカウントとすべてのオペレーターアカウントに、**移行前** パスワードを割り当てることを強くお勧めします。 **internal** のパスワードを指定していない場合、接続できません。 **internal** にパスワードを割り当てるには、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>**内部** パスワードは、すべてのトラッキングサーバーで同じである必要があります。 詳しくは、[ この節 ](../../installation/using/configuring-campaign-server.md#internal-identifier) および [ この節 ](../../platform/using/access-management.md) を参照してください。

### v7 の新機能 {#new-features-in-v7}

* 権限のないユーザーは、Adobe Campaignに接続できなくなりました。 ユーザーの権限は、例えば **connect** という権限を作成するなどして手動で追加する必要があります。

  この変更の影響を受けるユーザーは、アップグレード後に特定され、一覧表示されます。

* パスワードが空の場合、トラッキングは機能しなくなりました。 その場合は、エラーメッセージが表示され、再設定が求められます。
* ユーザーパスワードは、**xtk:sessionInfo** スキーマには保存されなくなりました。
* **`xtk:builder:EvaluateJavaScript`** 関数と **`xtk:builder:EvaluateJavaScriptTemplate`** 関数を使用するには、管理権限が必要になりました。

一部の標準スキーマは変更され、**admin** 権限を持つオペレーターの書き込みアクセス権でのみ、デフォルトでアクセスできるようになりました。

* ncm:publishing
* nl:monitoring
* nms:calendar
* xtk:builder
* xtk:connections
* xtk:dbInit
* xtk:entityBackupNew
* xtk:entityBackupOriginal
* xtk:entityOriginal
* xtk:form
* xtk:funcList
* xtk:fusion
* xtk:image
* xtk:javascript
* xtk:jssp
* xtk:jst
* xtk:navtree
* xtk:operatorGroup
* xtk:package
* xtk:queryDef
* xtk:resourceMenu
* xtk:rights
* xtk:schema
* xtk:scriptContext
* xtk:specFile
* xtk:sql
* xtk:sqlSchema
* xtk:srcSchema
* xtk:strings
* xtk:xslt

### Sessiontoken パラメーター {#sessiontoken-parameter}

v5 では、**sessiontoken** パラメーターは、クライアントサイド（概要タイプ画面のリスト、リンクエディターなど）でも機能していました サーバー側（web アプリケーション、レポート、jsp、jssp など）。 v7 では、サーバー側でのみ機能します。 v5 と同じように完全な機能に戻したい場合は、このパラメーターを使用してリンクを変更し、接続ページ経由で渡す必要があります。

リンク例：

```
/view/recipientOverview?__sessiontoken=<trusted login>
```

接続ページを使用した新しいリンク：

```
/nl/jsp/logon.jsp?login=<trusted login>&action=submit&target=/view/recipientOverview
```

>[!IMPORTANT]
>
>信頼できる IP マスクにリンクされたオペレーターを使用している場合は、そのオペレーターに最小権限が設定されていて、**sessionTokenOnly** モードのセキュリティゾーンに入っていることを確認してください。

### SQL 関数 {#sql-functions}

不明な SQL 関数呼び出しは、サーバーに自然に送信されなくなりました。 現在、すべての SQL 関数を **xtk:funcList** スキーマに追加する必要があります（詳しくは、[ この節 ](../../configuration/using/adding-additional-sql-functions.md) を参照してください）。 移行時には、アップグレード後に、古い未宣言の SQL 関数との互換性を維持できるオプションが追加されます。 これらの関数を引き続き使用する場合は、「**XtkPassUnknownSQLFunctionsToRDBMS**」オプションが **[!UICONTROL 管理/プラットフォーム/オプション]** ノードレベルで実際に定義されていることを確認します。

>[!IMPORTANT]
>
>このオプションは、セキュリティリスクがあるため、使用しないことを強くお勧めします。

### JSSP {#jssp}

例えば、セキュリティゾーンで実行される設定に関係なく、web アプリで（HTTPS ではなく） HTTP プロトコルを使用した特定のページへのアクセスを許可する場合、対応するリレールールで **httpAllowed=&quot;true&quot;** パラメーターを指定する必要があります。

匿名の JSSP を使用する場合は、JSSP のリレールールに **httpAllowed=&quot;true&quot;** パラメーターを追加する必要があります（**[!UICONTROL serverConf.xml]** ファイル）。

例：

```
<url IPMask="" deny="" hostMask="" httpAllowed="true" relayHost="true" relayPath="true"
           status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*/cus/myPublicPage.jssp"/>
```

## 構文 {#syntax}

### JavaScript {#javascript}

Adobe Campaign v7 は、より新しいJavaScript インタープリターを統合しています。 ただし、この更新により、特定のスクリプトが正しく機能しなくなる可能性があります。 以前のエンジンはより許容度が高かったので、特定の構文が機能しますが、これは新しいバージョンのエンジンでは異なります。

**[!UICONTROL myObject。@attribute]** 構文が XML オブジェクトに対してのみ有効になりました。 この構文は、配信とコンテンツ管理をパーソナライズするために使用できます。 非 XML オブジェクトに対してこのタイプの構文を使用すると、パーソナライゼーション機能は動作しなくなります。

その他のすべてのオブジェクトタイプでは、構文は **[!UICONTROL myObject`[`&quot;attribute&quot;`]`]** になりました。 例えば、**[!UICONTROL employee という構文を使用した非 XML オブジェクトなどです。@sn]** では、**[!UICONTROL employee`[`&quot;sn&quot;`]`]** の構文を使用する必要があります。

* 以前の構文：

  ```
  employee.@sn
  ```

* 新しい構文：

  ```
  employee["sn"]
  ```

XML オブジェクト内の値を変更するには、XML ノードを追加する前に値を更新することから始める必要があります。

* 古いJavaScriptコード：

  ```
  var cellStyle = node.style.copy();
  this.styles.appendChild(cellStyle);
  cellStyle.@width = column.@width;
  ```

* 新しいJavaScript コード：

  ```
  var cellStyle = node.style.copy();
  cellStyle.@width = column.@width;
  this.styles.appendChild(cellStyle);
  ```

XML 属性をテーブルキーとして使用できなくなりました。

* 以前の構文：

  ```
  if(serverForm.activities[ctx.activityHistory.activity[0].@name].type !="end")
  ```

* 新しい構文：

  ```
  if(serverForm.activities[String(ctx.activityHistory.activity[0].@name)].type !="end"
  ```

### SQLData {#sqldata}

インスタンスのセキュリティを強化するために、Adobe Campaign v7 に新しい構文が導入され、SQLData に基づく構文に置き換わりました。 この構文でこれらのコード要素を使用する場合は、変更する必要があります。 主な要素は次のとおりです。

* サブクエリによるフィルタリング：新しい構文は、サブクエリを定義する `<subQuery>` 要素に基づいています
* 集計：新しい構文は、「aggregate function （collection）」です
* 結合によるフィルタリング：新しい構文は `[schemaName:alias:xPath]` です

queryDef （xtk:queryDef） スキーマが変更されています：

* sqldata に含まれる SELECT を置き換える新しい `<subQuery>` 要素が利用可能です
* @setOperator 属性に「IN」と「NOT IN」という 2 つの新しい値が導入されました
* `<node>` 要素の子である新しい `<where>` 要素：これにより、SELECT で「サブ選択」を行うことができます。

「@expr」属性を使用すると、SQLData が存在する場合があります。 「SQLData」、「aliasSqlTable」、「sql」などの用語の検索を実行できます。

Adobe Campaign v7 インスタンスは、デフォルトで保護されています。 セキュリティは、**[!UICONTROL serverConf.xml]** ファイル内のセキュリティゾーンの定義に関して提供されます。**allowSQLInjection** 属性は、SQL 構文のセキュリティを管理します。

アップグレード後の実行中に SQLData エラーが発生した場合は、この属性を変更して、SQLData ベースの構文を一時的に使用できるようにし、コードを書き換えられるようにする必要があります。 これを行うには、**serverConf.xml** ファイルで次のオプションを変更する必要があります。

```
allowSQLInjection="true"
```

そのため、次のコマンドを使用してポストアップグレードを再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

セキュリティゾーンを設定してから（[ セキュリティ ](#security) を参照）、オプションを変更してセキュリティを再アクティブ化する必要があります。

```
allowSQLInjection="false"
```

次に、古い構文と新しい構文の比較例を示します。

**サブクエリによるフィルタリング**

* 以前の構文：

  ```
  <condition expr="@id NOT IN ([SQLDATA[SELECT iOperatorId FROM XtkOperatorGroup WHERE iGroupId = $(../@owner-id)]])" enabledIf="$(/ignored/@ownerType)=1"/>
  ```

* 新しい構文：

  ```
  <condition setOperator="NOT IN" expr="@id" enabledIf="$(/ignored/@ownerType)=1">
    <subQuery schema="xtk:operatorGroup">
       <select>
         <node expr="[@operator-id]" />
       </select>
       <where>
         <condition expr="[@group-id]=$long(../@owner-id)"/>
       </where>
     </subQuery>
  </condition>
  ```

* 以前の構文：

  ```
  <queryFilter name="dupEmail" label="Emails duplicated in the folder" schema="nms:recipient">
      <where>
        <condition sql="sEmail in (select sEmail from nmsRecipient where iFolderId=$(folderId) group by sEmail having count(sEmail)>1)" internalId="1"/>
      </where>
      <folder _operation="none" name="nmsSegment"/>
    </queryFilter>
  ```

* 新しい構文：

  ```
  <queryFilter name="dupEmail" label=" Emails duplicated in the folder " schema="nms:recipient">
      <where>
        <condition expr="@email" setOperator="IN" internalId="1">
          <subQuery schema="nms:recipient">
            <select><node expr="@email"/></select>
            <where><condition expr="[@folder-id]=$(folderId)"/></where>
            <groupBy><node expr="@email"/></groupBy>
            <having><condition expr="count(@email)>1"/></having>
          </subQuery>
        </condition>
      </where>
      <folder _operation="none" name="nmsSegment"/>
    </queryFilter>
  ```

**集計**

集計関数（コレクション）

* 以前の構文：

  ```
  <node sql="(select count(*) from NmsNewsgroup WHERE O0.iOperationId=iOperationId)" alias="@nbMessages"/>
  ```

* 新しい構文：

  ```
  <node expr="count([newsgroup/@id])" alias="../@nbMessages"/>
  ```

  >[!NOTE]
  >
  >集合関数の関節は自動的に実行されます。 O0.iOperationId=iOperationId という条件を指定する必要はなくなりました。
  >
  >「count （&#42;）」関数の使用は不可能になりました。 countall （）を使用する必要があります。

* 以前の構文：

  ```
  <node sql="(select Sum(iToDeliver) from NmsDelivery WHERE O0.iOperationId=iOperationId AND iSandboxMode=0 AND iState>=45)" alias="@nbMessages"/>
  ```

* 新しい構文：

  ```
  <node expr="Sum([delivery-linkedDelivery/properties/@toDeliver])" alias= "../@sumToDeliver">
                    <where><condition expr="[validation/@sandboxMode]=0 AND @state>=45" /></where></node>
  ```

**結合によるフィルター**

`[schemaName:alias:xPath]`

エイリアスはオプションです

* 以前の構文：

  ```
  <condition expr={"[" + joinPart.destination.nodePath + "] = [SQLDATA[W." + joinPart.source.SQLName + "]]"}
                                           aliasSqlTable={nodeSchemaRoot.SQLTable + " W"}/>
  ```

* 新しい構文：

  ```
  <condition expr={"[" + joinPart.destination.nodePath + "] = [" + nodeSchema.id + ":" + joinPart.source.nodePath + "]]"}/>
  ```

**ヒントとテクニック**

`<subQuery>` 要素内で、メイン `<queryDef>` ージの「フィールド」フィールドを参照するには   要素。次の構文を使用します。`[../@field]`

例：

```
<queryDef operation="select" schema="xtk:jobLog" startPath="/" xtkschema="xtk:queryDef">
  <select>
    <node expr="[job/@pid]" alias="@pid"/>
    <node expr="@id" ordered="true"/>
    <node expr="@logType"/>
  </select>
  <where>
    <condition expr="[@job-id]=99"/>
    <condition expr="@logType" setOperator="IN">
      <subQuery schema="xtk:jobLog">
        <select><node expr="@logType"/></select>
        <where><condition expr="[@job-id]=[../job/@id]"/></where>
        <groupBy><node expr="@logType"/></groupBy>
        <having><condition expr="count(@logType)>1"/></having>
      </subQuery>
    </condition>
  </where>
</queryDef>
```

## 競合 {#conflicts}

移行はアップグレード後に実行され、競合がレポート、フォームまたは web アプリケーションに現れる場合があります。 これらの競合はコンソールから解決できます。

リソースの同期後、**postupgrade** コマンドを使用すると、同期でエラーまたは警告が生成されるかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果は、次の 2 つの方法で表示できます。

* コマンドラインインターフェイスでは、エラーは 3 つの山形 **>>>** で具体化され、同期は自動的に停止します。 警告は二重の山形 **>>** で実体化され、同期が完了したら解決する必要があります。 アップグレード後に、コマンドプロンプトに概要が表示されます。 例：

  ```
  2013-04-09 07:48:39.749Z        00002E7A          1     info    log     =========Summary of the update==========
  2013-04-09 07:48:39.749Z        00002E7A          1     info    log     test instance, 6 warning(s) and 0 error(s) during the update.
  2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.750Z        00002E7A          1     warning log     The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
  2013-04-09 07:48:39.750Z        00002E7A          1     warning log     Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
  ```

  リソースの競合に関する警告の場合は、それを解決するためにオペレータの注意が必要です。

* postupgrade`>`.log **ファイルの** postupgrade_`<server version number>`_time には、同期結果が含まれます。 デフォルトでは、**installation directory/var/`<instance>`postupgrade** ディレクトリに格納されています。 エラーと警告は、**error** 属性と **warning** 属性で示されます。

### 競合の解決 {#resolve-a-conflict}

競合の解決は、高度なオペレーターおよび「管理者」権限を付与されたオペレーターのみが実行する必要があります。

競合を解決するには、次の手順に従います。

1. Adobe Campaign ツリー構造で、**[!UICONTROL 管理/設定/パッケージ管理/競合を編集]** にカーソルを置きます。
1. リストで解決する競合を選択します。

競合を解決する方法は 3 つあります。

* **[!UICONTROL 解決済みとして宣言]**：事前にオペレーターの介入が必要です。
* **[!UICONTROL 新しいバージョンを承認]**:Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合にお勧めします。
* **[!UICONTROL 現在のバージョンを保持]**：更新が拒否されることを意味します。

  >[!IMPORTANT]
  >
  この解決モードを選択すると、新しいバージョンでパッチが失われる可能性があります。 したがって、このオプションはエキスパートオペレーターのみに使用したり予約したりしないことを強くお勧めします。

手動で競合を解決する場合は、次の手順を実行します。

1. ウィンドウの下部で、コンフリクトがあるエンティティを検索する **`_conflict_ string`** を指定します。 新しいバージョンでインストールされたエンティティには **new** 引数が含まれ、以前のバージョンに一致するエンティティには **cus** 引数が含まれます。

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 保持しているエンティティの **`_conflict_argument_ string`** を削除します。

   ![](assets/s_ncs_production_conflict003.png)

1. あなたが解決したであろう競合に移動します。 **[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

<!--
## Tomcat {#tomcat}

The integrated Tomcat server in Adobe Campaign v7 has changed version. Its installation folder (tomcat-6) has therefore also changed (tomcat 7). After the postupgrade, make sure to check that the paths do link to the updated folder (in the **[!UICONTROL serverConf.xml]** file):

```
$(XTK_INSTALL_DIR)/tomcat-X/bin/bootstrap.jar 
$(XTK_INSTALL_DIR)/tomcat-X/bin/tomcat-juli.jar
$(XTK_INSTALL_DIR)/tomcat-X/lib/tomcat-util.jar
$(XTK_INSTALL_DIR)/tomcat-X/lib/tomcat-api.jar
$(XTK_INSTALL_DIR)/tomcat-X/lib/servlet-api.jar
$(XTK_INSTALL_DIR)/tomcat-X/lib/jsp-api.jar
$(XTK_INSTALL_DIR)/tomcat-X/lib/el-api.jar
```
-->

## インタラクション {#interaction}

### 前提条件 {#prerequisites}

**アップグレード後の前に**、v7 に存在しなくなるすべてのスキーマ参照を 6.02 から削除する必要があります。

* nms:emailOfferView
* nms:webOfferView
* nms:callCenterOfferView
* nms:mobileOfferView
* nms:paperOfferView

### オファーコンテンツ {#offer-content}

v7 では、オファーコンテンツが移動されました。 v6.02 では、コンテンツは各表現スキーマにありました（**nms:emailOfferView**）。 v7 では、コンテンツはオファースキーマに含まれるようになりました。 したがって、アップグレード後は、コンテンツはインターフェイスに表示されません。 アップグレード後は、オファーコンテンツを再作成するか、コンテンツを表現スキーマからオファースキーマに自動的に移動するスクリプトを開発する必要があります。

>[!IMPORTANT]
>
設定済みのオファーを使用する一部の配信を移行後に送信する場合は、v7 でこれらの配信をすべて削除して再作成する必要があります。 これができない場合は、「互換モード」が表示されます。 Interaction v7 のすべての新機能でメリットが得られるわけではないため、このモードはお勧めしません。 これは、実際の 6.1 移行の前に進行中のキャンペーンを完了できる移行モードです。 このモードに関する詳細については、お問い合わせください。

移動スクリプトの例（**interactionTo610_full_XX.js**）は、Adobe Campaign v7 フォルダー内の **Migration** フォルダーで使用できます。 このファイルは、オファーごとに 1 つのメール表現を使用するクライアント用のスクリプトの例を示しています（「**[!UICONTROL htmlSource]**」フィールドと **[!UICONTROL textSource]** フィールド）。 **NmsEmailOfferView** テーブルにあったコンテンツをオファーテーブルに移動しました。

>[!NOTE]
>
このスクリプトを使用しても、「コンテンツ管理」オプションと「レンダリング関数」オプションのメリットを得ることはできません。 これらの機能を活用するには、カタログオファー、特にオファーコンテンツと設定スペースを再考する必要があります。

```
loadLibrary("/nl/core/shared/nl.js");

NL.require("/nl/core/shared/xtk.js");

// 1. Restore old emailOfferView schema
logInfo("Restoring old emailOfferView schema");
var oldOfferViewSchemas = <entities schema="xtk:srcSchema"/>;

oldOfferViewSchemas.appendChild(
  <srcSchema img="nms:offerView.png"
             label="Email offer representations"
             labelSingular="Email offer representation"
             name="emailOfferView" namespace="nlmig"
             genAccessors="false" implements="xtk:persist">
    <element name="emailOfferView" template="nms:offerView" sqltable="NmsEmailOfferView">
      <element name="offer" revLabel="Email representation" revIntegrity="owncopy"/>
      <element   name="htmlSource"      type="html" label="HTML content"  xml="true"/>
      <element   name="textSource"      type="CDATA" label="Text content" xml="true"/>
      <element   name="htmlSource_jst"  type="CDATA" label="HTML script"  desc="HTML content calculation script."  xml="true" advanced="true"/>
      <element   name="textSource_jst"  type="CDATA" label="Text script" desc="Text content calculation script." xml="true" advanced="true"/>
    </element>
  </srcSchema>);

var oldOfferViewsPkg = <builder><package buildNumber="*">{oldOfferViewSchemas}</package></builder>;
xtk.builder.InstallPackage(oldOfferViewsPkg);

// 2. Migrate data from old emailOfferView table to nms:offer
logInfo("Moving data from old EmailOfferView table to NmsOffer");
var OFFER_STATUS_VALIDATED = 3;

var queryDef = xtk.queryDef.create(
  <queryDef operation="select" schema="nlmig:emailOfferView">
    <select>
      <node expr="[@offer-id]"/>
      <node expr="[@space-id]"/>
      <node expr="htmlSource_jst"/>
      <node expr="textSource_jst"/>
    </select>
  </queryDef>);
var res = queryDef.ExecuteQuery();

var processedOffers = {};
for each( var emailOfferView in res.emailOfferView )
{
  if( processedOffers[String(emailOfferView.@["offer-id"])] != undefined )
  {
    logWarning("Found 2 or more eff fffffmail representations for offer " + String(emailOfferView.@["offer-id"]) + ". Only keep the first one here.");
    continue;
  }
  xtk.session.Write(
    <offer id={emailOfferView.@["offer-id"]} status={OFFER_STATUS_VALIDATED} xtkschema="nms:offer">
      <view>
        {emailOfferView.mdSource_jst}
        {emailOfferView.textSource_jst}
      </view>
    </offer>
  );
  processedOffers[String(emailOfferView.@["offer-id"])] = 1;
}

// 3. Get rid of emailOfferView schema now that data has been moved.
logInfo("Deleting EmailOfferView schema");
xtk.session.Write(<srcSchema xtkschema="xtk:srcSchema" name="emailOfferView" namespace="nlmig" _operation="delete"/>);

logInfo("Done");
```

### テストと設定 {#tests-and-configuration}

環境が 1 つしかない場合は、オファーコンテンツを移動した後に従う手順を次に示します。 この場合は、「ENV」を例として見てみましょう。

1. すべての「環境」環境オファースペースで、使用するフィールドのリストを更新します。 例えば、**[!UICONTROL htmlSource]** のみを使用するオファースペースの場合、**[!UICONTROL view/htmlSource]** を追加する必要があります。

   ![](assets/migration_interaction_2.png)

1. 「**[!UICONTROL 一般]**」タブ内の「**[!UICONTROL 環境のタイプ]**」フィールドで、「**[!UICONTROL ライブ]**」を選択します。

   ![](assets/migration_interaction_3.png)

1. デザイン環境（「ENV_DESIGN」など）を作成し、ENV オンライン環境に接続します。

   ![](assets/migration_interaction_4.png)

1. すべての「ENV」環境オファースペースをデプロイし（右クリック/**[!UICONTROL アクション/デプロイ]**）、「ENV_DESIGN」環境を選択します。

   ![](assets/migration_interaction_5.png)

1. すべての「環境」環境オファーで同じ操作を行います。
1. 関連するチャネルですべての環境オファー「ENV_DESIGN」をアクティブ化します。
1. オファーの公開をテストする。 問題が発生しなかった場合は、最新のワークフロータスク **[!UICONTROL オファー通知]** （offerMgt）で保留中のタスクを実行し、すべてのオファーが有効になるようにします。

   ![](assets/migration_interaction_6.png)

1. 包括的なテストを実行します。

   >[!NOTE]
   >
   オンラインのカテゴリおよびオファーの名前は、運用開始後に変更されます。 受信チャネルで、オファーおよびカテゴリへのすべての参照を更新します。

## レポート {#reports}

### 標準レポート {#standard-reports}

現在、すべての標準レポートでレンダリングエンジン v6.x が使用されています。これらのレポートにJavaScriptを追加すると、特定の要素が機能しなくなる場合があります。 実際、古いバージョンのJavaScriptは v6.x レンダリングエンジンと互換性がありません。 そのため、JavaScript コードを確認し、後で調整する必要があります。 すべてのレポート、特にエクスポート関数をテストする必要があります。

### パーソナライズされたレポート {#personalized-reports}

<!--If you want to have the blue banner from v7 (allowing you access to the tabs), you must republish reports. If you encounter problems, you can force the v6.0 rendering engine. To do this, go to **[!UICONTROL Properties]** within the report, click **[!UICONTROL Rendering]** and choose the **[!UICONTROL Version 6.0 (Flash & OpenOffice)]** rendering engine.

![](assets/migration_reports_1.png)
-->
新しいレポート機能を活用する場合は、レポートを再公開する必要があります。 この場合は、すべてのスクリプトを確認し、必要に応じて変更します。 PDFの書き出しに関しては、Open Office 用に特定のスクリプトを追加した場合、これは新しいPDFの書き出しエンジン（PhantomJS）では機能しなくなります。

## web アプリケーション {#web-applications}

Web アプリケーション ファミリは次の 2 つです。

* 特定された web アプリケーション（一緒に表示、承認フォーム、エクストラネットの内部開発）、
* 匿名 web アプリケーション （web またはアンケートフォーム）。

### 特定された Web アプリケーション {#identified-web-applications}

レポート（[ 詳細情報 ](#reports)）と同様に、JavaScriptを追加している場合は、必要に応じて確認と適応を行う必要があります。 v7 の青いバナー（青いタブが含まれる）を利用する場合は、web アプリケーションを再公開する必要があります。

v7 で web アプリケーションの接続方法が変更されました。 特定された web アプリケーションで接続の問題が発生した場合は、**serverConf.xml** ファイルで **allowUserPassword** オプションと **sessionTokenOnly** オプションを一時的に有効にする必要があります。 アップグレード後に、次のオプション値を変更します。

```
allowUserPassword="true"
```

```
sessionTokenOnly="true"
```

そのため、次のコマンドを使用してポストアップグレードを再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

Web アプリケーションを公開する前に、v6.x レンダリングエンジンでテストします。 次に、これら 2 つのオプションを非アクティブにします。

```
allowUserPassword="false"
```

```
sessionTokenOnly="false"
```

### 匿名 Web アプリケーション {#anonymous-web-applications}

問題が発生した場合は、web アプリケーションを再公開します。
