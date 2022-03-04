---
product: campaign
title: 受信ボックスレンダリングテクニカルワークフロー
description: ここでは、受信ボックスレンダリングパッケージと共にインストールされるテクニカルワークフローについて説明します。
feature: Workflows, Inbox Rendering
source-git-commit: b94c4bfd478b4a8fbcefe6341608dd6a14bb31d3
workflow-type: tm+mt
source-wordcount: '73'
ht-degree: 100%

---


# 受信ボックスレンダリング（IR）{#inbox-rendering}

![](../../assets/common.svg)

以下に説明するワークフローは、デフォルトで&#x200B;**受信ボックスレンダリング (IR)** モジュールと共にインストールされます。受信ボックスレンダリングについて詳しくは、[この節](../../delivery/using/inbox-rendering.md)を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>受信ボックスレンダリング用のシードネットワークを更新</strong><br /> </td> 
   <td> <span class="uicontrol">updateRenderingSeeds</span> <br /> </td> 
   <td> このワークフローは、<strong>deliverability.neolane.net</strong> の HTTPS ポートが開いている場合にのみ、受信ボックスレンダリングで使用される E メールアドレスを更新します。<br /> </td> 
  </tr> 
 </tbody> 
</table>

