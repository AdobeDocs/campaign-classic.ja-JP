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
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2a11a73b0679c0a65dc10f71869bf2a6c6efc008

---


# 一時ファイル{#temporary-files}

システムを実稼働環境に移行すると、次のようなエラーメッセージが（特に配信ログに）表示される場合：

**ファイル&#39;/tmp/tmp0000.tmp&#39;の名前を/usr/local/neolane/nl6/bin/..//var/XXX/mta/86510470.xmlに変更できません。（errno=18、無効なデバイス間リンク） (iRc=-52)**

原因は以下の通り。

Adobe Campaignは、 **/tmp******. このエラーは、両方のフォルダ(**/tmp** 、 **/usr/local/neolane/nl6/var**(実際には/var/nl6 ****)が異なるデバイスに対応している場合に発生します。 dfコマ **ンドは** 、検証に使用します。

この問題を修正するには、一時ファイルを宛先と同じデバイスで生成する必要があります。 例えば、次のように実行します。

```
$ cd ~/nl6/var
$ mkdir tmp
$ vi ~/nl6/customer.sh
```

次に、次に追加します。

```
export TMPDIR=/usr/local/neolane/nl6/var/tmp 
```

