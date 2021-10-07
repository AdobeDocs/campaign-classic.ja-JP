---
product: campaign
title: 以前のバージョンにロールバック
description: 以前のバージョンにロールバックする方法を説明します
audience: migration
content-type: reference
topic-tags: rollback
exl-id: 5120a7c4-3760-48d9-94da-d587d333e8d8
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# 以前のバージョンにロールバック{#about-rollback}

![](../../assets/v7-only.svg)

移行後、問題が発生した場合は、以前のバージョンの Campaign にロールバックする必要が生じる場合があります。

ロールバック手順は、Campaign の最初のバージョンによって異なります。

## v6.1 の復元

v7 から v6.1 を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Adobe Campaign v6.back** フォルダー（Linux では **nl6.back**）を回復し、**Adobe Campaign v6**（Linux では **nl6**）に名前を変更して、元の場所に復元します。
1. IIS Web サイトレベルでAdobe Campaign v6.1 の統合を再確立するために、リスンポートを再割り当てして IIS を再設定します。
1. Adobe Campaign v7 サービスを停止します。
1. IIS を再起動します。
1. Adobe Campaign v6.1 サービスを再起動します。

## Campaign v6.02 への復元

v7 から v6.02 を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Neolane v6.back** フォルダー（Linux では **nl6.back**）を回復し、名前を **Neolane v6**（Linux では **nl6**）に変更して、元の場所に戻します。
1. IIS Web サイトレベルでAdobe Campaign v6.02 の統合を再確立するために、リスンポートを再割り当てして IIS を再設定します。
1. Adobe Campaign v6.1 サービスを停止します。
1. IIS を再起動します。
1. Adobe Campaign v6.02 サービスを再起動します。

## Campaign v5.11 への復元

v7 から v5.11 を復元する手順を次に示します。

1. データベースのバックアップをリカバリし、復元します。
1. **Neolane v5.back** フォルダー（Linux では **nl5.back**）を回復し、名前を **Neolane v5**（Linux では **nl5**）に変更して、元の場所に戻します。
1. リスンポートを再割り当てして IIS を再設定し、IIS Web サイトレベルで Neolane v5 の統合を再確立します。
1. Adobe Campaign v7 サービスを停止します。
1. IIS を再起動します。
1. Adobe Campaign v5 サービスを再起動します。
