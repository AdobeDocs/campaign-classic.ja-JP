---
solution: Campaign Classic
product: campaign
title: JSP の動作
description: JSP の動作
audience: production
content-type: reference
topic-tags: troubleshooting
translation-type: tm+mt
source-git-commit: 972885c3a38bcd3a260574bacbb3f507e11ae05b
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 16%

---


# JSP の動作{#jsp-behavior}

特定の&#x200B;**jsp**&#x200B;ジョブが正常に実行されない場合は、強制的に再コンパイルする必要があります。

この場合は、次のコマンドを入力します。

```
nlserver stop web
cd nl6/tomcat-8
rm -r work/
nlserver start web
```

**jsp**&#x200B;ジョブは、次回接続する際に再生成されます。
