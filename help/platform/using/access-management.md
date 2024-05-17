---
product: campaign
title: 権限の基本を学ぶ
description: Campaign 機能へのアクセスを許可する方法について説明します。
badge: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Access Management, Permissions
exl-id: 9b616715-33cd-43ba-8548-8d96a179408e
source-git-commit: e1a085384fb27ec165c487c112fbc70fe9738d9e
workflow-type: ht
source-wordcount: '342'
ht-degree: 100%

---

# 権限の基本を学ぶ{#access-management}


>[!CAUTION]
>
>Campaign Classic v7.3.1 以降、すべてのオペレーターは、[Adobe Identity Management System（IMS）](https://helpx.adobe.com/jp/enterprise/using/identity.html){target="_blank"}を使用して Campaign に接続する必要があります。
>
>セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、既存のすべてのオペレーター認証モードをログイン／パスワードのネイティブ認証から Adobe Identity Management System（IMS）に移行することを強くお勧めします。オペレーターを移行する方法については、[このページ](../../technotes/using/migrate-users-to-ims.md)を参照してください。
> 
>この移行後は、次の節は適用されないことに注意してください。Adobe IMS を使用して権限を設定する方法については、[Campaign v8 ドキュメント](https://experienceleague.adobe.com/docs/campaign/campaign-v8/admin/permissions/gs-permissions.html?lang=ja){target="_blank"}を参照してください。


Adobe Campaign は、様々なオペレーターに割り当てる一連の権利を定義したり、管理したりするのに役立ちます。以下の操作は、それらの権利に基づいて承認または拒否されます。

* 特定種類の機能に対するアクセス（ネームド権限など）
* 特定種類のレコードに対するアクセス
* レコード（アクション、連絡先、キャンペーン、グループなど）の作成、変更または削除

権限は、オペレーターのプロファイルまたはオペレーターグループに付与されます。

これらの操作は、オペレーターの Adobe Campaign に対する接続モードにリンクされた安全パラメーターに基づいて実行されます。セキュリティゾーンの詳細については、[こちらのページ](../../installation/using/security-zones.md)を参照してください。

ユーザーに付与できる権限には次の 2 種類があります。

* グループを使用する場合は、権利の付与対象とするオペレーターのグループを定義し、オペレーターを 1 つまたは複数のグループに関連付けます。これにより、権利を再利用することや、複数のオペレーターに一貫性の高いプロファイルを設定することができます。また、プロファイルの管理やメンテナンスをおこなううえでも便利な方法です。グループの作成と管理については、[こちらの節](access-management-groups.md)を参照してください。

* ネームド権限は、ユーザーに対して直接付与することができ、場合によっては、グループ経由で割り当てられた権限をオーバーロードすることもできます。 これらの権利については、[こちらのページ](access-management-named-rights.md)を参照してください。

>[!NOTE]
>
>権限の定義を開始する前に、[セキュリティ設定チェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)に目を通すことをお勧めします。

これらの節では、アクセスの許可および権限の設定方法について説明します。

* [オペレーターの作成](access-management-operators.md)

* [グループの定義](access-management-groups.md)

* [ネームド権限の追加](access-management-named-rights.md)

* [キャンペーンフォルダーへのアクセスの管理](access-management-folders.md)

* [アクセス権マトリックス](access-management-named-rights.md#access-rights-matrix)


関連トピック：

* [ワークフローの権限管理](../../workflow/using/managing-rights.md)
* [分散型マーケティングの権限管理](../../distributed/using/about-distributed-marketing.md#operators-and-entities)
* [インタラクションモジュールの権限管理](../../interaction/using/operator-profiles.md)
* [スキーマへのアクセスのフィルタリング](../../configuration/using/filtering-schemas.md)
* [個人情報表示の制限](../../configuration/using/restricting-pii-view.md)
