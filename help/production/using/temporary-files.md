---
solution: Campaign Classic
product: campaign
title: 一時ファイル
description: 一時ファイル
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 4%

---


# 一時ファイル{#temporary-files}

システムが実稼働環境に移行する際に、次のようなエラーメッセージが(特に配信ログで)表示される場合：

**ファイル&#39;/tmp/tmp0000.tmp&#39;を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに名前変更できません。(errno=18, Invalid cross-device link) (iRc=-52)**

原因は以下の通り。

Adobe Campaignは、 **/tmp**&#x200B;下に一時ファイルを生成し、名前を変更して/usr/local/neolane/nl6/varに移動します ****。 このエラーは、両方のフォルダ(**/tmp** と/usr/local/neolane/nl6/var **)が異なるデバイスに対応している場合に発生します。これは、**/var/nl6 ****&#x200B;へのシンボリックリンクです。 検証には **df** コマンドを使用します。

この問題を修正するには、一時ファイルを宛先と同じデバイスに生成する必要があります。 例えば、次を実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に、次に追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```

