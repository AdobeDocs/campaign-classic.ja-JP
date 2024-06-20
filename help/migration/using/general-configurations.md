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
source-git-commit: afbec7b3df810c8c1818a4fb93c5f7e30f7a753b
workflow-type: tm+mt
source-wordcount: '2612'
ht-degree: 4%

---

# 一般設定{#general-configurations}



この節では、v5.11 または v6.02 から移行する際に、Adobe Campaign v7 で実行される設定について詳しく説明します。

さらに、次の点に注意してください。

* v5.11 から移行する場合は、次の手順に従って設定も完了する必要があります [この節](../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11).
* v6.02 から移行する場合は、次の手順に従って設定も完了する必要があります。 [この節](../../migration/using/configuring-your-platform.md#specific-configurations-in-v6-02).

## タイムゾーン {#time-zones}

### マルチタイムゾーンモード {#multi-time-zone-mode}

v6.02 では、「マルチタイムゾーン」モードは PostgreSQL データベースエンジンでのみ使用できます。 どのようなタイプのデータベースエンジンを使用しても提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。

TIMESTAMP WITH TIMEZONE モードを使用するには、 **-userTimestamptz:1** アップグレード後のコマンドラインに対するオプション。

>[!IMPORTANT]
>
>次の場合 **-usetimestamptz:1** パラメーターが互換性のないデータベース エンジンで使用されています。データベースが破損し、データベースのバックアップを復元して、上記のコマンドを再実行する必要があります。

>[!NOTE]
>
>移行後にコンソール（**[!UICONTROL 管理/ プラットフォーム / オプション / WdbcTimeZone]** ノード）に含まれます。
>
>タイムゾーン管理の詳細については、次を参照してください [この節](../../installation/using/time-zone-management.md).

### Oracle {#oracle}

を取得した場合 **ORA 01805** アップグレード後にエラーが発生した場合、アプリケーション・サーバとデータベース・サーバ間のOracle・タイムゾーン・ファイルが同期されていません。 これらを再同期するには、次の手順に従います。

1. 使用されているタイムゾーンファイルを特定するには、次のコマンドを実行します。

   ```
   select * from v$timezone_file
   ```

   タイムゾーンファイルは通常、 **ORACLE_HOME/oracore/zoneinfo/** フォルダー。

1. タイムゾーンファイルが両方のサーバーで同じであることを確認します。

詳しくは、以下を参照してください。 [https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004](https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004).

クライアントとサーバーの間でタイムゾーンの不一致が発生した場合も、遅延が発生する可能性があります。 そのため、クライアントサイドとサーバーサイドで同じバージョンのOracleライブラリを使用することをお勧めします。両方のタイムゾーンが同じである必要があります。

両側が同じタイムゾーン上にあるかどうかを確認するには：

1. 次のコマンドを実行して、クライアント側のタイムゾーンファイルのバージョンを確認します。

   ```
   genezi -v
   ```

   genetzi は次の場所にある二項式です。 **$ORACLE_ホーム/bin** リポジトリ。

1. 次のコマンドを実行して、サーバー側のタイムゾーンファイルのバージョンを確認します。

   ```
   select * from v$timezone_file
   ```

1. クライアント側でタイムゾーンファイルを変更するには、 **ORA_TZFILE** 環境変数。

## セキュリティ {#security}

### セキュリティゾーン {#security-zones}

>[!IMPORTANT]
>
>セキュリティ上の理由から、Adobe Campaign プラットフォームにはデフォルトでアクセスできなくなりました。セキュリティゾーンを設定する必要があるので、オペレーターの IP アドレスを収集します。

Adobe Campaign v7 には、次の概念が含まれます **セキュリティゾーン**. インスタンスにログオンするには、各ユーザーをゾーンに関連付ける必要があります。また、ユーザーの IP アドレスは、セキュリティゾーンで定義されたアドレスまたはアドレスの範囲に含まれている必要があります。 セキュリティゾーンの設定は、Adobe Campaign サーバーの設定ファイルで行うことができます。 ユーザーが関連付けられているセキュリティゾーンは、コンソールで定義する必要があります（**[!UICONTROL 管理/ アクセス管理/ オペレーター]**）に設定します。

**移行前**&#x200B;移行後にアクティブ化するセキュリティ ゾーンを定義する方法については、ネットワーク管理者に問い合わせてください。

**アップグレード後** （サーバーを再起動する前に）セキュリティゾーンを設定する必要があります。

セキュリティゾーンの設定はにあります [この節](../../installation/using/security-zones.md).

### ユーザーパスワード {#user-passwords}

v7 では、 **内部** および **admin** オペレーター接続はパスワードで保護する必要があります。 これらのアカウントとすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧めします。 **移行前**. のパスワードを指定していない場合： **内部**&#x200B;に設定すると、接続できなくなります。 パスワードを割り当てるには **内部**&#x200B;を入力し、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>この **内部** パスワードはすべてのトラッキングサーバーで同一である必要があります。 詳しくは、次を参照してください。 [この節](../../installation/using/configuring-campaign-server.md#internal-identifier) および [この節](../../platform/using/access-management.md).

### v7 の新機能 {#new-features-in-v7}

* 権限のないユーザーは、Adobe Campaignに接続できなくなりました。 権限を手動で追加する必要があります（例：という権限を作成する） **接続**.

  この変更の影響を受けるユーザーは、アップグレード後に特定され、一覧表示されます。

* パスワードが空の場合、トラッキングは機能しなくなりました。 その場合は、エラーメッセージが表示され、再設定が求められます。
* ユーザーパスワードは、に保存されなくなりました。 **xtk:sessionInfo** スキーマ。
* を使用するための管理権限が必要になりました **`xtk:builder:EvaluateJavaScript`** および **`xtk:builder:EvaluateJavaScriptTemplate`** 関数。

一部の標準スキーマは変更され、デフォルトでは、を持つオペレーターの書き込みアクセス権でのみアクセスできるようになりました **admin** 権限：

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

v5 では、 **sessiontoken** パラメーターが両方のクライアント側（概要タイプ画面のリスト、リンクエディターなど）で機能していた サーバー側（web アプリケーション、レポート、jsp、jssp など）。 v7 では、サーバー側でのみ機能します。 v5 と同じように完全な機能に戻したい場合は、このパラメーターを使用してリンクを変更し、接続ページ経由で渡す必要があります。

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
>信頼できる IP マスクにリンクされたオペレーターを使用している場合は、そのオペレーターに最低限の権限があることと、のセキュリティゾーンにアクセスしていることを確認します **sessionTokenOnly** モード。

### SQL 関数 {#sql-functions}

不明な SQL 関数呼び出しは、サーバーに自然に送信されなくなりました。 現在、すべての SQL 関数をに追加する必要があります **xtk:funcList** スキーマ（詳しくは、次を参照してください） [この節](../../configuration/using/adding-additional-sql-functions.md)）に設定します。 移行時には、アップグレード後に、古い未宣言の SQL 関数との互換性を維持できるオプションが追加されます。 これらの関数を引き続き使用する場合は、 **XtkPassUnknownSQLFunctionsToRDBMS** オプションは、で実際に定義されます。 **[!UICONTROL 管理/ プラットフォーム / オプション]** ノードレベル。

>[!IMPORTANT]
>
>このオプションは、セキュリティリスクがあるため、使用しないことを強くお勧めします。

### JSSP {#jssp}

セキュリティゾーンで実行される設定に関係なく、web アプリで（HTTPS ではなく） HTTP プロトコルを使用した特定のページへのアクセスを許可したい場合、 **httpAllowed=&quot;true&quot;** 対応するリレールールのパラメーター。

匿名 JSSP を使用する場合は、を追加する必要があります **httpAllowed=&quot;true&quot;** JSSP のリレールールのパラメーター（**[!UICONTROL serverConf.xml]** ファイル）:

例：

```
<url IPMask="" deny="" hostMask="" httpAllowed="true" relayHost="true" relayPath="true"
           status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*/cus/myPublicPage.jssp"/>
```

## 構文 {#syntax}

### JavaScript {#javascript}

Adobe Campaign v7 は、より新しい JavaScript インタープリターを統合しています。 ただし、この更新により、特定のスクリプトが正しく機能しなくなる可能性があります。 以前のエンジンはより許容度が高かったので、特定の構文が機能しますが、これは新しいバージョンのエンジンでは異なります。

この **[!UICONTROL myObject.@attribute]** 構文が XML オブジェクトに対してのみ有効になりました。 この構文は、配信とコンテンツ管理をパーソナライズするために使用できます。 非 XML オブジェクトに対してこのタイプの構文を使用すると、パーソナライゼーション機能は動作しなくなります。

その他のすべてのオブジェクトタイプでは、構文はになります **[!UICONTROL myObject`[`&quot;attribute&quot;`]`]**. 例えば、次の構文を使用した非 XML オブジェクトなどです。 **[!UICONTROL 従業員。@sn]**&#x200B;は、次の構文を使用する必要があります。 **[!UICONTROL 被用者`[`&quot;sn&quot;`]`]**.

* 以前の構文：

  ```
  employee.@sn
  ```

* 新しい構文：

  ```
  employee["sn"]
  ```

XML オブジェクト内の値を変更するには、XML ノードを追加する前に値を更新することから始める必要があります。

* 古い JavaScript コード：

  ```
  var cellStyle = node.style.copy();
  this.styles.appendChild(cellStyle);
  cellStyle.@width = column.@width;
  ```

* 新しい JavaScript コード：

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

* サブクエリによるフィルタリング：新しい構文は、 `<subQuery>`  サブクエリを定義する要素
* 集計：新しい構文は、「aggregate function （collection）」です
* 結合によるフィルタリング：新しい構文は次のとおりです `[schemaName:alias:xPath]`

queryDef （xtk:queryDef） スキーマが変更されています：

* 新品 `<subQuery>`  要素は、SQLData に含まれる SELECT の代わりに使用できます。
* @setOperator 属性に「IN」と「NOT IN」という 2 つの新しい値が導入されました
* 新品 `<where>`  要素（の子） `<node>` 要素：これにより、SELECT で「サブ選択」を行うことができます

「@expr」属性を使用すると、SQLData が存在する場合があります。 「SQLData」、「aliasSqlTable」、「sql」などの用語の検索を実行できます。

Adobe Campaign v7 インスタンスは、デフォルトで保護されています。 セキュリティは、次のセキュリティゾーンの定義に関して提供されます **[!UICONTROL serverConf.xml]** ファイル： **allowSQLInjection** 属性は、SQL 構文のセキュリティを管理します。

アップグレード後の実行中に SQLData エラーが発生した場合は、この属性を変更して、SQLData ベースの構文を一時的に使用できるようにし、コードを書き換えられるようにする必要があります。 これを行うには、以下のオプションを **serverConf.xml** ファイル：

```
allowSQLInjection="true"
```

そのため、次のコマンドを使用してポストアップグレードを再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

セキュリティゾーンを設定する必要があります（を参照） [セキュリティ](#security)）を選択してから、オプションを変更してセキュリティを再アクティブ化します。

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
  >「count （&#42;）」関数を使用できます。 countall （）を使用する必要があります。

* 以前の構文：

  ```
  <node sql="(select Sum(iToDeliver) from NmsDelivery WHERE O0.iOperationId=iOperationId AND iSandboxMode=0 AND iState>=45)" alias="@nbMessages"/>
  ```

* 新しい構文：

  ```
  <node expr="Sum([delivery-linkedDelivery/properties/@toDeliver])" alias= "../@sumToDeliver">
                    <where><condition expr="[validation/@sandboxMode]=0 AND @state>=45" /></where></node>
  ```

**結合でフィルター**

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

In a `<subQuery>` メインの「フィールド」フィールドを参照する要素 `<queryDef>`   要素で、次の構文を使用します。 `[../@field]`

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

リソースの同期後、 **アップグレード後** コマンドを使用すると、同期でエラーまたは警告が生成されるかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果は、次の 2 つの方法で表示できます。

* コマンドラインインターフェイスでは、エラーは 3 つの山形で表現されます **>>>** 同期は自動的に停止します。 警告は二重の山形で実体化されます **>>** 同期が完了したらおよびを解決する必要があります。 アップグレード後に、コマンドプロンプトに概要が表示されます。 例：

  ```
  2013-04-09 07:48:39.749Z        00002E7A          1     info    log     =========Summary of the update==========
  2013-04-09 07:48:39.749Z        00002E7A          1     info    log     test instance, 6 warning(s) and 0 error(s) during the update.
  2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
  2013-04-09 07:48:39.750Z        00002E7A          1     warning log     The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
  2013-04-09 07:48:39.750Z        00002E7A          1     warning log     Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
  ```

  リソースの競合に関する警告の場合は、それを解決するためにオペレータの注意が必要です。

* この **postupgrade_`<server version number>`アップグレード後の時間（_T）`>`.log** ファイルに同期結果が含まれています。 デフォルトでは、次のディレクトリに格納されています。 **インストールディレクトリ/var/`<instance>`アップグレード後**. エラーおよび警告は、 **エラー** および **警告** 属性。

### 競合の解決 {#resolve-a-conflict}

競合の解決は、高度なオペレーターおよび「管理者」権限を付与されたオペレーターのみが実行する必要があります。

競合を解決するには、次の手順に従います。

1. Adobe Campaign ツリー構造で、カーソルをの上に置きます **[!UICONTROL 管理/設定/パッケージ管理/競合を編集]**.
1. リストで解決する競合を選択します。

競合を解決する方法は 3 つあります。

* **[!UICONTROL 解決済みと宣言されました]**：事前にオペレーターの介入が必要です。
* **[!UICONTROL 新しいバージョンを承認します]**:Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合にお勧めします。
* **[!UICONTROL 現在のバージョンを保持]**：更新が拒否されたことを意味します。

  >[!IMPORTANT]
  >
  この解決モードを選択すると、新しいバージョンでパッチが失われる可能性があります。 したがって、このオプションはエキスパートオペレーターのみに使用したり予約したりしないことを強くお勧めします。

手動で競合を解決する場合は、次の手順を実行します。

1. ウィンドウの下部で、 **`_conflict_ string`** 競合するエンティティを検索します。 新しいバージョンでインストールされるエンティティには、 **新規** 以前のバージョンと一致するエンティティを持つ引数 **cus** 引数。

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 を削除 **`_conflict_argument_ string`** 保持しているエンティティの。

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

**アップグレード後**:v7 に存在しない、6.02 からすべてのスキーマ参照を削除する必要があります。

* nms:emailOfferView
* nms:webOfferView
* nms:callCenterOfferView
* nms:mobileOfferView
* nms:paperOfferView

### オファーコンテンツ {#offer-content}

v7 では、オファーコンテンツが移動されました。 v6.02 では、コンテンツは各表現スキーマにありました（**nms:emailOfferView**）に設定します。 v7 では、コンテンツはオファースキーマに含まれるようになりました。 したがって、アップグレード後は、コンテンツはインターフェイスに表示されません。 アップグレード後は、オファーコンテンツを再作成するか、コンテンツを表現スキーマからオファースキーマに自動的に移動するスクリプトを開発する必要があります。

>[!IMPORTANT]
>
設定済みのオファーを使用する一部の配信を移行後に送信する場合は、v7 でこれらの配信をすべて削除して再作成する必要があります。 これができない場合は、「互換モード」が表示されます。 Interaction v7 のすべての新機能でメリットが得られるわけではないため、このモードはお勧めしません。 これは、実際の 6.1 移行の前に進行中のキャンペーンを完了できる移行モードです。 このモードに関する詳細については、お問い合わせください。

移動スクリプトの例（**interactionTo610_full_XX.js**）はで利用できます。 **移行** Adobe Campaign v7 フォルダー内のフォルダー。 このファイルは、オファーごとに 1 つのメール表現を使用するクライアント用のスクリプトの例を示しています（ **[!UICONTROL htmlSource]** および **[!UICONTROL textSource]** フィールド）に含まれます。 に含まれていたコンテンツ **NmsEmailOfferView** テーブルはオファーテーブルに移動しました。

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

1. すべての「環境」環境オファースペースで、使用するフィールドのリストを更新します。 例えば、のみを使用するオファースペースの場合、 **[!UICONTROL htmlSource]**。を追加する必要があります **[!UICONTROL view/htmlSource]**.

   ![](assets/migration_interaction_2.png)

1. が含まれる **[!UICONTROL 環境のタイプ]** 内のフィールド **[!UICONTROL 一般]** タブ、選択 **[!UICONTROL ライブ]**.

   ![](assets/migration_interaction_3.png)

1. デザイン環境（「ENV_DESIGN」など）を作成し、ENV オンライン環境に接続します。

   ![](assets/migration_interaction_4.png)

1. すべての「環境」環境オファースペースをデプロイする（右クリック > **[!UICONTROL アクション/デプロイ]**）を選択して、「ENV_DESIGN」環境を選択します。

   ![](assets/migration_interaction_5.png)

1. すべての「環境」環境オファーで同じ操作を行います。
1. 関連するチャネルですべての環境オファー「ENV_DESIGN」をアクティブ化します。
1. オファーの公開をテストする。 問題が発生しない場合は、最新のワークフロータスクで保留中のタスクを実行します **[!UICONTROL オファー通知]** （offerMgt）すべてのオファーを公開する場合。

   ![](assets/migration_interaction_6.png)

1. 包括的なテストを実行します。

   >[!NOTE]
   >
   オンラインのカテゴリおよびオファーの名前は、運用開始後に変更されます。 受信チャネルで、オファーおよびカテゴリへのすべての参照を更新します。

## レポート {#reports}

### 標準レポート {#standard-reports}

現在、すべての標準レポートでレンダリングエンジン v6.x が使用されています。これらのレポートに JavaScript を追加していた場合、特定の要素が機能しなくなる可能性があります。 実際、古いバージョンの JavaScript は v6.x レンダリングエンジンと互換性がありません。 そのため、JavaScript コードを確認し、後で調整する必要があります。 すべてのレポート、特にエクスポート関数をテストする必要があります。

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

レポートの場合と同様（[詳細を表示する](#reports)）、JavaScript を追加した場合は、必要に応じて確認と適応を行う必要があります。 v7 の青いバナー（青いタブが含まれる）を利用する場合は、web アプリケーションを再公開する必要があります。

v7 で web アプリケーションの接続方法が変更されました。 識別した web アプリケーションで接続の問題が発生した場合は、を一時的にアクティブ化する必要があります **allowUserPassword** および **sessionTokenOnly** のオプション **serverConf.xml** ファイル。 アップグレード後に、次のオプション値を変更します。

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
