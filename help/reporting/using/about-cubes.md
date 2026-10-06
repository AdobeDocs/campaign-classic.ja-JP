---
product: campaign
title: キューブについて
description: キューブの基本を学ぶ
feature: Reporting, Monitoring
badge-v8: label="Also applies to v8" type="Positive" tooltip="Also applies to Campaign v8"
hide: true
exl-id: ade4c857-9233-4bc8-9ba1-2fec84b7c3e6
product_v2:
  - id: dfc56824-e8b9-499e-85d4-21aedb507314
    internal-label: Campaign
  - id: fd6e6e36-54e4-4f1a-96fc-1a750e400d50
    internal-label: Campaign Classic v7
feature_v2:
  - id: c309ee4e-82e4-4f7e-b608-ef345678c34e
    internal-label: Dynamic reporting
  - id: c5474392-5419-4296-9e41-f6f4ce4f6e9b
    internal-label: Administration
subfeature_v2:
  - id: b3a4149f-2b3a-44d1-894e-e3ac4c77fb47
    internal-label: Reporting interface
  - id: e519a22f-a06a-42fc-9d09-d78a3ab2c434
    internal-label: Monitoring guidelines
source-git-commit: a43e591a565a18d79f583d975e3e812c5435b0c0
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 100%
---
# キューブの基本を学ぶ{#about-cubes}



## 用語 {#terminology}

キューブを扱う際の具体的な用語を以下に示します。

* **キューブ** - キューブは多次元情報の表現であり、インタラクティブなデータ分析用に設計された構造をエンドユーザーに提供します。

* **ファクトテーブル／スキーマ** - ファクトテーブル（またはファクトスキーマ）には、分析の基になる生データまたは基本データが含まれています。 主に大容量のテーブル（場合によってリンクされたテーブルを含む）で、長い計算が必要になる可能性があります。 例えば、broadLog テーブルや購入テーブルなどがファクトテーブルになります。

* **ディメンション** - ディメンションを使用すると、データをグループにセグメント化できます。作成したディメンションは、分析軸として機能します。 ほとんどの場合、指定されたディメンションに対して、複数のレベルが定義されます。 例えば、時間ディメンションの場合は、月、日、時間、分などのレベルがあります。この一連のレベルはディメンション階層を表し、様々なレベルのデータ分析を可能にします。

* **ビニング** - 一部のフィールドについては、ビニングを定義して値をグループ化し、情報を読み取りやすくすることができます。 ビニングは、レベルに適用されます。 多数の異なる値を扱う可能性がある場合は、ビニングを定義することをお勧めします。

* **測定値** - 最もよく使用される測定値は、合計、平均、最大、最小、標準偏差などです。測定値は計算できます。例えば、オファーの受け入れ率は、オファーの提供回数と承認回数の比率です。

## キューブワークスペース {#cube-workspace}

キューブは&#x200B;**[!UICONTROL 管理／設定／キューブ]**&#x200B;ノードに格納されます。

![](assets/s_advuser_cube_node.png)

キューブを使用する主なコンテキストは次のとおりです。

* データのエクスポートは、Adobe Campaign プラットフォームの「**[!UICONTROL レポート]**」タブで設計されたレポートで直接実行できます。

  それには、新しいレポートを作成し、使用するキューブを選択します。

  ![](assets/cube_create_new.png)

  キューブは、作成するレポートの基になるテンプレートのように表示されます。 テンプレートを選択したら、「**[!UICONTROL 作成]**」をクリックして、対応するレポートを設定および表示します。

  測定の適合化、表示モードの変更またはテーブルの設定をおこなってから、メインボタンを使用してレポートを表示できます。

  ![](assets/cube_display_new.png)

* レポートの「**[!UICONTROL クエリ]**」ボックスでキューブを参照して、その指標を使用することもできます（下図参照）。

  ![](assets/s_advuser_query_using_a_cube.png)

* キューブに基づいたピボットテーブルをレポートの任意のページに挿入することもできます。 それには、該当するページにあるピボットテーブルの「**[!UICONTROL データ]**」タブで、使用するキューブを参照します。

  ![](assets/s_advuser_cube_in_report.png)

  詳しくは、[レポートのデータを調べる](../../reporting/using/using-cubes-to-explore-data.md#exploring-the-data-in-a-report)を参照してください。
