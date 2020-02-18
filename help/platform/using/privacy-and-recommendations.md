---
title: プライバシーと推奨事項
seo-title: プライバシーと推奨事項
description: プライバシーと推奨事項
seo-description: null
page-status-flag: never-activated
uuid: a044bbea-521d-4c1e-8aab-7d51a87fc94b
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
discoiquuid: 14369acf-9149-4649-947a-c16289e35eb6
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 33bf5c5a08613cf88eaace91b85a76157cac7ba1

---


# プライバシーと推奨事項{#privacy-and-recommendations}

## プライバシーと同意について {#about-privacy-and-consent}

Adobe Campaign は、個人情報を含む膨大な量のデータを収集および処理するための強力なツールです。アドビは、Adobe Campaignの全ユーザーに対し、法制（DPA、CAN-SPAM、欧州プライバシーと電子通信に関する指令、欧州GDPR、CCPAなど）の範囲内での作業、個人情報の責任ある倫理的な使用、および迷惑メール、プッシュ通知、SMSメッセージ（「スパム」）の送信を禁止するよう勧めます。 当社は、顧客の生涯価値およびロイヤリティを促進するうえで許可型マーケティングの原則を重要視しています。したがって、未承諾メッセージの送信に Adobe Campaign を使用することを固く禁止しています。

詳しくは、[Adobe Experience Cloud のプライバシー](https://www.adobe.com/privacy/marketing-cloud.html)を参照してください。

ここで、[セキュリティとプライバシーチェックリスト](https://docs.campaign.adobe.com/doc/AC/getting_started/EN/security.html)を参照して、セキュリティとプライバシーに関してチェックすべき重要な要素を確認します。

## プライバシーの管理 {#privacy-management}

GDPR(General Data Protection Regulation)は、データ保護要件を調和し、最新化するEUプライバシー法です。 GDPR は、EU に居住しているデータ主体のデータを保有している Adobe Campaign の顧客に適用されます。

CCPA（カリフォルニア消費者プライバシー法）は、カリフォルニア州在住者に対して個人情報に関する新たな権利を提供し、カリフォルニア州でビジネスを行う特定の事業者に対するデータ保護責任を課します。

同意管理、データ保持設定、権限管理に加えて、Data Processorとしての役割に、特定のプライバシー要求に対するData Controllerとしての準備を容易にする追加機能を提供します。

この記事で [は](https://helpx.adobe.com/campaign/kb/acc-privacy.html)、Adobe Campaignが各種プライバシーキー機能の管理に役立つ方法について説明します。アクセス権、忘れ去られる権利、同意、データ保存、ユーザの役割 また、アドビのサービスを使用する際にプライバシーコンプライアンスに関するサポートを受けるためのベストプラクティスもご覧いただけます。

## Cookie とトラッキング機能 {#cookies-and-tracking-capabilities}

Adobe Campaign では、トラッキング機能を使用して、Web サイトでの配信の受信者のブラウジングをトラッキングすることができます。そのために、Adobe Campaign ではセッション Cookie および永続 Cookie を使用します。

「プライバシーと電子通信」に関する EU 指令 2009/136/CE および EU 一般データ保護規則（GDPR）では、企業は Cookie をインストールする前に Web サイトユーザーの同意を必要とすることを規定しています。Cookie のインストールを許可するためのチェックボックスを伴う認証リクエスト（例えばページ上に表示される）を使用して、サイトに Web トラッキングツールがあることをユーザーに通知したり、ランディングページの上部にバナーを追加したりする必要があります。ポップアップウィンドウはブラウザーでブロックされていることが多いので、避ける必要があります。

ユーザートラッキング管理の設定は、オプトアウトバナーのある Web アプリケーションおよびランディングページで実行できます。[このページ](../../web/using/web-application-tracking-opt-out.md)を参照してください。

Adobe Campaign は、次の 2 つのタイプの Cookie を使用します。

1. セッション Cookie（nlid）：連絡先に送信される E メールの識別子（broadlogId）およびメッセージテンプレートの識別子（deliveryId）が含まれています。Adobe Campaign が送信した E メールに含まれている URL を連絡先のユーザーがクリックすると追加され、この連絡先での Web 上の行動をトラッキングできるようになります。このセッション Cookie は、ブラウザーが閉じられると自動的に消去されます。連絡先のユーザーは、Cookie を拒否するようにブラウザーを設定できます。
1. 永続 Cookie（uuid230）：ユーザーが Web サイトを訪問したときに、Adobe Campaign とやり取りするユーザーを識別できるようになります。Adobe Campaign では、これを使用して、マーケティングキャンペーン中にクリック数および転送率の推定値をカウントします。連絡先のユーザーが E メール内をクリックしたとき、Adobe Campaign のフォームに入力したとき、またはインバウンドインタラクションエンジンの呼び出し中に Cookie は配布されます。ユーザーは、これを削除するか拒否するようにブラウザーを設定できます。

## データベースの整合性 {#database-integrity}

Adobe Campaign は豊富な機能を備えています。そのため、使用するデータベース構造も複雑です。データベースには、テーブル、フィールド、リンクおよびインデックスが数多く含まれています。特定の中間テーブルはインターフェイスに表示されません。特定のリンク、フィールドおよびインデックスは、ソフトウェアで自動的に作成、削除または変更されます。Adobe Campaign のインターフェイス（グラフィカルインターフェイス、インポートプログラム、サーバーモジュール、Web モジュール、配信サーバー、フィールドの追加、データベース拡張など）でのみ、整合性を保ちながらデータベースのコンテンツを変更できます。

**データベースのコンテンツまたは構造は、このソフトウェア以外のツールを使用して変更しないでください**。そのような変更はデータベースの破損の原因となる可能性が非常に高く、その結果、リンクの予期しない変更や消失、ゴーストレコードやリンクの作成、重大なエラーメッセージなどが発生し、Adobe Campaign で提供される保証および技術サポート契約が無効になります。

Adobe Campaign システムでは、すべてのデータはデータベースに保存されます。Adobe Campaign システム全体を適切に操作するには、このデータが使用可能である必要があります。データは、購読、管理および購読解除用の Web モジュール、管理画面、配信キュー、配信最適化メカニズムなどで使用されます。

## Apache Tomcat {#apache-tomcat}

Adobe Campaign には、Apache Software Foundation（[https://www.apache.org/](https://www.apache.org/)）が開発した Apache Tomcat が含まれています。
