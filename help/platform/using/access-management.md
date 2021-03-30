---
solution: Campaign Classic
product: campaign
title: 権限の基本を学ぶ
description: キャンペーン機能へのアクセスを許可する方法を学びます。
feature: アクセス管理
role: 営業者、管理者
level: 初心者
translation-type: tm+mt
source-git-commit: f2bd093d3a010e079b7f5adf3371e21d07a4f3ae
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 69%

---


# 権限の基本を学ぶ{#access-management}

Adobe Campaign は、様々なオペレーターに割り当てる一連の権利を定義したり、管理したりするのに役立ちます。以下の操作は、それらの権利に基づいて承認または拒否されます。

* 特定種類の機能に対するアクセス（ネームド権限など）
* 特定種類のレコードに対するアクセス
* レコード（アクション、連絡先、キャンペーン、グループなど）の作成、変更または削除

権限は、オペレーターのプロファイルまたはオペレーターグループに付与されます。

これらの操作は、オペレーターの Adobe Campaign に対する接続モードにリンクされた安全パラメーターに基づいて実行されます。[このページ](../../installation/using/security-zones.md)のセキュリティゾーンの詳細。

ユーザーに付与できる権限には次の 2 種類があります。

* グループを使用する場合は、権利の付与対象とするオペレーターのグループを定義し、オペレーターを 1 つまたは複数のグループに関連付けます。これにより、権利を再利用することや、複数のオペレーターに一貫性の高いプロファイルを設定することができます。また、プロファイルの管理やメンテナンスをおこなううえでも便利な方法です。グループの作成と管理は、[このセクション](access-management-groups.md)に記載されています。

* ネームド権限は、ユーザーに対して直接付与することができ、グループ経由で付与された権利を上書きする目的で使用することもできます。これらの権利は[このページ](access-management-named-rights.md)に表示されます。

>[!NOTE]
>
>権限の定義を開始する前に、[セキュリティ設定チェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html)を読むことをお勧めします。

アクセスを許可し、権限を設定する方法については、次の節を参照してください。

* [演算子の作成](access-management-operators.md)

* [グループの定義](access-management-groups.md)

* [追加ネームド権限](access-management-named-rights.md)

* [キャンペーンフォルダーアクセスの管理](access-management-folders.md)

* [アクセス権マトリックス](access-management-named-rights.md#access-rights-matrix)


関連項目：

* [ワークフローの権限の管理](../../workflow/using/managing-rights.md)
* [分散マーケティングの権限の管理](../../campaign/using/about-distributed-marketing.md#operators-and-entities)
* [インタラクションモジュールの権限の管理](../../interaction/using/operator-profiles.md)
* [スキーマへのアクセスのフィルター](../../configuration/using/filtering-schemas.md)
* [PI表示の制限](../../configuration/using/restricting-pii-view.md)
