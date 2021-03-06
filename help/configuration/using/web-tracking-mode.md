---
product: campaign
title: Web トラッキングモード
description: Web トラッキングモードの選択方法を説明します
exl-id: b0f30c1f-cdc9-4ad2-8a6c-19d5aae4feb3
source-git-commit: 56459b188ee966cdb578c415fcdfa485dcbed355
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Web トラッキングモード{#web-tracking-mode}

![](../../assets/v7-only.svg)

Adobe Campaignでは、アプリケーションでトラッキングログを処理する方法を定義する web トラッキングモードを選択できます。

次の 3 つの Web トラッキングモードが使用可能です。 **&quot;セッショントラッキング&quot;**,**&quot;永続的なトラッキング&quot;** および **&quot;匿名トラッキング&quot;**.

![](assets/s_ncs_install_deployment_wiz_tracking_mode.png)

各モードには、固有の特性があります。 「永続的な」Web トラッキングモードには「セッション」Web トラッキングモードの特性が含まれ、「匿名」モードには「永続」および「セッション」モードの特性が含まれます。

>[!IMPORTANT]
>
>「匿名」Web トラッキングモードは、「リード」パッケージが有効になっている場合、デフォルトで有効になります。 それ以外の場合は、「セッション」Web トラッキングモードがデフォルトで有効になっています。
>
>デフォルトのモードは、インスタンスデプロイウィザードでいつでも変更できます。

なお、 **永続的なウェブ** または **匿名** トラッキングモードの場合、トラッキングテーブル (trackingLogXXX) の「sourceID」列 (uuid230) にインデックスを追加する必要があります。

1. 永続的なトラッキングに関係するトラッキングテーブルを特定します。
1. 次の行を追加して、これらのテーブルに一致するスキーマを拡張します。

```
<dbindex name="sourceId">
 <keyfield xpath="@sourceId"/>
</dbindex>
```

**永続的** および **匿名** Web トラッキングモードには次の 2 つのオプションがあります。 **強制配信** および **最終配信**.

この **強制配信** 「 」オプションを使用すると、トラッキング中に配信の識別子 (@jobid) を指定できます。

この **最終配信** 「 」オプションを使用すると、現在のトラッキングログを最後にトラッキングした配信にリンクできます。

**セッション Web トラッキングの特徴：**

このモードでは、セッション Cookie を持つユーザーのトラッキングログが作成されます。 Adobe Campaignから送信された E メールの URL をクリックしたユーザーなので、以下の情報を追跡できます。

* 配信 ID
* 連絡先 ID
* 配信ログ
* 永続 Cookie (uuid230)
* トラッキング URL
* トラッキングログの日付

この Web トラッキングモードでは、情報の一部が見つからない場合、アプリケーションにトラッキングログは作成されません。

このモードは、ボリューム（trackingLog テーブルのレコード数は制限）と計算（紐付けなし）の点で経済的です。

**永続的な Web トラッキングモードの特性：**

この Web トラッキングモードでは、永続的な uuid230 cookie の存在に基づいてトラッキングログを作成できます。 訪問者がセッションを閉じた場合、Adobe Campaignは永続的な Cookie を使用して、以前のトラッキングログから情報を取得します。 現在のセッションの uuid230 がトラッキングテーブルに既に格納されている uuid230 と同じ値の場合、Adobe Campaignはトラッキングログを再挿入します。

つまり、uuid230 値に対する紐付けを有効にするには、訪問者が（配信を介して）Adobe Campaignで以前に識別されている必要があります。

デフォルトでは、以前のトラッキングログの検索は、「trackingLog」テーブルで実行されます。 リードパッケージが有効な場合、Adobe Campaignは「trackingLog」テーブルを検索する前に、「incomingLead」テーブルで以前のトラッキングログレコードを検索します。

このモードは、ログの紐付け中の計算の観点からはコストがかかります。

**匿名 Web トラッキングモードの特徴は次のとおりです。**

この Web トラッキングモードを使用すると、Adobe Campaignでの匿名ブラウジングにリンクされたトラッキングログを取得できます。 トラッキング対象 URL のクリックごとに、トラッキングログが自動的に作成されます。 このログには、uuid230 の値のみが含まれます。 マーケティングキャンペーン中、トラッキングログはすべての識別情報と共に自動的に作成されます（セッショントラッキングを参照）。 Adobe Campaignは、以前のログを自動的に検索し、このマーケティングキャンペーンのトラッキングログの値と等しい「uuid230」値を探します。 同じ値が見つかった場合、以前のすべてのトラッキングログに、マーケティングキャンペーントラッキングログのすべての情報が入力されます。

このモードは、計算とボリュームの点で最もコストがかかります。

>[!NOTE]
>
>この **[!UICONTROL リード]** パッケージがインストールされている場合は、アクティビティテーブル (**crm:incomingLead**)

次のスキーマは、3 つの Web トラッキングモードすべての機能を合計したものです。

![](assets/s_ncs_install_deployment_wiz_tracking_schema_mode.png)

**最後の配信に基づく永続的な Web トラッキングの例：**

Florence は配信を受け取り、E メールを開いてリンクをクリックし、小売サイトを閲覧しますが、何も購入しません。 次の日、Florence は小売サイトに戻り、閲覧して購入します。 永続的な Web トラッキング（最終配信）が有効なので、2 回目の訪問のすべてのログは、前日に送信された配信にリンクされます。
