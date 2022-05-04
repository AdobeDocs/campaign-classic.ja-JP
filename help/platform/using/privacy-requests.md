---
product: campaign
title: プライバシーリクエストの管理
description: プライバシーリクエストについての説明
audience: platform
content-type: reference
topic-tags: starting-with-adobe-campaign
exl-id: c7688c2a-f0a7-4c51-a4cf-bf96fe8bf9b6
source-git-commit: a8044037e889f59d4288a0746001e84d319f6bcf
workflow-type: ht
source-wordcount: '530'
ht-degree: 100%

---

# プライバシーリクエストについて {#privacy-requests}

![](../../assets/v7-only.svg)

プライバシー管理に関する一般的なプレゼンテーションについては、[この節](privacy-management.md)を参照してください。

この情報は、GDPR、CCPA、PDPA、LGPD に適用されます。これらの規制について詳しくは、[こちら](privacy-management.md#privacy-management-regulations)を参照してください。

>[!NOTE]
>
>個人情報の販売のオプトアウト（CCPA に特有）については、[この節](#sale-of-personal-information-ccpa)を参照してください。

<!--Installation procedures described in this document are applicable starting Campaign Classic 18.4 (build 8931+). If you are running on a previous version, refer to this [technote](https://helpx.adobe.com/campaign/kb/how-to-install-gdpr-package-on-legacy-versions.html).-->

プライバシーの準備を容易にするために、Adobe Campaign でアクセス要求と削除要求の処理が可能になりました。**アクセス権利**&#x200B;と&#x200B;**忘れられる権利**（削除要求）については、[この節](privacy-management.md#right-access-forgotten)で説明しています。

Adobe Campaign では、データ管理者は 2 とおりの方法でプライバシーのアクセスリクエストおよび削除リクエストをおこなうことができます。

* **Adobe Campaign インターフェイス**&#x200B;を使用する：データ管理者はプライバシーリクエストごとに Adobe Campaign で新しいプライバシーリクエストを作成できます。[こちらの節](privacy-requests-ui.md)を参照してください。
* **API** を使用する：Adobe Campaign の API により、SOAP を使用してプライバシーリクエストを自動処理できます。[こちらの節](privacy-requests-api.md)を参照してください。

>[!NOTE]
>
>個人データおよびデータを管理する様々なエンティティ（データ管理者、データ処理者、データ主体）について詳しくは、[個人データとペルソナ](privacy-and-recommendations.md#personal-data)を参照してください。

## 前提条件 {#prerequesites}

Adobe Campaign には、Adobe Campaign に保存されているデータに対するプライバシーリクエストの作成と処理をおこなうためのデータ管理者用ツールが用意されています。ただし、データ主体とのやり取り（E メール、カスタマーサポート、Web ポータル）はデータ管理者がおこなう必要があります。

また、要求者であるデータ主体の身元の確認、および要求者に返されるデータがデータ主体に関するものであることの確認は、データ管理者がおこないます。

## プライバシーパッケージのインストール {#install-privacy-package}

この機能を使用するには、**[!UICONTROL ツール]**／**[!UICONTROL 詳細設定]**／**[!UICONTROL パッケージをインポート]**／**[!UICONTROL Adobe Campaign パッケージ]**&#x200B;メニューから&#x200B;**[!UICONTROL プライバシーデータ保護規則]**&#x200B;パッケージをインストールする必要があります。パッケージのインストール方法について詳しくは、[詳細ドキュメント](../../installation/using/installing-campaign-standard-packages.md)を参照してください。

**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**&#x200B;に、プライバシー専用の 2 つのフォルダーが新しく作成されます。

* **[!UICONTROL プライバシーリクエスト]**：プライバシーリクエストを作成し、その推移をトラッキングする場所です。
* **[!UICONTROL 名前空間]**：Adobe Campaign データベースでデータ主体を識別するために使用するフィールドを定義する場所です。

![](assets/privacy-folders.png)

**[!UICONTROL 管理]**／**[!UICONTROL プロダクション]**／**[!UICONTROL テクニカルワークフロー]**&#x200B;で、プライバシーリクエストを処理するための 3 つのテクニカルワークフローが毎日実行されます。

![](assets/privacy-workflows.png)

* **[!UICONTROL プライバシーリクエストを収集]**：このワークフローでは、Adobe Campaign に保存されている受信者のデータを生成し、プライバシーリクエストの画面でダウンロードできるようにします。
* **[!UICONTROL プライバシーリクエストデータを削除]**：このワークフローでは、Adobe Campaign に保存されている受信者のデータを削除します。
* **[!UICONTROL プライバシーリクエストのクリーンアップ]**：このワークフローでは、90 日より古いアクセスリクエストファイルが消去されます。

**[!UICONTROL 管理]**／**[!UICONTROL アクセス管理]**／**[!UICONTROL ネームド権限]**&#x200B;に、**[!UICONTROL プライバシーデータ権限]**&#x200B;というネームド権限が追加されました。このネームド権限は、データ管理者がプライバシーツールを使用する場合に必要となります。これにより、新しいリクエストの作成、推移のトラッキング、API の使用などができるようになります。

![](assets/privacy-right.png)

## 名前空間 {#namesspaces}

プライバシーリクエストを作成する前に、使用する名前空間を定義する必要があります。これは、Adobe Campaign データベースでデータ主体を識別するために使用するキーです。

標準では、E メール、電話、携帯電話の 3 つの名前空間を使用できます。別の名前空間（受信者用のカスタムフィールドなど）が必要な場合、**[!UICONTROL 管理]**／**[!UICONTROL プラットフォーム]**／**[!UICONTROL 名前空間]**&#x200B;で新しく作成することができます。

>[!NOTE]
>
>最適なパフォーマンスを得るには、標準の名前空間を使用することをお勧めします。
