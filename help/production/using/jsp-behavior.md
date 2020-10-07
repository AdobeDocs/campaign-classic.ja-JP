---
title: JSP の動作
seo-title: JSP の動作
description: JSP の動作
seo-description: null
page-status-flag: never-activated
uuid: b9e9f348-968c-46e0-8340-df1f1fcaf3a3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: production
content-type: reference
topic-tags: troubleshooting
discoiquuid: 5dcc4090-effe-479e-8d5c-67e6a6542fbb
translation-type: tm+mt
source-git-commit: 70b143445b2e77128b9404e35d96b39694d55335
workflow-type: tm+mt
source-wordcount: '38'
ht-degree: 21%

---


# JSP の動作{#jsp-behavior}

特定の **jsp** ジョブが正常に実行されない場合は、再コンパイルを強制する必要があります。

この場合は、次のコマンドを入力します。

```
nlserver stop web
cd nl6/tomcat-7
rm -r work/
nlserver start web
```

次回の接続時に **jsp** ジョブが再生成されます。
