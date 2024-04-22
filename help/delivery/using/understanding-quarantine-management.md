---
product: campaign
title: 強制隔離管理について
description: 強制隔離管理について
badge-v8: label="v8 にも適用されます" type="Positive" tooltip="Campaign v8 にも適用されます"
feature: Monitoring, Deliverability
role: User
exl-id: cfd8f5c9-f368-4a31-a1e2-1d77ceae5ced
source-git-commit: e34718caefdf5db4ddd61db601420274be77054e
workflow-type: ht
source-wordcount: '3090'
ht-degree: 100%

---

# 強制隔離管理について{#understanding-quarantine-management}

Adobe Campaign では、強制隔離されたアドレスのリストを管理します。アドレスが強制隔離されている受信者は、配信分析時にデフォルトで除外され、ターゲットにされなくなります。例えば、メールボックスの容量が超過している場合や、アドレスが存在しない場合などに、メールアドレスを強制隔離できます。どのような場合でも、強制隔離手順は、次に説明する特定のルールに従います。

>[!NOTE]
>
>この節は、オンラインチャネル（メール、SMS、プッシュ通知）に当てはまります。

## 強制隔離管理により配信を最適化 {#optimizing-your-delivery-through-quarantines}

メールアドレスまたは電話番号が強制隔離されているプロファイルは、メッセージ準備の際に自動的に除外されます（[配信用の強制隔離アドレスを識別](#identifying-quarantined-addresses-for-a-delivery)を参照）。これによって配信が迅速になります。エラー率は配信の速度に大きく影響するからです。

一部のインターネットアクセスプロバイダーは、無効なアドレスの割合が高すぎる場合、メールを自動的にスパムと見なします。したがって、強制隔離を使用すると、これらのプロバイダーによってブロックリストに追加されるのを回避できます。

また、強制隔離は、誤りのある電話番号を配信から除外することで、SMS の送信コスト削減にも役立ちます。

配信を保護および最適化するベストプラクティスについて詳しくは、[このページ](delivery-best-practices.md)を参照してください。

### 強制隔離とブロックリストの比較 {#quarantine-vs-denylist}

強制隔離とブロックリストは、同じオブジェクトには適用されません。

* **強制隔離**&#x200B;は、プロファイル自体ではなく、**アドレス**（または電話番号など）にのみ適用されます。例えば、メールアドレスが強制隔離されているプロファイルは、プロファイルを更新して新しいアドレスを入力できるので、再び配信アクションのターゲットになる可能性があります。同様に、2 つのプロファイルの電話番号が同じ場合、その番号が強制隔離されると、両方のプロファイルが影響を受けます。

  強制隔離されたアドレスまたは電話番号は、[除外ログ](#identifying-quarantined-addresses-for-a-delivery)（配信の場合）または[強制隔離リスト](#identifying-quarantined-addresses-for-the-entire-platform)（プラットフォーム全体の場合）に表示されます。

* 一方、**ブロックリスト**&#x200B;への登録では、特定のチャネルを購読解除（オプトアウト）した後などは、**プロファイル**&#x200B;は配信のターゲットとなりません。例えば、メールチャネルのブロックリストのプロファイルに 2 つのメールアドレスがある場合、両方のアドレスが配信から除外されます。

  プロファイルが 1 つ以上のチャネルのブロックリストに含まれているかどうかは、プロファイルの「**[!UICONTROL 一般]**」タブの「**[!UICONTROL 今後の連絡は不要]**」セクションで確認できます。詳しくは、[この節](../../platform/using/editing-a-profile.md#general-tab)を参照してください。

>[!NOTE]
>
>強制隔離には、受信者がメッセージをスパムとして報告したり、「STOP」などのキーワードを使用して SMS メッセージに返信したりする場合に適用される&#x200B;**[!UICONTROL ブロックリスト登録済み]**&#x200B;ステータスが含まれます。この場合、プロファイルの関連するアドレスまたは電話番号は、**[!UICONTROL ブロックリスト登録済み]**&#x200B;ステータスで強制隔離に送信されます。STOP SMS メッセージの管理について詳しくは、[この節](../../delivery/using/sms-send.md#processing-inbound-messages)を参照してください。

## 強制隔離されたアドレスを識別 {#identifying-quarantined-addresses}

強制隔離されたアドレスは、特定の配信先またはプラットフォーム全体について一覧表示できます。

### 配信用の強制隔離アドレスを識別 {#identifying-quarantined-addresses-for-a-delivery}

特定の配信で強制隔離されたアドレスは、配信準備フェーズ中に配信ダッシュボードの配信ログに一覧表示されます（[配信ログおよび履歴](delivery-dashboard.md#delivery-logs-and-history)を参照）。

### プラットフォーム全体の強制隔離アドレスを識別 {#identifying-quarantined-addresses-for-the-entire-platform}

管理者は、プラットフォーム全体で強制隔離されたアドレスのリストを&#x200B;**[!UICONTROL 管理者／キャンペーン管理／配信不能件数の管理／配信不能件数およびアドレス]**&#x200B;ノードで表示できます。

>[!NOTE]
>
>このメニューでは、**メール**、**SMS** および&#x200B;**プッシュ通知**&#x200B;チャネルの強制隔離された要素のリストが表示されます。

アドレスごとに次の情報を表示できます。

![](assets/tech_quarant_npai.png)

>[!NOTE]
>
>強制隔離数の増加は、データベースの「老朽化」に関連する、正常な影響です。例えば、メールアドレスの寿命が 3 年と考えられ、受信者テーブルが毎年 50％増加する場合、強制隔離の増加は次のように計算できます。
>
>1 年目の終了時：(1&#42;0.33)/(1+0.5)=22%。
>
>2 年目の終了時：((1.22&#42;0.33)+0.33)/(1.5+0.75)=32.5%。

### 配信レポートの強制隔離アドレスを識別 {#identifying-quarantined-addresses-in-delivery-reports}

次のレポートには、強制隔離中のアドレスに関する情報が含まれます。

* 配信ごとに、配信ターゲットに含まれている強制隔離中のアドレス数が&#x200B;**[!UICONTROL 配信の概要]**&#x200B;レポートに表示されます。次のものが表示されます。

   * 配信分析時に強制隔離されたアドレス数

   * 配信アクション後に強制隔離されたアドレス数

* **[!UICONTROL 配達不能件数とバウンス数]**&#x200B;レポートには、強制隔離中のアドレスや発生したエラーのタイプなどに関する情報が表示され、エラーがドメイン別に分類されます。

プラットフォームのすべての配信について（**[!UICONTROL ホームページ／レポート]**）または特定の配信について、この情報を調べることができます。カスタマイズされたレポートを作成して、表示する情報を選択することもできます。

### 受信者の強制隔離アドレスを識別 {#identifying-quarantined-addresses-for-a-recipient}

あらゆる受信者のメールアドレスのステータスを調べることができます。そのためには、受信者のプロファイルを選択し、「**[!UICONTROL 配信]**」タブをクリックします。その受信者へのすべての配信について、アドレスへの配信が失敗したかどうか、分析時に強制隔離されたかどうかなどを調べることができます。フォルダーごとに、メールアドレスが強制隔離中の受信者のみを表示できます。そのためには、**[!UICONTROL 強制隔離されたメールアドレス]**&#x200B;アプリケーションフィルターを使用します。

![](assets/tech_quarant_recipients_filter.png)


## アドレスを強制隔離に送信するための条件 {#conditions-for-sending-an-address-to-quarantine}

Adobe Campaign では、エラーメッセージの選定で割り当てられた配信のエラータイプと理由に応じて強制隔離を管理します（[バウンスメールの選定](understanding-delivery-failures.md#bounce-mail-qualification)および[配信のエラータイプと理由](understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照）。

* **無視のエラー**：アドレスを強制隔離しません。
* **ハードエラー**：対応するメールアドレスがただちに強制隔離されます。
* **ソフトエラー**：ただちにアドレスが強制隔離されることはありませんが、エラーカウンターがインクリメントされます。詳しくは、[ソフトエラー管理](#soft-error-management)を参照してください。

ユーザーがメールをスパム（[フィードバックループ](https://experienceleague.adobe.com/docs/deliverability-learn/deliverability-best-practice-guide/transition-process/infrastructure.html?lang=ja#feedback-loops)）と見なした場合、メッセージは、アドビが管理するテクニカルメールボックスに自動的にリダイレクトされます。さらに、そのメールアドレスは自動的に強制隔離され、ステータスが「**[!UICONTROL ブロックリスト登録済み]**」となります。このステータスはアドレスのみに適用され、プロファイルはブロックリストに登録されていないので、ユーザーは引き続き SMS メッセージやプッシュ通知を受信します。

>[!NOTE]
>
>Adobe Campaign の強制隔離では、大文字と小文字が区別されます。後から再度ターゲットされることのないよう、メールアドレスは必ず小文字でインポートしてください。

隔離されたアドレスのリスト（[プラットフォーム全体の強制隔離されたアドレスの識別](#identifying-quarantined-addresses-for-the-entire-platform)を参照）の「**[!UICONTROL エラー理由]**」フィールドは、選択したアドレスが強制隔離された理由を示します。

![](assets/tech_quarant_error_reasons.png)

### ソフトエラー管理 {#soft-error-management}

ハードエラーとは異なり、ソフトエラーでただちにアドレスが強制隔離されることはありませんが、エラーカウンターがインクリメントされます。

再試行は、[配信期間](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)中に実行されます。エラーカウンターが制限しきい値に達すると、アドレスが強制隔離されます。詳しくは、[一時的な配信エラーの後の再試行](understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)を参照してください。

最後に重大なエラーが発生したのが 10 日以上前の場合、エラーカウンターが再初期化されます。アドレスのステータスが「**有効**」に変わり、[データベースクリーンアップ](../../production/using/database-cleanup-workflow.md)ワークフローが強制隔離のリストからアドレスを削除します。


ホストインストールまたはハイブリッドインストールで、[Enhanced MTA](sending-with-enhanced-mta.md) にアップグレードした場合、**[!UICONTROL エラー]**&#x200B;ステータスの場合に実行される再試行の最大数および再試行間の最小遅延は現在、IP が特定のドメインで過去と現在の両方でどの程度機能しているかに基づいています。

従来の Campaign MTA を使用したオンプレミスインストールおよびホスト／ハイブリッドインストールの場合、エラーの数と 2 つのエラーの間の期間を変更できます。これを行うには、[デプロイメントウィザード](../../installation/using/deploying-an-instance.md)（**[!UICONTROL メールチャネル]**／**[!UICONTROL 詳細設定パラメーター]**）または[配信レベルで](../../delivery/using/steps-sending-the-delivery.md#configuring-retries)対応する設定を変更します。


## 強制隔離からアドレスの削除 {#removing-a-quarantined-address}

### 自動更新 {#unquarantine-auto}

特定の条件に一致するアドレスは、[データベースクリーンアップ](../../production/using/database-cleanup-workflow.md)ワークフローによって強制隔離リストから自動的に削除されます。

次の場合、アドレスは強制隔離リストから自動的に削除されます。

* 「**[!UICONTROL エラーあり]**」ステータスのアドレスは、配信が正常に完了すると、強制隔離リストから削除されます。
* 「**[!UICONTROL エラーあり]**」ステータスのアドレスは、最後のソフトバウンスが 10 日以上前に発生した場合に、強制隔離リストから削除されます。ソフトエラー管理について詳しくは、[この節](#soft-error-management)を参照してください。
* 「**[!UICONTROL エラーあり]**」ステータスのアドレスで、**[!UICONTROL メールボックス容量超過]**&#x200B;エラーでバウンスしたアドレスは、30 日後に強制隔離リストから削除されます。

その後、ステータスは「**[!UICONTROL 有効]**」に変わります。

>[!IMPORTANT]
>
>アドレスのステータスが&#x200B;**[!UICONTROL 強制隔離中]**&#x200B;または&#x200B;**[!UICONTROL ブロックリスト登録済み]**&#x200B;の受信者は、メールを受信した場合でも削除されません。

### 手動更新 {#unquarantine-manual}

アドレスの強制隔離を手動で解除することもできます。 強制隔離リストからアドレスを手動で削除するには、ステータスを「**[!UICONTROL 有効]**」に変更します（**[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／配信不能件数およびアドレス]**&#x200B;ノードから）。

![](assets/tech_quarant_error_status.png)

### 一括更新 {#unquarantine-bulk}

例えば、ISP が停止した場合など、強制隔離リストで一括更新を実行する必要が生じる場合があります。 この場合、メールは受信者に正常に配信されないため、誤ってバウンスとマークされます。強制隔離リストからこれらのアドレスを削除する必要があります。

これを実行するには、ワークフローを作成し、強制隔離テーブルに&#x200B;**[!UICONTROL クエリ]**&#x200B;アクティビティを追加して、影響を受けたすべての受信者を除外します。 特定されると、それらは強制隔離リストから削除され、今後のキャンペーンメール配信に含めることができます。

このクエリで推奨されるガイドラインを次に示します。

* 強制隔離リストの&#x200B;**[!UICONTROL エラーテキスト]**&#x200B;フィールドにインバウンドメールルール情報が含まれている Campaign Classic v7 環境の場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;に「Momen_Code10_InvalidRecipient」が含まれる
   * **メールドメイン（@domain）**&#x200B;が domain1.com と等しい、または&#x200B;**メールドメイン（@domain）**&#x200B;が domain2.com と等しい、または&#x200B;**メールドメイン（@domain）**&#x200B;が domain3.com と等しい
   * **更新ステータス（@lastModified）**&#x200B;が `MM/DD/YYYY HH:MM:SS AM` 以降
   * **更新ステータス（@lastModified）**&#x200B;が `MM/DD/YYYY HH:MM:SS PM` 以前

* 強制隔離リストの「**[!UICONTROL エラーテキスト]**」フィールドに SMTP バウンス応答情報が含まれている Campaign Classic v7 インスタンスの場合：

   * **エラーテキスト（強制隔離テキスト）**&#x200B;には、「550-5.1.1」が含まれ、かつ&#x200B;**エラーテキスト（強制隔離テキスト）**&#x200B;には、「support.ISP.com」が含まれている

  例えば、「support.ISP.com」は「support.apple.com」または「support.google.com」になります

   * **更新ステータス（@lastModified）**&#x200B;が `MM/DD/YYYY HH:MM:SS AM` 以降
   * **更新ステータス（@lastModified）**&#x200B;が `MM/DD/YYYY HH:MM:SS PM` 以前

影響を受ける受信者のリストを受信したら、**[!UICONTROL データを更新]**&#x200B;アクティビティを追加して、メールアドレスのステータスを「**[!UICONTROL 有効]**」に設定し、**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローで強制隔離リストから削除されるようにします。また、強制隔離テーブルから削除するだけでもかまいません。

## プッシュ通知の強制隔離 {#push-notification-quarantines}

プッシュ通知の強制隔離メカニズムは、全体として通常のプロセスと同じです。ただし、プッシュ通知では一部のエラーの管理方法が異なります。例えば、一部のソフトエラーでは、同じ配信の再試行は実行されません。プッシュ通知特有の方式を以下に示します。再試行の方式（再試行の回数、頻度）はメールの場合と同じです。

強制隔離される項目はデバイストークンです。

### iOS での強制隔離 {#ios-quarantine}

HTTP/V2 プロトコルでは、プッシュ配信ごとの直接フィードバックおよびステータスを使用できます。HTTP/V2 プロトコルコネクタを使用する場合、フィードバックサービスが **[!UICONTROL mobileAppOptOutMgt]** ワークフローによって呼び出されることはありません。モバイルアプリケーションのアンインストールまたは再インストールがおこなわれた場合、トークンは登録解除されたものとみなされます。

同時に、APNs がメッセージに対して登録解除ステータスを返した場合、ターゲットトークンはただちに強制隔離されます。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>シナリオ</strong><br /> </td> 
   <td> <strong>ステータス</strong><br /> </td> 
   <td> <strong>エラーメッセージ</strong><br /> </td> 
   <td> <strong>エラータイプ</strong><br /> </td> 
   <td> <strong>エラーの理由</strong><br /> </td> 
   <td> <strong>再試行</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> ターゲットデバイスの電源がオン<br /> </td> 
   <td> OK<br /> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ターゲットデバイスの電源がオフ<br /> </td> 
   <td> OK<br /> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> ユーザーがアプリケーションの通知を無効化<br /> </td> 
   <td> OK<br /> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> メッセージの作成／分析フェーズ - ペイロードが大きすぎる<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> ペイロードが長すぎる<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> メッセージの作成／分析フェーズ - 予期しないコンテンツ形式の問題<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> エラーによってエラーメッセージが異なる<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 未定義<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> 証明書の問題（パスワード、破損など）と、APNs へのテスト接続の問題<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> エラーによってエラーメッセージが異なる<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> 送信中にネットワーク接続が切断<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 接続エラー<br /> </td> 
   <td> 未定義<br /> </td> 
   <td> 未到達<br /> </td> 
   <td> ○<br /> </td> 
  </tr> 
  <tr> 
   <td> APNs メッセージ却下：登録解除<br />ユーザーがアプリケーションを削除した、またはトークンの期限切れ<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 登録解除<br /> </td> 
   <td> ハード<br /> </td> 
   <td> 不明なユーザー<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> APNs メッセージ却下：その他のすべてのエラー<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> エラー拒否の原因がエラーメッセージに表示されます<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
 </tbody> 
</table>

### Android での強制隔離 {#android-quarantine}

**Android V1 の場合**

Adobe Campaign は通知ごとに FCM サーバーから直接同期エラーを受け取ります。Adobe Campaign はこれを即時に処理し、エラーの重大度に応じてハードエラーまたはソフトエラーを生成します。これにより再試行が実行できるようになります。

* ペイロードの長さの超過、接続の問題、サービスの使用可否の問題：再試行が実行され、ソフトエラーが生成されます。エラーの理由は「**[!UICONTROL 拒否]**」です。
* デバイスの割当量の超過：再試行はなく、ソフトエラーが生成されます。エラーの理由は「**[!UICONTROL 拒否]**」です。
* 無効または登録解除されたトークン、予期しないエラー、送信者のアカウントの問題：再試行はなく、ハードエラーが生成されます。エラーの理由は「**[!UICONTROL 拒否]**」です。

**[!UICONTROL mobileAppOptOutMgt]** ワークフローは 6 時間ごとに実行されます。このワークフローは **AppSubscriptionRcp** テーブルを更新します。登録解除または無効と宣言されたトークンについて、「**無効**」フィールドが「**True**」に設定され、そのデバイストークンにリンクされている購読は自動的にそれ以降の配信から除外されます。

配信分析中に、ターゲットから除外されたすべてのデバイスが自動的に **excludeLogAppSubRcp** テーブルに追加されます。

>[!NOTE]
>
>Baidu コネクタを使用している場合、さらに別の種類のエラーがあります。
>
>* 配信開始時の接続の問題：エラータイプは「**[!UICONTROL 未定義]**」で、エラーの理由は「**[!UICONTROL 未到達]**」です。再試行は実行されます。
>* 配信中の接続切断：ソフトエラーが生成され、エラーの理由は「**[!UICONTROL 拒否]**」です。再試行は実行されます。
>* 送信中に Baidu により同期エラーが返される：ハードエラーが生成され、エラーの理由は「**[!UICONTROL 拒否]**」です。再試行はありません。
>
>Adobe Campaign は 10 分ごとに Baidu サーバーにアクセスし、送信済みメッセージのステータスを取得し、broadLog を更新します。メッセージが送信済みと宣言されると、broadLog のメッセージのステータスが「**[!UICONTROL 受信済み]**」に設定されます。Baidu がエラーを宣言すると、ステータスは「**[!UICONTROL 失敗]**」に設定されます。

**Android V2 の場合**

Android V2 の強制隔離メカニズムでは、Android V1 と同じプロセスを使用しており、同じことがサブスクリプションと除外の更新にも当てはまります。詳しくは、[Android V1](#android-quarantine) の節を参照してください。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>シナリオ</strong><br /> </td> 
   <td> <strong>ステータス</strong><br /> </td> 
   <td> <strong>エラーメッセージ</strong><br /> </td> 
   <td> <strong>エラータイプ</strong><br /> </td> 
   <td> <strong>エラーの理由</strong><br /> </td> 
   <td> <strong>再試行</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> メッセージの作成／分析フェーズ：カスタムフィールドでの不正なキーワードの使用<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 次のキーワードは使用できません：{1}<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> メッセージの作成／分析フェーズ：ペイロードが大きすぎる<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 通知が長すぎます：{1} ビット。許可されているのは {2} ビットのみです<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> 送信中にネットワーク接続が切断<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 次のアドレスの Firebase Cloud Messaging サービスからの応答がありません：{1}<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 未到達<br /> </td> 
   <td> ○<br /> </td> 
  </tr> 
  <tr> 
   <td> FCM メッセージ却下：FCM サーバーが一時的に使用不可（タイムアウトなど）<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> Firebase Cloud Messaging サービスを一時的に利用できません<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 未到達<br /> </td> 
   <td> ○<br /> </td> 
  </tr> 
  <tr> 
   <td> FCM メッセージ却下：送信者アカウントの認証中にエラー発生<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 開発者アカウントを識別できませんでした。ID とパスワードを確認してください<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> FCM メッセージ却下：デバイスの割当量を超過<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> </td> 
   <td> ソフト<br /> </td> 
   <td> 拒否<br /> </td> 
   <td> ○<br /> </td> 
  </tr> 
  <tr> 
   <td> FCM メッセージ却下：無効な登録または未登録<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> </td> 
   <td> ハード<br /> </td> 
   <td> 不明なユーザー<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
  <tr> 
   <td> FCM メッセージ却下：その他すべてのエラー<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> Firebase Cloud Messaging サーバーから予期しないエラーコードが返されました：{1} </td> 
   <td> </td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr> 
    <tr> 
   <td> FCM メッセージ却下：無効な引数<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> INVALID_ARGUMENT </td> 
   <td> 無視</td> 
   <td> 未定義<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> FCM メッセージ却下：サードパーティ認証エラー<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> THIRD_PARTY_AUTH_ERROR </td> 
   <td> 無視</td>
   <td> 拒否<br /> </td> 
   <td> ○<br /> </td> 
  </tr>
    <tr> 
   <td> FCM メッセージ却下：送信者 ID が一致しません<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> SENDER_ID_MISMATCH </td> 
   <td> ソフト</td>
   <td> 不明なユーザー<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> FCM メッセージ却下：登録解除<br /> </td> 
   <td> 失敗<br /> </td>
   <td> UNREGISTERED </td> 
   <td> ハード</td> 
   <td> 不明なユーザー<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> FCM メッセージ却下：内部<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> INTERNAL </td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ○<br /> </td> 
  </tr>
    <tr> 
   <td> FCM メッセージ却下：使用不可<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> UNAVAILABLE</td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ○<br /> </td> 
  </tr>
    <tr> 
   <td> FCM メッセージ却下：予期しないエラーコード<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 予期しないエラーコード</td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
  <tr> 
   <td> 認証：接続の問題<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 認証サーバーに接続できません </td> 
   <td> 無視</td>
   <td> 拒否<br /> </td> 
   <td> ○<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：リクエストで許可されていないクライアントまたは範囲です。<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> unauthorized_client </td> 
   <td> 無視</td>
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：クライアントは、このメソッドを使用してアクセストークンを取得する権限がありません。または、要求された範囲に対してクライアントが承認されていません。<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> unauthorized_client </td> 
   <td> 無視</td>
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：アクセス拒否<br /> </td> 
   <td> 失敗<br /> </td>
   <td> access_denied</td> 
   <td> 無視</td>
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：無効なメール<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> Invalid_grant </td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：無効な JWT<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> Invalid_grant </td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：無効な JWT 署名<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> Invalid_grant </td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：無効な OAuth 範囲または ID トークンオーディエンスが指定されました<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> unauthorized_client</td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
    <tr> 
   <td> 認証：OAuth クライアントが無効です<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> Disabled_client</td> 
   <td> 無視</td> 
   <td> 拒否<br /> </td> 
   <td> ×<br /> </td> 
  </tr>
 </tbody> 
</table>

## SMS の強制隔離 {#sms-quarantines}

**標準コネクタの場合**

SMS メッセージの強制隔離メカニズムは、全体として通常のプロセスと同じものです。[強制隔離について](#about-quarantines)を参照してください。SMS 特有の方式を以下に示します。

>[!NOTE]
>
>**[!UICONTROL 配信ログの選定]**&#x200B;テーブルは、**拡張された汎用 SMPP** コネクタには適用されません。

<table> 
 <tbody> 
  <tr> 
   <td> <strong>シナリオ</strong><br /> </td> 
   <td> <strong>ステータス</strong><br /> </td> 
   <td> <strong>エラーメッセージ</strong><br /> </td> 
   <td> <strong>エラータイプ</strong><br /> </td> 
   <td> <strong>エラーの理由</strong><br /> </td> 
  </tr> 
  <tr> 
   <td> プロバイダーに送信済み<br /> </td> 
   <td> 送信済み<br /> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> モバイルで受信済み<br /> </td> 
   <td> 受信済み<br /> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> プロバイダーがエラーを返した<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> データの受信中にエラーが発生しました (SR または MO)<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 未到達<br /> </td> 
  </tr> 
  <tr> 
   <td> MT 確認が無効<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> 送信クエリの確認フレームの処理中にエラー「{1}」が発生しました<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 未到達<br /> </td> 
  </tr> 
  <tr> 
   <td> MT の送信中にエラーが発生<br /> </td> 
   <td> 失敗<br /> </td> 
   <td> メッセージの送信中にエラーが発生<br /> </td> 
   <td> ソフト<br /> </td> 
   <td> 未到達<br /> </td> 
  </tr> 
 </tbody> 
</table>

**拡張された汎用 SMPP コネクタの場合**

SMPP プロトコルを使用して SMS メッセージを送信する場合のエラー管理の方法は異なります。拡張された汎用 SMPP コネクタについて詳しくは、[このページ](sms-set-up.md#creating-an-smpp-external-account)を参照してください。

SMPP コネクタは、返された SR（ステータスレポート）メッセージからデータを取得し、正規表現（regex）を使用して、そのコンテンツをフィルター処理します。このデータは、次に、**[!UICONTROL 配信ログの検証]**&#x200B;テーブル（**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**&#x200B;メニューから使用できます）に見つかった情報と照合されます。

新しいタイプのエラーが検証される前に、エラーの理由はデフォルトで常に「**拒否**」に設定されます。

>[!NOTE]
>
>エラーのタイプと理由はメールの場合と同じです。[配信エラーのタイプと理由](understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照してください。
>
>配信ログの検証テーブルに適切なエラータイプおよび理由を設定するために、ステータスコードおよびエラーコードのリストをプロバイダーに問い合わせてください。

生成されるメッセージの例：

```
SR Generic DELIVRD 000|#MESSAGE#
```

* SMS のエラーコードをメールのエラーコードと区別するために、すべてのエラーメッセージは **SR** で始まります。
* エラーメッセージの 2 つ目の部分（この例では **Generic**）は、SMSC 実装の名前（例えば、SMS 外部アカウントの「**[!UICONTROL SMSC 実装名]**」フィールドに定義されている名前）を指します。[このページ](sms-set-up.md#creating-an-smpp-external-account)を参照してください。

  同じエラーコードであってもプロバイダーごとに意味が異なる場合があるので、エラーコードを生成したプロバイダーがこのフィールドでわかります。これにより、該当するプロバイダーのドキュメントでエラーを調べることができます。

* エラーメッセージの 3 つ目の部分（この例では **DELIVRD**）は、SMS 外部アカウントに定義されたステータス抽出用正規表現を使用して SR から取得されたステータスコードに対応します。

  この正規表現は、外部アカウントの「**[!UICONTROL SMSC 特異性]**」タブで指定します。[このページ](sms-set-up.md#creating-an-smpp-external-account)を参照してください。

  ![](assets/tech_quarant_error_regex.png)

  デフォルトでは、**SMPP 3.4 仕様**&#x200B;の&#x200B;**付録 B** に規定されているとおり、**stat:** フィールドが抽出されます。

* エラーメッセージの 4 つ目の部分（この例では **000**）は、SMS 外部アカウントに定義されたエラーコード抽出用正規表現を使用して SR から抽出されたエラーコードに対応します。

  この正規表現は、外部アカウントの「**[!UICONTROL SMSC 特異性]**」タブで指定します。[このページ](sms-set-up.md#creating-an-smpp-external-account)を参照してください。

  デフォルトでは、**SMPP 3.4 仕様**&#x200B;の&#x200B;**付録 B** に規定されているとおり、**err:** フィールドが抽出されます。

* パイプ記号（|）以降の文字列は、**[!UICONTROL 配信ログの検証]**&#x200B;テーブルの&#x200B;**[!UICONTROL 最初のテキスト]**&#x200B;列にのみ表示されます。このコンテンツは、常に、メッセージが正規化された後に **#MESSAGE#** で置き換えられます。これにより、同じようなエラーに対して複数のエントリが含まれるのを防ぐことができます。これは、メールの場合と同じです。詳しくは、[バウンスメールの選定](understanding-delivery-failures.md#bounce-mail-qualification)を参照してください。

拡張された汎用 SMPP コネクタは、ヒューリスティックを適用して実用的なデフォルト値を見つけます。例えば、**DELIV** で始まるステータスは、ほとんどのプロバイダーでよく使用されている **DELIVRD** または **DELIVERED** と一致するので、成功とみなされます。これ以外のステータスはハードエラーとみなされます。
