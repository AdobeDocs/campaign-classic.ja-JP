---
title: リリース18.6
seo-title: リリース18.6
description: リリース18.6
seo-description: null
page-status-flag: never-activated
uuid: 72941f8f-0b84-4868-a768-8aa972459ef2
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: rn
content-type: reference
topic-tags: latest-release-notes
discoiquuid: 79a6d3cf-2425-49b9-9b92-b56be26438bf
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: d046304657f04312d78176c49a650690b05e4c94

---


# Release 18.6{#release-18-6}

## リリース18.6.2 — ビルド8949{#release-18-6-3-build-8949}

2018年8月23日

>[!CAUTION]
>
>このビルドはリコールされました。[最新ビルドにアップグレードする](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)か、[テクニカルサポート](https://support.neolane.net/)にお問い合わせください。

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> 機能<br /> </th> 
   <th> 説明<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> Query Banding<br /> </td> 
   <td> <p>複数のキャンペーンユーザーが同じ FDA Teradata 外部アカウントに接続したときに、各ユーザーに固有のクエリバンド（キー/値のペア）を渡すことができるようになりました。Campaign ユーザーが Teradata データベースに対してクエリを実行するたびに、Adobe Campaign はそのユーザーに関連付けられたメタデータを送信できます。これらのデータはキーと値のリストで構成されており、Teradata 管理者が監査目的やアクセス権限の管理などに利用できます。</p><p>詳しくは、<a href="https://docs.campaign.adobe.com/doc/AC/en/PTF_Administration_basics_External_accounts.html#Teradata_external_account">詳細ドキュメント</a>を参照してください。</p> </td>
  </tr> 
 </tbody> 
</table>

**強化点**

* E メールのアーカイブログが強化され、どの E メールが正常に配信されたかまたは BCC アーカイブで失敗したかがより簡単にはっきりと確認できるようになりました。（NEO-10675）
* トラッキングブロードログでカスタマー IP の代わりにロードバランサー IP が表示されてしまうという問題を修正しました。（NEO-11295）
* 配信のプロパティが誤って上書きされるというランダム問題を修正しました。（NEO-11015）
* エンリッチメントアクティビティの結果を並べ替えるときの構文エラーを修正しました。（NEO-11394）
* Fixed an issue when using calculated fields in a **[!UICONTROL Survey answers]** workflow activity. （NEO-11382）
* Tomcat は脆弱性の悪用を避けるために更新されました。（NEO-11503）
* PostgreSQL データベースへの FDA 接続を使用するときに LATIN1 エンコードで発生するエラーを修正しました。（NEO-11299）
* 配信オプションの使用時に発生する問題を修 **[!UICONTROL Prepare the personalization data with a workflow]** 正しました。 （NEO-11047）
* 拡張コネクタの使用時に SMS が送信されることを妨げるポストアップグレードの問題を修正しました。
* パッケージのインポート/エクスポートを改善しました（ログと領域がインターフェイスに追加されました）。
* Fixed an issue which displayed useless errors in the postupgrade log when a **[!UICONTROL Survey answers]** workflow activity was not fully configured.

**技術面の変更点**

Query Banding

Teradata ユーザーまたは役割を Campaign ユーザーに関連付けるには、固有のキー（PROXYUSER または PROXYROLE）を使用します。このプロキシユーザーや役割を使用できる新しい権限が追加されました。GRANT CONNECT THROUGH アクセス権をデータベースアカウント（Teradata 外部アカウントで定義されたもの）に追加する必要があります。

Teradata 外部アカウントに新しいタブが追加されました。The **[!UICONTROL Query banding]** tab includes the following options:

* **[!UICONTROL Active]**:このチェックボックスをオンにして、機能をアクティブにします。
* **[!UICONTROL Default]**:ユーザーに関連するクエリバンディングがない場合に使用するデフォルトのクエリバンディングを入力します。 デフォルトの Query Banding が定義されていないと、Query Banding が関連付けられていないユーザーは Teradata を使用できません。
* **[!UICONTROL Users]**:各ユーザーに対して、クエリーのバンディングを指定します。 キーと値のペアを必要な数だけ追加できます。例：‘priority=1;workload=high;’

Query Banding について詳しくは、以下の記事を参照してください。

* [https://docs.teradata.com/reader/cY5~BoeEUFWjgN2kBnH3Vw/a5G1~zve68yTMa24kVjVw](https://docs.teradata.com/reader/cY5B%7EoeEUFWjgN2kBnH3Vw/a5G1iz%7Eve68yTMa24kVjVw)
* [https://docs.teradata.com/reader/rgAb27O_xRmMVc_aQq2VGw/qVNfdszBssrZ7ttrE7AtmQ](https://docs.teradata.com/reader/rgAb27O_xRmMVc_aQq2VGw/qVNfdszBssrZ7ttrE7AtmQ)

## リリース18.6 — ビルド8947{#release-18-6-build-8947}

2018年6月25日

>[!CAUTION]
>
>このビルドはリコールされました。[最新ビルドにアップグレードする](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/buildUpgrade.html)か、[テクニカルサポート](https://support.neolane.net/)にお問い合わせください。

**新機能?**

<table> 
 <thead> 
  <tr> 
   <th> 機能<br /> </th> 
   <th> 説明<br /> </th> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td> セキュリティの強化<br /> </td> 
   <td> Campaign Classic に対して一連のセキュリティ強化が追加されました。機能強化および修正点を次に示します。<br /> </td> 
  </tr> 
  <tr> 
   <td> Windows Server 2016 のサポート<br /> </td> 
   <td> Adobe Campaign は現在、Windows Server 2016 に対応しています。<a href="https://helpx.adobe.com/campaign/kb/compatibility-matrix.html">Campaign Classic の互換性マトリックス</a>を参照してください。<br /> </td> 
  </tr> 
 </tbody> 
</table>

**セキュリティの機能強化**

decryptString

**decryptString** 関数は廃止される予定です。[廃止される機能および削除された機能](https://helpx.adobe.com/campaign/kb/deprecated-and-removed-features.html)についての記事を参照してください。

新規のお客様は、ランディングページで受信者の暗号化 ID を復号化する際にのみ、この関数を使用します。外部アカウントに保管されているパスワードを復号化するには、新しい **decryptPassword** 関数を使用します。

既存のお客様にとっては、この関数の動作は変わりませんが、**decryptString** の代わりに **decryptPassword** を使用することをお勧めします。この関数を引き続き使用できるように、**XtkSecurity_Unsafe_DecryptString** 互換性オプションがアップグレード後に追加されて、デフォルトで有効になります。**decryptString** を無効にする場合は、このオプションを無効にします。

decryptPassword

**decryptPassword** 関数が追加されました。この関数を使用して、外部アカウントに格納されたパスワードを復号化できます。詳しくは、[JSAPI](https://helpx.adobe.com/campaign/kb/compatibility-matrix.html) ドキュメントを参照してください。

ファイル API

新規インストールでは、ファイル API を介したフォルダーアクセスが、Adobe Campaign の **var**、**sftp**、一時フォルダーに限定されます。

既存のお客様は、ファイル API で Adobe Campaign の **conf** フォルダーにアクセスできなくなりました。他のフォルダーにアクセスできるように、**XtkSecurity_Disable_JSFileSandboxing** 互換性オプションがアップグレード後に追加されて、デフォルトで有効になります。アクセスを Adobe Campaign の **var**、**sftp**、一時フォルダーに限定する場合は、このオプションを無効にします。

**パッチ**

* SMS トランザクションメッセージのパフォーマンスを低下させる可能性のある問題を修正しました。（NEO-9812）
