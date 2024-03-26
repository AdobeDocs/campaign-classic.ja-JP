---
product: campaign
title: 権限の基本を学ぶ
description: Campaign 機能へのアクセスを許可する方法について説明します。
badge: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
feature: Access Management, Permissions
exl-id: 9b616715-33cd-43ba-8548-8d96a179408e
source-git-commit: 6dc6aeb5adeb82d527b39a05ee70a9926205ea0b
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 100%

---

# 権限の基本を学ぶ{#access-management}



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
