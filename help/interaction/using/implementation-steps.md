---
title: 実装の手順
seo-title: 実装の手順
description: 実装の手順
seo-description: null
page-status-flag: never-activated
uuid: 11582071-00a2-4245-af3e-bc81174ce223
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: interaction
content-type: reference
topic-tags: general-operation
discoiquuid: 7f79c0d8-77b0-4cc6-a888-7dbd32d2f3b6
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: 20f835c357d016643ea1f3209ee4dfb6d3239f90

---


# 実装の手順{#implementation-steps}

## インタラクションの設定 {#configuring-interaction}

>[!NOTE]
>
>次の手順は、**管理者**&#x200B;プロファイルによって、デザイン環境でのみ実行される必要があります。

1. ユーザープロファイルを作成します。詳しくは、[オペレーターのプロファイル](../../interaction/using/operator-profiles.md)を参照してください。
1. ターゲティングディメンションに基づいてオファー環境を作成します。詳しくは、[オファー環境の作成](../../interaction/using/live-design-environments.md#creating-an-offer-environment)を参照してください。
1. 各環境で使用するタイポロジルールを作成します。詳しくは、[オファープレゼンテーションルールの作成および参照](../../interaction/using/managing-offer-presentation.md#creating-and-referencing-an-offer-presentation-rule)を参照してください。
1. 各環境用にオファースペースを作成し、レンダリング関数を設定します。詳しくは、[オファースペースの作成](../../interaction/using/creating-offer-spaces.md)を参照してください。

   >[!NOTE]
   >
   >スペースが識別モードで単一のチャネルによって定義される場合は、このスペースの詳細設定パラメーターを指定する必要があります。

1. 1 つまたは複数のオファーを提示および更新するために、インバウンドインタラクション向けのオファーエンジンを設定します。

   様々な統合モードについて詳しくは、[インバウンドチャネルについて](../../interaction/using/about-inbound-channels.md)を参照してください。

   >[!NOTE]
   >
   >インバウンド Web チャネルにスペースを作成する場合、オファーが表示されるサイトに対しても設定が必要です。

## オファーカタログの管理 {#managing-the-offer-catalog-}

>[!NOTE]
>
>次の手順は、**オファーマネージャー**&#x200B;によって実行される必要があります。

1. デザイン環境にオファーカテゴリを作成します。詳しくは、[オファーカテゴリの作成](../../interaction/using/creating-offer-categories.md)を参照してください。
1. デザイン環境にオファーを作成します。詳しくは、[オファーの作成](../../interaction/using/creating-an-offer.md)を参照してください。
1. 1 つまたは複数のスペース上で、オファーを承認してパブリッシュし、ライブ環境で配信責任者によるオファーの利用を可能にします。詳しくは、[オファーの承認と有効化](../../interaction/using/approving-and-activating-an-offer.md)を参照してください。

## オファーカタログの使用 {#using-the-offer-catalog-}

>[!NOTE]
>
>次の手順は、**配信責任者**&#x200B;プロファイルによって実行される必要があります。配信責任者は、ライブ環境でのみオファーを編集できます。

1. キャンペーンを作成します。
1. キャンペーンまたはキャンペーン配信でオファーを参照します。詳しくは、[アウトバウンドチャネルについて](../../interaction/using/about-outbound-channels.md)を参照してください。

