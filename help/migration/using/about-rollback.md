---
product: campaign
title: 以前のバージョンにロールバック
description: 以前のバージョンにロールバックする方法を説明します
audience: migration
content-type: reference
topic-tags: rollback
exl-id: 5120a7c4-3760-48d9-94da-d587d333e8d8
source-git-commit: 8610d29a3df1080f1622a2cb3685c0961fb40092
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 以前のバージョンにロールバック{#about-rollback}

![](../../assets/v7-only.svg)

移行後、問題が発生した場合は、以前のバージョンの Campaign へのロールバックが必要になる場合があります。

ロールバック手順は、Campaign の最初のバージョンに応じて異なります。

## Campaign v6.1 への復元

v7 から v6.1 を復元する手順を次に示します。

1. データベースのバックアップを復元し、復元します。
1. 次を回復します。 **Adobe Campaign v6.back** フォルダー (**nl6.back** （Linux の場合）、名前をに変更します。 **Adobe Campaign v6** (**nl6** Linux の場合 )、を元の場所に戻します。
1. IIS Web サイトレベルでAdobe Campaign v6.1 の統合を再確立するために、リスンポートを再割り当てして IIS を再設定します。
1. Adobe Campaign v7 サービスを停止します。
1. IIS を再起動します。
1. Adobe Campaign v6.1 サービスを再起動します。

## Campaign v6.02 に復元

v7 から v6.02 を復元する手順を次に示します。

1. データベースのバックアップを復元し、復元します。
1. 次を回復します。 **Neolane v6.back** フォルダー (**nl6.back** （Linux の場合）、名前をに変更します。 **Neolane v6** (**nl6** Linux の場合 )、を元の場所に戻します。
1. IIS Web サイトレベルでAdobe Campaign v6.02 の統合を再確立するために、リスンポートを再割り当てして IIS を再設定します。
1. Adobe Campaign v6.1 サービスを停止します。
1. IIS を再起動します。
1. Adobe Campaign v6.02 サービスを再起動します。

## Campaign v5.11 への復元

v7 から v5.11 を復元する手順を次に示します。

1. データベースのバックアップを復元し、復元します。
1. 次を回復します。 **Neolane v5.back** フォルダー (**nl5.back** （Linux の場合）、名前をに変更します。 **Neolane v5** (**nl5** Linux の場合 )、を元の場所に戻します。
1. リスンポートを再割り当てして IIS を再設定し、IIS Web サイトレベルで Neolane v5 の統合を再確立します。
1. Adobe Campaign v7 サービスを停止します。
1. IIS を再起動します。
1. Adobe Campaign v5 サービスを再起動します。
