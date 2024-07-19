---
product: campaign
title: 一時ファイル
description: 一時ファイル
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: e77800f5-c0ae-446d-8ff3-bc8a18c97dbd
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 11%

---

# 一時ファイル{#temporary-files}



システムが実稼動環境に移行されると、次のようなエラーメッセージ（特に配信ログ内）が表示される場合があります。

*ファイル「/tmp/tmp0000.tmp」の名前を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません；（errno=18、無効なクロスデバイスリンク）（iRc=-52）*

原因は以下のとおりです。

Adobe Campaignは **/tmp** の下に一時ファイルを生成し、それらの名前を変更して **/usr/local/neolane/nl6/var** に移動します。 このエラーは、両方のフォルダー（**/tmp** と **/usr/local/neolane/nl6/var** （実際には **/var/nl6** へのシンボリックリンク）が異なるデバイスに対応している場合に発生します。 検証には **df** コマンドを使用します。

この問題を修正するには、一時ファイルを宛先と同じデバイスに生成する必要があります。

例えば、次を実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に、以下を追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```
