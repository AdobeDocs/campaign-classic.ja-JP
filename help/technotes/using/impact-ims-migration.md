---
title: IMS 移行後の Campaign インターフェイスの更新
description: Adobe Identity Management System 移行インターフェイスの影響をアクティブ化する方法について説明します
exl-id: 8b13fe4d-d8d3-43b3-bbe4-c8c5574f585a
source-git-commit: 8eadea9f9cc0a44522726024bfbc825e3b4cad98
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 100%

---

# IMS 移行後の Campaign インターフェイスの更新 {#impact-ims-migration}

[Campaign テクニカルオペレーターを Developer Console に移行](ims-migration.md)し、[エンドユーザー認証用に IMS に移行](migrate-users-to-ims.md)したら、最後の手順として、ユーザーインターフェイスと API の制限を有効にして、ネイティブ認証に固有のオプションと機能を削除します。この更新は、Campaign v7.4.1 以降で使用できます。

## IMS 制限を有効にする {#ims-restrictions}

Adobe Identify Management System（IMS）への移行を完了するには、新規ネイティブユーザーの作成、ネイティブユーザーのログイン、ネイティブオペレーターの API アクセスをブロックする必要があります。これにより、環境が保護され、標準化されます。

Managed Cloud Service／ホスト環境のユーザーの場合は、アドビに連絡して、この制限と製品ユーザーインターフェイスの関連する更新を有効にします。

オンプレミス環境／ハイブリッド環境のユーザーの場合は、次の手順に従います。

1. インスタンス設定ファイルの `<imsConfig>` セクションを参照します。
1. UI の制限を有効にするには、次のように、`nonIMSOperatorMgmtInClientConsole` 要素内の `nonIMSOperatorMgmtInClientConsoleRestricted` オプションを `true` に更新します。


   ```xml
   <serverConf>
   <shared>
       <imsConfig>
           <nonIMSOperatorMgmtInClientConsole nonIMSOperatorMgmtInClientConsoleRestricted="true"/>
       </imsConfig>
   </shared>
   </serverConf>
   ```

1. API の制限を有効にするには、次のように、`nonIMSAuthnAPI` 要素内の `disableAPI` オプションを `true` に更新します。

   ```xml
   <serverConf>
   <shared>
       <imsConfig>
           <nonIMSAuthnAPI disableAPI="true">
               ...
           </nonIMSAuthnAPI>
       </imsConfig>
   </shared>
   </serverConf>
   ```

一部のオペレーターは、ネイティブ認証を使用して Adobe Campaign に接続することを許可されています。これらのテクニカルオペレーターは、デフォルトで有効になっており、変更できません。この例外を許可するために、これらのテクニカルオペレーターは、デフォルトで許可リストに追加されます。このリストは、インスタンス設定ファイルの `<imsConfig>` セクションの `nonIMSAuthnAPI` 要素内の `allowOperator` オプションにあります。

```xml
<serverConf>
  <shared>
    <imsConfig>
        <nonIMSAuthnAPI disableAPI="true">
            <allowOperator name="admin"/>
            <allowOperator name="aemserver"/>
            <allowOperator name="campaign-loginmonitor"/>
            <allowOperator name="internal|monitoring"/>
        </nonIMSAuthnAPI>
    </imsConfig>
  </shared>
</serverConf>
```

許可リストにオペレーターを追加する必要がある場合は、オペレーターの名前を指定した新しい `allowOperator` 要素を追加します。例えば、`test` という名前の新しいオペレーターを追加する場合は、このセクションを次のように更新します。

```xml
<serverConf>
  <shared>
    <imsConfig>
        <nonIMSAuthnAPI disableAPI="true">
            <allowOperator name="admin"/>
            <allowOperator name="aemserver"/>
            <allowOperator name="campaign-loginmonitor"/>
            <allowOperator name="internal|monitoring"/>
            <allowOperator name="test"/>
        </nonIMSAuthnAPI>
    </imsConfig>
  </shared>
</serverConf>
```

## ユーザーインターフェイスへの影響 {#ims-impacts}

移行が完了し、以下に説明する制限が適用されると、製品とそのユーザーインターフェイスに次の変更が適用されます。

### オペレーター管理 {#manage-admin}

クライアントコンソールからネイティブ認証を使用してオペレーターを作成、編集、更新、削除できなくなりました。

その結果、これらのアクションはクライアントコンソールで無効になりました。

オペレーターの管理は Adobe Admin Console に一元化されて、次のタスクはこのコンソールを通じてのみ管理されるようになりました。ユーザーを作成し、権限を割り当てる方法については、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/admin/permissions/manage-permissions){target="_blank"}を参照してください。

### 使用できないオプション {#unavailable-migration}

移行後、クライアントコンソールで次のタスクは使用できなくなります。

* [「選択した行を結合」オプション](../../platform/using/updating-data.md#merge-data)を使用して、オペレーターを結合。

* オペレーターの次のフィールドを更新：
   * 名前
   * パスワード
   * ラベル
   * メール

* [Campaign パスワードをリセット](../../production/using/lost-password.md)

* オペレーターの XML ソースを編集

* オペレーターを複製。


>[!MORELIKETHIS]
>
>* [エンドユーザーの IMS への移行](migrate-users-to-ims.md)
>* [Adobe Developer Console へのテクニカルオペレーターの移行](ims-migration.md)
>* [Adobe Campaign Classic v7 最新リリースノート](../../rn/using/latest-release.md)
>* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}
