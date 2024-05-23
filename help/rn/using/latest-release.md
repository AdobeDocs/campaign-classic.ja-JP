---
product: campaign
title: 最新リリース
description: 最新の Campaign Classic v7 リリースノート
feature: Release Notes
role: User
level: Beginner
exl-id: d65869ca-a785-4327-8e8d-791c28e4696c
source-git-commit: 8fec4d038eddaa3c5a2aade1b619f2543453d4de
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 100%

---

# 最新リリース{#latest-release}

このページには、**最新の Campaign Classic v7 リリース**&#x200B;の新機能、改善点および修正点が記載されています。新しいビルドごとに、色分けされたステータスが表示されます。Campaign Classic v7 のビルドステータスについて詳しくは、[このページ](rn-overview.md)を参照してください。

## リリース 7.3.5 - ビルド 9368 {#release-7-3-5}

[!BADGE 一般公開（GA）]{type=Positive url="https://experienceleague.adobe.com/docs/campaign-classic/using/release-notes/rn-overview.html?lang=ja#rn-statuses" tooltip="一般公開（GA）"}


_2023年12月5日（PT）_


### セキュリティの機能強化 {#release-7-3-5-security}


* Campaign Classic v7.3.5 では、認証プロセスが改善され、セキュリティが強化されました。テクニカルオペレーターは、Adobe Identity Management System（IMS）を使用して Campaign に接続する必要があります。既存のテクニカルアカウントを移行する方法については、[このテクニカルノート](../../technotes/using/ims-migration.md)を参照してください。

* また、セキュリティと認証プロセスを強化する取り組みの一環として、Adobe Campaign では、エンドユーザー認証モードをログイン／パスワードのネイティブ認証から Adobe Identity Management System（IMS）に移行することを強く推奨しています。オペレーターを移行する方法については、[このテクニカルノート](../../technotes/using/migrate-users-to-ims.md)を参照してください。

* 現在、Web フォームのステータスが&#x200B;**保留中の公開**&#x200B;になっている場合、自動的にライブにならなくなります。セキュリティの問題を防ぐには、**オンライン**&#x200B;になる前に公開し、Web ブラウザーの Web フォーム URL からアクセスする必要があります。[詳細情報](../../web/using/publishing-a-web-form.md#life-cycle-of-a-form)

### パッチ {#release-7-3-5-patches}

* Google Big Query データベースのデータを使用し、Oracle データベースのデータを更新する際の問題を修正しました。ワークフロー一時テーブルですべてのキーを `0` に設定しました。（NEO-65091）
* Google Big Query データベース上の 2 つのクエリを&#x200B;**和集合**&#x200B;ワークフローアクティビティで組み合わせると、ワークフローの実行が失敗する原因となっていた問題を修正しました。（NEO-63705）
* キャンペーンレポートで `Back` ボタンをクリックした際に、ユーザーに再認証をリクエストしていた問題を修正しました。（NEO-65087）
* 配達確認の前に配信を削除した際に発生していた、データベースクリーンアップワークフローのエラーを修正しました。（NEO-48114）
* クライアントコンソールへの接続時に、TLS 検証に関する最近の更新により、接続エラーが発生していた問題を修正しました。（NEO-50488）
* Campaign の 7.3.1 へのアップグレード後の HTTP プロキシ認証に関する問題を修正しました。Campaign ワークフローの HTTP リクエストが `error 407 – proxy auth required is returned` で失敗していました。（NEO-49624）
* **スクリプト**&#x200B;ワークフローアクティビティにおける、GPG 復号化での断続的なエラーを修正しました。関連するエラーメッセージは `gpg: decryption failed: No secret key` でした。（NEO-50257）
  <!--* Workflow temporary tables now have a primary index in Teradata with a Federated Data Access (FDA) connection. (NEO-62575)-->

