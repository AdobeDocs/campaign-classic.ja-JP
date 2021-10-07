---
product: campaign
title: JSP の動作
description: JSP の動作
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 858d00d0-7c65-43be-8bae-f0f945f71f1a
source-git-commit: 20509f44c5b8e0827a09f44dffdf2ec9d11652a1
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 16%

---

# JSP の動作{#jsp-behavior}

![](../../assets/v7-only.svg)

特定の **jsp** ジョブが正常に実行されない場合は、再コンパイルを強制する必要があります。

この場合は、次のコマンドを入力します。

```
nlserver stop web
cd nl6/tomcat-8
rm -r work/
nlserver start web
```

**jsp** ジョブは次回接続すると再生成されます。
