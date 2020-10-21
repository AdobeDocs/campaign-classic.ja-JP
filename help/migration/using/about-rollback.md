---
title: 前のバージョンにロールバック
description: 前のバージョンにロールバックする方法を説明します。
page-status-flag: never-activated
uuid: 9d404ca5-e38c-48ba-b5e0-8e70a40482c2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: migration
content-type: reference
topic-tags: rollback
discoiquuid: 0e17abea-5e86-43b5-8bca-ee39d9b24c90
translation-type: tm+mt
source-git-commit: 7a3cdf40da579fc3c4c7fc26b10c160543cc45d7
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# 前のバージョンにロールバック{#about-rollback}

移行後、問題が発生した場合は、以前のバージョンのキャンペーンにロールバックする必要がある場合があります。

ロールバックの手順は、キャンペーンの最初のバージョンによって異なります。

## v6.1 の復元

v7からv6.1を復元する手順を次に示します。

1. データベースのバックアップを回復し、復元します。
1. Adobe Campaignv6.back **Adobe Campaign(Linuxでは** nl6.back **)を回復し、フォルダ名を** v6に変更し(Linuxでは ******** nl6)、元の場所に戻します。
1. リスンポートを再割り当てしてIISを再設定し、Adobe Campaignv6.1の統合をIIS Webサイトレベルで再確立します。
1. Adobe Campaignv7サービスを停止します。
1. IISの再開始。
1. Adobe Campaignv6.1サービスを再起動します。

## キャンペーンv6.02への復元

v7からv6.02を復元する手順を次に示します。

1. データベースのバックアップを回復し、復元します。
1. Neolane v6.back **フォルダー(Linuxでは** nl6.back **)を回復し、** Neolane v6 **.backフォルダー(Linuxでは** nl6.back **** )に名前を変更し、元の場所に戻します。
1. リスンポートを再割り当てしてIIS WebサイトレベルでAdobe Campaignv6.02の統合を再確立し、IISを再設定します。
1. Adobe Campaignv6.1サービスを停止します。
1. IISの再開始。
1. Adobe Campaignv6.02サービスを再起動します。

## キャンペーンv5.11へのリストア

v5.11をv7から復元する手順を次に示します。

1. データベースのバックアップを回復し、復元します。
1. Neolane v5.back **フォルダ(Linuxでは** nl5.back **)を回復し、名前を** Neolane v5 **(Linuxでは****** nl5)に変更し、元の場所に戻します。
1. リスンポートを再割り当てしてIIS WebサイトレベルでNeolane v5の統合を再確立し、IISを再設定します。
1. Adobe Campaignv7サービスを停止します。
1. IISの再開始。
1. Adobe Campaignv5サービスを再開始します。
