---
product: campaign
title: 一時ファイル
description: 一時ファイル
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: e77800f5-c0ae-446d-8ff3-bc8a18c97dbd
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 4%

---

# 一時ファイル{#temporary-files}

![](../../assets/v7-only.svg)

システムが実稼動環境に移行すると、次のようなエラーメッセージが（特に配信ログに）表示される場合があります。

*ファイルの名前を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません。（errno=18、無効なクロスデバイスリンク） (iRc=-52)*

原因は次のとおりです。

Adobe Campaignは **/tmp** の下に一時ファイルを生成し、名前を変更して **/usr/local/neolane/nl6/var** に移動します。 このエラーは、両方のフォルダー（**/tmp** と **/usr/local/neolane/nl6/var**、実際には **/var/nl6** へのシンボリックリンク）が異なるデバイスに対応している場合に発生します。 **df** コマンドは検証に使用されます。

この問題を解決するには、一時ファイルを宛先と同じデバイスに生成する必要があります。

例えば、次のコマンドを実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に、以下を追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```
