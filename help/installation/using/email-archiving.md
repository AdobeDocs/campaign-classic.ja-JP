---
product: campaign
title: メールのアーカイブ
description: メールのアーカイブ
feature: Installation, Instance Settings, Email
audience: installation
content-type: reference
topic-tags: additional-configurations
exl-id: 424faf25-2fd5-40d1-a2fc-c715fc0b8190
source-git-commit: b666535f7f82d1b8c2da4fbce1bc25cf8d39d187
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 82%

---

# メール BCC の設定 {#email-archiving}



プラットフォームから送信された電子メールのコピーを保持するようにAdobe Campaignを設定できます。

ただし、Adobe Campaign自体はアーカイブされたファイルを管理しません。 これにより、選択したメッセージを専用のアドレスに送信し、外部システムを使用して処理およびアーカイブできます。

これを行うには、送信された電子メールに対応する.emlファイルを、SMTP電子メールサーバーなどのリモートサーバーに転送します。 アーカイブ先は、指定する必要がある BCC 電子メールアドレス(配信受信者には表示されません)です。

## Recommendationsと制限事項 {#recommendations-and-limitations}

* 「BCC でメールを送信」はオプションの機能です。ライセンス契約をご確認ください。
* ホ **スト型およびハイブリッド型アーキテクチャの場合は**、アカウント担当者に問い合わせてアクティブ化してください。 BCC に設定するメールアドレスをアドビ システムズにご提供いただく必要があります。
* **オンプレミスインストール** の場合は、以下のガイドラインに従ってアクティブ化します。[ メール BCC のアクティブ化（オンプレミス） ](#activating-email-archiving--on-premise-) および [BCC メールアドレスの設定（オンプレミス） ](#configuring-the-bcc-email-address--on-premise-) の節を参照してください。
* BCC に設定できるメールアドレスは 1 つだけです。
* 「BCC で E メールを送信」を設定したら、配信テンプレートまたは「**[!UICONTROL BCC で E メールを送信]**」オプション経由の配信で、その機能が有効になっていることを確認します。 詳しくは、[この節](../../delivery/using/sending-messages.md#archiving-emails)を参照してください。
* 正常に送信された電子メールのみが考慮され、バウンスは考慮されません。
* Adobe Campaign17.2（ビルド8795）で電子メールアーカイブシステムが変更されました。 既にメールのアーカイブを使用している場合は、新しいメール BCC システムに手動でアップグレードする必要があります。 詳しくは、[ 新しいメール BCC への移行 ](#updated-email-archiving-system--bcc-) の節を参照してください。

## 「BCC で E メールを送信」の有効化（オンプレミス） {#activating-email-archiving--on-premise-}

[!BADGE オンプレミスおよびハイブリッド]{type=Caution url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"}


Adobe Campaignがオンプレミスでインストールされている場合にBCC電子メールアーカイブをアクティブにするには、次の手順に従います。

### ローカルフォルダー {#local-folder}

送信済み電子メールを BCC 電子メールアドレスに転送できるようにするには、送信済み電子メールの正確な生コピーを、まず.emlファイルとしてローカルフォルダに保存する必要があります。

ローカルフォルダーのパスは、設定の **config-`<instance>`.xml** ファイルで指定する必要があります。 例：

```
<mta dataLogPath="C:\emails">
```

>[!NOTE]
>
>セキュリティ設定で **dataLogPath** パラメーターを使用して定義されたフォルダーへのアクセスが許可されていることを確認するのは、プロジェクトの導入チームの責任です。

フルパスは次のとおりです。 **`<datalogpath>  YYYY-MM-DDHHh`**. 日時は、MTAサーバーの時計(UTC)に従って設定されます。 例：

```
C:\emails\2018-12-02\13h
```

アーカイブファイル名は、電子メールのステータスが「 **`<deliveryid>-<broadlogid>.eml`** 送信されていません **&#x200B;**」のときに付けられます。 ステータスが「 **[!UICONTROL 送信済み]**」に変わると、ファイル名がに変わり **`<deliveryid>-<broadlogid>-sent.eml`**&#x200B;ます。 例：

```
C:\emails\2018-12-02\13h\4012-8040-sent.eml
```

>[!NOTE]
>
>ミッドソーシングインスタンスでは、BCC メールのディレクトリは、ミッドソーシングサーバー上にあります。
>
>deliveryIDとbroadlogIDは、電子メールのステータスが送信されない場合に、ミッドソーシングサーバーから取得されます。 ステータスが「 **[!UICONTROL 送信済み]**」に変わると、これらのIDはマーケティングサーバーから取得されます。

### パラメーター {#parameters}

ローカルフォルダーパスを定義したら、 **config-`<instance name>.xml`** fileで必要に応じて次の要素を追加および編集します。 次にデフォルト値を示します。

```
<archiving autoStart="false" compressionFormat="0" compressBatchSize="10000"
           archivingType="1" expirationDelay="2" purgeArchivesDelay="7"
           pollDelay="600" acquireLimit="5000" smtpNbConnection="2"/>
```

* **compressionFormat**:.emlファイルを圧縮する際に使用する形式。 可能な値は次のとおりです。

  **0**:no compression（デフォルト値）

  **1**:圧縮（.zip形式）

* **compressBatchSize**:アーカイブ（.zipファイル）に追加された.emlファイルの数。


* **archivingType**:アーカイブ方法を使用します。 使用できる値は **1** だけです。 送信されたメールの生のコピーは、.eml 形式で **dataLogPath** フォルダーに保存され、SMTP 経由で BCC メールアドレスに送信されます。 電子メールコピーがBCCアドレスに送信されると、アーカイブファイル名 **`<deliveryid>-<broadlogid>-sent-archived.eml`** がになり、ファイルが **&#x200B;**&#x200B;dataLogPath/archivesフォルダーに移動されます。 次に、送信およびBCCアーカイブされた電子メールファイルのパスを示 **`<datalogpath>archivesYYYY-MM-DDHHh<deliveryid>- <broadlogid>-sent-archived.eml`**&#x200B;します。

  <!--
  **0**: raw copies of sent emails are saved in .eml format to the **dataLogPath** folder (default value). An archiving copy of the **`<deliveryid>-<broadlogid>-sent.eml`** file is saved to the **dataLogPath/archives** folder. The sent email file path becomes **`<datalogpath>archivesYYYY-MM-DDHHh <deliveryid>-<broadlogid>-sent.eml`**.-->

* **expirationDelay**:アーカイブ用に保持される.emlファイルの日数。 その後、圧縮用に **dataLogPath/archivesフォルダーに自動的に移動されます** 。 デフォルトでは、.emlファイルは2日後に期限切れになります。
* **purgeArchivesDelay**:アーカイブが **dataLogPath/`<archives>`** フォルダーに保存される日数。 その期間を過ぎると、それらは完全に削除されます。 削除は、MTAが開始された時点で開始されます。 デフォルトでは、7日ごとに実行されます。
* **pollDelay**:dataLogPath **&#x200B;**&#x200B;フォルダーに新しく送信される電子メールの頻度（秒）を確認しています。 例えば、このパラメーターを60に設定した場合、毎分、アーカイブ処理は **dataLogPath/`<date and time>`** フォルダー内の.emlファイルを調べ、必要に応じて削除を適用し、BCCアドレスに電子メールコピーを送信し、アーカイブファイルを圧縮します。
* **acquireLimit**:pollDelay **&#x200B;**&#x200B;パラメーターに従ってアーカイブ処理が再適用される前に一度に処理された.emlファイルの数。 例えば、pollDelay **パラメーターが60に設定されている間に、** acquireLimit **&#x200B;**&#x200B;パラメーターを100に設定すると、1分あたり100個の.emlファイルが処理されます。
* **smtpNbConnection**:BCC 電子メールアドレスへのSMTP接続数。

電子メール送信のスループットに従って、これらのパラメーターを必ず調整してください。 例えば、MTAが1時間に30,000通のメールを送信する設定では、 **pollDelay** パラメーターを600に、 **acquireLimitパラメーターを5000に、**&#x200B;**&#x200B;** smtpNbConnectionパラメーターを2に設定できます。 つまり、2つのSMTP接続を使用している場合、10分ごとに5,000通の電子メールがBCCアドレスに送信されます。

## BCC メールアドレスの設定（オンプレミス） {#configuring-the-bcc-email-address--on-premise-}

[!BADGE オンプレミスおよびハイブリッド]{type=Caution url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="オンプレミスデプロイメントとハイブリッドデプロイメントにのみ適用されます"}


>[!IMPORTANT]
>
>プライバシー上の理由から、BCC電子メールは、個人の身元を特定できる情報(PII)を安全に保存できるアーカイブシステムで処理する必要があります。

**config-`<instance name>.xml`** ファイルで、次のパラメーターを使用して、保存されたファイルの転送先となるSMTP電子メールサーバーを定義します。

```
<archiving smtpBccAddress="" smtpEnableTLS="false" smtpRelayAddress="" smtpRelayPort="25"/>
```

* **smtpBccAddress**:アーカイブターゲット先
* **smtpEnableTLS**:保護されたSMTP接続（TLS/SSLプロトコル）の使用
* **smtpRelayAddress**:使用するリレーアドレス
* **smtpRelayPort**:使用するリレーポート

>[!NOTE]
>
>SMTPリレーを使用している場合、リレーによる電子メールへの変更はアーカイブ処理では考慮されません。
>
>また、リレーは、送信されていない電子メールも含め、すべての電子メールに **[!UICONTROL 送信済み]** ステータスを割り当てます。 したがって、すべてのメッセージはアーカイブされます。

<!--
## Moving to the new Email BCC {#updated-email-archiving-system--bcc-}

[!BADGE On-premise & Hybrid]{type=Caution url="https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/architecture-and-hosting-models/hosting-models-lp/hosting-models.html?lang=ja" tooltip="Applies to on-premise and hybrid deployments only"}

>[!IMPORTANT]
>
>The email archiving system (BCC) changed with Adobe Campaign 17.2 (build 8795). If you are upgrading from an older build and were already using email archiving capabilities, you must upgrade manually to the new email archiving system (BCC).

To do this, make the following changes to the **`config-<instance>.xml`** file:

1. Remove the **zipPath** parameter from the **`<archiving>`** node.
1. Set the **compressionFormat** parameter to **1** if needed.
1. Set the **archivingType** parameter to **1**.

Once email BCC is configured, make sure you select the **[!UICONTROL Email BCC]** option in the delivery template or the delivery. For more on this, see [this section](../../delivery/using/sending-messages.md#archiving-emails).
-->

## BCC で E メールを送信のベストプラクティス {#best-practices}

* **BCCアドレスメールボックス**:MTAから送信されるすべての電子メールをアーカイブするのに十分な受信容量があることを確認します。
* **MTA プーリング**:BCC アーカイブ機能は、MTA レベルで機能します。 MTAから送信されるすべての電子メールを重複できます。 MTA は、複数のインスタンス（開発、テスト、実稼動など）または複数のクライアント（ミッドソーシング環境の場合）にわたってプールできるので、この機能を設定するとセキュリティに影響します。

   * 複数のクライアントとMTAを共有し、そのうちの1つがこのオプションをアクティブにしている場合、このクライアントは同じMTAを共有する他のクライアントの電子メールにすべてアクセスします。 このような状況を回避するには、クライアントごとに異なるMTAを使用します。
   * 1つのクライアントに対して複数のインスタンス（開発、テスト、実稼動）で同じMTAを使用する場合、3つのインスタンスすべてから送信されるメッセージは、dataLogPathオプションで複製されます。

* **接続ごとの電子メール**:BCC電子メールのアーカイブは、接続を開き、その接続を介してすべてのメールを送信しようとすることで動作します。Adobeは、社内のテクニカルコンタクトに、特定の接続で受け入れられる電子メールの数を確認することを推奨します。 この数を増やすと、BCCのスループットに大きな影響を与える可能性があります。
* **BCC送信IP**:現在、BCC電子メールは、通常のMTAプロキシを通じて送信されません。 代わりに、MTAサーバーから宛先の電子メールサーバーへの直接接続が開かれます。 つまり、メールサーバーの設定によっては、ネットワーク上の許可リストに IP を追加する必要がある場合があります。

<!--## Email BCC with Enhanced MTA {#email-bcc-with-enhanced-mta}

For **hosted and hybrid architectures**, if you have the latest instance of Adobe Campaign, or if you have upgraded to the Enhanced MTA and using Adobe Campaign 19.2 or later, you can use Email BCC with Enhanced MTA, which is more reliable, efficient, and has lower latency.

### Activating Email BCC with Enhanced MTA

To activate this feature, you must contact your account executive to communicate the BCC email address to be used for archiving.

>[!NOTE]
>
>If you were already using BCC email archiving, you can provide the same address as you were using before or use a new one. If you keep the same, you still have to contact your account executive to set it up for you.

### Specificities and recommendations

Email BCC with Enhanced MTA is not activated at the delivery level: once this feature is enabled, **all sent deliveries** are sent to the BCC email address. There is no need to select the **[!UICONTROL Email BCC]** option in the delivery template or in the delivery.

If you were already using BCC and if you keep the same address, you could see a significant increase in the volumes sent to the BCC address.

Consequently, make sure:
* The BCC address has enough reception capacity to archive all the emails that are sent.
* You have the required MTA infrastructure capacity to receive 100% of your email volume delivered to a single address.

### Limitations

* Email BCC with Enhanced MTA delivers to the BCC email address before delivering to the recipients, which can result in BCC messages being sent even though the original deliveries may have bounced. For more on bounces, see [Understanding delivery failures](../../delivery/using/understanding-delivery-failures.md).

* There is no reporting available on the delivery status of the emails sent to the BCC email address.-->