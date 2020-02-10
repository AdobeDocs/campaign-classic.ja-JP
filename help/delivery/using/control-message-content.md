---
title: Adobe Campaign Classicの配信品質について
description: Adobe Campaign Classicでの配信品質の管理について説明します。
page-status-flag: never-activated
uuid: 2681042b-3018-42ae-b252-2367b56616bd
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: deliverability-management
discoiquuid: 6a394eeb-fbe1-4712-bb13-db5d7965fb73
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 68756f920fbc8658cff552615adbf023b4c5e3aa

---


# メッセージ内容の制御{#control-message-content}

電子メールの配信品質を向上させ、電子メールが確実に受信者に届くようにするには、電子メールは以下に説明する一定の数のルールを守る必要があります。

## 送信者のアドレス {#sender-address}

特定の ISP は、メッセージを受け付ける前に、送信者アドレス（From）の有効性をチェックします。正しくない形式のアドレスは、受信サーバーによって拒否される可能性があります。You must make sure a correct address is given at the instance level (menu **[!UICONTROL Tools > Advanced > Deployment wizard...]**) or in the most frequently-used scenarios.

## オプトアウトリンクとフォーム {#opt-out}

デフォルトでは、メッセージが分析される場合、タイポロジルールでオプトアウトリンクが含まれているかどうかがチェックされ、見つからない場合は警告が表示されます。このルールを変更して、単純な警告ではなくエラーを表示し、このリンクなしに配信がおこなわれないようにすることができます。

毎回、送信前に、オプトアウトリンクが適切に機能することを確認する必要があります。For example, when sending the proof, make sure the link is valid, that the form is on-line and that validating this changes the value of the **[!UICONTROL No longer contact this recipient]** field to **[!UICONTROL Yes]**. リンクの入力時やフォームの変更時にヒューマンエラーが発生する可能性は常にあるので、このチェックは体系的におこなう必要があります。

オプトアウトリンクをクリックした受信者が選択を確認できないとしても、配信開始後に購読解除に関する問題が検出された場合は購読解除を手動で実行できます（一括更新機能を使用するなど）。

原則として、例えば E メールアドレスや名前などのフィールドを入力するよう求めることで、オプトアウトしたい受信者を邪魔しないでください。フォームには 1 つの検証ボタンのみを表示し、紐付けは暗号化された識別子にのみ実行します。追加の確認のリクエストは信頼できません。ユーザーが 2 つの E メールアドレスを同じボックスにリダイレクトさせている可能性があります（firstname.lastname@club.com と firstname.lastname@internet-club.com など）。受信者が最初のアドレスのみを覚えていて、もう 1 つのアドレスに送信されたメッセージを使用して購読解除する場合、暗号化された識別子と入力された E メールアドレスが一致しないので、フォームはこれを拒否します。

## SpamAssassin {#spamassassin}

SpamAssassin と連携するように Adobe Campaign を設定できます。連携することで、E メールを評価し、受信時に使用されるスパム対策ツールによってメッセージがスパムと見なされるリスクがあるかどうかを判断できます。

配信を開始する前に、「プレビュー」タブでリスクを評価できます。テストの結果が警告メッセージとして表示されます。

Learn more in this [section](../../delivery/using/spamassassin.md).