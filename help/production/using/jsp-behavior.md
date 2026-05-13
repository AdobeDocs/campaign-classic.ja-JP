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
TQID: https://experienceleague.adobe.com/IQSjBaSbnZcsqs0glv8z1aIwOBbtVO2roeXlJiYgEfo
product_v2: id: dfc56824-e8b9-499e-85d4-21aedb507314
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 4c295c0dabae8aba298390a3da2422a3fa1219f9
workflow-type: tm+mt
source-wordcount: 66
ht-degree: 54%

---

# JSP の動作{#jsp-behavior}



特定の&#x200B;**jsp** ジョブが正常に実行されない場合は、強制的に再コンパイルする必要があります。

これには、次のコマンドを入力します。

```
nlserver stop web
cd nl6/tomcat-X
rm -r work/
nlserver start web
```

次回の接続時に&#x200B;**jsp** ジョブが再生成されます。
