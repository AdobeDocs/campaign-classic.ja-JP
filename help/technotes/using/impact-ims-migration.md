---
title: IMS 移行後の Campaign インターフェイスの更新
description: Identity Management System migration Interface のAdobeの影響を有効にする方法を説明します
source-git-commit: ab1bb91bdbc9961b4f3f0feba7cfd354b02b6511
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 4%

---

# IMS 移行後の Campaign インターフェイスの更新 {#impact-ims-migration}

一度身に着ければ [campaign テクニカルオペレーターを開発者コンソールに移行しました](ims-migration.md) および [エンドユーザー認証用に IMS に移行](migrate-users-to-ims.md)最後の手順は、ユーザーインターフェイスと API 制限を有効にして、ネイティブ認証に固有のオプションと機能を削除することです。 この更新は、Campaign v7.4.1 以降で利用できます。

## IMS 制限の有効化 {#ims-restrictions}

AdobeIMS （Identify Management System）への移行を完了するには、ネイティブ・オペレーターの新しいネイティブ・ユーザーの作成、ネイティブ・ユーザー・ログイン、および API アクセスをブロックする必要があります。 これにより、環境が保護され、標準化されます。

管理対象Cloud Service/ホステッド環境のユーザーとして、この制限を有効にするには、Adobeにお問い合わせください。また、関連する更新が製品ユーザーインターフェイスで行われます。

オンプレミス/ハイブリッドユーザーは、次の手順に従います。

1. を参照してください。 `<imsConfig>` インスタンス設定ファイルの「」セクション。
1. UI 制限を有効にするには、 `nonIMSOperatorMgmtInClientConsoleRestricted` オプション、内部 `nonIMSOperatorMgmtInClientConsole` 要素、終了#セツメイ# `true`を次のように設定します。


   ```xml
   <serverConf>
   <shared>
       <imsConfig>
           <nonIMSOperatorMgmtInClientConsole nonIMSOperatorMgmtInClientConsoleRestricted="true"/>
       </imsConfig>
   </shared>
   </serverConf>
   ```

1. API 制限を有効にするには、 `disableAPI` オプション、内部 `nonIMSAuthnAPI` 要素、終了#セツメイ# `true`を次のように設定します。

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

いくつかの演算子は、ネイティブ認証を使用してAdobe Campaignに接続できます。 これらのテクニカルオペレーターはデフォルトで有効になっており、変更しないでください。 この例外を許可するために、これらのテクニカルオペレーターは、デフォルトで許可リストに追加されます。 このリストは、 `<imsConfig>` インスタンス設定ファイルの「」セクション `allowOperator` オプション内部 `nonIMSAuthnAPI` 要素。

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

許可リストに演算子を追加する必要がある場合は、新しい `allowOperator` 演算子の名前を持つ要素。 例えば、という名前で新しい演算子を追加する場合 `test`この節を更新する手順は次のとおりです。

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

移行が完了し、以下に説明するように制限が適用されると、製品とそのユーザーインターフェイスに次の変更が適用されます。

### オペレーターの管理 {#manage-admin}

クライアントコンソールからネイティブ認証を使用してオペレーターを作成、編集、更新、削除できなくなりました。

そのため、これらのアクションはクライアントコンソールで無効になっています。

オペレーターの管理はAdobe Admin Consoleで一元化されており、現在、次のタスクはこのコンソールでのみ管理できます。 でユーザーを作成し、権限を割り当てる方法を説明します [Campaign v8 ドキュメント](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/admin/permissions/manage-permissions){target="_blank"}.

### 使用できないオプション {#unavailable-migration}

移行後、次のタスクはクライアントコンソールで使用できなくなります。

* の使用 [選択した行を結合オプション](../../platform/using/updating-data.md#merge-data) 演算子を結合します。

* オペレーターの次のフィールドを更新します。
   * 名前
   * パスワード
   * ラベル
   * メール

* [Campaign パスワードのリセット](../../production/using/lost-password.md)

* 演算子の XML ソースを編集

* 演算子が重複しています。


>[!MORELIKETHIS]
>
>* [エンドユーザーの IMS への移行](migrate-users-to-ims.md)
>* [Adobe Developer コンソールへのテクニカルオペレーターの移行](ims-migration.md)
>* [Adobe Campaign Classic v7 の最新のリリースノート](../../rn/using/latest-release.md)
>* [Adobe Identity Management System（IMS）とは](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}

