---
title: 一時ファイル
seo-title: 一時ファイル
description: 一時ファイル
seo-description: null
page-status-flag: never-activated
uuid: ae7ec619-e93f-41fb-ba7c-fcbcf4cba84f
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: f18237b0-ef54-46a6-9c14-34b038f9de18
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 6%

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

