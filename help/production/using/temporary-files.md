---
product: campaign
title: 一時ファイル
description: 一時ファイル
feature: Monitoring
badge-v7-prem: label="オンプレミス/ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: e77800f5-c0ae-446d-8ff3-bc8a18c97dbd
source-git-commit: 14ba450ebff9bba6a36c0df07d715b7279604222
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 9%

---

# 一時ファイル{#temporary-files}



システムが実稼動環境に移行されると、次のようなエラーメッセージ（特に配信ログ内）が表示される場合があります。

*ファイル名「/tmp/tmp0000.tmp」を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません；（errno=18、無効なクロスデバイスリンク）（iRc=-52）*

原因は以下のとおりです。

Adobe Campaignは、次の場所にある一時ファイルを **/tmp**&#x200B;に変更してから、移動先の名前に変更します **/usr/local/neolane/nl6/var**. このエラーは、両方のフォルダー（**/tmp** および **/usr/local/neolane/nl6/var**（実際にはへのシンボリックリンク） **/var/nl6**）は異なるデバイスに対応します。 この **df** 検証にはコマンドが使用されます。

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
