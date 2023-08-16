---
product: campaign
title: 一時ファイル
description: 一時ファイル
feature: Monitoring
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
badge-v7-prem: label="オンプレミスおよびハイブリッド" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: e77800f5-c0ae-446d-8ff3-bc8a18c97dbd
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 18%

---

# 一時ファイル{#temporary-files}



システムが実稼動環境に移行されると、次のようなエラーメッセージが（特に配信ログで）表示される場合があります。

*ファイル名「/tmp/tmp0000.tmp」を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません。（errno=18、無効なクロスデバイスリンク） (iRc=-52)*

原因は以下の通りです。

Adobe Campaignは、の下に一時ファイルを生成します。 **/tmp**&#x200B;の名前を変更して、に移動させます。 **/usr/local/neolane/nl6/var**. このエラーは、両方のフォルダー (**/tmp** および **/usr/local/neolane/nl6/var**&#x200B;これは、実際には、 **/var/nl6**) は様々なデバイスに対応します。 The **df** コマンドは、検証に使用されます。

この問題を解決するには、宛先と同じデバイスで一時ファイルを生成する必要があります。

例えば、次のコードを実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に、以下を追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```
