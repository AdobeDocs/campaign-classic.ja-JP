---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
feature: Release Notes
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: 631188b5974eaa4cd1bf667c5df9f2ff0f983cf0
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---

# 最新リリース {#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。新しいビルドごとに、色分けされたステータスが表示されます。Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.4.2 - ビルド 9390 {#release-7-4-2}

[!BADGE 限定提供（LA）]{type=Informative url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="限定提供（LA）"}

_2025年3月21日（PT）_

>[!AVAILABILITY]
>
>このリリースは&#x200B;**限定提供**（LA）中です。ホスト環境／Managed Services 環境のユーザーのみに制限されます。このリリースは、近日中にハイブリッドおよびオンプレミスのお客様に提供される予定です。

<!--
### Compatibility updates {#comp-7-4-2}

This release comes with the following compatibility updates:

* JQuery library update: fixes multiple UI issues (reports, web apps)
* PostgreSQL 15 and 16

-->

### セキュリティの強化 {#security-7-4-2}

このリリースには、いくつかのセキュリティ修正が含まれています。

**[!UICONTROL Adobe Experience Cloud]** 外部アカウントを通じてアドビソリューションおよびアプリとの接続が更新され、セキュリティが強化されました。

### 修正点 {#release-7-4-2-fixes}

このリリースには、次の主な修正が含まれています。

* TLS／SMPP 接続 - SMPP の安定性の問題を修正しました

* Google BigQuery の修正点：

   * ブール値データタイプに関する不具合を修正しました
   * プロキシ設定の問題を修正しました
   * 日時データタイプに関する不具合を修正しました
   * 一括読み込みの安定性を修正しました
   * ODBC バージョンの内部テストを改善しました
   * 接続文字列の特殊文字に関する問題を修正しました
   * Google BigQuery クエリのデフォルトのタイムアウト（5 分）を削除しました

* メール転送エージェント（MTA）- 孤立した MTA の子が&#x200B;**[!UICONTROL 開始を保留中]**&#x200B;ステータスで停止する問題を修正しました。

また、このリリースでは、次の問題も修正されています。

NEO-47269、NEO-59059、NEO-62455、NEO-65774、NEO-66462、NEO-66989、NEO-77898、NEO-78843、NEO-79373、NEO-79598、NEO-80145、NEO-80245、NEO-80434、NEO-80683、NEO-81222、NEO-81433、NEO-81864、NEO-82351、NEO-82781、NEO-82838、NEO-82923、NEO-83252、NEO-83809、NEO-83826、NEO-84024、NEO-84553、NEO-85150

