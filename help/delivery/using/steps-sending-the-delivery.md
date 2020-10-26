---
title: 配信の設定と送信
seo-title: 配信の設定と送信
description: 配信の設定と送信
seo-description: null
page-status-flag: never-activated
uuid: 8bf70ea4-5f28-4d85-b5ce-0bd3ed3eea55
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: about-deliveries-and-channels
discoiquuid: df29492f-ed73-4ab8-b075-e76b3b9ebce3
translation-type: ht
source-git-commit: b447e316bed8e0e87d608679c147e6bd7b0815eb
workflow-type: ht
source-wordcount: '1620'
ht-degree: 100%

---


# 配信の設定と送信 {#configuring-and-sending-the-delivery}

>[!NOTE]
>
>配信のオーナーのみが配信を開始できます。別のオペレーター（またはオペレーターグループ）が配信を開始できるようにするには、レビュー担当者として「**[!UICONTROL 配信開始：]**」フィールドに追加する必要があります。
>
>詳しくは、[この節](../../campaign/using/marketing-campaign-approval.md#selecting-reviewers)を参照してください。

## 配信の追加パラメーター {#delivery-additiona-parameters}

配信を送信する前に、配信プロパティの「**[!UICONTROL 配信]**」タブで送信パラメーターを定義できます。

![](assets/s_ncs_user_wizard_delivery.png)

* **[!UICONTROL 配信の優先順位]**：このオプションにより、配信の優先順位レベル（標準、高、低）を設定して、配信の送信順序に影響を与えることができます。これは、より緊急度の高い配信をそれ以外の配信よりも優先させるのに便利です。

* **[!UICONTROL メッセージのバッチサイズ]**：このオプションでは、1 つの XML 配信パッケージ内でグループ化するメッセージの件数を定義できます。このパラメーターが 0 に設定されている場合、メッセージは自動的にグループ化されます。パッケージサイズは、`<delivery size>/1024` という計算に基づいて決定されます（ただし、パッケージあたりのメッセージ件数は最小 8、最大 256）。

   >[!CAUTION]
   >
   >配信が重複した場合はパラメーターがリセットされます。

* **[!UICONTROL 複数のウェーブを使用して送信]**：詳しくは、[複数のウェーブを使用した送信](#sending-using-multiple-waves)を参照してください。

* **[!UICONTROL SMTP 配信をテスト]**：このオプションを使用すると、SMTP を使用した配信の送信をテストできます。配信は、SMTP サーバーに接続するところまで進められますが、送信されません。

   >[!NOTE]
   >
   >MTA を呼び出さない、ミッドソーシングを使用するインストールの場合、このオプションを使用することは望ましくありません。
   >
   >SMTP サーバーの設定について詳しくは、[この節](../../installation/using/configuring-campaign-server.md#personalizing-delivery-parameters)を参照してください。

* **[!UICONTROL BCC で E メールを送信]**：このオプションを使用すると、BCC アドレスをメッセージのターゲットに追加するだけで、BCC 経由で E メールを外部システムに保存することができます。詳しくは、[この節](../../delivery/using/sending-messages.md#archiving-emails)を参照してください。

配信の設定が終わり、送信準備が整ったら、必ず[配信分析](../../delivery/using/steps-validating-the-delivery.md#analyzing-the-delivery)を実行してください。完了したら、「**[!UICONTROL 配信を確定]**」をクリックし、メッセージの配信を開始します。

![](assets/s_ncs_user_email_del_send.png)

その後、配信ウィザードを閉じて、「**[!UICONTROL 配信]**」タブで配信の実行をトラッキングできます。このタブには、配信の詳細または配信リストからアクセスできます。

メッセージを送信した後は、配信を監視およびトラッキングできます。詳しくは、以下の節を参照してください。

* [配信の監視](../../delivery/using/monitoring-a-delivery.md)
* [配信エラーの理解](../../delivery/using/understanding-delivery-failures.md)
* [メッセージトラッキングについて](../../delivery/using/about-message-tracking.md)

## 配信送信のスケジュール設定 {#scheduling-the-delivery-sending}

配信をスケジュールしたり、母集団に対する営業頻度を管理して過剰な営業活動をしないようするために、メッセージの配信を遅らせることができます。

1. 「**[!UICONTROL 送信]**」ボタンをクリックし、「**[!UICONTROL 配信を延期]**」オプションを選択します。

1. 「**[!UICONTROL コンタクト日]**」フィールドに開始日を入力します。

![](assets/dlv_email_del_plan.png)

1. その後、配信分析を開始し、配信の送信を確定します。ただし、配信の送信は、「**[!UICONTROL コンタクト日]**」フィールドで指定した日付まで開始されません。

>[!CAUTION]
>
>分析を開始すると、定義したコンタクト日が固定されます。この日付を修正する場合は、修正内容が考慮されるように、分析を再度実行する必要があります。

![](assets/s_ncs_user_email_del_start_delayed.png)

配信リストには、配信が「**[!UICONTROL 保留中]**」ステータスで表示されます。

![](assets/s_ncs_user_email_del_waiting.png)

スケジュールは、配信の「**[!UICONTROL スケジュール設定]**」ボタンを使用してアップストリーム設定することも可能です。

![](assets/s_ncs_user_email_del_save_in_calendar_ico.png)

これにより、配信を後の日付まで遅らせたり、暫定カレンダーに配信を保存したりできます。

* 「**[!UICONTROL 予約配信（自動実行なし）]**」オプションでは、配信の暫定的な分析をスケジュールできます。

   この設定を保存すると、配信のステータスは「**[!UICONTROL ターゲティングを保留中]**」に変化します。分析は指定した日付に開始されます。

* 「**[!UICONTROL 予約配信（予約された日になると自動実行）]**」オプションでは、配信日を指定できます。

   「**[!UICONTROL 送信]**」をクリックし、「**[!UICONTROL 配信を延期]**」を選択してから、分析を開始して配信を確定します。分析が完了すると、配信ターゲットの準備ができた状態になり、メッセージは指定した日付が来ると自動的に送信されます。

日付と時刻は、作業しているオペレーターのタイムゾーンに基づいて表されます。コンタクト日の入力フィールドの下にある&#x200B;**[!UICONTROL タイムゾーン]**&#x200B;ドロップダウンリストを使用すると、入力した日付と時刻が、指定したタイムゾーンに自動変換されます。

例えば、ロンドン時間の 8:00 に配信を自動実行するスケジュールを設定すると、時間は選択したタイムゾーンに自動的に変換されます。

![](assets/s_ncs_user_email_del_plan_calendar_timezone.png)

## 複数のウェーブを使用した送信 {#sending-using-multiple-waves}

負荷を分散するには、配信を複数のバッチに分割します。全体の配信を基準にしてバッチの数とその比率を設定します。

>[!NOTE]
>
>定義できるのは、サイズと 2 つの連続するウェーブの間隔のみです。受信者の選択条件をウェーブごとに設定することはできません。

1. 配信プロパティウィンドウを開き、「**[!UICONTROL 配信]**」タブをクリックします。
1. 「**[!UICONTROL 複数のウェーブを使用して送信]**」オプションを選択し、「**[!UICONTROL ウェーブを定義...]**」リンクをクリックします。

   ![](assets/s_ncs_user_wizard_waves.png)

1. ウェーブを設定するには、次のいずれかをおこないます。

   * 各ウェーブのサイズを定義します。例えば、対応するフィールドに **[!UICONTROL 30％]**&#x200B;と入力した場合、各ウェーブは、配信に含まれるメッセージの 30％を表します（ただし、最後のウェーブは除きます。最後のウェーブは、メッセージの 10％を表します）。

      「**[!UICONTROL 期間]**」フィールドで、2 つの連続するウェーブの開始間隔を指定します。例えば、**[!UICONTROL 2d]** と入力した場合、最初のウェーブは直ちに開始され、2 番目のウェーブは 2 日後に、3 番目のウェーブは 4 日後にといった具合に開始されます。

      ![](assets/s_ncs_user_wizard_waves_create_size.png)

   * 各ウェーブを送信するためのカレンダーを定義します。

      「**[!UICONTROL 開始日]**」列では、2 つの連続するウェーブの開始間隔を指定します。「**[!UICONTROL サイズ]**」列では、固定の数値または割合を入力します。

      以下の例では、最初のウェーブは、配信に含まれるメッセージ総数の 25％を表しており、直ちに開始されます。次の 2 つのウェーブで配信が完了しますが、これらのウェーブは、6 時間間隔で開始するように設定されています。

      ![](assets/s_ncs_user_wizard_waves_create.png)
   特別なタイポロジルールである「**[!UICONTROL ウェーブスケジュールの検証]**」では、最後のウェーブが配信の有効期限の前に計画されているかどうかが確認されます。キャンペーンタイポロジとそのルールは、配信プロパティの「**[!UICONTROL タイポロジ]**」タブで設定します。詳しくは、[タイポロジを使用したプロセスの検証](../../delivery/using/steps-validating-the-delivery.md#validation-process-with-typologies)を参照してください。

   >[!CAUTION]
   >
   >最後の 2 つのウェーブが配信期限を過ぎないことを確認してください。配信期限は、「**[!UICONTROL 有効性]**」タブで定義されています。配信期限を過ぎると、一部のメッセージが送信されない場合があります。
   >
   >また、最後のウェーブを設定するときに、再試行の時間を十分にみておく必要があります。[この節](../../delivery/using/steps-sending-the-delivery.md#configuring-retries)を参照してください。

1. 送信状況を監視するには、配信ログを参照してください。[このページ](../../delivery/using/monitoring-a-delivery.md#delivery-logs-and-history)を参照してください。

   処理済みのウェーブで既に送信された配信（ステータスが&#x200B;**[!UICONTROL 送信済み]**）と、残りのウェーブで送信されるウェーブ（ステータスが&#x200B;**[!UICONTROL 保留中]**）を確認できます。

以下の 2 つの例は、最も一般的な複数のウェーブの使用例です。

* **ランプアッププロセス時**

   新しいプラットフォームを使用して E メールが送信された場合、インターネットサービスプロバイダー（ISP）は認識されない IP アドレスを疑わしく思います。多くの場合、大量の E メールが突然送信されると、ISP はそれらの E メールをスパムとしてマークします。

   ウェーブを使用して送信するボリュームを徐々に増やすことで、スパムとしてマークされないようにできます。この方法により、スタートアップフェーズをスムーズに進め、無効なアドレスが全体に占める割合を減らすことができます。

   そのためには、「**[!UICONTROL カレンダーに従ってウェーブをスケジュール]**」オプションを選択します。例えば、最初のウェーブを 10％に、2 番目のウェーブを 15％にといった具合に設定します。

   ![](assets/s_ncs_user_wizard_waves_ramp-up.png)

* **コールセンターが関与するキャンペーン**

   電話によるロイヤリティキャンペーンを管理する場合、組織が処理できる購読者への電話の本数には限界があります。

   ウェーブを使用して、1 日あたりのメッセージ数を 20 に制限できます（コールセンターの 1 日あたりの処理能力）。

   これをおこなうには、「**[!UICONTROL 同じサイズの複数のウェーブをスケジュール]**」オプションを選択します。ウェーブのサイズとして **[!UICONTROL 20]** を入力し、「**[!UICONTROL 期間]**」フィールドに **[!UICONTROL 1d]** と入力します。

   ![](assets/s_ncs_user_wizard_waves_call_center.png)

## 再試行の設定 {#configuring-retries}

**ソフト**&#x200B;または&#x200B;**無視**&#x200B;のエラーによって一時的に配信できなかったメッセージは、自動再試行の対象となります。配信エラーのタイプと理由については、[この節](../../delivery/using/understanding-delivery-failures.md#delivery-failure-types-and-reasons)を参照してください。

配信パラメーターの「**[!UICONTROL 配信]**」タブの中央のセクションには、配信の翌日に実行する再試行回数と、再試行を繰り返す際の最小間隔が表示されます。

![](assets/s_ncs_user_wizard_retry_param.png)

デフォルトでは、配信後の最初の日には、最低 1 時間の間隔をおいて 24 時間のうちに 5 回の再試行がスケジュールされます。その後は、「**[!UICONTROL 有効性]**」タブで指定される配信期限が来るまで、1 日 1 回の再試行がスケジュールされます（[有効期間の定義](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)を参照）。

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで、Enhanced MTA にアップグレードした場合、Campaign では配信の再試行設定が使用されなくなります。ソフトバウンスの再試行とその間隔は、メッセージの E メールドメインから返されるバウンス応答のタイプと重大度に基づいて、Enhanced MTA が決定します。
>
>すべての影響について詳しくは、[Adobe Campaign Enhanced MTA](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html) ドキュメントを参照してください。


## 有効期間の定義 {#defining-validity-period}

メッセージの送信（および再試行）が可能な期間は、配信が開始されたときから配信期限までです。配信期限は、配信プロパティの「**[!UICONTROL 有効性]**」タブに表示されます。

![](assets/s_ncs_user_email_del_valid_period.png)

* 「**[!UICONTROL 配信期間]**」フィールドには、グローバルでおこなう配信再試行の期限を入力できます。Adobe Campaign は、開始日にメッセージの送信を開始した後、エラーのみを返すメッセージについて、設定された定期的な再試行を、有効期限日に達するまで実行します。

   日付を指定することもできます。そのためには、「**[!UICONTROL 有効期限を明示的に設定]**」を選択します。この場合、配信および有効期限日に時刻を指定することもできます。デフォルト値は現在時刻ですが、入力フィールドを使用して直接変更できます。

* **リソースの有効期限**：「**[!UICONTROL 有効期限]**」フィールドは、アップロードされたリソース（主にミラーページと画像）に関して使用されます。ディスクスペースを節約するために、このページ上のリソースが有効な期間は限られています。

   このフィールドの値は、[この節](../../platform/using/adobe-campaign-workspace.md#default-units)にリストされている単位で表示できます。

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールで、Enhanced MTA にアップグレードした場合、キャンペーン配信の「**[!UICONTROL 配信期間]**」設定は、**3.5** 日以下に設定された場合にのみ使用されます。3.5 日を超える値を定義した場合、その値は考慮されません。
>
>すべての影響について詳しくは、[Adobe Campaign Enhanced MTA](https://helpx.adobe.com/jp/campaign/kb/acc-campaign-enhanced-mta.html) ドキュメントを参照してください。
