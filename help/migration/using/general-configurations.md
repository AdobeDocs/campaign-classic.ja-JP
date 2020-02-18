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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9f7cf3d530f141a661df5fcc8cbcf0bb4c8d3e89

---


# 一般設定{#general-configurations}

この節では、v5.11またはv6.02から移行する場合にAdobe Campaign v7で実行する設定について説明します。

さらに、

* v5.11から移行する場合は、v5.11の「特定の設定」の節で詳しく説明され [ている設定も実行する必要があります](../../migration/using/specific-configurations-in-v5-11.md) 。
* v6.02から移行する場合は、「v6.02の具体的な設定」の節で詳しく説明され [ている設定も実行する必要があります](../../migration/using/specific-configurations-in-v6-02.md) 。

## タイムゾーン {#time-zones}

### マルチタイムゾーンモード {#multi-time-zone-mode}

v6.02では、「マルチタイムゾーン」モードはPostgreSQLデータベースエンジンでのみ使用可能でした。 どのタイプのデータベースエンジンが使用されても提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。

TIMESTAMP WITH TIMEZONEモードを使用するには、 **-userTimestamptz:1** オプションをpostupgradeコマンドラインに追加する必要もあります。

>[!IMPORTANT]
>
>-usetimestamptz:1 **** パラメータが互換性のないデータベースエンジンで使用されている場合、データベースは破損し、データベースのバックアップを復元し、上記のコマンドを再実行する必要があります。

>[!NOTE]
>
>コンソール（ノード）を介した移行後にタイムゾーンを変更するこ&#x200B;**[!UICONTROL Administration > Platform > Options > WdbcTimeZone]** とができます。
>
>For more on time zone management, refer to [this section](../../installation/using/time-zone-management.md).

### Oracle {#oracle}

アップグレード後に **ORA 01805** エラーが発生した場合は、アプリケーション・サーバーとデータベース・サーバー間のOracleタイムゾーン・ファイルの同期がとれていません。 再同期するには、次の手順を適用します。

1. 使用するタイムゾーンファイルを識別するには、次のコマンドを実行します。

   ```
   select * from v$timezone_file
   ```

   タイムゾーン・ファイルは、通常、 **ORACLE_HOME/oracle/zoneinfo/フォルダにあり** ます。

1. タイムゾーンファイルが両方のサーバーで同じであることを確認します。

詳しくは、次を参照してください。https://download.oracle.com/docs/cd/E11882_01/server.112/e10729/ch4datetime.htm [](http://download.oracle.com/docs/cd/E11882_01/server.112/e10729/ch4datetime.htm).

また、クライアントとサーバー間のタイムゾーンのずれによって、一部の遅延が生じる場合があります。 そのため、クライアント側とサーバー側で同じバージョンのOracleライブラリを使用することをお勧めします。両方のタイムゾーンを同じにする必要があります。

両方が同じタイムゾーンにあるかどうかを確認するには：

1. 次のコマンドを実行して、クライアント側のタイムゾーンファイルのバージョンを確認します。

   ```
   genezi -v
   ```

   geneziは、 **$ORACLE_HOME/binリポジトリにあるバイナリ** 。

1. 次のコマンドを実行して、サーバー側のタイムゾーンファイルのバージョンを確認します。

   ```
   select * from v$timezone_file
   ```

1. クライアント側のタイムゾーン・ファイルを変更するには、 **ORA_TZFILE** 環境変数を使用します。

## セキュリティ {#security}

### Security zones {#security-zones}

>[!IMPORTANT]
>
>セキュリティ上の理由から、Adobe Campaignプラットフォームはデフォルトでアクセスできなくなりました。セキュリティゾーンを設定し、オペレータのIPアドレスを収集する必要があります。

Adobe Campaign v7には、セキュリティゾーンの概念が **含まれます**。 インスタンスにログオンするには、各ユーザーをゾーンに関連付ける必要があります。また、セキュリティゾーンで定義されたアドレスまたはアドレス範囲に、ユーザーのIPアドレスを含める必要があります。 セキュリティゾーンの設定は、Adobe Campaignサーバー設定ファイルで行うことができます。 ユーザーが関連付けられているセキュリティ・ゾーンは、コンソールで定義する必要があり&#x200B;**[!UICONTROL Administration > Access management > Operators]**&#x200B;ます()。

**移行する前に**、移行後にアクティブ化するセキュリティゾーンを定義する際に、ネットワーク管理者に問い合わせてください。

**アップグレード後** （サーバーを再起動する前）に、セキュリティゾーンを設定する必要があります。

セキュリティゾーンの構成は、このセクシ [ョンにありま](../../installation/using/configuring-campaign-server.md#defining-security-zones)す。

### ユーザーパスワード {#user-passwords}

v7では、内部と **管理者の****演算子の接続は** 、パスワードで保護する必要があります。 移行前に、これらのアカウントとすべての演算子アカウントにパスワードを割り当てることを強 **くお勧めしま**&#x200B;す。 内部用のパスワードを指定しな **いと**、接続できません。 内部にパスワードを割り当てる **には**、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>内部パ **スワードは** 、すべてのトラッキングサーバーで同じにする必要があります。 詳しくは、この節とこの節 [を参照](../../installation/using/campaign-server-configuration.md#internal-identifier) し [てください](../../platform/using/access-management.md#about-permissions)。

### v7の新機能 {#new-features-in-v7}

* 権限を持たないユーザーは、Adobe Campaignに接続できなくなりました。 権限は、例えば、 **connectという名前の権限を作成して手動で追加する必要があります**。

   この変更の影響を受けたユーザーは、アップグレード後に識別され、一覧表示されます。

* パスワードが空の場合に追跡が機能しなくなりました。 この場合、エラーメッセージが表示され、再設定を求められます。
* ユーザーパスワードは、 **xtk:sessionInfoスキーマに保存されなくなりました** 。
* xtk:builder:EvaluateJavaScript関数と **xtk:builder** :EvaluateJavaScriptTemplate関数を使用するには、管理権限が必要に **なりました** 。

あらかじめ用意されている一部のスキーマが変更され、デフォルトでは、管理者権限を持つ演算子の書き込みアクセス権のみを持つようにな **りました** 。

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
* xtk:schema
* xtk:scriptContext
* xtk:specFile
* xtk:sql
* xtk:sqlSchema
* xtk:srcSchema
* xtk:strings
* xtk:xslt

### Sessiontokenパラメーター {#sessiontoken-parameter}

v5では、sessiontokenパラメー **ターは** 、クライアント側（概要タイプ画面のリスト、リンクエディターなど）で機能していました。およびサーバー側（Webアプリケーション、レポート、JSP、jsspなど） v7では、サーバー側でのみ機能します。 v5と同様に完全な機能に戻す場合は、このパラメーターを使用してリンクを変更し、接続ページを渡す必要があります。

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
>信頼されたIPマスクにリンクされた演算子を使用する場合は、その演算子に最小限の権限があり、 **sessionTokenOnlyモードのセキュリティゾーンにあることを確** 認します。

### SQL関数 {#sql-functions}

不明なSQL関数呼び出しが、自動的にサーバーに送信されることはなくなりました。 現在、すべてのSQL関数は **xtk:funcList** スキーマに追加する必要があります(詳しくは、この節を参 [照してください](../../configuration/using/adding-additional-sql-functions.md))。 移行時に、アップグレード後に、古い非宣言のSQL関数との互換性を維持できるオプションが追加されます。 これらの関数を引き続き使用する場合は、XtkPassUnknownSQLFunctionsToRDBMS **()オプションがノードレベルで定義されていることを確****[!UICONTROL Administration > Platform > Options]** 認します。

>[!IMPORTANT]
>
>セキュリティ上のリスクがあるので、このオプションの使用を強くお勧めしません。

### JSSP {#jssp}

例えば、セキュリティゾーンで実行される設定に関係なく、HTTPプロトコル（HTTPSではなく）を使用して特定のページへのアクセスを許可する場合は、対応するリレールールで **httpAllowed=&quot;true&quot;** パラメーターを指定する必要があります。

匿名JSSPを使用する場合は、JSSP （ファイル）のリレー規則に **httpAllowed=&quot;true&quot;** パラメーターを追加する必要があ&#x200B;**[!UICONTROL serverConf.xml]** ります。

次に例を示します。

```
<url IPMask="" deny="" hostMask="" httpAllowed="true" relayHost="true" relayPath="true"
           status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*/cus/myPublicPage.jssp"/>
```

## 構文 {#syntax}

### JavaScript {#javascript}

Adobe Campaign v7は、より新しいJavaScriptインタープリターを統合します。 ただし、この更新により、特定のスクリプトが機能しなくなる可能性があります。 以前のエンジンの方が許容度が高いので、新しいバージョンのエンジンではなくなった構文も使えます。

構文がXML **[!UICONTROL myObject.@attribute]** オブジェクトに対してのみ有効になるようになりました。 この構文は、配信とコンテンツ管理を個人化するために使用できます。 XML以外のオブジェクトに対してこのタイプの構文を使用した場合、パーソナライゼーション機能は動作しなくなります。

その他すべてのオブジェクトタイプの構文は、「attribute」 **[!UICONTROL myObject`[`になりました`]`]**。 例えば、XML以外のオブジェクトで次の構文を使用します。では、次&#x200B;**[!UICONTROL employee.@sn]**の構文を使用する必要があります。「**[!UICONTROL employee`[` sn」`]`]**。

* 以前の構文：

   ```
   employee.@sn
   ```

* 新しい構文：

   ```
   employee["sn"]
   ```

XMLオブジェクトの値を変更するには、XMLノードを追加する前に、値を更新することから開始する必要があります。

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

インスタンスのセキュリティを強化するために、SQLDataに基づく構文を置き換える新しい構文がAdobe Campaign v7に導入されました。 この構文でこれらのコード要素を使用する場合は、変更する必要があります。 主な要素は次のとおりです。

* サブクエリによるフィルタ：新しい構文は、サブクエリを定義 `<subQuery>` する要素に基づいています
* 集計：新しい構文は「aggregate function(collection)」です。
* 結合によるフィルタ：新しい構文は、 `[schemaName:alias:xPath]`

queryDef (xtk:queryDef)スキーマが変更されました：

* sqldataに含ま `<subQuery>` れるSELECTを置き換える新しい要素を使用できます。
* @setOperator属性に、2つの新しい値「IN」と「NOT IN」が導入されました
* 新しい `<where>` 要素（要素の子） `<node>` :これにより、SELECTで「サブセレクション」を作成できます。

「@expr」属性を使用する場合、SQLDataが存在する可能性があります。 次の用語を検索できます。&quot;SQLData&quot;、&quot;aliasSqlTable&quot;、&quot;sql&quot;

Adobe Campaign v7のインスタンスは、デフォルトで保護されています。 セキュリティは、ファイル内のセキュリティゾーンの定義に関して次のように扱 **[!UICONTROL serverConf.xml]** われます。allowsqlinjection属性は **** 、SQL構文セキュリティを管理します。

アップグレード後の実行中にSQLDataエラーが発生した場合は、この属性を変更して、SQLDataベースの構文の使用を一時的に許可し、コードの書き直しを可能にする必要があります。 これを行うには、 **serverConf.xmlファイルで次のオプションを変更する必要があります** 。

```
allowSQLInjection="true"
```

したがって、次のコマンドを使用してアップグレード後の処理を再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

セキュリティ・ゾーンを構成し( [Security](#security)を参照)、次のオプションを変更してセキュリティを再アクティブ化する必要があります。

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

Aggregate関数（コレクション）

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
   >集計関数に対して、ジョイントが自動的に実行されます。 条件WHERE O0.iOperationId=iOperationIdを指定する必要はなくなりました。
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

**結合によるフィルタ**

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

要素内 `<subQuery>` で、メイン要素の「field」フィールドを参照するに `<queryDef>` は、次の構文を使用します。 `[../@field]`

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

移行はアップグレード後に実行され、競合がレポート、フォーム、Webアプリケーションに表示される場合があります。 これらの競合は、コンソールから解決できます。

リソースの同期後、postupgradeコマンドを使 **用して** 、同期でエラーまたは警告が生成されたかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果は、次の2つの方法で表示できます。

* In the command-line interface, errors are materialized by a triple chevron **>>>** and synchronization is stopped automatically. Warnings are materialized by a double chevron **>>** and must be resolved once synchronization is complete. ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。次に例を示します。

   ```
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     =========Summary of the update==========
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     test instance, 6 warning(s) and 0 error(s) during the update.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
   ```

   警告がリソースの競合に関するものである場合は、その解決にオペレーターの注意が必要です。

* The **postupgrade_`<server version number>`_time of postupgrade`>`.log** file contains the synchronization result. デフォルトでは、次のディレクトリで使用できます。インス **トールディレクトリ/var/`<instance>`postupgrade**。 Errors and warnings are indicated by the **error** and **warning** attributes.

### 競合の解決 {#resolve-a-conflict}

競合の解決は、上級演算子と「管理者」権限を付与された演算子でのみ実行する必要があります。

競合を解決するには、次のプロセスを適用します。

1. Adobe Campaignツリー構造の上にカーソルを置きます **[!UICONTROL Administration > Configuration > Package management > Edit conflicts]**。
1. リストで解決する競合を選択します。

競合を解決する方法は3つあります。

* **[!UICONTROL Declared as resolved]**:事前に演算子の介入が必要です。
* **[!UICONTROL Accept the new version]**:adobe Campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL Keep the current version]**:は、更新が拒否されたことを意味します。

   >[!IMPORTANT]
   この解像度モードを選択すると、新しいバージョンでパッチが失われる可能性があります。 したがって、このオプションは、エキスパート演算子のみに使用したり、予約したりしないことを強くお勧めします。

競合を手動で解決する場合は、次の手順に従います。

1. In the lower section of the window, search for the **`_conflict_ string`** to locate the entities with conflicts. The entity installed with the new version contains the **new** argument, the entity that matches the previous version contains the **cus** argument.

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 Delete the **`_conflict_argument_ string`** of the entity you are keeping.

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。 アイコンをクリ **[!UICONTROL Actions]** ックし、を選択しま **[!UICONTROL Declare as resolved]**&#x200B;す。
1. 変更を保存します。これにより競合が解決します。

## Tomcat {#tomcat}

Adobe Campaign v7の統合Tomcatサーバーのバージョンが変更されました(Tomcat 7)。 したがって、そのインストールフォルダ(tomcat-6)も変更されました(tomcat 7)。 アップグレード後に、パスが更新されたフォルダー（ファイル内）にリンクしていることを確認し **[!UICONTROL serverConf.xml]** てください。

```
$(XTK_INSTALL_DIR)/tomcat-7/bin/bootstrap.jar 
$(XTK_INSTALL_DIR)/tomcat-7/bin/tomcat-juli.jar
$(XTK_INSTALL_DIR)/tomcat-7/lib/tomcat-util.jar
$(XTK_INSTALL_DIR)/tomcat-7/lib/tomcat-api.jar
$(XTK_INSTALL_DIR)/tomcat-7/lib/servlet-api.jar
$(XTK_INSTALL_DIR)/tomcat-7/lib/jsp-api.jar
$(XTK_INSTALL_DIR)/tomcat-7/lib/el-api.jar
```

## インタラクション {#interaction}

### 前提条件 {#prerequisites}

**アップグレード後に**、v7に存在しなくなるすべてのスキーマ参照を6.02から削除する必要があります。

* nms:emailOfferView
* nms:webOfferView
* nms:callCenterOfferView
* nms:mobileOfferView
* nms:paperOfferView

### オファーコンテンツ {#offer-content}

v7では、オファーのコンテンツが移動されました。 v6.02では、コンテンツは各表現スキーマ(**nms:emailOfferView**)にありました。 v7では、コンテンツはオファースキーマに追加されました。 したがって、アップグレード後には、コンテンツはインターフェイスに表示されません。 アップグレード後に、オファーコンテンツを再作成するか、コンテンツを表現スキーマからオファースキーマに自動的に移動するスクリプトを作成する必要があります。

>[!IMPORTANT]
移行後に、設定済みオファーを使用する一部の配信を送信する必要がある場合は、これらの配信をすべてv7で削除して再作成する必要があります。 それができない場合は、「互換性モード」が提供されます。 Interaction v7のすべての新機能からメリットが得られるわけではないので、このモードはお勧めしません。 これは移行モードで、実際の6.1への移行前に進行中のキャンペーンを完了できます。 このモードの詳細については、弊社までお問い合わせください。

移動スクリプトの例(**interactionTo610_full_XX.js**)は、Adobe Campaign v7フォルダー内の **Migration** （移行）フォルダーにあります。 このファイルは、オファーごとに1つの電子メール表現（およびフィールド）を使用するクライアント用のスクリプト **[!UICONTROL htmlSource]** の例を **[!UICONTROL textSource]** 示しています。 NmsEmailOfferViewテーブル内のコンテ **ンツは** 、オファーテーブルに移動されました。

>[!NOTE]
このスクリプトを使用しても、「コンテンツ管理」および「レンダリング関数」オプションを利用することはできません。 これらの機能を活用するには、カタログオファー、特にオファーコンテンツと設定スペースを再考する必要があります。

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

環境が1つだけの場合、オファーコンテンツを移動した後に実行する手順を次に示します。 この場合、例として「ENV」を挙げます。

1. すべての「ENV」環境オファースペースで、使用するフィールドのリストを更新します。 例えば、オファーを使用するオファースペースの場合は、 **[!UICONTROL htmlSource]**&#x200B;を追加する必要がありま **[!UICONTROL view/htmlSource]**&#x200B;す。

   ![](assets/migration_interaction_2.png)

1. タブ内のフ **[!UICONTROL Type of Environment]** ィールドで、を **[!UICONTROL General]** 選択しま **[!UICONTROL Live]**&#x200B;す。

   ![](assets/migration_interaction_3.png)

1. 設計環境（例：「ENV_DESIGN」）を作成し、ENVオンライン環境に接続します。

   ![](assets/migration_interaction_4.png)

1. すべての「ENV」環境オファースペースを展開し(右クリック/ **[!UICONTROL Actions > Deploy]**)、「ENV_DESIGN」環境を選択します。

   ![](assets/migration_interaction_5.png)

1. すべての「ENV」環境オファーに対して同じ手順を実行します。
1. 関連するチャネルに関するすべての環境オファー「ENV_DESIGN」をアクティブにします。
1. オファーをライブにするテスト。 問題が発生しない場合は、最新のワークフロータスク **[!UICONTROL Offer notification]** (offerMgt)で保留中のタスクを実行し、すべてのオファーを有効にします。

   ![](assets/migration_interaction_6.png)

1. 包括的なテストを実行します。

   >[!NOTE]
   オンラインでのカテゴリとオファーの名前は、ライブ後に変更されます。 受信チャネルで、オファーとカテゴリへのすべての参照を更新します。

## レポート {#reports}

### 標準レポート {#standard-reports}

すべての標準レポートは、現在レンダリングエンジンv6.xを使用しています。これらのレポートにJavaScriptを追加した場合、一部の要素が機能しなくなる可能性があります。 実際、古いバージョンのJavaScriptはv6.xレンダリングエンジンと互換性がありません。 したがって、JavaScriptコードを確認し、後でそれを適応させる必要があります。 すべてのレポート、特にエクスポート機能をテストする必要があります。

### Personalized reports {#personalized-reports}

v7の青いバナー（ユニバーサルへのアクセスを可能にする）を使用する場合は、レポートを再公開する必要があります。 問題が発生した場合は、v6.0レンダリングエンジンを強制的に使用できます。 これを行うには、レポート内 **[!UICONTROL Properties]** でをクリックし、レンダリ **[!UICONTROL Rendering]** ングエンジンを **[!UICONTROL Version 6.0 (Flash & OpenOffice)]** 選択します。

![](assets/migration_reports_1.png)

新しいレポート機能を活用したい場合は、v.6.xレンダリングエンジンを選択する必要があります。 この場合は、すべてのスクリプトを確認し、必要に応じて変更します。 PDFの書き出しに関して、OpenOffice用の特定のスクリプトを追加した場合、新しいPDF書き出しエンジン(PhantomJS)では動作しなくなります。

## Web アプリケーション {#web-applications}

Webアプリケーションのファミリーは2つあります。

* 特定されたWebアプリケーション（共に閲覧される、承認フォーム、エクストラネット内部開発）、
* 匿名Webアプリケーション（Webフォームまたはアンケートフォーム）。

### 特定されたWebアプリケーション {#identified-web-applications}

レポート(「レポート」を参照 [](#reports))と同様に、JavaScriptを追加した場合は、必要に応じてチェックして適応する必要があります。 v7の青いバナー（ユニバーサルを含む）を活用したい場合は、Webアプリケーションを再公開する必要があります。 JavaScriptコードが動作している場合は、v6.xレンダリングエンジンを選択できます。 そうでない場合は、コードを適応させながらv6.0レンダリングエンジンを使用し、次にv6.xレンダリングエンジンを使用できます。

>[!NOTE]
レンダリングエンジンを選択する手順は、レポートを選択する手順と同じです。 パーソナライズ [されたレポートを参照し](#personalized-reports)。

v7では、Webアプリケーションの接続方法が変更されました。 識別したWebアプリケーションで接続の問題が発生した場合は、 **serverConf.xmlファイルで** allowUserPassword **オプションと** sessionTokenOnly **オプションを一時的にアクティブにする必要があります** 。 アップグレード後に、次のオプション値を変更します。

```
allowUserPassword="true"
```

```
sessionTokenOnly="true"
```

したがって、次のコマンドを使用してアップグレード後の処理を再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

公開する前に、v6.xレンダリングエンジンでWebアプリケーションをテストします。 次に、この2つのオプションを非アクティブにします。

```
allowUserPassword="false"
```

```
sessionTokenOnly="false"
```

### 匿名Webアプリケーション {#anonymous-web-applications}

問題が発生した場合は、Webアプリケーションを再公開します。 問題が解決しない場合は、v6.0レンダリングエンジンを選択できます。 JavaScriptを追加していない場合は、v6.xのレンダリングエンジンを選択し、その新機能を活用できます。

>[!NOTE]
レンダリングエンジンを選択する手順は、レポートを選択する手順と同じです。 パーソナライズ [されたレポートを参照し](#personalized-reports)。

## 赤帽 {#red-hat}

すぐに使用できるスキーマがv6.02またはv5.11で削除されている場合は、アップグレード後にスキーマを編集できなくなる可能性があります。 この場合は、次のコマンドを実行します。

```
su - neolane
nlserver config -postupgrade -instance:<instance name> -force
```
