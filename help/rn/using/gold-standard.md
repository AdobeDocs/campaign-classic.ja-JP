---
product: campaign
title: '[!DNL Gold Standard] リリースノート'
description: Campaign Classic  [!DNL Gold Standard] のリリースノート
feature: Overview
role: User
level: Beginner
exl-id: 9e3a11b1-3070-4d90-91d5-7c559bdd500e
source-git-commit: 2c548465a73bcd817c6d2b18853f4f074ed6adfa
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 87%

---

# [!DNL Gold Standard] リリースノート{#gold-standard}

![](../../assets/v7-only.svg)

このページには、[!DNL Gold Standard] のリリースがリストされています。Campaign [!DNL Gold Standard] の詳細については、[このページ](gs-overview.md)を参照してください。

## ![](assets/do-not-localize/limited_2.png) [!DNL Gold Standard] 12 リリース{#gs-12}

_2021年8月28日_

ビルド(9032@99a3894)には、以下の修正が含まれています。

* トラッキング署名機能が改善され、サードパーティツール（Eメールクライアント、インターネットブラウザーなど）に関連するエラーが 特殊文字を処理します。 URLパラメーターがエンコードされるようになりました。
* コンソールにブロッカーのエラーメッセージが表示される可能性がある日付選択機能の問題を修正しました。 （NEO-36345）

## ![](assets/do-not-localize/green_2.png) [!DNL Gold Standard] 11 リリース{#gs-11}

_2021 年 4 月 14 日_

ビルド 9032@d030c36 には、以下の修正が含まれています。

* IMS 接続画面で永続的なエラーメッセージが発生する原因となっていたクライアントコンソールの不具合を修正しました。 （NEO-34821）
* このコンソールビルドは、[IMSアクセス](../../technotes/using/ims-updates.md)を維持するために必要です。

**コンソールのアップグレードのみ必須です。サーバーのアップグレードは必要ありません。**

>[!CAUTION]
>
> * Adobe IDを使用してCampaignにAdobeIdentity Managementサービス(IMS)で接続している場合、2021年6月30日以降にCampaignに接続できるようにするには、Campaignサーバーとクライアントコンソールの両方のアップグレードが必須です。 ****[詳細情報](../../technotes/using/ims-updates.md)
> * このリリースには、[セキュリティ修正](https://helpx.adobe.com/jp/security/products/campaign/apsb21-04.html)が含まれています。環境のセキュリティを強化するには、アップグレードが必要です。
> * OAuth 認証を通じた Experience Cloud トリガー統合を使用する場合は、 [こちらのページ](../../integrations/using/configuring-adobe-io.md)の説明に従って Adobe I/O に移行する必要があります。[Campaignの従来のoAuth認証モードは、**2021年8月19日(PT)に廃止](https://experienceleaguecommunities.adobe.com/t5/adobe-analytics-discussions/adobe-analytics-legacy-api-end-of-life-notice/td-p/385411)されました。** ホスト環境のメリットは、**2021年11月30日(PT)までです。** オンプレミスまたはハイブリッドのお客様は、Adobeカスタマーケアに連絡して、サポートを2021年11月30日まで延長してください。 Adobeに[OAuthアプリケーション](../../integrations/using/configuring-pipeline.md?lang=en#step-optional)のAppIDを指定する必要があります。

>
>詳しくは、[[!DNL Gold Standard] 11アップグレードに関するFAQ](https://helpx.adobe.com/jp/campaign/kb/gold-standard-upgrade.html)を参照してください。

_2021 年 3 月 2 日_

ビルド 9032@10c2709 には、以下の修正が含まれています。

* 配信での日付選択や画像管理など、コンソールの一部のコンポーネントを使用できないリグレッションを修正しました。 （NEO-31453、NEO-31454）

**コンソールのアップグレードのみ必須です。サーバーのアップグレードは必要ありません。**

>[!NOTE]
>
> [アドビのソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/campaign.html?lang=ja)に接続して、新しいバージョンをダウンロードします。 [このページ](../../installation/using/client-console-availability-for-windows.md)では、すべてのエンドユーザーに対してコンソールの更新を提案する方法について説明します。

_2020 年 12 月 22 日_

<!--
>[!CAUTION]
>
> * This release comes with a new connection protocol: if you are connecting to Campaign through Adobe Identity Service (IMS), upgrade is mandatory for both Campaign server and client console to be able to connect to Campaign after **June 30, 2021**. [Learn more](../../technotes/using/ims-updates.md)
> * This release comes with a [security fix](https://helpx.adobe.com/security/products/campaign/apsb21-04.html): upgrade is mandatory to reinforce your environment security. 
> * If you are using the Experience Cloud Triggers integration through oAuth authentication, you need to move to Adobe I/O as described [in this page](../../integrations/using/configuring-adobe-io.md). Legacy oAuth authentication mode with Campaign will be retired on **November 30, 2021**.
>
>Learn more in the [[!DNL Gold Standard] 11 upgrade FAQ](https://helpx.adobe.com/campaign/kb/gold-standard-upgrade.html).
-->
ビルド 9032@d3b452f には、次の機能強化および修正が含まれています。

* 接続プロトコルは、新しい IMS 認証メカニズムに従うように更新されました。

* パイプラインにアクセスするために当初は oAUTH 認証設定に基づいていた Triggers 統合認証が変更され、Adobe I/O に移動しました。[詳細情報](../../integrations/using/configuring-adobe-io.md)

* [iOS APN レガシーバイナリプロトコルのサポート終了](https://developer.apple.com/news/?id=c88acm2b)後は、このプロトコルを使用するすべてのインスタンスがアップグレード後に HTTP/2 プロトコルに更新されます。

* サーバーサイドリクエストフォージェリ（SSRF）問題に対する保護を強化するために、セキュリティ問題を修正しました。（NEO-27777）

* **エンリッチメント**&#x200B;アクティビティの実行時にワークフローが失敗する可能性がある問題を修正しました。（NEO-17338）

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard]  10 リリース{#gs-10}

_2020 年 7 月 7 日_

ビルド 9032@efd8a94 には、以下の修正が含まれています。

署名機能が無効な場合にトラッキングが機能しない問題を修正しました。（NEO-26411）

>[!CAUTION]
>
>クライアントコンソールをこのリリースに含まれるものにアップグレードすることをお勧めします。[このページ](../../installation/using/installing-the-client-console.md)を参照してください。

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 9 リリース{#gs-9}

_2020 年 6 月 22 日_

ビルド（9032@800be2e）には、以下の修正が含まれています。

* iOS HTTP2 コネクタが強化されました（サードパーティのアップデートおよびエラー管理）。（NEO-25904、NEO-25903、NEO-25799）

以下はトラッキングリンクのセキュリティメカニズムに関する修正です（詳しくは、[セキュリティとプライバシーのチェックリスト](https://helpx.adobe.com/jp/campaign/kb/acc-security.html#signature-mechanism)を参照してください）。

* 「通知クリック数」のトラッキングが機能しない問題を修正しました（iOS および Android のプッシュ通知）。（NEO-25965）
* 一部のレガシーバージョンの Outlook を使用する場合に、トラッキング URL を開いたりクリックしたりできない問題を修正しました。（NEO-25688）
* パーソナライゼーションパラメーター（シャープ記号の付いたアンカータグ）のフラグメントを使用した URL のトラッキングが機能しなかった問題を修正しました。（NEO-25774）
* フィッシング詐欺対策サービスの問題を修正しました。（NEO-25283）
* 特定のカスタムトラッキング式を使用する場合のトラッキングの問題を修正しました。（NEO-25277）

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 8 リリース{#gs-8}

_2020 年 4 月 29 日_

ビルド（9032@3a9dc9c）には、以下の修正が含まれています。

* E メール内のリンクの追跡に関するセキュリティを改善。これは、あらゆる顧客に対してデフォルトで有効です。さらに、強化されたセキュリティ機能が利用できます。この機能はカスタマーケアにご連絡いただくと有効にできます。これを非ホスト型顧客が有効にするための手順と機能の詳細については、[セキュリティおよびプライバシーチェックリスト](https://helpx.adobe.com/campaign/kb/acc-security.html#signature-mechanism)を参照してください。

>[!CAUTION]
>
>トラッキングリンクを使用したプッシュ通知、またはアンカータグを使用した配信で問題が発生した場合は、トラッキングリンク用の新しい署名メカニズムを無効にすることをお勧めします。手順について詳しくは、[このページ](https://helpx.adobe.com/campaign/kb/acc-security.html#signature-mechanism)を参照してください。

* LINE 配信に画像が表示されない可能性がある問題を修正しました。（NEO-23207）
* SFTP キーに基づく認証が Debian 9 で動作しない&#x200B;**ファイル転送**&#x200B;アクティビティの問題を修正しました。（NEO-23183）
* 高い頻度で送信されたときにプッシュ通知に影響を与える可能性がある問題を修正しました。（NEO-20516）
* Web サーバーのクラッシュを引き起こす可能性があるオファー応答管理の問題を修正しました。（NEO-19482）
* LibreOffice 管理で、レポートをエクスポートできなかったエラーを修正しました。（NEO-20982）
* 調査アクティビティを使用して多数のワークフローをアップグレードする場合にエラーが発生する問題を修正しました。
* .odt ファイルを含む E メールプレビューでエラーが発生しないように、LibreOffice の管理を改善しました。
* Apache 接続の管理を改善し、Web サービスでの待ち時間を回避しました。
* **バージョン情報**&#x200B;メニューでのバージョンタグ（7 桁）の表示を改善しました。
* リスト管理でオファーが公開されない問題を修正しました。
* クリーンアップワークフローがクラッシュする原因となる問題を修正しました。
* クリーンアップワークフローログの軽度の問題を修正しました。

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 6 リリース{#gs-6}

_2020 年 3 月 9 日_

ビルド（9032@19f73c5）には、以下の修正が含まれています。

* FTP over SSL を使用する外部アカウントの問題を修正しました。（NEO-20498）

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 5 リリース{#gs-5}

_2019 年 12 月 17 日_

ビルド（9032@d6b8062）には、以下の修正が含まれています。

* モバイル（SMS、MMS）、プッシュ（iOS、Android）およびソーシャルネットワーク（Facebook、Twitter）の各通信チャネルでのトラッキングの問題を修正しました。（NEO-19595）

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 4 リリース{#gs-4}

_2019 年 12 月 11 日_

ビルド（9032@bc4a935）には、以下の修正が含まれています。

* MSSQL データベースでメッセージを送信する際のパフォーマンスの問題を修正しました。（NEO-17558）

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 3 リリース{#gs-3}

_2019 年 11 月 20 日_

ビルド（9032@3468c7b）には、以下の修正が含まれています。

* IMS 認証を使用したログインの問題を修正しました。（NEO-17312）
* 複数の配信に関する累積レポートを表示する際の問題を修正しました。（NEO-18165）
* Web サーバーがブロックまたはクラッシュする可能性がある問題を修正しました。

## ![](assets/do-not-localize/red_2.png) [!DNL Gold Standard] 2 リリース{#gs-2}

_2019 年 9 月 19 日_

ビルド（9032@cee805c）には、以下の修正が含まれています。

* Salesforce 用 CRM コネクタを使用する際の問題を修正しました。（NEO-17712）
* トランザクションメッセージの送信時にパフォーマンスの問題を引き起こす可能性があるインデックスの問題を修正しました。

## ![](assets/do-not-localize/red_2.png) リリース 19.1.4 - ビルド 9032{#release-19-1-4-build-9032}

_2019 年 8 月 13 日_

初期の 19.1.4 ビルドには以下の修正が含まれています。

* スケジューラーアクティビティで、ウィザード設定時に望ましくないエラーメッセージが生成される問題を修正しました。NEO-11662 から、更新を元に戻します。（NEO-17097）
* テストアクティビティが 2 回実行された際にワークフローが停止する、NEO-12727 が原因の回帰を修正しました。（NEO-16835）
* 無効な、または期限切れのセッショントークンが API 呼び出しで使用されると、間違った HTTP コード（HTTP 403 Forbidden ではなく HTTP 200 OK）が返される問題を修正しました。（NEO-16826）
* DKIM キーが E メールに埋め込まれなくなった結果、配信品質が低下していた問題を修正しました。（NEO-16804）
* スケジューリングワークフローの様々な問題を修正しました。ワークフローは、スケジューラー設定を考慮することなく、1 日 1 回実行されるようにスケジュールされていました。（NEO-16619、NEO-16426）
