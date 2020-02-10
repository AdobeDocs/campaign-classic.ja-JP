---
title: マルチブランディングの設定
seo-title: マルチブランディングの設定
description: マルチブランディングの設定
seo-description: null
page-status-flag: never-activated
uuid: 61b4235c-da03-4da8-b14b-7ffb12c8d4c8
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: message-center
content-type: reference
topic-tags: instance-configuration
discoiquuid: 907d82c8-9262-4952-b8df-21144dd55824
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: d5eac80743d4cc82cdf55aa9287e8bb4fcc84356

---


# マルチブランディングの設定{#configuring-multibranding}

この節では、Adobe Campaign でトランザクションメッセージのためのブランドごとのトラッキングとミラーページの URL を設定する方法について説明します。

## 前提条件 {#prerequisites}

* All of the hosts must be added to the configuration file of the instance (`config-<instance>.xml`).
* 各ブランドはそれぞれ 1 つのサブドメインに割り当てられていなければなりません。
* HTTPS ページで Web トラッキングをしている場合、すべてのブランドについて HTTPS 証明証を持っていなければなりません。

## 典型的な手順 {#typical-process}

マルチブランディングを設定するには、実行インスタンスとコントロールインスタンスの両方を設定する必要があります。実行インスタンスで、以下の手順に従います。

1. 各ブランドごとに外部アカウントを 1 つ作成します。

   >[!NOTE]
   >
   >Creating an execution instance type external account is presented in the [Control instance](../../message-center/using/creating-a-shared-connection.md#control-instance) section.

1. nms:extAccount スキーマを拡張し、トラッキング URL を追加します。

   ```
   <attribute advanced="true" desc="URL of the tracking servers" label="Tracking server URL"
   length="100" name="trackingURL" type="string"/>
   ```

   >[!NOTE]
   >
   >既存のスキーマの拡張は、[スキーマの拡張](../../configuration/using/extending-a-schema.md)の節で説明されています。

1. nms:extAccount フォームを変更します。

   ```
   <container label="Message domain branding" type="frame">
        <static type="help"> These parameters are used to override the DNS alias and addresses used during message delivery. When not populated, the values of the 'NmsServer_MirrorPageUrl' and 'NmsEmail_DefaultErrorAddr' options are used.</static>
        <input xpath="@mirrorURL"/>
        <input xpath="@trackingURL"/>
        <input img="nms:sendemail.png" menuId="deliveryMenuBuilder" type="scriptEdit">
               xpath="errorAddress"/>
      </container>
   ```

1. NmsTracking_OpenFormula および NmsTracking_ClickFormula オプションを変更し、グローバルオプションの代わりに外部アカウントを使用するようにします。

   これには、

   ```
   <%@ include option='NmsTracking_ServerUrl' %>
   ```

   を以下で置き換えます。

   ```
   <%@ value object="provider" xpath="@trackingURL" %>
   ```

   >[!CAUTION]
   >
   >これらの変更は、アップグレードの際に競合を引き起こすことがあります。これらの数式と新しいバージョンの数式とを手動で統合させなければならない可能性があります。

コントロールインスタンスでは、配信テンプレートと外部アカウントをリンクする必要があります。そのためには、以下の手順を実行します。

1. 手順 1 で定義したように、各ブランドにつき外部アカウントを 1 つ作成し、内部名を同一にします。
1. 各ブランドにつきデフォルトの配信テンプレートを 1 つ作成します。
1. In the delivery template&#39;s **[!UICONTROL Properties]** , set the routing to the external account of the brand.

