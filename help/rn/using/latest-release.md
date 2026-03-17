---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
feature: Release Notes
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: b9a716f327b8fdd68c3bf36dbe864535308def30
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 28%

---

# 最新リリース {#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。新しいビルドごとに、色分けされたステータスが表示されます。Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.4.3 - ビルド 9394 {#release-7-4-3}

[!BADGE 一般公開（GA）]{type=Positive url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="一般公開（GA）"}

_2026 年 3 月 16 日_

>[!CAUTION]
>
> クライアントコンソールのアップグレードは必須です。

### セキュリティの強化 {#security-7-4-3}

* 最適なセキュリティ、安定性、コンプライアンスを維持するために、Debian はバージョン 13 に、PostgreSQL はバージョン 17 にアップグレードされました。 [ 互換性マトリックス ](compatibility-matrix.md) を参照してください。

### 修正点 {#fixes-7-4-3}

* バーコードコンポーネントで境界なしの高さパラメーターが許可され、セキュリティの脆弱性が発生する可能性がある問題を修正しました。 （NEO-89984）
* ワークフローを介して作成されたリストの列挙フィールドに一時的な名前属性が欠落していて、誤ったまたは空の列挙ラベルがインターフェイスに表示される問題を修正しました。 （NEO-91158）
* 一部の配信（特に成功指標に影響する）の配信統計が完全に再計算されない問題を修正しました。 （NEO-88106）
* 重複排除アクティビティを含むワークフローで targetData フィールドを使用すると、パーソナライゼーションエラーが発生して配信の準備が失敗する問題を修正しました。 （NEO-87693）
* PostgreSQL 15 では、タイプキャストの要件により、単一文字の文字列フィールドを他の文字列と連結できない問題を修正しました。 （NEO-88028）
* 親と子の配信 ID の不一致が原因で、分散型マーケティングの共同キャンペーンのトラッキングログがデータベースに書き込まれない問題を修正しました。 （NEO-86836）
* 配信ログに、正常に送信されたメッセージでもキャンセル済みと表示される問題を修正しました。特に、ウェーブスケジュールを使用した配信に影響を与えました。 （NEO-78933）
* データベースクリーンアップワークフローでデータを効率的にパージできず、パフォーマンスに影響を与える可能性がある問題を修正しました。 （NEO-76439）

