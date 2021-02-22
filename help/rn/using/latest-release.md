---
solution: Campaign Classic
product: campaign
title: 最新リリース
description: 最新の Campaign Classic リリース注意
audience: rns
content-type: reference
topic-tags: latest-release-notes
translation-type: tm+mt
source-git-commit: 5b5aae1b8c19e9fed5f3172d796b0f25022b6d58
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 18%

---


# 最新リリース{#latest-release}

このページには、**最新の Campaign Classic リリース候補バージョン**&#x200B;に加えられた新機能、改善点、および修正点が記載されています。

Campaign Classic Gold Standard バージョン（最新の GA ビルド）については、[このページを参照してください](../../rn/using/gold-standard.md)。

## ![](assets/do-not-localize/blue_2.png) リリース 21.1.1 - ビルド 9277 {#release-21-1-1-build-9277}

_2021年2月22日_

**セキュリティの機能強化**

* コンソール認証メカニズムが強化され、セキュリティが最適化されました。 （NEO-26944）
* サーバーサイドリクエストフォージェリ（SSRF）問題に対する保護を強化するために、セキュリティ問題を修正しました。（NEO-28532）

**互換性の更新**

Campaign で次のシステムがサポートされるようになりました。

* Salesforce CRM外部アカウントの使用時に、Salesforce APIバージョン49がサポートされるようになりました。

**非推奨（廃止予定）の機能**

**Technical Deliverability Monitoring**&#x200B;レポートは非推奨となりました。

詳しくは、[非推奨（廃止予定）の機能と削除された機能のページ](../../rn/using/deprecated-features.md)を参照してください。

**改善点**

**Email Feedback Service(EFS)** は、拡張MTAから直接フィードバックを取り込むスケーラブルサービスで、レポートの正確性が向上します。この機能はプライベートベータ版としてリリースされており、今後のリリースですべての顧客が段階的に利用できるようになります。

* フィードバックのすべてのカテゴリが収集され、完全で正確なレポートが可能になりました。
* 配信済み指標の計算は、精度と反応性を向上させるために、拡張 MTA からのリアルタイムフィードバックに基づいておこなわれるようになりました。
* EFS は、同期ソフトバウンスレポートの遅延の問題を解決します。

詳しくは、[詳細ドキュメント](../../delivery/using/sending-with-enhanced-mta.md#efs)を参照してください。このプライベートベータ版への参加を希望される場合は、[フォーム](https://forms.office.com/Pages/ResponsePage.aspx?id=Wht7-jR7h0OUrtLBeN7O4Rol2vQGupxItW9_BerXV6VUQTJPN1Q5WUI4OFNTWkYzQjg3WllUSDAxWi4u)に記入し、お問い合わせください。

**その他の変更**

* 大きなトラッキングログの転送速度が、圧縮を使用して向上しました。
* 複数のアクティビティでワークフローを実行する場合のタイムアウトを回避するため、ワークフローヒートマップが改善されました。 （NEO-27423）
* 終了日が過ぎた場合でもオファーが表示される可能性がある問題を修正しました。 Campaign Classicでは、終了日の日付のみでなく、終了日のタイムスタンプ全体が考慮されるようになりました。 （NEO-27590）
* Google+リンクは、**ソーシャルネットワーク共有リンク**&#x200B;個人設定ブロックから削除されました。
* 前回のリリースでバグ修正が実装された後の問題を修正しました。 SSL/TLSを使用して接続する際に、ホスト名にチェックが追加され、SMS配信が失敗する原因となりました。 POP3、SMS、プロキシを使用したHTTPなど、ほとんどのプロトコルでホスト名の検証が無効になり、SMS外部アカウントの証明書チェックが3つの値で改善されました(NEO-29581)。 [詳細情報](../../delivery/using/sms-protocol.md#skip-tls)

**パッチ**

* Tab、Enter、Escキーボードショートカットが新しいログオン画面で動作しない問題を修正しました。
* 更新時に、新しく作成したワークフローの名前が保存後にデフォルト値に置き換わる問題を修正しました。(NEO-26106)
* **外部ファイル**&#x200B;ターゲットマッピングを使用して、**配信**&#x200B;アクティビティの前に&#x200B;**エンリッチメント**&#x200B;アクティビティの一部として新しいフィールドが追加されたワークフローの実行時に発生していた問題を修正しました。不要なフィールドが&#x200B;**外部ファイル**&#x200B;ターゲットマッピングーに追加されました。 （NEO-27687）
* 以前に作成して保存したWebアプリケーションを再び開くと、ソースコード内の一部の文字が変更される問題を修正しました。 （NEO-27597）
* リンクを追跡するための新しいキャンペーンメカニズム（ビルド19.1.4および20.2から）を含むビルドにアップグレードする場合に発生する可能性がある問題を修正しました。複数のテンプレートがイベントに関連付けられている場合、アップグレードすると、トランザクションメッセージの送信時に誤ったテンプレートが選択される可能性があります。 （NEO-28326）
* MTAが応答しなくなり、再起動しない限り配信を処理できなくなる問題を修正しました。 （NEO-27455）
* 日時型列の一括読み込み操作中のタイムスタンプ管理に関連するMSSQLデータベースの問題を修正しました。
* Redshift xtk関数を使用する場合のワークフロークエリの問題を修正しました。 SubDays、SubSeconds、SubMinutes、SubHoursは、両方のRedshiftタイムスタンプの種類(NEO-24962)を受け入れるようになりました。
* 匿名アクセスでレポートをプレビューしようとするとスクリプトエラーメッセージが表示される問題を修正しました。 （NEO-27081）
* 配信分析を実行する際に、サーバーのメモリ使用量が減少する可能性がある問題を修正しました。
* 特定の複雑なクエリを実行しようとすると、インスタンスが動作しなくなる可能性がある問題を修正しました。
* **Twitterページ**&#x200B;の同期テクニカルワークフローが実行できない問題を修正しました。 （NEO-28634）
* **ツイート(twitter)**&#x200B;配信テンプレートを使用してTwitterに投稿しようとすると、decryptPassword関数に関連するエラーメッセージが表示される問題を修正しました。 （NEO-28216）
* **Javascript**&#x200B;アクティビティを使用してワークフロー内でHTTPリクエストを行う際に発生していた問題を修正しました。 ホスト名にポート番号を定義した後、呼び出しは次のエラーで失敗します(NEO-29146)。

```
IOB-090020 Error in SSL library: 'IOB-090013 error:14090086:SSL routines:ssl3_get_server_certificate:certificate verify failed (code 336134278)'
```

* ターゲットデータのパーソナライゼーションを含む新しい配信が送信されない問題を修正しました。
* マーケティングインスタンスで複数のクラッシュが発生し、コアファイルが発生する問題を修正しました。
* **追跡**&#x200B;ワークフローが次のエラーで失敗する問題を修正しました。(NEO-25206)

```
There is no index on the sourceId field of the 'NmsTrackingLogRcp' table required for the current Web tracking mode. Please add this index.
```

* キャンペーンの&#x200B;**「ターゲット設定とワークフロー**」タブ内で配信を作成および保存する際に発生していた問題を修正しました。プレビューは次のエラーで失敗します。(NEO-29440)

```
XTK-170024 The temporary 'temp:deliveryEmail-all' schema is not defined in the current context
```

* マーケティングインスタンスとAdobe Campaign Standardインスタンス間またはCampaign Classicミッドソーシングインスタンス間の外部アカウントを設定し、「DisableFOH2=1」オプションを使用すると発生していたエラーを修正しました。 外部アカウントで「DisableFOH2=1」オプションを使用すると、接続が正しく閉じられず、重なり合って次のエラーが発生しました。(NEO-26258)

```
The maximum number of connections has been reached (50) by connections pool 'nms:extAccount:acsDefaultRelayAccount XXX'. The server is overloaded. Please try again later.
```

* サーバーとプロバイダーの間で接続の問題が発生した場合のSMSのエラーを修正しました。 接続は、MTAの子によって自動的に無効になります。 Adobe Campaign Classicは、新しい子が起動していない限り、この接続に接続しようとはしません。
