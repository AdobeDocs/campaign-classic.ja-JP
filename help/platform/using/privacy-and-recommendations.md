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
translation-type: ht
source-git-commit: be148d7cd55097b9014d2f4d3b095c65a5ca8c54
workflow-type: ht
source-wordcount: '824'
ht-degree: 100%

---


# プライバシーと推奨事項{#privacy-and-recommendations}

## プライバシーと同意について {#about-privacy-and-consent}

Adobe Campaign は、個人情報を含む膨大な量のデータを収集および処理するための強力なツールです。当社では、Adobe Campaign のすべてのユーザーに対し、法律（DPA、CAN-SPAM、プライバシーと電子通信に関する EU 指令、欧州 GDPR、CCPA など）の範囲内で使用すること、個人情報の倫理的な使用に責任を持つこと、未承諾の電子メールやプッシュ通知、SMS メッセージ（「スパム」）の送信を控えることを奨励しています。当社は、顧客の生涯価値およびロイヤリティを促進するうえで許可型マーケティングの原則を重要視しています。したがって、未承諾メッセージの送信に Adobe Campaign を使用することを固く禁止しています。

詳しくは、[Adobe Experience Cloud のプライバシー](https://www.adobe.com/privacy/marketing-cloud.html)を参照してください。

ここで、[セキュリティとプライバシーチェックリスト](https://docs.campaign.adobe.com/doc/AC/getting_started/JA/security.html)を参照して、セキュリティとプライバシーに関してチェックすべき重要な要素を確認します。

## プライバシーの管理 {#privacy-management}

Adobe Campaign には、プライバシー規制（GDPR、CCPA など）を遵守するのに役立つ一連のツールが用意されています。

GDPR（EU 一般データ保護規則）は欧州連合（EU）で施行されるプライバシー保護法律で、データ保護要件を現代の状況に合わせて整合化することを目的としています。GDPR は、EU に居住しているデータ主体のデータを保有している Adobe Campaign の顧客に適用されます。

CCPA（カリフォルニア州消費者プライバシー法）は、カリフォルニア州民に個人情報に関する新しい権利を提供し、カリフォルニア州でビジネスをおこなう特定の事業者に対してデータ保護の責任を課します。

特定のプライバシー要求に対応するデータ管理者としての準備を円滑に進められるよう、アドビは、既に提供している同意管理、データ保持設定および権限管理に加え、データ処理者として追加の機能を提供します。

この[記事](https://helpx.adobe.com/jp/campaign/kb/acc-privacy.html)では、Adobe Campaign がアクセスする権利、忘れられる権利、同意、データ保持、ユーザの役割などの、様々なプライバシーに関する主な機能を管理する方法について説明します。また、アドビのソルーションを利用する際にプライバシーの遵守に役立つベストプラクティスもご覧いただけます。

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
