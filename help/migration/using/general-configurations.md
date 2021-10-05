---
product: campaign
title: 一般設定
description: 一般設定
audience: migration
content-type: reference
topic-tags: configuration
exl-id: 7aad0e49-8d9c-40c7-9d6a-42fee0ae5870
source-git-commit: eef2a12738ce299686857720c3dc8456ffdd0c80
workflow-type: tm+mt
source-wordcount: '2719'
ht-degree: 2%

---

# 一般設定{#general-configurations}

![](../../assets/v7-only.svg)

この節では、v5.11 または v6.02 から移行する場合にAdobe Campaign v7 で実行する設定について詳しく説明します。

さらに、次の点に注意してください。

* v5.11 から移行する場合は、 [v5.11 の特定の設定 ](../../migration/using/specific-configurations-in-v5-11.md) の節で詳しく説明されている設定も完了する必要があります。
* v6.02 から移行する場合は、 [v6.02](../../migration/using/specific-configurations-in-v6-02.md) の特定の設定の節で説明されている設定も完了する必要があります。

## タイムゾーン {#time-zones}

### マルチタイムゾーンモード {#multi-time-zone-mode}

v6.02 では、「マルチタイムゾーン」モードは PostgreSQL データベースエンジンでのみ使用できました。 どのタイプのデータベースエンジンを使用しても、提供されるようになりました。 ベースを「マルチタイムゾーン」ベースに変換することを強くお勧めします。

TIMESTAMP WITH TIMEZONE モードを使用するには、**-userTimestamptz:1** オプションを postupgrade コマンドラインに追加する必要もあります。

>[!IMPORTANT]
>
>**-usetimestamptz:1** パラメータが互換性のないデータベースエンジンで使用されている場合、データベースは破損し、データベースのバックアップを復元し、上記のコマンドを再実行する必要があります。

>[!NOTE]
>
>移行後に、コンソール（**[!UICONTROL 管理/プラットフォーム/オプション/ WdbcTimeZone]** ノード）を使用してタイムゾーンを変更できます。
>
>タイムゾーン管理について詳しくは、[ この節 ](../../installation/using/time-zone-management.md) を参照してください。

### Oracle {#oracle}

アップグレード後に **ORA 01805** エラーが発生した場合は、アプリケーションサーバーとデータベースサーバーの間のOracleタイムゾーンファイルが同期されていません。 再同期するには、次の手順に従います。

1. 使用するタイムゾーンファイルを識別するには、次のコマンドを実行します。

   ```
   select * from v$timezone_file
   ```

   タイムゾーンファイルは通常、**ORACLE_HOME/oracle/zoneinfo/** フォルダーにあります。

1. タイムゾーンファイルが両方のサーバーで同じであることを確認します。

詳しくは、以下を参照してください。[https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004](https://docs.oracle.com/cd/E11882_01/server.112/e10729/ch4datetime.htm#NLSPG004).

クライアントとサーバーの間のタイムゾーンのずれが原因で、エラーが発生する場合もあります。 そのため、クライアント側とサーバー側で同じバージョンのOracleライブラリを使用することをお勧めします。両方のタイムゾーンは同じにする必要があります。

両方の辺が同じタイムゾーンにあるかどうかを確認するには：

1. 次のコマンドを実行して、クライアント側のタイムゾーンファイルのバージョンを確認します。

   ```
   genezi -v
   ```

   genezi は、**$ORACLE_HOME/bin** リポジトリにあるバイナリです。

1. 次のコマンドを実行して、サーバー側のタイムゾーンファイルのバージョンを確認します。

   ```
   select * from v$timezone_file
   ```

1. クライアント側のタイムゾーンファイルを変更するには、環境変数 **ORA_TZFILE** を使用します。

## セキュリティ {#security}

### セキュリティゾーン {#security-zones}

>[!IMPORTANT]
>
>セキュリティ上の理由により、Adobe Campaignプラットフォームは、デフォルトではアクセスできなくなりました。セキュリティゾーンを設定し、オペレーターの IP アドレスを収集する必要があります。

Adobe Campaign v7 には、**セキュリティゾーン** の概念が含まれます。 インスタンスにログオンするには、各ユーザーがゾーンに関連付けられている必要があり、ユーザーの IP アドレスがセキュリティゾーンで定義されたアドレスまたはアドレス範囲に含まれている必要があります。 セキュリティゾーンの設定は、Adobe Campaignサーバー設定ファイルでおこなえます。 ユーザーが関連付けられているセキュリティゾーンは、コンソール（**[!UICONTROL 管理/アクセス管理/オペレーター]**）で定義する必要があります。

**移行する前に**、ネットワーク管理者に問い合わせて、移行後にアクティブ化するセキュリティゾーンを定義してください。

**アップグレード後** （サーバーを再起動する前）に、セキュリティゾーンを設定する必要があります。

セキュリティゾーンの設定は、[ このセクション ](../../installation/using/security-zones.md) にあります。

### ユーザーパスワード {#user-passwords}

v7 では、**内部** および **管理** 演算子の接続はパスワードで保護する必要があります。 移行前に、これらのアカウントとすべてのオペレーターアカウントにパスワードを割り当てることを強くお勧めします。******内部** のパスワードを指定していない場合、接続できません。 **内部** にパスワードを割り当てるには、次のコマンドを入力します。

```
nlserver config -internalpassword
```

>[!IMPORTANT]
>
>**内部** パスワードは、すべてのトラッキングサーバーで同じにする必要があります。 詳しくは、[ この節 ](../../installation/using/configuring-campaign-server.md#internal-identifier) と [ この節 ](../../platform/using/access-management.md) を参照してください。

### v7 の新機能 {#new-features-in-v7}

* 権限を持たないユーザーは、Adobe Campaignに接続できなくなりました。 権限は、例えば **connect** という名前の権限を作成して、手動で追加する必要があります。

   この変更の影響を受けたユーザーは、アップグレード後に特定され、リストに表示されます。

* パスワードが空の場合、追跡は機能しなくなりました。 その場合は、エラーメッセージが表示され、再設定を求められます。
* ユーザーのパスワードは、 **xtk:sessionInfo** スキーマに保存されなくなりました。
* **xtk:builder:EvaluateJavaScript** 関数と **xtk:builder:EvaluateJavaScriptTemplate** 関数を使用するには、管理権限が必要になりました。

あらかじめ用意されている特定のスキーマが変更され、デフォルトで **admin** 権限を持つオペレーターの書き込みアクセス権でのみアクセスできるようになりました。

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

### Sessiontoken パラメーター {#sessiontoken-parameter}

v5 では、**sessiontoken** パラメーターはクライアント側（概要タイプの画面のリスト、リンクエディターなど）で およびサーバー側（web アプリケーション、レポート、jsp、jssp など） v7 では、サーバー側でのみ機能します。 v5 と同様にすべての機能に戻る場合は、このパラメーターを使用してリンクを変更し、接続ページを渡す必要があります。

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
>信頼できる IP マスクにリンクされたオペレーターを使用する場合は、オペレーターに最小限の権限が付与され、**sessionTokenOnly** モードのセキュリティゾーンにあることを確認します。

### SQL 関数 {#sql-functions}

不明な SQL 関数呼び出しは、サーバーに自然に送信されなくなりました。 現在、すべての SQL 関数を **xtk:funcList** スキーマに追加する必要があります（詳しくは、[ この節 ](../../configuration/using/adding-additional-sql-functions.md) を参照してください）。 移行時に、アップグレード後にオプションが追加され、古い宣言されていない SQL 関数との互換性を維持できます。 これらの関数を引き続き使用する場合は、**XtkPassUnknownSQLFunctionsToRDBMS** オプションが **[!UICONTROL 管理/プラットフォーム/オプション]** ノードレベルで定義されていることを確認します。

>[!IMPORTANT]
>
>セキュリティ上のリスクがあるので、このオプションの使用は強くお勧めしません。

### JSSP {#jssp}

（HTTPS ではなく）HTTP プロトコルを使用して特定のページへのアクセスを許可する場合は、Web アプリで、例えば、セキュリティゾーンでの設定に関係なく、対応するリレールールで **httpAllowed=&quot;true&quot;** パラメーターを指定する必要があります。

匿名 JSSP を使用する場合、JSSP（**[!UICONTROL serverConf.xml]** ファイル）のリレールールに **httpAllowed=&quot;true&quot;** パラメーターを追加する必要があります。

例：

```
<url IPMask="" deny="" hostMask="" httpAllowed="true" relayHost="true" relayPath="true"
           status="blacklist" targetUrl="https://localhost:8080" timeout="" urlPath="*/cus/myPublicPage.jssp"/>
```

## 構文 {#syntax}

### JavaScript {#javascript}

Adobe Campaign v7 は、より新しい JavaScript インタープリターを統合します。 ただし、この更新により、特定のスクリプトが正常に機能しなくなる場合があります。 前のエンジンはもっと許容的だったので、特定の構文は機能し、エンジンの新しいバージョンとは異なります。

**[!UICONTROL myObject。@attribute]** 構文は、XML オブジェクトに対してのみ有効です。 この構文は、配信とコンテンツ管理をパーソナライズする場合に使用します。 このタイプの構文を XML 以外のオブジェクトで使用した場合、パーソナライゼーション機能は機能しなくなります。

その他のすべてのオブジェクトタイプでは、構文は **[!UICONTROL myObject`[`&quot;attribute&quot;`]`]** になりました。 例えば、次の構文を使用した非 XML オブジェクトがあるとします。**[!UICONTROL 従業員@sn]**。次の構文を使用する必要があります。**[!UICONTROL employee`[`&quot;sn&quot;`]`]**.

* 以前の構文：

   ```
   employee.@sn
   ```

* 新しい構文：

   ```
   employee["sn"]
   ```

XML オブジェクトの値を変更するには、XML ノードを追加する前に値を更新して開始する必要があります。

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

インスタンスのセキュリティを強化するために、SQLData に基づく構文を置き換える新しい構文がAdobe Campaign v7 で導入されました。 この構文でこれらのコード要素を使用する場合は、変更する必要があります。 主な要素は次のとおりです。

* サブクエリによるフィルタリング：新しい構文は、サブクエリを定義する `<subQuery>` 要素に基づいています
* 集計：新しい構文は、「集計関数（コレクション）」です。
* 結合によるフィルタ：新しい構文は `[schemaName:alias:xPath]` です。

queryDef (xtk:queryDef) スキーマが変更されました。

* 新しい `<subQuery>` 要素は、SQLData に含まれる SELECT を置き換えるために使用できます。
* @setOperator属性に、「IN」と「NOT IN」の 2 つの新しい値が追加されました。
* 新しい `<where>` 要素（`<node>` 要素の子）:これにより、SELECT で「サブ選択」を作成できます。

「@expr」属性を使用すると、SQLData が存在する場合があります。 次の用語の検索を実行できます。&quot;SQLData&quot;, &quot;aliasSqlTable&quot;, &quot;sql&quot;.

Adobe Campaign v7 インスタンスは、デフォルトで保護されます。 セキュリティは、**[!UICONTROL serverConf.xml]** ファイルのセキュリティゾーンの定義に基づいています。**allowSQLInjection** 属性は、SQL 構文セキュリティを管理します。

アップグレード後の実行中に SQLData エラーが発生した場合は、この属性を変更して、SQLData ベースの構文を一時的に使用できるようにし、コードの書き換えを可能にする必要があります。 これをおこなうには、**serverConf.xml** ファイルで次のオプションを変更する必要があります。

```
allowSQLInjection="true"
```

そのため、次のコマンドを使用してアップグレード後に再起動します。

```
nlserver config -postupgrade -instance:<instance_name> -force
```

セキュリティゾーンを設定（[ セキュリティ ](#security) を参照）してから、次のオプションを変更してセキュリティを再アクティブ化する必要があります。

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
   >ジョイントは集計関数に対して自動的に実行されます。 条件 WHERE O0.iOperationId=iOperationId を指定する必要はなくなりました。
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

エイリアスはオプションです。

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

`<subQuery>` 要素で、メイン `<queryDef>` の「field」フィールドを参照します。   要素には、次の構文を使用します。`[../@field]`

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

移行はポストアップグレードを通じて実行され、レポート、フォーム、Web アプリケーションに競合が表示される場合があります。 これらの競合はコンソールから解決できます。

リソースの同期後に、**postupgrade** コマンドを使用して、同期でエラーまたは警告が発生したかどうかを検出できます。

### 同期結果の表示 {#view-the-synchronization-result}

同期結果は、次の 2 つの方法で表示できます。

* コマンドラインインターフェイスでは、エラーは 3 重の山形記号 **>>** で実現され、同期は自動的に停止されます。 警告は二重山括弧 **>** で示され、同期が完了したら解決する必要があります。 ポストアップグレードの最後に概要がコマンドプロンプトで表示されます。例：

   ```
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     =========Summary of the update==========
   2013-04-09 07:48:39.749Z        00002E7A          1     info    log     test instance, 6 warning(s) and 0 error(s) during the update.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'mobileAppDeliveryFeedback' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.749Z        00002E7A          1     warning log     The document with identifier 'opensByUserAgent' and type 'xtk:report' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     The document with identifier 'deliveryValidation' and type 'nms:webApp' is in conflict with the new version.
   2013-04-09 07:48:39.750Z        00002E7A          1     warning log     Document of identifier 'nms:includeView' and type 'xtk:srcSchema' updated in the database and found in the file system. You will have to merge the two versions manually.
   ```

   リソースの競合に関する警告が表示された場合は、解決に向けてオペレーターの注意が必要です。

* **postupgrade_`<server version number>`_time of postupgrade`>`.log** ファイルには同期結果が含まれます。 デフォルトでは、次のディレクトリで使用できます。**インストールディレクトリ/var/`<instance>` ポストアップグレード**。 エラーと警告は、**error** および **warning** 属性で示されます。

### 競合の解決 {#resolve-a-conflict}

競合の解決は、上級オペレーターと、「管理者」権限を付与されたオペレーターのみが実行する必要があります。

競合を解決するには、次の手順に従います。

1. Adobe Campaignツリー構造で、**[!UICONTROL 管理/設定/パッケージ管理/競合を編集]** の上にカーソルを置きます。
1. リストで解決する競合を選択します。

競合を解決する方法は 3 つあります。

* **[!UICONTROL 解決済みとして宣言]**:事前にオペレーターの介入が必要です。
* **[!UICONTROL 新しいバージョンを受け入れる]**:Adobe Campaignで提供されるリソースがユーザーによって変更されていない場合に推奨されます。
* **[!UICONTROL 現在のバージョンを保持]**:は、更新が拒否されたことを示します。

   >[!IMPORTANT]
   この解決モードを選択すると、新しいバージョンのパッチが失われるおそれがあります。 したがって、このオプションは、エキスパートオペレーターにのみ使用または予約しないことを強くお勧めします。

競合を手動で解決する場合は、次の手順に従います。

1. ウィンドウの下部のセクションで **`_conflict_ string`** を検索し、競合するエンティティを探します。 新しいバージョンでインストールされたエンティティには **new** 引数が含まれ、前のバージョンに一致するエンティティには **cus** 引数が含まれます。

   ![](assets/s_ncs_production_conflict002.png)

1. 保持しないバージョンを削除します。 保持するエンティティの **`_conflict_argument_ string`** を削除します。

   ![](assets/s_ncs_production_conflict003.png)

1. 解決した競合に移動します。 **[!UICONTROL アクション]**&#x200B;アイコンをクリックし、「**[!UICONTROL 解決済みとして宣言]**」を選択します。
1. 変更を保存します。これにより競合が解決します。

## Tomcat {#tomcat}

Adobe Campaign v7 の統合 Tomcat サーバーのバージョンが変更されました。 したがって、インストールフォルダ (tomcat-6) も変更されました (tomcat 7)。 アップグレード後は、パスが（**[!UICONTROL serverConf.xml]** ファイル内の）更新済みフォルダーにリンクされていることを確認します。

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

**アップグレード後**&#x200B;は、v7 に存在しなくなる 6.02 のすべてのスキーマ参照を削除する必要があります。

* nms:emailOfferView
* nms:webOfferView
* nms:callCenterOfferView
* nms:mobileOfferView
* nms:paperOfferView

### オファーコンテンツ {#offer-content}

v7 では、オファーコンテンツが移動されました。 v6.02 では、コンテンツは各表現スキーマ (**nms:emailOfferView**) に含まれていました。 v7 では、コンテンツはオファースキーマに含まれます。 アップグレード後は、コンテンツがインターフェイスに表示されなくなります。 アップグレード後に、オファーコンテンツを再作成するか、表示スキーマからオファースキーマにコンテンツを自動的に移動するスクリプトを作成する必要があります。

>[!IMPORTANT]
移行後に、設定済みオファーを使用する一部の配信が送信される場合は、v7 でこれらの配信をすべて削除して再作成する必要があります。 それができない場合は、「互換モード」が提供されます。 インタラクション v7 のすべての新機能のメリットが得られるわけではないので、このモードはお勧めしません。 これは、実際の 6.1 移行前に継続中のキャンペーンを完了できる移行モードです。 このモードの詳細については、お問い合わせください。

移動スクリプトの例 (**interactionTo610_full_XX.js**) は、Adobe Campaign v7 フォルダー内の **Migration** フォルダーにあります。 このファイルは、1 つのオファーにつき 1 つの電子メール表現（**[!UICONTROL htmlSource]** フィールドと **[!UICONTROL textSource]** フィールド）を使用するクライアントのスクリプトの例を示しています。 **NmsEmailOfferView** テーブル内の内容が、オファーテーブルに移動されました。

>[!NOTE]
このスクリプトを使用しても、「コンテンツ管理」および「レンダリング関数」オプションを利用できません。 これらの機能を活用するには、カタログオファー、特にオファーコンテンツと設定スペースを考え直す必要があります。

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

環境が 1 つのみの場合は、オファーコンテンツを移動した後に実行する手順を以下に示します。 この場合、「ENV」を例に取り上げます。

1. すべての「ENV」環境オファースペースで、使用するフィールドのリストを更新します。 例えば、**[!UICONTROL htmlSource]** のみを使用するオファースペースの場合、**[!UICONTROL view/htmlSource]** を追加する必要があります。

   ![](assets/migration_interaction_2.png)

1. 「**[!UICONTROL 一般]**」タブ内の「**[!UICONTROL 環境のタイプ]**」フィールドで、「**[!UICONTROL ライブ]**」を選択します。

   ![](assets/migration_interaction_3.png)

1. デザイン環境（例：「ENV_DESIGN」）を作成し、ENV オンライン環境に接続します。

   ![](assets/migration_interaction_4.png)

1. すべての「ENV」環境オファースペースをデプロイ（右クリック > **[!UICONTROL アクション > デプロイ]**）し、「ENV_DESIGN」環境を選択します。

   ![](assets/migration_interaction_5.png)

1. すべての「ENV」環境オファーに対しても同じ操作を行います。
1. 関連するチャネルですべての環境オファー「ENV_DESIGN」をアクティベートします。
1. オファーをライブにするテスト。 問題が発生しない場合は、最新のワークフロータスク **[!UICONTROL オファー通知]**(offerMgt) で保留中のタスクを実行して、すべてのオファーをライブにします。

   ![](assets/migration_interaction_6.png)

1. 包括的なテストを実行します。

   >[!NOTE]
   オンラインでのカテゴリとオファーの名前は、運用開始後に変更されます。 受信チャネルで、オファーとカテゴリへの参照をすべて更新します。

## レポート {#reports}

### 標準レポート {#standard-reports}

現在、すべての標準レポートでレンダリングエンジン v6.x が使用されています。これらのレポートに JavaScript を追加した場合、一部の要素が機能しなくなる可能性があります。 実際、古いバージョンの JavaScript は v6.x のレンダリングエンジンと互換性がありません。 そのため、JavaScript コードを確認し、後で適応させる必要があります。 すべてのレポート、特にエクスポート機能をテストする必要があります。

### パーソナライズされたレポート {#personalized-reports}

<!--If you want to have the blue banner from v7 (allowing you access to the tabs), you must republish reports. If you encounter problems, you can force the v6.0 rendering engine. To do this, go to **[!UICONTROL Properties]** within the report, click **[!UICONTROL Rendering]** and choose the **[!UICONTROL Version 6.0 (Flash & OpenOffice)]** rendering engine.

![](assets/migration_reports_1.png)
-->
新しいレポート機能を活用したい場合は、レポートを再公開する必要があります。 この場合は、すべてのスクリプトを確認し、必要に応じて変更します。 PDF エクスポートに関しては、Open Office 用の特定のスクリプトを追加した場合、新しい PDF エクスポートエンジン (PhantomJS) では動作しなくなります。

## web アプリケーション {#web-applications}

次の 2 つの Web アプリケーションファミリーがあります。

* 特定された web アプリケーション（まとめて表示、承認フォーム、外部内部開発）
* 匿名の web アプリケーション（web またはアンケートフォーム）

### 識別された Web アプリケーション {#identified-web-applications}

レポート（[ 詳細 ](#reports)）と同様に、JavaScript を追加した場合は、必要に応じて確認し、適応する必要があります。 v7 の青いバナー（青いタブを含む）のメリットを受けたい場合は、Web アプリケーションを再公開する必要があります。

Web アプリケーションの接続方法は、v7 で変更されました。 識別された Web アプリケーションで接続の問題が発生した場合は、**serverConf.xml** ファイルの **allowUserPassword** オプションと **sessionTokenOnly** オプションを一時的に有効にする必要があります。 アップグレード後に、次のオプション値を変更します。

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

## Red-Hat {#red-hat}

標準のスキーマが v6.02 または v5.11 で削除された場合、ポストアップグレード後にスキーマを編集できなくなる可能性があります。 これが発生した場合は、次のコマンドを実行します。

```
su - neolane
nlserver config -postupgrade -instance:<instance name> -force
```
