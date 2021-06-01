---
product: campaign
title: 一時ファイル
description: 一時ファイル
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: e77800f5-c0ae-446d-8ff3-bc8a18c97dbd
source-git-commit: 98d646919fedc66ee9145522ad0c5f15b25dbf2e
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 4%

---

# 一時ファイル{#temporary-files}

システムが実稼動環境に移行されると、次のようなエラーメッセージ（特に配信ログ）が表示される場合があります。

*ファイル名を/tmp/tmp0000.tmpから/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません。（errno=18、無効なクロスデバイスリンク） (iRc=-52)*

原因は次のとおりです。

Adobe Campaignは&#x200B;**/tmp**&#x200B;の下に一時ファイルを生成し、名前を変更して&#x200B;**/usr/local/neolane/nl6/var**&#x200B;に移動します。 このエラーは、フォルダー（**/tmp**&#x200B;と&#x200B;**/usr/local/neolane/nl6/var**、実際には&#x200B;**/var/nl6**&#x200B;へのシンボリックリンク）が異なるデバイスに対応する場合に発生します。 **df**&#x200B;コマンドは検証に使用されます。

この問題を解決するには、一時ファイルを宛先と同じデバイスに生成する必要があります。

例えば、次の操作を実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に、以下を追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```
