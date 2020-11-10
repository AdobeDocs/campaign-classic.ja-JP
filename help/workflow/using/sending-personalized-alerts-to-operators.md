---
title: パーソナライズされたアラートのオペレーターへの送信
description: 操作者にパーソナライズされたアラートを送信する方法を説明します。
page-status-flag: never-activated
uuid: 10dd46b9-df28-4043-91f9-c9316a7c69d3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: workflow
content-type: reference
topic-tags: use-cases
discoiquuid: 4d72db10-29bd-4b3c-adb3-bead02890271
translation-type: tm+mt
source-git-commit: 6be6c353c3464839a74ba857d8d93d0f68bc8865
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 97%

---


# パーソナライズされたアラートのオペレーターへの送信{#sending-personalized-alerts-to-operators}

この例では、ニュースレターを開封したがそれに含まれるリンクをクリックしなかったプロファイルの名前を記載したアラートをオペレーターに送信します。

プロファイルの氏名フィールドは&#x200B;**[!UICONTROL 受信者]**&#x200B;ターゲティングディメンションにリンクされているのに対して、**[!UICONTROL アラート]**&#x200B;アクティビティは&#x200B;**[!UICONTROL オペレーター]**&#x200B;ターゲティングディメンションにリンクされています。結果として、2 つのターゲティングディメンション間で、紐付けを実行し、氏名フィールドを取得して、アラートアクティビティに表示するのに使用できるフィールドはありません。

このプロセスでは、次のようにワークフローを構築できます。

1. **[!UICONTROL クエリ]**&#x200B;アクティビティを使用して、データをターゲットにします。
1. **[!UICONTROL JavaScript コード]**&#x200B;アクティビティをワークフローに追加して、クエリからインスタンス変数に母集団を保存します。
1. **[!UICONTROL テスト]**&#x200B;アクティビティを使用して、母集団の数を確認します。
1. **[!UICONTROL アラート]**&#x200B;アクティビティを使用して、**[!UICONTROL テスト]**&#x200B;アクティビティの結果に応じて、オペレーターにアラートを送信します。

![](assets/uc_operator_1.png)

## 母集団のインスタンス変数への保存 {#saving-the-population-to-the-instance-variable}

以下のコードを **[!UICONTROL JavaScript コード]**&#x200B;アクティビティに追加します。

```
var query = xtk.queryDef.create(  
    <queryDef schema="temp:query" operation="select">  
      <select>  
       <node expr="[target/recipient.@firstName]"/>  
       <node expr="[target/recipient.@lastName]"/>  
      </select>  
     </queryDef>  
  );  
  var items = query.ExecuteQuery();
```

JavaScript コードがワークフロー情報に対応していることを確認します。

* **[!UICONTROL queryDef schema]** タグは、クエリアクティビティで使用されるターゲティングディメンションの名前に対応している必要があります。
* **[!UICONTROL node expr]** タグは、取得するフィールドの名前に対応している必要があります。

![](assets/uc_operator_3.png)

これらの情報を取得するには、以下の手順に従います。

1. **[!UICONTROL クエリ]**&#x200B;アクティビティからアウトバウンドトランジションを右クリックし、「**[!UICONTROL ターゲットを表示]**」を選択します。

   ![](assets/uc_operator_4.png)

1. リストを右クリックして、「**[!UICONTROL リストを設定]**」を選択します。

   ![](assets/uc_operator_5.png)

1. クエリターゲティングディメンションおよびフィールド名がリストに表示されます。

   ![](assets/uc_operator_6.png)

## 母集団の数のテスト {#testing-the-population-count}

以下のコードを&#x200B;**[!UICONTROL テスト]**&#x200B;アクティビティに追加して、ターゲットにした母集団が少なくとも 1 つのプロファイルを含むかどうかを確認します。

```
var.recCount>0
```

![](assets/uc_operator_7.png)

## アラートの設定 {#setting-up-the-alert}

これで、母集団が目的のフィールドを含むインスタンス変数に追加されたので、これらの情報を&#x200B;**[!UICONTROL アラート]**&#x200B;アクティビティに追加できます。

そのためには、「**[!UICONTROL ソース]**」タブに以下のコードを追加します。

```
<ul>
<%
var items = new XML(instance.vars.items)
for each (var item in items){
%>
<li><%= item.target.@firstName %> <%= item.target.@lastName %></li>
<%
} %></ul>
```

>[!NOTE]
>
>**[!UICONTROL 「&lt;%= item.target.recipient.@fieldName %>」]** コマンドを使用すると、**[!UICONTROL JavaScript コード]**&#x200B;アクティビティでインスタンス変数に保存したフィールドのいずれかを追加できます。\
>フィールドが JavaScript コードに追加されている限り、フィールドを好きな数だけ追加できます。

![](assets/uc_operator_8.png)

