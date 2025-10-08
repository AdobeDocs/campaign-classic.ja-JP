---
product: campaign
title: 権限の基本を学ぶ
description: Campaign 機能へのアクセスを許可する方法について説明します。
badge: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Access Management, Permissions
exl-id: 9b616715-33cd-43ba-8548-8d96a179408e
source-git-commit: a5bbd2e6c102a8afa4cd5931b77b0c83705a7bfa
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 65%

---

# 権限の基本を学ぶ{#access-management}


>[!CAUTION]
>
>Campaign Classic v7.3.1 以降、すべてのオペレーターは、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}を使用して Campaign に接続する必要があります。
>
>セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、既存のすべてのオペレーター認証モードをログイン／パスワードのネイティブ認証から Adobe Identity Management System（IMS）に移行することを強くお勧めします。オペレーターを移行する方法については、[このページ](../../technotes/using/migrate-users-to-ims.md)を参照してください。
> 
>この移行後は、次の節が適用されないことに注意してください。Adobe IMS を使用して権限を設定する方法については、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/gs-permissions.html?lang=ja){target="_blank"}を参照してください。


Adobe Campaign は、様々なオペレーターに割り当てる一連の権利を定義したり、管理したりするのに役立ちます。以下の操作は、それらの権利に基づいて承認または拒否されます。

* 特定種類の機能に対するアクセス（ネームド権限など）
* 特定種類のレコードに対するアクセス
* レコード（アクション、連絡先、キャンペーン、グループなど）の作成、変更または削除

>[!BEGINTABS]

>[!TAB 権限に関するドキュメント]

**Campaign の権限** について詳しくは、**[Adobe Campaign v8 （コンソール）ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/admin/permissions/gs-permissions?lang=ja#_blank){target=_blank}** を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/admin/permissions/gs-permissions?lang=ja#_blank){target=_blank}


>[!TAB  フォルダーに対する権限の管理 ]

**フォルダーに対する権限** を定義する方法については、**[Campaign v8 （コンソール）ドキュメント ](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/admin/permissions/folder-permissions){target=_blank}** を参照してください。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](https://experienceleague.adobe.com/ja/docs/campaign/campaign-v8/admin/permissions/folder-permissions){target=_blank}


>[!TAB  ネイティブ認証 ]

Campaign v7 では、引き続き、ログイン/パスワードを使用したネイティブ認証も使用できますが、セキュリティと認証プロセスを強化するために、Adobe Campaignでは、ネイティブ認証からAdobe Identity Management System （IMS）に [ エンドユーザー認証モードを移行 ](../../technotes/using/ac-ims.md) することを強くお勧めします。 Campaign v8 では、ネイティブ認証を使用してに接続することはできません。

[![画像](../../assets/do-not-localize/learn-more-button.svg)](../../technotes/using/ac-ims.md)


>[!ENDTABS]



<!--
The permissions apply to operator profiles or operator groups.

They are completed by safety parameters linked to the operator's connection mode to Adobe Campaign. For more about security zones in [this page](../../installation/using/security-zones.md).

There are two types of permissions you can grant to a user:

* You can define groups of operators to which you attribute rights, then associate the operators with one or more groups. This enables you to reuse rights and make operator profiles more consistent. It also facilitates the management and maintenance of profiles. Group creation and management are presented in [this section](access-management-groups.md).

* You can attribute named rights directly to users, in some cases to overload the rights allocated via groups. These rights are presented in [this page](access-management-named-rights.md).

>[!NOTE]
>
> * Before starting defining permissions, Adobe recommends you to read the [Security configuration checklist](https://helpx.adobe.com/campaign/kb/acc-security.html).
> * To learn more about permissions, please refer to the detailed explanation on the [Campaign v8 documentation](https://experienceleague.adobe.com/en/docs/campaign/campaign-v8/admin/permissions/gs-permissions){target=_blank}.

Learn how to grant access and set up permissions in these sections:

* [Create operators](access-management-operators.md)

* [Define groups](access-management-groups.md)

* [Add Named rights](access-management-named-rights.md)

* [Manage Campaign folder access](access-management-folders.md)

* [Access rights matrix](access-management-named-rights.md#access-rights-matrix)


See also:

* [Manage permissions for workflows](../../workflow/using/managing-rights.md)
* [Manage permissions for distributed marketing](../../distributed/using/about-distributed-marketing.md#operators-and-entities)
* [Manage permissions for the interaction module](../../interaction/using/operator-profiles.md)
* [Filter access to schemas](../../configuration/using/filtering-schemas.md)
* [Restricting PI view](../../configuration/using/restricting-pii-view.md)
-->