---
title: 強制隔離管理の理解
seo-title: 強制隔離管理の理解
description: 強制隔離管理の理解
seo-description: null
page-status-flag: never-activated
uuid: 9421e26c-bdcc-4588-8e44-fa6f31051081
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: monitoring-deliveries
discoiquuid: 56cbf48a-eb32-4617-8f80-efbfd05976ea
translation-type: ht
source-git-commit: fd75f7f75e8e77d7228233ea311dd922d100417c
workflow-type: ht
source-wordcount: '2896'
ht-degree: 100%

---


# 強制隔離管理の理解{#understanding-quarantine-management}

## 強制隔離について {#about-quarantines}

Adobe Campaign では、強制隔離されたアドレスのリストを管理します。アドレスが強制隔離されている受信者は、配信分析時にデフォルトで除外され、ターゲットにされなくなります。例えば、メールボックスの容量が超過している場合や、アドレスが存在しない場合などに、E メールアドレスを強制隔離できます。どのような場合でも、強制隔離手順は、次に説明する特定のルールに従います。

>[!NOTE]
>
>この節は、オンラインチャネル（E メール、SMS、プッシュ通知）に当てはまります。

### 強制隔離による配信の最適化 {#optimizing-your-delivery-through-quarantines}

E メールアドレスまたは電話番号が強制隔離されているプロファイルは、メッセージ準備の際に自動的に除外されます（[配信用の強制隔離アドレスの識別](#identifying-quarantined-addresses-for-a-delivery)を参照）。これによって配信が迅速になります。エラー率は配信の速度に大きく影響するからです。

一部のインターネットアクセスプロバイダーは、無効なアドレスの割合が高すぎる場合、E メールを自動的にスパムとみなします。したがって、強制隔離を使用すると、これらのプロバイダーによってブロックリストに追加されるのを回避できます。

また、強制隔離は、誤りのある電話番号を配信から除外することで、SMS の送信コスト削減にも役立ちます。配信を保護および最適化するベストプラクティスについて詳しくは、[このページ](../../delivery/using/delivery-best-practices.md)を参照してください。

### 強制隔離対ブロックリスト{#quarantine-vs-denylist}

**強制隔離**&#x200B;は、プロファイル自体ではなく、アドレスのみに適用されます。つまり、2 つのプロファイルに同じ E メールアドレスがある場合、そのアドレスが強制隔離されると、両方のプロファイルが影響を受けます。

同様に、E メールアドレスが強制隔離されているプロファイルは、プロファイルを更新して新しいアドレスを入力できるので、再び配信アクションのターゲットになる可能性があります。

一方、**ブロックリスト**&#x200B;への登録では、登録されたプロファイルが、購読解除（オプトアウト）後のように、それ以降はどのような配信のターゲットにもならなくなります。

>[!NOTE]
>
>SMS 配信からのオプトアウトのために「STOP」のようなキーワードを使ってユーザーが SMS メッセージに返信しても、そのユーザーのプロファイルは、E メールのオプトアウトプロセスのようにはブロックリストに登録されません。強制隔離されるのはプロファイルの電話番号なので、そのユーザーは引き続き E メールメッセージを受信できます。

## 強制隔離アドレスの識別 {#identifying-quarantined-addresses}

強制隔離されたアドレスは、特定の配信またはプラットフォーム全体を対象としてリストすることができます。

### 配信用の強制隔離アドレスの識別 {#identifying-quarantined-addresses-for-a-delivery}

特定の配信について強制隔離されたアドレスのリストは、配信準備フェーズの途中で、配信ダッシュボードの配信ログに記録されます（[配信ログと履歴](../../delivery/using/monitoring-a-delivery.md#delivery-logs-and-history)を参照）。

### プラットフォーム全体の強制隔離アドレスの識別 {#identifying-quarantined-addresses-for-the-entire-platform}

管理者は、プラットフォーム全体で強制隔離されたアドレスのリストを&#x200B;**[!UICONTROL 管理者／キャンペーン管理／配信不能件数の管理／配信不能件数およびアドレス]**&#x200B;ノードで表示できます。

>[!NOTE]
>
>このメニューでは、**E メール**、**SMS** および&#x200B;**プッシュ通知**&#x200B;チャネルの強制隔離された要素のリストが表示されます。

アドレスごとに次の情報を表示できます。

![](assets/tech_quarant_npai.png)

>[!NOTE]
>
>強制隔離数の増加は、データベースの「老朽化」に関連する、正常な影響です。例えば、E メールアドレスの寿命が 3 年と考えられ、受信者テーブルが毎年 50％増加する場合、強制隔離の増加は次のように計算できます。
>
>1 年目の終了時：(1*0.33)/(1+0.5)=22%
2 年目の終了時：((1.22*0.33)+0.33)/(1.5+0.75)=32.5%

### 配信レポートでの強制隔離アドレスの識別 {#identifying-quarantined-addresses-in-delivery-reports}

次のレポートには、強制隔離中のアドレスに関する情報が含まれます。

* 配信ごとに、配信ターゲットに含まれている強制隔離中のアドレス数が&#x200B;**[!UICONTROL 配信の概要]**&#x200B;レポートに表示されます。次のものが表示されます。

   * 配信分析時に強制隔離されたアドレス数

   * 配信アクション後に強制隔離されたアドレス数

* **[!UICONTROL 配達不能件数とバウンス数]**&#x200B;レポートには、強制隔離中のアドレスや発生したエラーのタイプなどに関する情報が表示され、エラーがドメイン別に分類されます。

プラットフォームのすべての配信について（**[!UICONTROL ホームページ／レポート]**）または特定の配信について、この情報を調べることができます。カスタマイズされたレポートを作成して、表示する情報を選択することもできます。

### 受信者の強制隔離アドレスの識別 {#identifying-quarantined-addresses-for-a-recipient}

あらゆる受信者の E メールアドレスのステータスを調べることができます。そのためには、受信者のプロファイルを選択し、「**[!UICONTROL 配信]**」タブをクリックします。その受信者へのすべての配信について、アドレスへの配信が失敗したかどうか、分析時に強制隔離されたかどうかなどを調べることができます。フォルダーごとに、E メールアドレスが強制隔離中の受信者のみを表示できます。そのためには、**[!UICONTROL 強制隔離された E メールアドレス]**&#x200B;アプリケーションフィルターを使用します。

![](assets/tech_quarant_recipients_filter.png)

### 強制隔離されたアドレスの削除 {#removing-a-quarantined-address}

必要に応じて、強制隔離リストから手動でアドレスを削除できます。これに加えて、特定の条件に一致するアドレスは、**[!UICONTROL データベースクリーンアップ]**&#x200B;ワークフローによって強制隔離リストから自動的に削除されます。

強制隔離リストからアドレスを手動で削除するには、以下を実行します。

* **[!UICONTROL 管理／キャンペーン管理／配信不能件数の管理／配信不能件数およびアドレス]**&#x200B;ノードから、ステータスを「**[!UICONTROL 有効]**」に変更できます。

   ![](assets/tech_quarant_error_status.png)

* ステータスを「**[!UICONTROL 許可リストに登録済み]**」に変更することもできます。この場合、アドレスは強制隔離リストに残りますが、エラーが発生した場合でも、自動的にターゲットに設定されます。

次の場合、アドレスは強制隔離リストから自動的に削除されます。

* 「**[!UICONTROL エラーあり]**」ステータスのアドレスは、配信が正常に完了すると、強制隔離リストから削除されます。
* 「**[!UICONTROL エラーあり]**」ステータスのアドレスは、最後のソフトバウンスが 10 日以上前に発生した場合に、強制隔離リストから削除されます。ソフトエラー管理について詳しくは、[この節](#soft-error-management)を参照してください。
* 「**[!UICONTROL エラーあり]**」ステータスのアドレスで、**[!UICONTROL メールボックス容量超過]**&#x200B;エラーでバウンスしたアドレスは、30 日後に強制隔離リストから削除されます。

その後、ステータスは「**[!UICONTROL 有効]**」に変わります。

>[!IMPORTANT]
アドレスのステータスが「**[!UICONTROL 強制隔離中]**」または「**[!UICONTROL ブロックリストに登録済み]**」の受信者は、E メールを受信した場合でも削除されません。

エラー数およびエラーの間隔も変更できます。そのためには、デプロイメントウィザードの設定（**[!UICONTROL E メールチャネル]**／**[!UICONTROL 詳細設定パラメーター]**）を変更します。デプロイメントウィザードについて詳しくは、[この節](../../installation/using/deploying-an-instance.md)を参照してください。

## アドレスを強制隔離する条件 {#conditions-for-sending-an-address-to-quarantine}

Adobe Campaign では、エラーメッセージの選定で割り当てられた配信のエラータイプと理由に応じて強制隔離を管理します（[バウンスメールの選定](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)および[配信のエラータイプと理由](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照）。

* **無視のエラー**：アドレスを強制隔離しません。
* **ハードエラー**：対応する E メールアドレスがただちに強制隔離されます。
* **ソフトエラー**：ただちにアドレスが強制隔離されることはありませんが、エラーカウンターがインクリメントされます。詳しくは、[ソフトエラー管理](#soft-error-management)を参照してください。

ユーザーが E メールをスパム（[フィードバックループ](../../delivery/using/technical-recommendations.md#feedback-loop)）と評価した場合、メッセージはアドビが管理するテクニカルメールボックスに自動的にリダイレクトされます。さらに、その E メールアドレスは自動的に強制隔離されます。

強制隔離されたアドレスのリストの「**[!UICONTROL エラー理由]**」フィールドには、選択されたアドレスが強制隔離された理由が示されます。Adobe Campaign の強制隔離では、大文字と小文字が区別されます。後から再度ターゲットされることのないよう、E メールアドレスは必ず小文字でインポートしてください。

![](assets/tech_quarant_error_reasons.png)

### ソフトエラー管理 {#soft-error-management}

ハードエラーとは異なり、ソフトエラーでただちにアドレスが強制隔離されることはありませんが、エラーカウンターがインクリメントされます。

* エラーカウンターが制限しきい値に達すると、アドレスが強制隔離されます。
* デフォルトの設定では、しきい値はエラー 5 回に設定されています。2 つのエラーは、24 時間以上間隔を開けて発生した場合に別のエラーとしてカウントされます。5 回目のエラー発生時にアドレスが強制隔離されます。
* エラーカウンターのしきい値は変更できます。詳しくは、[一時的な配信エラーの後の再試行](../../delivery/using/understanding-delivery-failures.md#retries-after-a-delivery-temporary-failure)を参照してください。

最後に重大なエラーが発生したのが 10 日以上前の場合、エラーカウンターが再初期化されます。アドレスのステータスが「**有効**」に変わり、**データベースクリーンアップ**&#x200B;ワークフローが強制隔離のリストからアドレスを削除します。

## プッシュ通知の強制隔離 {#push-notification-quarantines}

プッシュ通知の強制隔離メカニズムは、全体として通常のプロセスと同じものです。[強制隔離について](#about-quarantines)を参照してください。ただし、プッシュ通知では一部のエラーの管理方法が異なります。例えば、一部のソフトエラーでは、同じ配信の再試行は実行されません。プッシュ通知特有の方式を以下に示します。再試行の方式（再試行の回数、頻度）は E メールの場合と同じです。

強制隔離される項目はデバイストークンです。

### iOS での強制隔離 {#ios-quarantine}

**iOS の場合：バイナリコネクタ**

>[!NOTE]
Campaign 20.3 リリース以降、iOS レガシーバイナリコネクタは非推奨となりました。このコネクタを使用する場合は、それに応じて実装を適応させる必要があります。[詳細情報](https://helpx.adobe.com/jp/campaign/kb/migrate-to-http2.html)

Adobe Campaign は通知ごとに APNs サーバーから同期エラーと非同期エラーを受け取ります。次の同期エラーについては、ソフトエラーが生成されます。

* ペイロード長の問題：再試行はありません。エラーの理由は「**[!UICONTROL 未到達]**」です。
* 証明書の有効期限の問題：再試行はありません。エラーの理由は「**[!UICONTROL 未到達]**」です。
* 配信中の接続切断：再試行が実行されます。エラーの理由は「**[!UICONTROL 未到達]**」です。
* サービス設定の問題（証明書が無効、証明書のパスワードが無効、証明書がない）：再試行はありません。エラーの理由は「**[!UICONTROL 未到達]**」です。

APNs サーバーは Adobe Campaign に対し、デバイストークンが（モバイルアプリケーションがユーザーによりアンインストールされた時点で）登録解除されたことを非同期的に通知します。**[!UICONTROL mobileAppOptOutMgt]** ワークフローは 6 時間ごとに実行されます。このワークフローは APNs フィードバックサービスにアクセスし、**AppSubscriptionRcp** テーブルを更新します。無効になっているすべてのトークンについて、「**無効**」フィールドが「**True**」に設定され、そのデバイストークンにリンクされている購読は自動的にそれ以降の配信から除外されます。

**iOS の場合 - HTTP/V2 コネクタ**

HTTP/V2 プロトコルでは、プッシュ配信ごとの直接フィードバックおよびステータスを使用できます。HTTP/V2 プロトコルコネクタを使用する場合、フィードバックサービスが **[!UICONTROL mobileAppOptOutMgt]** ワークフローによって呼び出されることはありません。登録解除されたトークンの処理は、iOS バイナリコネクタと iOS HTTP/V2 コネクタで異なります。モバイルアプリケーションのアンインストールまたは再インストールがおこなわれた場合、トークンは登録解除されたものとみなされます。

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
Baidu コネクタを使用している場合、さらに別の種類のエラーがあります。
* 配信開始時の接続の問題：エラータイプは「**[!UICONTROL 未定義]**」で、エラーの理由は「**[!UICONTROL 未到達]**」です。再試行は実行されます。
* 配信中の接続切断：ソフトエラーが生成され、エラーの理由は「**[!UICONTROL 拒否]**」です。再試行は実行されます。
* 送信中に Baidu により同期エラーが返される：ハードエラーが生成され、エラーの理由は「**[!UICONTROL 拒否]**」です。再試行はありません。

Adobe Campaign は 10 分ごとに Baidu サーバーにアクセスし、送信済みメッセージのステータスを取得し、broadLog を更新します。メッセージが送信済みと宣言されると、broadLog のメッセージのステータスが「**[!UICONTROL 受信済み]**」に設定されます。Baidu がエラーを宣言すると、ステータスは「**[!UICONTROL 失敗]**」に設定されます。

**Android V2 の場合**

Android V2 の強制隔離メカニズムでは、Android V1 と同じプロセスを使用しており、購読と除外の更新についても同様です。詳しくは、[Android V1](#android-quarantine) の節を参照してください。

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
   <td> 認証：無効な E メール<br /> </td> 
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
**[!UICONTROL 配信ログの選定]**&#x200B;テーブルは、**拡張された汎用 SMPP** コネクタには適用されません。

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

SMPP プロトコルを使用して SMS メッセージを送信する場合のエラー管理の方法は異なります。拡張された汎用 SMPP コネクタについて詳しくは、[このページ](../../delivery/using/sms-channel.md#creating-an-smpp-external-account)を参照してください。

SMPP コネクタは、返された SR（ステータスレポート）メッセージからデータを取得し、正規表現（regex）を使用して、そのコンテンツをフィルター処理します。このデータは、次に、**[!UICONTROL 配信ログの検証]**&#x200B;テーブル（**[!UICONTROL 管理]**／**[!UICONTROL キャンペーン管理]**／**[!UICONTROL 配信不能件数の管理]**&#x200B;メニューから使用できます）に見つかった情報と照合されます。

新しいタイプのエラーが検証される前に、エラーの理由はデフォルトで常に「**拒否**」に設定されます。

>[!NOTE]
エラーのタイプと理由は E メールの場合と同じです。[配信エラーのタイプと理由](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照してください。
配信ログの検証テーブルに適切なエラータイプおよび理由を設定するために、ステータスコードおよびエラーコードのリストをプロバイダーに問い合わせてください。

生成されるメッセージの例：

```
SR Generic DELIVRD 000|#MESSAGE#
```

* SMS のエラーコードを E メールのエラーコードと区別するために、すべてのエラーメッセージは **SR** で始まります。
* エラーメッセージの 2 つ目の部分（この例では **Generic**）は、SMSC 実装の名前（例えば、SMS 外部アカウントの「**[!UICONTROL SMSC 実装名]**」フィールドに定義されている名前）を指します。[このページ](../../delivery/using/sms-channel.md#creating-an-smpp-external-account)を参照してください。

   同じエラーコードであってもプロバイダーごとに意味が異なる場合があるので、エラーコードを生成したプロバイダーがこのフィールドでわかります。これにより、該当するプロバイダーのドキュメントでエラーを調べることができます。

* エラーメッセージの 3 つ目の部分（この例では **DELIVRD**）は、SMS 外部アカウントに定義されたステータス抽出用正規表現を使用して SR から取得されたステータスコードに対応します。

   この正規表現は、外部アカウントの「**[!UICONTROL SMSC 特異性]**」タブで指定します。[このページ](../../delivery/using/sms-channel.md#creating-an-smpp-external-account)を参照してください。

   ![](assets/tech_quarant_error_regex.png)

   デフォルトでは、**SMPP 3.4 仕様**&#x200B;の&#x200B;**付録 B** に規定されているとおり、**stat:** フィールドが抽出されます。

* エラーメッセージの 4 つ目の部分（この例では **000**）は、SMS 外部アカウントに定義されたエラーコード抽出用正規表現を使用して SR から抽出されたエラーコードに対応します。

   この正規表現は、外部アカウントの「**[!UICONTROL SMSC 特異性]**」タブで指定します。[このページ](../../delivery/using/sms-channel.md#creating-an-smpp-external-account)を参照してください。

   デフォルトでは、**SMPP 3.4 仕様**&#x200B;の&#x200B;**付録 B** に規定されているとおり、**err:** フィールドが抽出されます。

* パイプ記号（|）以降の文字列は、**[!UICONTROL 配信ログの検証]**&#x200B;テーブルの&#x200B;**[!UICONTROL 最初のテキスト]**&#x200B;列にのみ表示されます。このコンテンツは、常に、メッセージが正規化された後に **#MESSAGE#** で置き換えられます。これにより、同じようなエラーに対して複数のエントリが含まれるのを防ぐことができます。これは、E メールの場合と同じです。詳しくは、[バウンスメールの選定](../../delivery/using/understanding-delivery-failures.md#bounce-mail-qualification)を参照してください。

拡張された汎用 SMPP コネクタは、ヒューリスティックを適用して実用的なデフォルト値を見つけます。例えば、**DELIV** で始まるステータスは、ほとんどのプロバイダーでよく使用されている **DELIVRD** または **DELIVERED** と一致するので、成功とみなされます。これ以外のステータスはハードエラーとみなされます。
