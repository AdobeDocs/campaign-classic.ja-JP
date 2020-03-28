---
title: Adobe Campaign Classic の受信ボックスレンダリングテクニカルワークフロー
description: ここでは、Adobe Campaign Classic の受信ボックスレンダリングパッケージと共にインストールされるテクニカルワークフローについて説明します。
page-status-flag: never-activated
uuid: f60a09f0-47a0-4fc0-b0ac-47178af6ad55
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: technical-workflows
discoiquuid: da0779dc-b734-483b-81e9-ff4706a2b6de
index: y
internal: n
snippet: y
translation-type: ht
source-git-commit: e1bd878c45576932e085b579f91eb72f5d36d6fd

---


# 受信ボックスレンダリング (IR){#inbox-rendering}

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

