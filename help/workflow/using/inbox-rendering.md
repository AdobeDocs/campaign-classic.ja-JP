---
title: Adobe Campaign Classicのインボックスレンダリング技術ワークフロー
description: ここでは、Adobe Campaign Classicのインボックスレンダリングパッケージと共にインストールされる技術ワークフローについて説明します。
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
translation-type: tm+mt
source-git-commit: e1bd878c45576932e085b579f91eb72f5d36d6fd

---


# Inbox rendering (IR){#inbox-rendering}

The workflow detailed below is installed with the **Inbox rendering (IR)** module by default. インボックスのレンダリングの詳細については、この節を参照し [てくださ](../../delivery/using/inbox-rendering.md)い。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>ラベル</strong><br /> </td> 
   <td> <strong>内部名</strong><br /> </td> 
   <td> <strong>説明</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> <strong>受信ボックスレンダリング用のシードネットワークを更新</strong><br /> </td> 
   <td> <span class="uicontrol">updateRenderingSeeds</span><br /> </td> 
   <td> This workflow updates email addresses used for Inbox rendering and only works if the HTTPS port is open for <strong>deliverability.neolane.net</strong>.<br /> </td> 
  </tr> 
 </tbody> 
</table>

