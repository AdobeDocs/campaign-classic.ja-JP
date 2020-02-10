---
title: 配信に関するレポート
seo-title: 配信に関するレポート
description: 配信に関するレポート
seo-description: null
page-status-flag: never-activated
uuid: 83ea834e-08f7-441b-8f15-a25ec07c4aab
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: reporting
content-type: reference
topic-tags: accessing-built-in-reports
discoiquuid: cc832666-ad18-49ce-afcc-f9169b683ae8
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: f7655cd93a7dc8ecd35cd379da350ad279cae725

---


# 人／ユーザーと受信者 {#person-people-and-recipients}

このサンプルは、Adobe Campaign における人／ユーザーと受信者との違いを理解するのに役立ちます。ここでは、次の指標に対する計算方式を説明しながら、ユーザーと受信者の違いに注目するために何人かのユーザーに配信を送信します。

* **[!UICONTROL Clicks]**
* **[!UICONTROL Distinct clicks for the population reached]**
* **[!UICONTROL Distinct opens for the population reached]**
* **[!UICONTROL Estimation of forwards]**
* **[!UICONTROL Raw reactivity]**

>[!NOTE]
>
>These indicators are used in the **[!UICONTROL Tracking indicators]** report. For more on this, refer to [Tracking indicators](#tracking-indicators).

3 つのリンクが配信に追加されています。これが 4 人の受信者に送信されます。

![](assets/s_ncs_user_indicators_example_1.png)

* **[!UICONTROL John Davis]**：この受信者は E メールを開封していません（したがって、リンクもクリックしていません）。
* **[!UICONTROL Marie Stuart]**：E メールを開封しましたが、リンクはクリックしていません。
* **[!UICONTROL Florian David]**：E メールを開封してリンクを 9 回クリックしました。また、この E メールを他のユーザーに転送し、このユーザーが E メールを開封してリンクを 2 回クリックしました。
* **[!UICONTROL Henry Macdonald]**：この受信者は、インターネットブラウザーで cookie を拒否するように設定しています。E メールを開封してリンクを 4 回クリックしました。

次のトラッキングログが返されます。

![](assets/s_ncs_user_indicators_example_2.png)

ユーザーと受信者のカウント方法についてより明確に理解するために、各プロファイルのログを分析します。

## 手順1:ジョン {#step-1--john}

**[!UICONTROL John Davis]** は E メールを開封していません（したがって、リンクもクリックしていません）。

![](assets/s_ncs_user_indicators_example_8.png)

John は E メールを開封しておらずクリックもしていないので、ログには表示されません。

**中間計算：**

|  | クリックした受信者数 | クリックしたユーザー数 | 開封した受信者数 |
|---|---|---|---|
| John | - | - | - |
| 小計 | 0 | 0 | 0 |

## 手順2:麻里恵 {#step-2--marie}

**[!UICONTROL Marie Stuart]** は E メールを開封しましたが、リンクはクリックしていません。

![](assets/s_ncs_user_indicators_example_7.png)

Marie の開封は次のログに表示されています。

![](assets/s_ncs_user_indicators_example_4bis.png)

開封は受信者に割り当てられます。マリー。 Adobe Campaign によって新しい受信者がカウントに追加されます。

**中間計算：**

|  | クリックした受信者数 | クリックしたユーザー数 | 開封した受信者数 |
|---|---|---|---|
| John | - | - | - |
| Marie | - | - | +1 |
| 小計 | 0 | 0 | 1 |

## 手順3:フロリアン {#step-3--florian}

**[!UICONTROL Florian David]** は、E メールを開封してリンクを 9 回クリックしました。また、この E メールを他のユーザーに転送し、このユーザーが E メールを開封してリンクを 2 回クリックしました。

![](assets/s_ncs_user_indicators_example_9.png)

Florian のアクション（1 回の開封と 9 回のクリック）は、次のログに表示されています。

![](assets/s_ncs_user_indicators_example_3bis.png)

**受信者**：開封とクリックは同じ受信者（Florian）に割り当てられています。受信者が前の受信者（Marile）と異なるので、Adobe Campaign によって新しい受信者がカウントに追加されます。

People: Since this recipient&#39;s browser accepts cookies, we can see that the same identifier (UUID) is assigned to all click logs: **`fe37a503 [...]`**. Adobe Campaign は、これらのクリックが同じユーザーに属することを正しく識別します。新しいユーザーがカウントに追加されます。

**中間計算：**

|  | クリックした受信者数 | クリックしたユーザー数 | 開封した受信者数 |
|---|---|---|---|
| John | - | - | - |
| Marie | - | - | +1 |
| Florian | +1 | +1 | +1 |
| 小計 | 1 | 1 | 2 |

次のログは、Florian が E メールを転送したユーザーによって実行された開封および 2 回のクリックと一致します。

![](assets/s_ncs_user_indicators_example_6bis.png)

**受信者**：開封とクリックは E メールを転送した受信者（Florian）に割り当てられています。この受信者は既にカウントされているので、受信者のカウントは同じままです。

![](assets/s_ncs_user_indicators_example_12.png)

**人**:クリック数に関しては、すべてのログに同じ識別子(UUID)が割り当てられていることがわかります。 **`9ab648f9 [...]`**. この識別子はまだカウントされていません。したがって、新しいユーザーがカウントに追加されます。

![](assets/s_ncs_user_indicators_example_13.png)

**中間計算：**

|  | クリックした受信者数 | クリックしたユーザー数 | 開封した受信者数 |
|---|---|---|---|
| John | - | - | - |
| Marie | - | - | +1 |
| Florian | +1 | +1 | +1 |
| 不明なユーザー | - | +1 | - |
| 小計 | 1 | 2 | 2 |

## 手順4:ヘンリー {#step-4--henry}

**[!UICONTROL Henry Macdonald]** は、インターネットブラウザーでcookieを拒否するように設定しています。 E メールを開封してリンクを 4 回クリックしました。

![](assets/s_ncs_user_indicators_example_10.png)

Henry が実行した開封と 4 回のクリックは、次のログに表示されています。

![](assets/s_ncs_user_indicators_example_5bis.png)

**受信者**：開封とクリックは同じ受信者（Henry）に割り当てられています。この受信者はまだカウントされていないので、Adobe Campaign によって 1 人の受信者がカウントに追加されます。

**人**:Henryのブラウザーはcookieを受け入れないので、クリックごとに新しい識別子(UUID)が生成されます。 4 回のクリックのそれぞれを、異なるユーザーがおこなっていると解釈されます。これらの識別子はまだカウントされていないので、カウントに追加されます。

**中間計算：**

|  | クリックした受信者数 | クリックしたユーザー数 | 開封した受信者数 |
|---|---|---|---|
| John | - | - | - |
| Marie | - | - | +1 |
| Florian | +1 | +1 | +1 |
| 不明なユーザー | - | +1 | - |
| Henry | +1 | +4 | +1 |
| 小計 | 2 | 2018 年 | 3 |

## まとめ {#summary}

配信レベルでは、次の結果が得られます。

![](assets/s_ncs_user_indicators_example.png)

* **[!UICONTROL Clicks]** （クリックした受信者）:2
* **[!UICONTROL Distinct clicks for the population reached]** （クリックした人）:6
* **[!UICONTROL Distinct opens for the population reached]** （開いた受信者）:3

反応率（生データ）と推定転送数は、下記のように計算されます。

![](assets/s_ncs_user_indicators_example11.png)

* **[!UICONTROL Estimation of forwards]** = **B - A** （したがって6 - 2 = 4）
* **[!UICONTROL Raw reactivity]** = **A / C** （つまり2 / 3 = 66,67%）

>[!NOTE]
>
>この計算式について：
>
>* A represents the **[!UICONTROL Clicks]** indicator (recipients who clicked).
>* Bはインジケータ **[!UICONTROL Distinct clicks for the population reached]** ー（クリックした人）を表します。
>* Cはインジケータ **[!UICONTROL Distinct opens for the population reached]** ー（開いた受信者）を表します。