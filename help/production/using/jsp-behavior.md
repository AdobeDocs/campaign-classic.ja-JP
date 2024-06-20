---
product: campaign
title: JSP の動作
description: JSP の動作
feature: Monitoring
badge-v7-prem: label="オンプレミス／ハイブリッドのみ" type="Caution" url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"
audience: production
content-type: reference
topic-tags: troubleshooting
exl-id: 858d00d0-7c65-43be-8bae-f0f945f71f1a
source-git-commit: 757e3a5395f24e0bdd04737aba0458881e4ea780
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 36%

---

# JSP の動作{#jsp-behavior}



特定の場合 **jsp** ジョブが正常に実行されていません。強制的に再コンパイルする必要があります。

それには、次のコマンドを入力します。

```
nlserver stop web
cd nl6/tomcat-X
rm -r work/
nlserver start web
```

この **jsp** ジョブは、次回接続する際に再生成されます。
