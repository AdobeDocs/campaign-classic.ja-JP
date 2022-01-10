---
product: campaign
title: 一般設定
description: 一般設定
audience: migration
content-type: reference
topic-tags: configuration
exl-id: 7aad0e49-8d9c-40c7-9d6a-42fee0ae5870
source-git-commit: 8610d29a3df1080f1622a2cb3685c0961fb40092
workflow-type: tm+mt
source-wordcount: '2680'
ht-degree: 4%

---

# 一般設定{#general-configurations}

![](../../assets/v7-only.svg)

この節では、v5.11 または v6.02 からの移行時にAdobe Campaign v7 で実行する設定について詳しく説明します。

さらに、次の点に注意してください。

* v5.11 から移行する場合は、 [この節](../../migration/using/configuring-your-platform.md#specific-configurations-in-v5-11).
* v6.02 から移行する場合は、 [この節](../../migration/using/configuring-your-platform.md#specific-configurations-in-v6-02).

## タイムゾーン {#time-zones}

### マルチタイムゾーンモード {#multi-time-zone-mode}

v6.02 では、「マルチタイムゾーン」モードは PostgreSQL データベースエンジンでのみ使用可能でした。 どのタイプのデータベースエンジンを使用しても、提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。

TIMESTAMP WITH TIMEZONE モードを使用するには、 **-userTimestamptz:1** オプションを選択します。

>[!IMPORTANT]
>
>この **-usetimestamptz:1** パラメータが互換性のないデータベースエンジンで使用されている場合、データベースが破損し、データベースのバックアップを復元し、上記のコマンドを再実行する必要があります。

>[!NOTE]
>
>コンソール (**[!UICONTROL 管理/プラットフォーム/オプション/ WdbcTimeZone]** ノード ) で使用できます。
>
>タイムゾーン管理について詳しくは、 [この節](../../installation/using/time-zone-management.md).

### Oracle {#oracle}

もし **ORA 01805** ポストアップグレード中にエラーが発生しました。これは、アプリケーションサーバーとデータベースサーバーの間のOracleタイムゾーンファイルが同期されていないことを意味します。 再同期するには、次の手順に従います。

1. 使用するタイムゾーンファイルを識別するには、次のコマンドを実行します。

   ```
   select * from v$timezone_file
   ```

   タイムゾーンファイルは通常、 **ORACLE_HOME/oracle/zoneinfo/** フォルダー。

1. タイムゾーンファイルが両方のサーバーで同じであることを確認します。

詳しくは、以下を参照してください。 [https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004](https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004).

クライアントとサーバーの間のタイムゾーンのずれも、一部のラグの原因となる場合があります。 そのため、クライアント側とサーバー側で同じバージョンのOracleライブラリを使用することをお勧めします。両方のタイムゾーンを同じにする必要があります。

両方の辺が同じタイムゾーンにあるかどうかを確認するには：

1. 次のコマンドを実行して、クライアント側でタイムゾーンファイルのバージョンを確認します。

   ```
   genezi -v
   ```

   genezi は、 **$ORACLE_ホーム/bin** リポジトリ。

1. 次のコマンドを実行して、サーバー側のタイムゾーンファイルのバージョンを確認します。

   ```
   select * from v$timezone_file
   ```

1. クライアント側のタイムゾーンファイルを変更するには、 **ORA_TZFILE** 環境変数。

## セキュリティ {#security}

### セキュリティゾーン {#security-zones}

>[!IMPORTANT]
>
>セキュリティ上の理由により、Adobe Campaignプラットフォームは、デフォルトではアクセスできなくなりました。セキュリティゾーンを設定し、オペレーターの IP アドレスを収集する必要があります。

Adobe Campaign v7 には **セキュリティゾーン**. インスタンスにログオンするには、各ユーザーをゾーンに関連付ける必要があります。また、ユーザーの IP アドレスが、セキュリティゾーンで定義されたアドレスまたはアドレス範囲に含まれている必要があります。 セキュリティゾーンの設定は、Adobe Campaignサーバー設定ファイルでおこなうことができます。 ユーザーが関連付けられているセキュリティゾーンは、コンソール (**[!UICONTROL 管理/アクセス管理/オペレーター]**) をクリックします。

**移行前**&#x200B;移行後にアクティブ化するセキュリティゾーンを定義する際に役立つよう、ネットワーク管理者に依頼します。

**アップグレード後** （サーバーを再起動する前に）、セキュリティゾーンを構成する必要があります。

セキュリティゾーンの構成が次の場所に見つかりました： [この節](../../installation/using/security-zones.md).

### ユーザーパスワード {#user-passwords}

v7 では、 **内部** および **admin** オペレーターの接続は、パスワードで保護する必要があります。 これらのアカウントおよびすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧めします。 **移行前**. パスワードを指定していない場合は、 **内部**&#x200B;接続できなくなります。 パスワードをに割り当てるには **内部**、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>この **内部** パスワードは、すべてのトラッキングサーバーで同一である必要があります。 詳しくは、 [この節](../../installation/using/configuring-campaign-server.md#internal-identifier) および [この節](../../platform/using/access-management.md).

### v7 の新機能 {#new-features-in-v7}

* 権限を持たないユーザーはAdobe Campaignに接続できなくなりました。 権限は、例えば、 **接続**.

   この変更の影響を受けるユーザーは、アップグレード後に特定され、一覧表示されます。

* パスワードが空の場合、トラッキングは機能しなくなりました。 その場合は、エラーメッセージが表示され、再設定を求められます。
* ユーザーパスワードが **xtk:sessionInfo** スキーマ。
* 現在は、 **xtk:builder:EvaluateJavaScript** および **xtk:builder:EvaluateJavaScriptTemplate** 関数

あらかじめ用意されている特定のスキーマが変更され、デフォルトでは、を持つオペレーターの書き込みアクセス権でのみアクセスできるようになりました。 **admin** 権限：

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

v5 では、 **sessiontoken** クライアント側（概要タイプの画面のリスト、リンクエディターなど）の両方で機能するパラメーター およびサーバー側（web アプリケーション、レポート、jsp、jssp など） v7 では、サーバー側でのみ機能します。 v5 と同様にすべての機能に戻りたい場合は、このパラメーターを使用してリンクを変更し、接続ページを経由する必要があります。

リンクの例：

```
/view/recipientOverview?__sessiontoken=<trusted login>
```

接続ページを使用した新しいリンク：

```
/nl/jsp/logon.jsp?login=<trusted login>&action=submit&target=/view/recipientOverview
```

>[!IMPORTANT]
>
>信頼された IP マスクにリンクされたオペレーターを使用する場合は、そのオペレーターに最小限の権限が付与され、その権限が **sessionTokenOnly** モード。

### SQL 関数 {#sql-functions}

不明な SQL 関数呼び出しは、サーバーに自然に送信されなくなりました。 現在、すべての SQL 関数を **xtk:funcList** スキーマ ( 詳しくは、 [この節](../../configuration/using/adding-additional-sql-functions.md)) をクリックします。 移行時に、ポストアップグレード中にオプションが追加され、古い宣言されていない SQL 関数との互換性を維持できます。 これらの関数を引き続き使用する場合は、 **XtkPassUnknownSQLFunctionsToRDBMS** オプションが **[!UICONTROL 管理/プラットフォーム/オプション]** ノードレベル。

>[!IMPORTANT]
>
>セキュリティ上のリスクがあるので、このオプションは使用しないことを強くお勧めします。

### JSSP {#jssp}

HTTP プロトコル（HTTPS ではなく）を使用して特定のページへのアクセスを許可する場合は、セキュリティゾーンで実行された設定に関係なく、Web アプリで、 **httpAllowed=&quot;true&quot;** パラメーターを設定してください。

匿名 JSSP を使用する場合は、 **httpAllowed=&quot;true&quot;** JSSP のリレールールのパラメーター (**[!UICONTROL serverConf.xml]** ファイル ):

例：

```
<url IPMask="" deny="" hostMask="" httpAllowed="true" relayHost="true" relayPath="true"
           status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*/cus/myPublicPage.jssp"/>
```

## 構文 {#syntax}

### JavaScript {#javascript}

Adobe Campaign v7 は、より新しい JavaScript インタープリターを統合します。 ただし、この更新により、特定のスクリプトが機能しなくなる場合があります。 以前のエンジンの方が許容度が高いので、新しいバージョンのエンジンでは使用できなくなった構文もあります。

この **[!UICONTROL myObject.@attribute]** 構文は、XML オブジェクトに対してのみ有効になりました。 この構文は、配信とコンテンツ管理をパーソナライズするために使用できます。 XML 以外のオブジェクトでこのタイプの構文を使用した場合、パーソナライゼーション機能は機能しなくなります。

他のすべてのオブジェクトタイプの場合、構文はになりました。 **[!UICONTROL myObject`[`&quot;attribute&quot;`]`]**. 例えば、次の構文を使用した非 XML オブジェクトの場合、 **[!UICONTROL 従業員@sn]**&#x200B;では、次の構文を使用する必要があります。 **[!UICONTROL 従業員`[`&quot;sn&quot;`]`]**.

* 以前の構文：

   ```
   employee.@sn
   ```

* 新しい構文：

   ```
   employee["sn"]
   ```

XML オブジェクト内の値を変更するには、XML ノードを追加する前に値を更新して開始する必要があります。

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

インスタンスのセキュリティを強化するために、Adobe Campaign v7 で、SQLData に基づく構文を置き換える新しい構文が導入されました。 これらのコード要素をこの構文で使用する場合は、変更する必要があります。 主な要素は次のとおりです。

* サブクエリによるフィルタリング：新しい構文は、 `<subQuery>`  サブクエリを定義する要素
* 集計：新しい構文は「集計関数（コレクション）」です。
* 結合によるフィルタ：新しい構文は、 `[schemaName:alias:xPath]`

queryDef (xtk:queryDef) スキーマが変更されました。

* 新しい `<subQuery>`  要素は、SQLData に含まれる SELECT を置き換えるために使用できます
* @setOperator属性には、「IN」と「NOT IN」の 2 つの新しい値が追加されました。
* 新しい `<where>`  要素 ( `<node>` 要素：これにより、SELECT で「サブ選択」を行うことができます。

「@expr」属性を使用すると、SQLData が存在する場合があります。 以下の用語の検索を実行できます。&quot;SQLData&quot;, &quot;aliasSqlTable&quot;, &quot;sql&quot;.

Adobe Campaign v7 インスタンスは、デフォルトで保護されています。 セキュリティは、 **[!UICONTROL serverConf.xml]** ファイル：の **allowSQLInjection** 属性は、SQL 構文のセキュリティを管理します。

アップグレード後の実行中に SQLData エラーが発生した場合は、この属性を変更して、SQLData に基づく構文の使用を一時的に許可し、コードを書き換える必要があります。 これをおこなうには、 **serverConf.xml** ファイル：

```
allowSQLInjection="true"
```

そのため、次のコマンドを使用してアップグレード後に再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

セキュリティゾーンを設定する必要があります ( [セキュリティ](#security)) を有効にしてから、次のオプションを変更してセキュリティを再アクティブ化します。

```
allowSQLInjection="false"
```

以下に、古い構文と新しい構文の比較例を示します。

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
   >集計関数に対して、ジョイントが自動的に実行されます。 条件 WHERE O0.iOperationId=iOperationId を指定する必要がなくなりました。
   >
   >「count(*)」関数は使用できなくなりました。 「countall()」を使用する必要があります。

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

内 `<subQuery>` 要素（メインの「フィールド」フィールドを参照） `<queryDef>`   要素には、次の構文を使用します。 `[../@field]`

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

移行はポストアップグレードを通じて実行され、レポート、フォーム、Web アプリケーションに競合が表示される場合があります。 これらの競合は、コンソールから解決できます。

リソースの同期後、 **postupgrade** コマンドを使用すると、同期でエラーまたは警告が生成されたかどうかを検出できます。

### 同期結果を表示 {#view-the-synchronization-result}

同期結果は、次の 2 つの方法で表示できます。

* コマンドラインインターフェイスでは、エラーは 3 つの山形記号で表されます。 **>>>** 同期は自動的に停止します。 警告は二重山形記号で表されます **>>** 同期が完了したら、解決する必要があります。 ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。例：

   ```
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     =========Summary of the update==========
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     test instance, 6 warning(s) and 0 error(s) during the update.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
   ```

   この警告がリソースの競合に関係する場合は、解決するためにオペレーターの注意が必要です。

* この **postupgrade_`<server version number>`ポストアップグレードの時刻 (_T)`>`.log** ファイルには同期結果が含まれます。 デフォルトでは、次のディレクトリで使用できます。 **installation directory/var/`<instance>`postupgrade**. エラーと警告は、 **エラー** および **警告** 属性。

### 競合の解決 {#resolve-a-conflict}

競合の解決は、上級オペレーターと、「管理者」権限を付与されたオペレーターのみが実行する必要があります。

競合を解決するには、次の手順に従います。

1. Adobe Campaignツリー構造で、 **[!UICONTROL 管理/設定/パッケージ管理/競合を編集]**.
1. リストで解決する競合を選択します。

競合を解決する方法は 3 つあります。

* **[!UICONTROL 解決済みとして宣言済み]**:事前にオペレーターの介入が必要です。
* **[!UICONTROL 新しいバージョンを承認]**:Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL 現在のバージョンを保持]**:は、更新が却下されたことを示します。

   >[!IMPORTANT]
   この解決モードを選択すると、新しいバージョンでパッチが失われるおそれがあります。 したがって、このオプションは使用しない、またはエキスパートオペレーター向けにのみ予約することを強くお勧めします。

競合を手動で解決する場合は、次の手順に従います。

1. ウィンドウの下部のセクションで、を検索します。 **`_conflict_ string`** 競合するエンティティを検索します。 新しいバージョンでインストールされたエンティティには、 **新規** 引数を指定する場合、以前のバージョンに一致するエンティティには、 **カス** 引数。

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 を削除します。 **`_conflict_argument_ string`** 保持するエンティティの数を指定します。

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。 **[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

## Tomcat {#tomcat}

Adobe Campaign v7 の統合 Tomcat サーバーのバージョンが変更されました。 したがって、インストールフォルダ (tomcat-6) も変更されました (tomcat 7)。 アップグレード後は、更新されたフォルダー ( **[!UICONTROL serverConf.xml]** ファイル ):

```
$(XTK_INSTALL_DIR)/tomcat-8/bin/bootstrap.jar 
$(XTK_INSTALL_DIR)/tomcat-8/bin/tomcat-juli.jar
$(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-util.jar
$(XTK_INSTALL_DIR)/tomcat-8/lib/tomcat-api.jar
$(XTK_INSTALL_DIR)/tomcat-8/lib/servlet-api.jar
$(XTK_INSTALL_DIR)/tomcat-8/lib/jsp-api.jar
$(XTK_INSTALL_DIR)/tomcat-8/lib/el-api.jar
```

## インタラクション {#interaction}

### 前提条件 {#prerequisites}

**ポストアップグレード前**&#x200B;の場合は、v7 に存在しなくなった 6.02 のすべてのスキーマ参照を削除する必要があります。

* nms:emailOfferView
* nms:webOfferView
* nms:callCenterOfferView
* nms:mobileOfferView
* nms:paperOfferView

### オファーコンテンツ {#offer-content}

v7 では、オファーコンテンツが移動されました。 v6.02 では、コンテンツは各表現スキーマ (**nms:emailOfferView**) をクリックします。 v7 では、コンテンツはオファースキーマに含まれます。 そのため、アップグレード後、コンテンツはインターフェイスに表示されません。 アップグレード後に、オファーコンテンツを再作成するか、表示域スキーマからオファースキーマにコンテンツを自動的に移動するスクリプトを作成する必要があります。

>[!IMPORTANT]
設定されたオファーを使用する一部の配信が移行後に送信される必要がある場合は、v7 でこれらの配信をすべて削除して再作成する必要があります。 できない場合は、「互換性モード」が提供されます。 インタラクション v7 のすべての新機能のメリットが得られるわけではないので、このモードはお勧めしません。 これは、実際の 6.1 移行前に継続中のキャンペーンを完了できる遷移モードです。 このモードの詳細は、お問い合わせください。

移動スクリプトの例 (**interactionTo610_full_XX.js**) が **移行** Adobe Campaign v7 フォルダー内のフォルダー。 このファイルは、オファーごとに 1 つの E メール表現 ( **[!UICONTROL htmlSource]** および **[!UICONTROL textSource]** フィールド ) を参照してください。 に含まれていたコンテンツ **NmsEmailOfferView** テーブルがオファーテーブルに移動されました。

>[!NOTE]
このスクリプトを使用しても、「コンテンツ管理」および「レンダリング関数」オプションを利用できません。 これらの機能を活用するには、カタログオファー、特にオファーコンテンツおよび設定スペースを考え直す必要があります。

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

環境が 1 つのみの場合は、オファーコンテンツを移動した後に、以下の手順に従います。 この場合、「ENV」を例として取り上げます。

1. すべての「ENV」環境オファースペースで、使用するフィールドのリストを更新します。 例えば、 **[!UICONTROL htmlSource]**&#x200B;を追加する場合は、 **[!UICONTROL view/htmlSource]**.

   ![](assets/migration_interaction_2.png)

1. 内 **[!UICONTROL 環境のタイプ]** 内の **[!UICONTROL 一般]** タブ、選択 **[!UICONTROL ライブ]**.

   ![](assets/migration_interaction_3.png)

1. デザイン環境（例：ENV_DESIGN）を作成し、ENV オンライン環境に接続します。

   ![](assets/migration_interaction_4.png)

1. すべての「ENV」環境オファースペースをデプロイします ( 右クリック > **[!UICONTROL アクション/デプロイ]**) をクリックし、「ENV_DESIGN」環境を選択します。

   ![](assets/migration_interaction_5.png)

1. すべての「ENV」環境オファーに対しても同じ操作をおこないます。
1. 関連するチャネルに関するすべての環境オファー「ENV_DESIGN」をアクティブ化します。
1. オファーを有効にするテスト。 問題が発生しない場合は、最新のワークフロータスクで保留中のタスクを実行します **[!UICONTROL オファー通知]** (offerMgt) を使用して、すべてのオファーを有効にします。

   ![](assets/migration_interaction_6.png)

1. 包括的なテストを実行します。

   >[!NOTE]
   オンラインのカテゴリやオファーの名前は、運用を開始した後に変更されます。 受信チャネルで、オファーとカテゴリへの参照をすべて更新します。

## レポート {#reports}

### 標準レポート {#standard-reports}

現在、すべての標準レポートでレンダリングエンジン v6.x が使用されています。これらのレポートに JavaScript を追加した場合、一部の要素が機能しなくなることがあります。 実際、古いバージョンの JavaScript は v6.x レンダリングエンジンと互換性がありません。 そのため、JavaScript コードを確認し、後でそれを適応させる必要があります。 すべてのレポート（特にエクスポート機能）をテストする必要があります。

### パーソナライズされたレポート {#personalized-reports}

<!--If you want to have the blue banner from v7 (allowing you access to the tabs), you must republish reports. If you encounter problems, you can force the v6.0 rendering engine. To do this, go to **[!UICONTROL Properties]** within the report, click **[!UICONTROL Rendering]** and choose the **[!UICONTROL Version 6.0 (Flash & OpenOffice)]** rendering engine.

![](assets/migration_reports_1.png)
-->
新しいレポート機能のメリットを享受したい場合は、レポートを再公開する必要があります。 この場合、すべてのスクリプトを確認し、必要に応じて変更します。 PDFのエクスポートに関して、Open Office 用に特定のスクリプトを追加した場合、新しいPDFエクスポートエンジン (PhantomJS) では動作しなくなります。

## web アプリケーション {#web-applications}

次の 2 つの Web アプリケーションファミリーがあります。

* 特定された web アプリケーション（まとめて閲覧、承認フォーム、外部の内部開発）
* 匿名の Web アプリケーション（Web またはアンケートフォーム）

### 特定された Web アプリケーション {#identified-web-applications}

レポートと同様 ([詳細情報](#reports)) を読み込む場合は、必要に応じて JavaScript を追加し、それを確認して適応させる必要があります。 v7 ブルーバナー（青いタブを含む）のメリットを受けたい場合、Web アプリケーションを再公開する必要があります。

Web アプリケーションの接続方法は、v7 で変更されました。 特定された Web アプリケーションで接続の問題が発生した場合は、 **allowUserPassword** および **sessionTokenOnly** オプション **serverConf.xml** ファイル。 アップグレード後に、次のオプション値を変更します。

```
allowUserPassword="true"
```

```
sessionTokenOnly="true"
```

そのため、次のコマンドを使用してアップグレード後に再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

公開する前に、v6.x レンダリングエンジンで Web アプリケーションをテストします。 次に、これら 2 つのオプションを無効にします。

```
allowUserPassword="false"
```

```
sessionTokenOnly="false"
```

### 匿名 Web アプリケーション {#anonymous-web-applications}

問題が発生した場合は、Web アプリケーションを再公開します。
