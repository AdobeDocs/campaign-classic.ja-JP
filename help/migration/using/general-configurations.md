---
title: 一般設定
seo-title: 一般設定
description: 一般設定
seo-description: null
page-status-flag: never-activated
uuid: 317a145d-36b0-40fe-a272-ad5e35b0b190
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: configuration
discoiquuid: f4b1c108-7f71-4aa1-8394-a7f660834c9c
translation-type: tm+mt
source-git-commit: d509dc584cd4ae17c6dda85c09fceee8c6162dba
workflow-type: tm+mt
source-wordcount: '2882'
ht-degree: 2%

---


# 一般設定{#general-configurations}

この節では、v5.11またはv6.02から移行する場合にAdobe Campaignv7で実行する設定について説明します。

さらに、次の項目があります。

* v5.11から移行する場合は、v5.11の「 [固有の設定」の節に詳しく説明されている設定も実行する必要があります](../../migration/using/specific-configurations-in-v5-11.md) 。
* v6.02から移行する場合は、「v6.02の [固有の設定」の節で詳しく説明した設定も行う必要があります](../../migration/using/specific-configurations-in-v6-02.md) 。

## タイムゾーン {#time-zones}

### マルチタイムゾーンモード {#multi-time-zone-mode}

v6.02では、「マルチタイムゾーン」モードはPostgreSQLデータベースエンジンでのみ使用できました。 どの種類のデータベースエンジンを使用しても提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。

TIMESTAMP WITH TIMEZONEモードを使用するには、 **-userTimestamptz:1** オプションをpostupgradeコマンドラインに追加する必要もあります。

>[!IMPORTANT]
>
>互換性のないデータベースエンジンで **-usetimestamptz:1** パラメータが使用されている場合、データベースは破損し、データベースのバックアップを復元し、上記のコマンドを再実行する必要があります。

>[!NOTE]
>
>コンソール(**[!UICONTROL 管理/プラットフォーム/オプション/WdbcTimeZone]** ノード)を使用して、移行後にタイムゾーンを変更できます。
>
>For more on time zone management, refer to [this section](../../installation/using/time-zone-management.md).

### Oracle {#oracle}

アップグレード後に **ORA 01805** エラーが発生した場合は、アプリケーション・サーバーとデータベース・サーバーの間のOracleタイムゾーン・ファイルが同期されていません。 再同期するには、次の手順を適用します。

1. 使用するタイムゾーンファイルを識別するには、次のコマンドを実行します。

   ```
   select * from v$timezone_file
   ```

   タイムゾーンのファイルは、通常、 **ORACLE_HOME/oracle/zoneinfo/** フォルダーにあります。

1. タイムゾーンファイルは、両方のサーバーで同一にする必要があります。

詳しくは、次を参照してください。 [https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004](https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004).

クライアントとサーバーのタイムゾーンのずれも、遅延の原因になる場合があります。 そのため、クライアント側とサーバー側で同じバージョンのOracleライブラリを使用することをお勧めします。両方のタイムゾーンは同じにする必要があります。

両方が同じタイムゾーンにあるかどうかを確認するには：

1. 次のコマンドを実行して、クライアント側のタイムゾーンファイルのバージョンを確認します。

   ```
   genezi -v
   ```

   geneziは、 **$ORACLE_HOME/bin** リポジトリにあるバイナリです。

1. 次のコマンドを実行して、サーバー側のタイムゾーンファイルのバージョンを確認します。

   ```
   select * from v$timezone_file
   ```

1. クライアント側のタイムゾーンファイルを変更するには、 **ORA_TZFILE** 環境変数を使用します。

## セキュリティ {#security}

### Security zones {#security-zones}

>[!IMPORTANT]
>
>セキュリティ上の理由から、Adobe Campaignプラットフォームはデフォルトでアクセスできなくなりました。セキュリティゾーンを構成し、オペレーターのIPアドレスを収集する必要があります。

Adobe Campaignv7には、 **セキュリティゾーンの概念が含まれます**。 インスタンスにログオンするには、各ユーザーをゾーンに関連付ける必要があります。また、ユーザーのIPアドレスは、セキュリティゾーンで定義されたアドレスまたはアドレス範囲に含まれている必要があります。 セキュリティゾーンの設定は、Adobe Campaignサーバーの設定ファイルで行うことができます。 ユーザーが関連付けられているセキュリティゾーンは、コンソールで定義する必要があります(**[!UICONTROL 管理/アクセス管理/演算子]**)。

**移行の前に**、ネットワーク管理者に問い合わせて、移行後にアクティブ化するセキュリティゾーンを定義するお手伝いをしてください。

**アップグレード後** （サーバーを再起動する前）に、セキュリティゾーンを構成する必要があります。

セキュリティゾーンの構成は、 [このセクションにあり](../../installation/using/configuring-campaign-server.md#defining-security-zones)ます。

### ユーザーパスワード {#user-passwords}

v7では、 **内部** / **管理** 演算子の接続は、パスワードで保護する必要があります。 移行 **前に、これらのアカウントおよびすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧め**&#x200B;します。 **内部用のパスワードを指定していない場合**、接続できません。 パスワードを **内部に割り当てるには**、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>内 **** 部パスワードは、すべてのトラッキングサーバーで同一にする必要があります。 詳しくは、 [この節](../../installation/using/campaign-server-configuration.md#internal-identifier) および [この節を参照してください](../../platform/using/access-management.md#about-permissions)。

### v7の新機能 {#new-features-in-v7}

* 権限を持たないユーザーは、Adobe Campaignに接続できなくなります。 権限は、手動で追加する必要があります。例えば、 **connect**&#x200B;という名前の権限を作成します。

   この変更の影響を受けたユーザーは、アップグレード後に識別され、一覧表示されます。

* パスワードが空の場合に追跡が機能しなくなりました。 この場合、エラーメッセージが表示され、再設定を求められます。
* ユーザーのパスワードは、 **xtk:sessionInfo** スキーマに格納されなくなります。
* xtk:builder:EvaluateJavaScript **関数とxtk:builder:EvaluateJavaScriptTemplate関数を使用するには、管理権限が必要にな** りました **** 。

あらかじめ用意されている特定のスキーマが変更され、デフォルトで **admin** 権限を持つオペレーターの書き込みアクセス権限でのみアクセスできるようになりました。

* ncm：公開
* nl：監視
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
* xtk:スキーマ
* xtk:scriptContext
* xtk:specFile
* xtk:sql
* xtk:sqlSchema
* xtk:srcSchema
* xtk:strings
* xtk:xslt

### Sessiontokenパラメーター {#sessiontoken-parameter}

v5では、 **sessiontoken** パラメーターはクライアント側(概要タイプの画面のリスト、リンクエディターなど)で機能していました。 とサーバー側（webアプリケーション、レポート、jsp、jsspなど） v7では、サーバー側でのみ機能します。 v5と同様に機能全体に戻したい場合は、このパラメーターを使用してリンクを変更し、接続ページを渡す必要があります。

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
>信頼できるIPマスクとリンクされた演算子を使用する場合は、その演算子に最小限の権限があり、 **sessionTokenOnly** モードのセキュリティゾーンにあることを確認してください。

### SQL関数 {#sql-functions}

不明なSQL関数の呼び出しが、自動的にサーバーに送信されることはなくなりました。 現在、すべてのSQL関数は **xtk:funcList** スキーマに追加する必要があります(詳しくは [この節を参照](../../configuration/using/adding-additional-sql-functions.md))。 移行時に、アップグレード後に、古い宣言されていないSQL関数との互換性を維持できるオプションが追加されます。 これらの関数を引き続き使用する場合は、 **XtkPassUnknownSQLFunctionsToRDBMS** ()オプションが、 **[!UICONTROL 管理/プラットフォーム/オプション]** ・ノード・レベルで実際に定義されていることを確認してください。

>[!IMPORTANT]
>
>セキュリティ上のリスクが伴うので、このオプションの使用を強くお勧めしません。

### JSSP {#jssp}

HTTPSではなくHTTPプロトコルを介して（HTTPSではなく）特定のページへのアクセスを許可する場合は、セキュリティゾーンで行われた設定にかかわらず、対応するリレールで **httpAllowed=&quot;true&quot;** パラメーターを指定する必要があります。

匿名JSSPを使用する場合は、JSSP( **serverConf.xml** ファイル)のリレー規則にhttpAllowed=&quot;true&quot;**** パラメーターを追加する必要があります。

例：

```
<url IPMask="" deny="" hostMask="" httpAllowed="true" relayHost="true" relayPath="true"
           status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*/cus/myPublicPage.jssp"/>
```

## 構文 {#syntax}

### JavaScript {#javascript}

Adobe Campaignv7は、より新しいJavaScriptインタープリタを統合しています。 ただし、この更新により、一部のスクリプトが正常に機能しなくなる場合があります。 以前のエンジンの方が権限があるので、新しいバージョンのエンジンでは使用できない構文も使用できます。

myObject **[!UICONTROL です。@attribute]** 構文は、XMLオブジェクトに対してのみ有効になりました。 この構文は、配信とコンテンツ管理を個人化するために使用できます。 XML以外のオブジェクトに対してこのタイプの構文を使用した場合、パーソナライズ機能は動作しなくなります。

その他のすべてのオブジェクトタイプの構文は、 **[!UICONTROL myObject`[`&quot;attribute&quot;`]`]**&#x200B;です。 例えば、XML以外のオブジェクトで次の構文が使用されているとします。 **[!UICONTROL employee.@sn]**。次の構文を使用する必要があります。 **[!UICONTROL employee`[`&quot;sn&quot;`]`]**.

* 以前の構文：

   ```
   employee.@sn
   ```

* 新しい構文：

   ```
   employee["sn"]
   ```

XMLオブジェクトの値を変更するには、XMLノードを追加する前に値を更新して開始する必要があるようになりました。

* 古いJavaScriptコード：

   ```
   var cellStyle = node.style.copy();
   this.styles.appendChild(cellStyle);
   cellStyle.@width = column.@width;
   ```

* 新しいJavaScriptコード：

   ```
   var cellStyle = node.style.copy();
   cellStyle.@width = column.@width;
   this.styles.appendChild(cellStyle);
   ```

XML属性をテーブルキーとして使用できなくなりました。

* 以前の構文：

   ```
   if(serverForm.activities[ctx.activityHistory.activity[0].@name].type !="end")
   ```

* 新しい構文：

   ```
   if(serverForm.activities[String(ctx.activityHistory.activity[0].@name)].type !="end"
   ```

### SQLData {#sqldata}

インスタンスのセキュリティを強化するために、Adobe Campaignv7でSQLDataに基づく構文を置き換える新しい構文が導入されました。 これらのコード要素をこの構文で使用する場合は、それらを変更する必要があります。 関連する主な要素は次のとおりです。

* 副クエリによるフィルタ：新しい構文は、下位クエリを定義する `<subQuery>` 要素に基づいています
* 集計:新しい構文は「集計関数（コレクション）」です。
* 結合によるフィルタ：新しい構文は、 `[schemaName:alias:xPath]`

queryDef (xtk:queryDef)スキーマが変更されました：

* SQLDataに含まれるSELECTを置き換える新しい `<subQuery>` 要素を使用できます。
* @setOperator属性には、2つの新しい値「IN」と「NOT IN」が追加されました
* 新しい `<where>` 要素（要素の子） `<node>` 。これにより、SELECTで「サブセクション」を作成できます。

「@expr」属性を使用する場合は、SQLDataが存在する可能性があります。 次の用語の検索を実行できます。&quot;SQLData&quot;、&quot;aliasSqlTable&quot;、&quot;sql&quot;

Adobe Campaignv7のインスタンスは、デフォルトで保護されています。 セキュリティは、 **[!UICONTROL serverConf.xml]** ファイルのセキュリティゾーンの定義に関する用語で示されます。allowSQLInjection **属性は** 、SQL構文セキュリティを管理します。

アップグレード後の実行中にSQLDataエラーが発生した場合は、この属性を変更して、SQLDataベースの構文の使用を一時的に許可し、コードを書き直せるようにする必要があります。 これを行うには、 **serverConf.xmlファイルで次のオプションを変更する必要があります** 。

```
allowSQLInjection="true"
```

したがって、次のコマンドを使用してアップグレード後に再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

セキュリティゾーンを構成した後( [セキュリティ](#security)を参照)、次のオプションを変更してセキュリティを再アクティブ化する必要があります。

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
   >ジョイントは、集計機能に対して自動的に実行されます。 条件WHERE O0.iOperationId=iOperationIdを指定する必要はなくなりました。
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

要素で、メ `<subQuery>` イン要素の「field」フィールドを参照するには、次の構文を使用し `<queryDef>` ます。 `[../@field]`

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

移行はアップグレード後に実行され、レポート、フォーム、Webアプリケーションに競合が表示される場合があります。 これらの競合はコンソールから解決できます。

リソースの同期後に、 **postupgrade** コマンドを使用して、同期でエラーまたは警告が生成されたかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果は、次の2つの方法で表示できます。

* In the command-line interface, errors are materialized by a triple chevron **>>>** and synchronization is stopped automatically. Warnings are materialized by a double chevron **>>** and must be resolved once synchronization is complete. ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。例：

   ```
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     =========Summary of the update==========
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     test instance, 6 warning(s) and 0 error(s) during the update.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
   ```

   警告がリソースの競合に関するものである場合は、解決にはオペレーターの注意が必要です。

* The **postupgrade_`<server version number>`_time of postupgrade`>`.log** file contains the synchronization result. デフォルトでは、次のディレクトリで使用できます。 **installation directory/var/`<instance>`postupgrade**. Errors and warnings are indicated by the **error** and **warning** attributes.

### 競合の解決 {#resolve-a-conflict}

競合の解決は、上級演算子と「管理者」権限を持つ演算子でのみ実行する必要があります。

競合を解決するには、次のプロセスを適用します。

1. Adobe Campaignツリー構造で、 **[!UICONTROL 管理/設定/パッケージ管理/競合の編集の上にカーソルを置きます]**。
1. リスト内で解決する競合を選択します。

競合を解決するには、次の3つの方法が考えられます。

* **[!UICONTROL 解決済みとして宣言]**:には、事前に演算子の介入が必要です。
* **[!UICONTROL 新しいバージョンを承認する]**:adobe campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL 現在のバージョンを保持]**:は、更新が拒否されたことを意味します。

   >[!IMPORTANT]
   この解決モードを選択すると、新しいバージョンでパッチが失われるおそれがあります。 したがって、このオプションは、エキスパート演算子に対してのみ使用または予約しないことを強くお勧めします。

競合を手動で解決する場合は、次の手順に従います。

1. In the lower section of the window, search for the **`_conflict_ string`** to locate the entities with conflicts. The entity installed with the new version contains the **new** argument, the entity that matches the previous version contains the **cus** argument.

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 Delete the **`_conflict_argument_ string`** of the entity you are keeping.

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した可能性のある競合に移動します。 **[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

## Tomcat {#tomcat}

Adobe Campaignv7の統合Tomcatサーバーは、バージョン(Tomcat 7)を変更しました。 したがって、インストールフォルダ(tomcat-6)も変更されました(tomcat 7)。 アップグレード後に、パスが( **[!UICONTROL serverConf.xml]** ファイル内の)更新済みフォルダーにリンクしていることを確認します。

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

**アップグレード後に**、v7に存在しなくなるすべてのスキーマ参照を6.02から削除する必要があります。

* nms:emailOfferView
* nms:webOfferView
* nms:callCenterOfferView
* nms:mobileOfferView
* nms:paperOfferView

### オファー量 {#offer-content}

v7では、オファーコンテンツは移動されました。 v6.02では、コンテンツは各表現スキーマ(**nms:emailOfferView**)に含まれていました。 v7では、コンテンツはオファースキーマに追加されました。 したがって、アップグレード後は、コンテンツはインターフェイスに表示されません。 アップグレード後に、オファーのコンテンツを再作成するか、コンテンツを表現スキーマからオファースキーマに自動的に移動するスクリプトを作成する必要があります。

>[!IMPORTANT]
設定済みのオファーを使用する一部の配信が移行後に送信される場合は、これらの配信をすべて削除してv7で再作成する必要があります。 それができない場合は、「互換モード」が提供されます。 Interaction v7のすべての新機能が役立つとは限らないので、このモードはお勧めしません。 これは、実際の6.1移行前に継続的なキャンペーンを完了できる遷移モードです。 このモードの詳細については、お問い合わせください。

移動スクリプトの例(**interactionTo610_full_XX.js**)は、Adobe Campaignv7フォルダー内の **Migration** フォルダーにあります。 このファイルは、オファーごとに1つの電子メール表現を使用するクライアントのスクリプトの例を示しています( **[!UICONTROL htmlSource]** フィールドと **[!UICONTROL textSource]** フィールド)。 NmsEmailOfferView **テーブルの内容がオファーテーブルに移動されました** 。

>[!NOTE]
このスクリプトを使用しても、「コンテンツ管理」オプションと「レンダリング関数」オプションを利用できません。 これらの機能を活用するには、カタログオファー、特にオファーのコンテンツや設定スペースを再考する必要があります。

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

環境が1つだけの場合、オファーコンテンツを移動した後に実行する手順を次に示します。 この場合、「ENV」を例にとってみましょう。

1. すべての「ENV」環境オファースペースで、使用するフィールドのリストを更新します。 例えば、htmlSourceのみを使用するオファースペースの場合は、 **[!UICONTROL 表示]**/htmlSource ****&#x200B;を追加する必要があります。

   ![](assets/migration_interaction_2.png)

1. 「 **[!UICONTROL 一般]** 」タブ内の「環境の **[!UICONTROL タイプ]** 」フィールドで、「 **[!UICONTROL ライブ]**」を選択します。

   ![](assets/migration_interaction_3.png)

1. 設計環境（「ENV_DESIGN」など）を作成し、ENVオンライン環境に接続します。

   ![](assets/migration_interaction_4.png)

1. すべての「ENV」環境オファースペースをデプロイ(右クリック/ **[!UICONTROL アクション/デプロイ]**)し、「ENV_DESIGN」環境を選択します。

   ![](assets/migration_interaction_5.png)

1. すべての「ENV」環境オファーに対して同じようにします。
1. 関連するチャネル上のすべての環境オファー「ENV_DESIGN」をアクティブにします。
1. オファーを実稼動にするテスト。 問題が発生しない場合は、最新のワークフロータスク **[!UICONTROL オファー通知]** (offerMgt)で保留中のタスクを実行して、すべてのオファーを稼働させます。

   ![](assets/migration_interaction_6.png)

1. 包括的なテストを実行します。

   >[!NOTE]
   オンラインでのカテゴリやオファーの名前は、公開後に変更されます。 受信チャネルで、オファーとカテゴリへの参照をすべて更新します。

## レポート {#reports}

### 標準レポート {#standard-reports}

すべての標準レポートは、現在レンダリングエンジンv6.xを使用しています。これらのレポートにJavaScriptを追加した場合、一部の要素が機能しなくなる可能性があります。 実際、古いバージョンのJavaScriptはv6.xのレンダリングエンジンと互換性がありません。 したがって、JavaScriptコードを確認し、後でそれを適合させる必要があります。 すべてのレポート、特にエクスポート機能をテストする必要があります。

### Personalized reports {#personalized-reports}

v7の青いバナー（ユニバーサルへのアクセスを許可）を使用する場合は、レポートを再公開する必要があります。 問題が発生した場合は、v6.0のレンダリングエンジンを強制的に使用できます。 これを行うには、レポート内の **[!UICONTROL プロパティ]** に移動し、「 **[!UICONTROL レンダリング]** 」をクリックし、 **** Version 6.0(FlashとOpenOffice)レンダリングエンジンを選択します。

![](assets/migration_reports_1.png)

新しいレポート機能を活用したい場合は、v.6.xレンダリングエンジンを選択する必要があります。 この場合は、すべてのスクリプトを確認し、必要に応じて変更します。 PDFの書き出しに関しては、OpenOfficeに対して特定のスクリプトを追加した場合、新しいPDF書き出しエンジン(PhantomJS)では動作しなくなります。

## Web アプリケーション {#web-applications}

Webアプリケーションファミリには2つあります。

* 特定されたウェブアプリケーション（共に閲覧、承認フォーム、エクストラネット内部開発）、
* 匿名Webアプリケーション（webまたはアンケートフォーム）。

### 特定されたWebアプリケーション {#identified-web-applications}

レポート( [レポートを参照](#reports))と同様に、JavaScriptを追加した場合も、必要に応じてチェックし、対応する必要があります。 v7の青いバナー（ユニバーサルを含む）を活用したい場合は、Webアプリケーションを再公開する必要があります。 JavaScriptコードが動作している場合は、v6.xレンダリングエンジンを選択できます。 そうでない場合は、コードを調整しながらv6.0レンダリングエンジンを使用し、次にv6.xレンダリングエンジンを使用します。

>[!NOTE]
レンダリングエンジンを選択する手順は、レポートを選択する手順と同じです。 詳しくは、 [パーソナライズされたレポートを参照してください](#personalized-reports)。

v7ではWeb アプリケーション接続方法が変更されました。 特定したWebアプリケーションで接続に問題が発生した場合は、 **serverConf.xml** ファイルで、allowUserPassword **オプションと** sessionTokenOnly **** オプションを一時的にアクティブにする必要があります。 アップグレード後に、次のオプション値を変更します。

```
allowUserPassword="true"
```

```
sessionTokenOnly="true"
```

したがって、次のコマンドを使用してアップグレード後に再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

v6.xレンダリングエンジンでWebアプリケーションをテストしてから、公開します。 次に、これら2つのオプションを非アクティブにします。

```
allowUserPassword="false"
```

```
sessionTokenOnly="false"
```

### 匿名Webアプリケーション {#anonymous-web-applications}

問題が発生した場合は、Webアプリケーションを再公開します。 問題が解決しない場合は、v6.0レンダリングエンジンを選択できます。 JavaScriptを追加していない場合は、v6.xレンダリングエンジンを選択して、新機能を活用できます。

>[!NOTE]
レンダリングエンジンを選択する手順は、レポートを選択する手順と同じです。 詳しくは、 [パーソナライズされたレポートを参照してください](#personalized-reports)。

## Red-Hat {#red-hat}

v6.02またはv5.11で既製のスキーマが削除されている場合は、アップグレード後にスキーマを編集できなくなる可能性があります。 この場合は、次のコマンドを実行します。

```
su - neolane
nlserver config -postupgrade -instance:<instance name> -force
```
