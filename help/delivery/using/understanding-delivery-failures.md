---
title: 配信エラーの理解
seo-title: 配信エラーの理解
description: 配信エラーの理解
seo-description: null
page-status-flag: never-activated
uuid: 03a91f84-77fe-40a9-8be9-a6a35a873ae1
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: delivery
content-type: reference
topic-tags: monitoring-deliveries
discoiquuid: 78b58a7a-b387-4d5d-80d5-01c06f83d759
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: e5a2ef47108c6779a744197638e2de9d1072cfe3

---


# 配信エラーの理解{#understanding-delivery-failures}

## 配信エラーについて {#about-delivery-failures}

メッセージ（E メール、SMS、プッシュ通知）をプロファイルに送信できない場合、リモートサーバーは自動的にエラーメッセージを送信します。このメッセージは Adobe Campaign プラットフォームによってピックアップされ、その E メールアドレスまたは電話番号を強制隔離するかどうかを決定するために評価されます。[バウンスメールの管理](#bounce-mail-management)を参照してください。

>[!NOTE]
>
>E メールメッセージ（「バウンス」）は inMail プロセスによって評価されます。SMS エラーメッセージ（ステータスレポートを表す「SR」）は MTA プロセスによって評価されます。

メッセージの送信後、配信ログによって各プロファイルの配信ステータスと、関連するエラーのタイプおよび理由を確認できます。

アドレスが強制隔離されているか、プロファイルがブラックリストに登録されている場合、配信準備の際にメッセージを除外することもできます。除外されたメッセージのリストは、配信ダッシュボードに表示されます。

**関連トピック：**

* [配信ログと履歴](../../delivery/using/monitoring-a-delivery.md#delivery-logs-and-history)
* [失敗ステータス](../../delivery/using/monitoring-a-delivery.md#failed-status)
* [配信エラーのタイプと理由](#delivery-failure-types-and-reasons)

## 配信エラーのタイプと理由 {#delivery-failure-types-and-reasons}

メッセージエラーには次の 3 つのタイプがあります。それぞれのエラータイプによって、アドレスが強制隔離されるかどうかが決まります。詳しくは、[アドレスを強制隔離する条件](../../delivery/using/understanding-quarantine-management.md#conditions-for-sending-an-address-to-quarantine)を参照してください。

* **ハード**：「ハード」エラーは無効なアドレスの存在を示します。このエラーは、アドレスが無効であることを明示的に示すエラーメッセージ（例：「不明なユーザー」）を伴います。
* **ソフト**：これは一時的なエラーか、「無効なドメイン」または「メールボックス容量超過」など、分類が不可能なエラーです。
* **無視**：これは、「外出中」など一時的であることがわかっているエラーまたは送信者タイプが「postmaster」である場合などの技術的エラーです。

配信エラーの理由として考えられるものを以下に示します。

<table> 
 <tbody> 
  <tr> 
   <td> エラーラベル </td> 
   <td> エラータイプ </td> 
   <td> 技術値 </td> 
   <td> 説明 </td> 
  </tr> 
  <tr> 
   <td> 無効なアカウント </td> 
   <td> ソフト／ハード </td> 
   <td> 4 </td> 
   <td> アドレスにリンクされているアカウントはもはやアクティブではありません。インターネットアクセスプロバイダー（IAP）は、長期間使用されていないことを検出すると、そのユーザーのアカウントをクローズできます。そのユーザーのアドレスへの配信は不可能になります。アカウントが 6 ヶ月間使用されていないことが原因で一時的に無効になっていて、まだ有効化することができる場合は、エラーありステータスが割り当てられ、エラーカウンターが 5 に達するまでアカウントが再試行されます。アカウントが永続的に無効化されたことをエラーが示している場合は、アカウントは直接強制隔離に設定されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> 強制隔離中のアドレス </td> 
   <td> ハード </td> 
   <td> 9 </td> 
   <td> アドレスは強制隔離されました。<br /> </td> 
  </tr> 
  <tr> 
   <td> アドレスが未指定 </td> 
   <td> ハード </td> 
   <td> 7 </td> 
   <td> 受信者のアドレスが指定されていません。<br /> </td> 
  </tr> 
  <tr> 
   <td> 低品質のアドレス </td> 
   <td> 無視 </td> 
   <td> 14 </td> 
   <td> このアドレスの品質評価が低すぎます。<br /> </td> 
  </tr> 
  <tr> 
   <td> ブラックリストに登録されたアドレス </td> 
   <td> ハード </td> 
   <td> 8 </td> 
   <td> このアドレスは送信時にブラックリストに登録されていました。このステータスは、データを Adobe Campaign の強制隔離リストにインポートするときに外部リストおよび外部システムからデータをインポートするために使用します。<br /> </td> 
  </tr> 
  <tr> 
   <td> 制御アドレス </td> 
   <td> 無視 </td> 
   <td> 127 </td> 
   <td> 受信者のアドレスはコントロール母集団に含まれています。<br /> </td> 
  </tr> 
  <tr> 
   <td> 重複 </td> 
   <td> 無視 </td> 
   <td> 10 </td> 
   <td> 受信者のアドレスがこの配信に既に存在しました。<br /> </td> 
  </tr> 
  <tr> 
   <td> 無視されたエラー </td> 
   <td> 無視 </td> 
   <td> 25 </td> 
   <td> アドレスはホワイトリストに含まれています。したがってエラーは無視され、E メールは送信されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> 判別後に除外 </td> 
   <td> 無視 </td> 
   <td> 12 </td> 
   <td> 受信者が「判別」タイプのキャンペーンタイポロジルールによって除外されました。<br /> </td> 
  </tr> 
  <tr> 
   <td> SQL ルールによって除外 </td> 
   <td> 無視 </td> 
   <td> 11 </td> 
   <td> 受信者が「SQL」タイプのキャンペーンタイポロジルールによって除外されました。<br /> </td> 
  </tr> 
  <tr> 
   <td> 無効なドメイン </td> 
   <td> ソフト </td> 
   <td> 2 </td> 
   <td> E メールアドレスのドメインが正しくないか、存在しません。このプロファイルは、エラーカウントが 5 にならない限り、再びターゲットになります。その後、レコードは強制隔離ステータスに設定され、以降は再試行されなくなります。<br /> </td> 
  </tr> 
  <tr> 
   <td> メールボックス容量超過 </td> 
   <td> ソフト </td> 
   <td> 5 </td> 
   <td> このユーザーのメールボックスはいっぱいになっていて、メッセージをこれ以上受け入れることができません。このプロファイルは、エラーカウントが 5 にならない限り、再びターゲットになります。その後、レコードは強制隔離ステータスに設定され、以降は再試行されなくなります。<br />このタイプのエラーはクリーンアッププロセスによって管理されます。アドレスは 30 日後に有効なステータスに設定されます。<br />警告：強制隔離されたアドレスのリストからアドレスを自動的に削除するには、データベースクリーンアップテクニカルワークフローを開始する必要があります。<br /> </td> 
  </tr> 
  <tr> 
   <td> 未接続 </td> 
   <td> 無視 </td> 
   <td> 6 </td> 
   <td> メッセージが送信されたときに受信者の携帯電話の電源が切れていたか、ネットワークに接続されていませんでした。<br /> </td> 
  </tr> 
  <tr> 
   <td> 未定義 </td> 
   <td> 未定義 </td> 
   <td> 0 </td> 
   <td> エラーがまだインクリメントされていないので、アドレスは検証中です。このタイプのエラーは、サーバーが新しいエラーメッセージを送信すると発生します。単独のエラーである可能性もありますが、再度発生した場合はエラーカウンターがインクリメントされ、テクニカルチームに警告されます。その後、テクニカルチームは、ツリー構造の<span class="uicontrol">管理</span>／<span class="uicontrol">キャンペーン管理</span>／<span class="uicontrol">配信不能件数の管理</span>ノードからメッセージの分析を実行し、このエラーを検証します。<br /> </td> 
  </tr> 
  <tr> 
   <td> オファーを受ける資格がない </td> 
   <td> 無視 </td> 
   <td> 16 </td> 
   <td> 受信者には配信でオファーを受ける資格がありませんでした。<br /> </td> 
  </tr> 
  <tr> 
   <td> 拒否 </td> 
   <td> ソフト／ハード </td> 
   <td> 20 </td> 
   <td> アドレスは、スパムレポートであるというセキュリティフィードバックが原因で強制隔離されました。アドレスは、エラーに応じて、エラーカウンターが 5 に達するまで再試行されるか、直接強制隔離されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> サイズが制限されたターゲット </td> 
   <td> 無視 </td> 
   <td> 17 </td> 
   <td> 受信者に対する最大配信サイズに達しました。<br /> </td> 
  </tr> 
  <tr> 
   <td> 未適合のアドレス </td> 
   <td> 無視 </td> 
   <td> 2019 年 </td> 
   <td> 郵便物の送付先住所が選定されていません。<br /> </td> 
  </tr> 
  <tr> 
   <td> 未到達 </td> 
   <td> ソフト／ハード </td> 
   <td> 3 </td> 
   <td> メッセージ配信チェーンでエラーが発生しました。SMTP リレーに関するインシデント、ドメインへの一時的な未到達などの可能性があります。アドレスは、エラーに応じて、エラーカウンターが 5 に達するまで再試行されるか、直接強制隔離されます。<br /> </td> 
  </tr> 
  <tr> 
   <td> 不明なユーザー </td> 
   <td> ハード </td> 
   <td> 1 </td> 
   <td> アドレスが存在しません。このプロファイルに対する配信はこれ以上試行されません。<br /> </td> 
  </tr> 
 </tbody> 
</table>

## 一時的な配信エラーの後の再試行 {#retries-after-a-delivery-temporary-failure}

一時的な&#x200B;**ソフト**&#x200B;または&#x200B;**無視**&#x200B;のエラーによるメッセージエラーが発生した場合、再試行が配信期間中におこなわれます

>[!NOTE]
>
>一時的に配信できなかったメッセージは、**ソフト**&#x200B;または&#x200B;**無視**&#x200B;のエラーにのみ関係するもので、**ハード**&#x200B;エラーは関係ありません（[配信エラーのタイプと理由](#delivery-failure-types-and-reasons)を参照）。

配信の期間を変更するには、配信の高度なパラメーターまたは配信テンプレートにアクセスし、対応するフィールドで希望の期間を指定します。高度な配信プロパティについては、[この節](../../delivery/using/steps-sending-the-delivery.md#defining-validity-period)で説明しています。

デフォルトの設定では、1 時間間隔で 5 回、その後 4 日間は 1 日に 1 回再試行されます。再試行の回数の変更は、グローバルに（アドビの技術管理者にお問い合わせください）、または配信または配信テンプレートごとに（[この節](../../delivery/using/steps-sending-the-delivery.md#configuring-retries)を参照）おこなうことができます。

## 同期エラーと非同期エラー {#synchronous-and-asynchronous-errors}

メッセージは、ただちにエラーになることも（同期エラー）、送信後しばらくしてエラーになることも（非同期エラー）あります。

* 同期エラー：Adobe Campaign 配信サーバーによってアクセスされたリモートメールサーバーがエラーメッセージを返します。配信をプロファイルのサーバーに送ることは許可されません。Adobe Campaign が個々のエラーを評価して、その E メールアドレスを強制隔離すべきかどうかを判断します。[バウンスメールの選定](#bounce-mail-qualification)を参照してください。
* 非同期エラー：バウンスメールまたは SR が受信サーバーによって後で再送信された場合です。このメールは、メッセージにエラーのラベルを付けるためにアプリケーションが使用するテクニカルメールボックスに読み込まれます。非同期エラーは、配信の送信から 1 週間が経過するまで発生する可能性があります。

   >[!NOTE]
   >
   >バウンスメールボックスの設定については、[この節](../../installation/using/deploying-an-instance.md#managing-bounced-emails)で詳しく説明しています。

   フィードバックループはバウンス E メールのように機能します。ユーザーが E メールをスパムとみなしたら、Adobe Campaign で E メールルールを設定して、このユーザーへのすべての配信をブロックできます。E メールをスパムとみなしたユーザーに送信されたメッセージは、この目的用に特別に作成された E メールボックスに自動的にリダイレクトされます。このようなユーザーのアドレスは、購読解除リンクをクリックしなかった場合でも、ブラックリストに登録されます。アドレスは、（**NmsRecipient**）受信者テーブルではなく、（**NmsAddress**）強制隔離テーブルでブラックリストに登録されます。

   >[!NOTE]
   >
   >苦情数管理については、[配信品質の管理](../../delivery/using/about-deliverability.md)の節で詳しく説明しています。

## バウンスメール管理 {#bounce-mail-management}

Adobe Campaign プラットフォームでは、バウンスメール機能を使用して、E メール配信の失敗を管理できます。E メールを受信者に配信できない場合は、リモートメッセージングサーバーが、専用のテクニカル受信ボックスにエラーメッセージ（バウンスメール）を自動的に返します。E メール管理ルールのリストを充実させるために、エラーメッセージは Adobe Campaign プラットフォームによって収集され、inMail プロセスによって評価されます。

### バウンスメール強制隔離 {#bounce-mail-qualification}

E メールの配信が失敗すると、Adobe Campaign の配信サーバーはメッセージングサーバーまたはリモート DNS サーバーからエラーメッセージを受け取ります。エラーのリストは、リモートサーバーが返したメッセージに含まれる文字列で構成されます。エラータイプと理由が各エラーメッセージに割り当てられます。

このリストはノードを介して使用で **[!UICONTROL Administration > Campaign Management > Non deliverables Management > Delivery log qualification]** きます。 このリストには、配信エラーを評価するために Adobe Campaign が使用するすべてのルールが含まれています。このリストは、完成されたものではなく、Adobe Campaign によって定期的に更新されます。ユーザーが管理することもできます。

![](assets/tech_quarant_rules_qualif.png)

* The message returned by the remote server on the first occurrence of this error type is displayed in the **[!UICONTROL First text]** column of the **[!UICONTROL Delivery log qualification]** table. If this column is not displayed, click the **[!UICONTROL Configure list]** button at the right bottom of the list to select it.

![](assets/tech_quarant_rules_qualif_text.png)

Adobe Campaignフィルターは、変数の内容（ID、日付、電子メールアドレス、電話番号など）を削除するためにこのメッセージを送信します。フィルタ結果を列に表示し **[!UICONTROL Text]** ます。 変数は、**`#xxx#`** で置き換えられます（ただし、アドレスは **`*`** で置き換えられます）。

このプロセスで同じタイプのすべてのエラーをまとめることにより、同じようなエラーの複数のエントリが配信ログの検証テーブルに含まれないようにすることができます。

>[!NOTE]
>
>The **[!UICONTROL Number of occurrences]** field displays the number of occurrences of the message in the list. 上限は 100,000 回です。このフィールドは、リセットする場合など、必要に応じて編集できます。

バウンスメールは、次の検証ステータスを持つことができます。

* **[!UICONTROL To qualify]** :バウンスメールが正しくなかった。 選定を配信品質チームに割り当てて、効率的なプラットフォーム配信品質を保証する必要があります。選定されていないバウンスメールは、E メール管理ルールのリストのエンリッチメントには使用されません。
* **[!UICONTROL Keep]** :バウンスメールは、既存の電子メール管理ルールと比較してリストを強化するために **** 、配信品質のワークフローとして「更新」で使用される資格があります。
* **[!UICONTROL Ignore]** :バウンスメールはキャンペーンMTAでは無視され、このバウンスによって受信者のアドレスが隔離されることはありません。 配信品質ワークフローのために更新で **は使用されず** 、クライアントインスタンスには送信されません。

![](assets/deliverability_qualif_status.png)

>[!NOTE]
>
>ホストインストールまたはハイブリッドインストールの場合、拡張MTAにアップグレード済みの場合：
>
>* 表の直帰条件は、同期 **[!UICONTROL Delivery log qualification]** 配信障害のエラーメッセージには使用されません。 拡張MTAは、バウンスのタイプと条件を決定し、その情報をキャンペーンに返します。
   >
   >
* 非同期バウンスは、inMailプロセスでもルールを通じて認定さ **[!UICONTROL Inbound email]** れます。 For more on this, see [Email management rules](#email-management-rules).
   >
   >
* 拡張MTAを ******[!UICONTROL Inbound email]** Webhooks/EFSなしで使用する場合、ルールは、非同期バウンス電子メールと同じ電子メールアドレスを使用して、拡張MTAからの同期バウンス電子メールの処理にも使用されます。
>
>
Adobe Campaign Enhanced MTA について詳しくは、この[ドキュメント](https://helpx.adobe.com/jp/campaign/kb/campaign-enhanced-mta.html)を参照してください。

### E メール管理ルール {#email-management-rules}

メールルールはノードを介してアクセス **[!UICONTROL Administration > Campaign Management > Non deliverables Management > Mail rule sets]** されます。 E メール管理ルールがウィンドウの下部に表示されます。

![](assets/tech_quarant_rules.png)

>[!NOTE]
>
>プラットフォームのデフォルトのパラメーターは、デプロイウィザードで設定します。詳しくは、[この節](../../installation/using/deploying-an-instance.md)を参照してください。

デフォルトのルールは次のとおりです。

>[!IMPORTANT]
>
>* パラメーターを変更した場合は、配信サーバー（MTA）を再起動する必要があります。
>* 管理ルールを変更または作成できるのは、エキスパートユーザーのみです。


#### インバウンド E メール {#inbound-email}

これらのルールには、リモートサーバーが返すことができ、エラー（**ハード**、**ソフト**&#x200B;または&#x200B;**無視**）を検証できる文字列のリストが含まれます。

E メールが失敗すると、リモートサーバーがプラットフォームのパラメーターで指定されたアドレスにバウンスメールを返します。Adobe Campaign compares the content of each bounce mail to the strings in the list of rules, and then assigns it one of the three [error types](#delivery-failure-types-and-reasons).

>[!NOTE]
>
>ユーザーは独自のルールを作成できます。パッケージをインポートしたり、**配信品質の更新**&#x200B;ワークフローでデータを更新すると、ユーザーが作成したルールが上書きされます。

バウンスメールの資格について詳しくは、この節を参 [照してくださ](#bounce-mail-qualification)い。

>[!IMPORTANT]
>
>ホストインストールまたはハイブリッドインストールの場合、拡張MTAにアップグレードし、インスタンスに **Webhooks****[!UICONTROL Inbound email]** /EFS機能がある場合、同期配信障害エラーメッセージにルールは使用されなくなります。 詳しくは、[この節](#bounce-mail-qualification)を参照してください。
>
>Adobe Campaign Enhanced MTA について詳しくは、この[ドキュメント](https://helpx.adobe.com/jp/campaign/kb/campaign-enhanced-mta.html)を参照してください。

#### ドメイン管理 {#domain-management}

Adobe Campaignメッセージングサーバは、すべてのドメ **インに** 1つのドメイン管理規則を適用します。

<!--![](assets/tech_quarant_domain_rules_02.png)-->

* 特定の識別標準や、**送信者 ID**、**DomainKeys**、**DKIM**、**S/MIME** などドメイン名をチェックするための暗号鍵を有効化するかどうかを選択できます。
* The **SMTP relay** parameters let you configure the IP address and the port of a relay server for a particular domain. 詳しくは、[この節](../../installation/using/configuring-campaign-server.md#smtp-relay)を参照してください。

メッセージがOutlookで表示され、送信者のアドレス **[!UICONTROL on behalf of]** が表示される場合は、 **** Sender IDを使用して電子メールに署名しないようにしてください。これは、Microsoftが提供する古い独自の電子メール認証標準です。 このオプションが有 **[!UICONTROL Sender ID]** 効な場合は、対応するボックスのチェックを外し、Adobe Campaignサポートに連絡します。 配信品質に影響はありません。

>[!IMPORTANT]
>
>For hosted or hybrid installations, if you have upgraded to the Enhanced MTA, the **[!UICONTROL Domain management]** rules are no longer used. **DKIM(DomainKeys Identified Mail)電子メール認証の署名は** 、すべてのドメインを持つすべてのメッセージに対して拡張MTAによって行われます。 拡張MTAレベルで特に指定され **ていない限り、** Sender ID **、** DomainKeys **、** S/MIMEを使用して署名することはできません。
>
>Adobe Campaign Enhanced MTA について詳しくは、この[ドキュメント](https://helpx.adobe.com/jp/campaign/kb/campaign-enhanced-mta.html)を参照してください。

#### MX 管理 {#mx-management}

* MX管理ルールは、特定のドメインの送信電子メールのフローを制御するために使用されます。 このルールは、バウンスメッセージをサンプリングし、必要に応じて送信をブロックします。

* Adobe Campaign のメッセージングサーバーは、ドメイン独自のルールを適用します。一般的なケース用のルールは、ルールのリストにアスタリスクで表されます。

* MX管理ルールを設定するには、しきい値を設定し、特定のSMTPパラメーターを選択します。 **しきい値**&#x200B;とは、特定のドメイン宛てのメッセージをブロックする基準となるエラー率です。エラー率がこの値を超えると、特定のドメイン宛てのすべてのメッセージがブロックされます。例えば一般的なケースでは、300 件以上のメッセージに対してエラー率が 90％に達すると、E メールの送信が 3 時間ブロックされます。

MX 管理について詳しくは、[この節](../../installation/using/email-deliverability.md#mx-configuration)を参照してください。

>[!IMPORTANT]
>
>For hosted or hybrid installations, if you have upgraded to the Enhanced MTA, the **[!UICONTROL MX management]** delivery throughput rules are no longer used. Enhanced MTA は独自の MX ルールを使用します。これにより、独自の E メールレピュテーション履歴および E メールを送信しているドメインから送信されるリアルタイムのフィードバックに基づいて、スループットをドメインごとにカスタマイズすることができます。
>
>Adobe Campaign Enhanced MTA について詳しくは、この[ドキュメント](https://helpx.adobe.com/jp/campaign/kb/campaign-enhanced-mta.html)を参照してください。
