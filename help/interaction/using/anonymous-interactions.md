---
product: campaign
title: 匿名インタラクション
description: 匿名インタラクション
feature: Interaction, Offers
audience: interaction
content-type: reference
topic-tags: unitary-interactions
exl-id: a8face46-a933-4f2c-8299-ccb66f05967d
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 87%

---

# 匿名インタラクション{#anonymous-interactions}



![](assets/do-not-localize/how-to-video.png)識別されたターゲットと匿名ターゲットへのオファーの配信方法の概要については、この[ビデオ](https://helpx.adobe.com/jp/campaign/classic/how-to/indetified-and-anonymous-interaction-in-acv6.html?playlist=/ccx/v1/collection/product/campaign/classic/segment/digital-marketers/explevel/intermediate/applaunch/get-started/collection.ccx.js&amp;ref=helpx.adobe.com)をご覧ください。

## 匿名インタラクション向け環境のターゲティングと保存 {#targeting-and-storing-an-environment-for-anonymous-interactions}

デフォルトでは、インタラクションには、受信者テーブルをターゲットとするように事前設定された環境（識別されたオファー）が 1 つ用意されています。別のテーブル（匿名オファー用の訪問者テーブルまたは特定の受信者テーブル）をターゲットにする場合は、ターゲットマッピングアシスタントを使用して環境を作成する必要があります。 詳しくは、[オファー環境の作成](../../interaction/using/live-design-environments.md#creating-an-offer-environment)を参照してください。

マッピング作成アシスタントを使用して匿名環境を作成すると、環境の **[!UICONTROL 一般]** タブで「**[!UICONTROL 受信する匿名インタラクション専用の環境]** ボックスが自動的にオンになります。

「**[!UICONTROL ターゲティングディメンション]**」は自動的に入力されます。デフォルトでは、このフィールドは訪問者テーブルにリンクされます。

「**[!UICONTROL 訪問者フォルダー]**」フィールドが表示され、**[!UICONTROL 訪問者]**&#x200B;フォルダーへのリンクが自動的に入力されます。このフィールドでは、訪問者プロファイルを格納する場所を選択できます。

![](assets/anonymous_environment_option.png)

>[!NOTE]
>
>1 つまたは複数のブランドを提供する匿名オファーの場合など、複数のタイプの訪問者にフィルターするには、各ブランドに環境を作成して、各環境用に&#x200B;**[!UICONTROL 訪問者]**&#x200B;タイプのフォルダーを作成する必要があります。

## 匿名インタラクション用のオファーカタログ {#offer-catalog-for-anonymous-interactions}

アウトバウンドインタラクションと同様に、インバウンドインタラクションは、カテゴリとオファーで構成されるオファーカタログに整理されます。

カテゴリやスペースを作成するには、識別された訪問者の場合と同じ手順を適用します（[オファーカテゴリの作成](../../interaction/using/creating-offer-categories.md)および[オファー環境の作成](../../interaction/using/live-design-environments.md#creating-an-offer-environment)を参照）。

## 匿名の訪問者 {#anonymous-visitors}

匿名の訪問者が接続する際に、それらの訪問者が Cookie 識別プロセスに送信されることがあります。この暗黙の認識は、訪問者のブラウザーの履歴に基づいています。

この手順では、Cookie から復元されたデータとデータベースのデータの比較がおこなわれます。訪問者が認識される（暗黙的に識別される）場合もあれば、認識されない（したがって匿名のままになる）場合もあります。

この分析を実行するには、オファースペースで、「**[!UICONTROL ブラウザー履歴に基づいて個人を暗黙的に推測]**」オプションをオンにします。

![](assets/identification_anonymous_visitors.png)

## 識別されていない匿名訪問者の処理 {#processing-unidentified-anonymous-visitors}

分析の結果、匿名の訪問者が識別されなかった場合、そのデータを所定のスペースに格納できます。これにより、指定したタイポロジルールに合致する、特にこのタイプの訪問者向けのオファーを提案できます。

コンタクト先を識別できる要素がない場合や、暗黙的な推測が可能なコンタクト先に識別済みオファーを提案する意思がない場合は、匿名環境のフォールバックを実行できます。

それには、「**[!UICONTROL 個人が識別されなかった場合、匿名環境にフォールバックします]**」をオンにして、オファースペースを指定する際に、「**[!UICONTROL リンクされた匿名スペース]**」で識別されない訪問者専用の環境を指定します。

![](assets/anonymous_to_anonymous_environment.png)
