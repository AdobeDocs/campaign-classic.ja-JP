---
product: campaign
title: メンテナンスのタイプ
description: メンテナンスのタイプ
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: database-maintenance
exl-id: 08e179aa-fd83-4c0a-879e-ab7aec168d92
source-git-commit: 0ed70b3c57714ad6c3926181334f57ed3b409d98
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 4%

---

# メンテナンスのタイプ{#types-of-maintenance}



## アプリケーション保守 {#application-maintenance}

Adobe Campaignには、特定のデータベースのメンテナンスタスクをスケジュールできる組み込みのワークフロー **データベースクリーンアップワークフロー** が用意されています。 このワークフローは、次のタスクを実行します。

* 期限切れレコードの削除、
* 孤立したレコードの削除および期限切れオブジェクトのステータス再初期化
* データベース統計を更新しています。

>[!IMPORTANT]
>
>クリーンアップタスクは、RDBMS レベルのメンテナンス（統計の更新を除く）ではなく、主にアプリケーションレベルのメンテナンスを扱うことに注意してください。 ただし、データベースに対してメンテナンス操作が必要になります。 データベースクリーンアップワークフローが正常に実行されても、データベースが最適に調整されているわけではありません。

## 技術的保守 {#technical-maintenance}

データベースクリーンアップワークフローには、データベースメンテナンスツールは含まれていません。メンテナンスを整理するのはユーザー次第です。 これを行うには、次のいずれかを実行します。

* データベース管理者と協力して、サードパーティのツールを使用したデータベースのメンテナンスを設定します。
* Adobe Campaign ワークフローエンジンを使用して、これらのメンテナンスアクティビティをスケジュールおよびトラックします。

これらのメンテナンス手順は定期的に実行する必要があり、次のものが含まれます。

* 頻繁に更新されるテーブルの再インデックス、
* 断片化を避けるために、テーブルを圧縮/再構築します。

### メンテナンススケジュール {#maintenance-schedule}

これらのメンテナンスアクティビティを実行するための適切なスロットを見つける必要があります。 実行中にデータベースのパフォーマンスに大きな影響を与えたり、（ロックが原因で）アプリケーションがブロックされたりする場合があります。

これらのタスクは通常、バックアップ、データの再ロード、または集計計算と競合しない低アクティビティの期間に、週に 1 回実行されます。 要求の厳しいシステムには、より頻繁なメンテナンスが必要となるものもあります。

フルテーブルの再構築など、より詳細なメンテナンスは、月に 1 回実行できます。システムが使用できなくなるため、アプリケーションを完全に停止することが望ましいです。

### テーブルの再構築 {#rebuilding-a-table}

複数の戦略を利用できます。

<table> 
 <thead> 
  <tr> 
   <th> 運用 </th> 
   <th> 説明 </th> 
   <th> 利点 </th> 
   <th> 欠点 </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> オンラインでの最適化 <br /> </td> 
   <td> ほとんどのデータベース・エンジンは、最適化の方法を提供しています。<br /> </td> 
   <td> データベースのデフラグ方法を使用するだけです。 これらのメソッドは通常、最適化中にデータをロックすることで、整合性の問題に対処します。<br /> </td> 
   <td> データベースによっては、これらのデフラグ方式を RDBMS オプション （Oracle）として提供することができ、大きなテーブルを処理する最も効率的な方法とは限りません。<br /> </td> 
  </tr> 
  <tr> 
   <td> ダンプとリストア <br /> </td> 
   <td> テーブルをファイルにダンプし、データベースでテーブルを削除してダンプから復元します <br /> </td> 
   <td> これは、テーブルを最適化する最も簡単な方法です。 また、データベースがほぼ満杯の場合の唯一の解決策です。<br /> </td> 
   <td> テーブルは削除および再作成されるので、読み取り専用モードでもアプリケーションをオンラインのままにできません（リストア段階ではテーブルを使用できません）。<br /> </td> 
  </tr> 
  <tr> 
   <td> 複製、名前変更、およびドロップ <br /> </td> 
   <td> これにより、テーブルとそのインデックスのコピーが作成され、既存のコピーをドロップして、コピーの名前を変更します。<br /> </td> 
   <td> この方法は、生成される IO が少ないので（ファイルとしてのコピーがなく、このファイルから読み取られる）、最初のアプローチよりも高速です。<br /> </td> 
   <td> 2 倍の容量が必要です。<br /> プロセス中にテーブルに書き込むアクティブなプロセスはすべて停止する必要があります。 ただし、テーブルは再構築後の最後の時点でスワップされるため、読み取りプロセスは影響を受けません。<br /> </td> 
  </tr> 
 </tbody> 
</table>
