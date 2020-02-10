---
title: JSPの動作
seo-title: JSPの動作
description: JSPの動作
seo-description: null
page-status-flag: never-activated
uuid: b9e9f348-968c-46e0-8340-df1f1fcaf3a3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 5dcc4090-effe-479e-8d5c-67e6a6542fbb
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 579329d9194115065dff2c192deb0376c75e67bd

---


# JSPの動作{#jsp-behavior}

特定の **jspジョブが** 、正常に実行されない場合は、再コンパイルを強制する必要があります。

この場合は、次のコマンドを入力します。

```
nlserver stop web
cd nl6/tomcat-7
rm -r work/
nlserver start web
```

次回 **接続すると** 、JSPジョブが再生成されます。
