---
title: E メールのアーカイブ
seo-title: E メールのアーカイブ
description: E メールのアーカイブ
seo-description: null
page-status-flag: never-activated
uuid: a5ed0659-be61-4d73-98e7-db3da24d92f3
contentOwner: sauviat
products: SG_CAMPAIGN/CLASSIC
audience: installation
content-type: reference
topic-tags: additional-configurations
discoiquuid: d6467875-949b-4b47-940f-620efd4db5e0
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 5b9c57b3cba0e8c24300396c2abac613f6e1193a

---


# E メールのアーカイブ{#email-archiving}

プラットフォームから送信された電子メールのコピーを保持するようにAdobe Campaignを設定できます。

ただし、Adobe Campaign自体はアーカイブされたファイルを管理しません。 これにより、選択したメッセージを専用のアドレスに送信し、外部システムを使用して処理およびアーカイブできます。

これを行うには、送信された電子メールに対応する.emlファイルを、SMTP電子メールサーバなどのリモートサーバに転送します。 アーカイブ先は、指定する必要があるBCC電子メールアドレス（配信の受信者には見えません）です。

## 推奨事項と制限事項 {#recommendations-and-limitations}

* 電子メールアーカイブ機能はオプションです。 使用許諾契約書を確認してください。
* ホストア **ーキテクチャとハイブリッドアーキテクチャの場合**、アカウント担当者に問い合わせてアクティブ化してください。 選択したBCCアドレスは、アドビのチームに提供され、アドビがお客様に合わせて設定する必要があります。
* オンプレ **ミスでのインストールの場合**、以下のガイドラインに従ってアクティブ化します。 [Activating email archiving (on premise)と](#activating-email-archiving--on-premise-) Configuring the BCC email address (on premise)の節を参照してください [](#configuring-the-bcc-email-address--on-premise-) 。
* BCC電子メールアドレスは1つだけ使用できます。
* 電子メールBCCを設定したら、配信テンプレートまたは配信で、この機能が有効になっていることを確認します（オプションを使用） **[!UICONTROL Archive emails]** 。 For more on this, see [this section](../../delivery/using/sending-messages.md#archiving-emails).
* 正常に送信された電子メールのみが考慮され、バウンスは考慮されません。
* 電子メールアーカイブシステムは、Adobe Campaign 17.2（ビルド8795）で変更されました。 既に電子メールのアーカイブを使用している場合は、新しい電子メールアーカイブシステム(BCC)に手動でアップグレードする必要があります。 詳しくは、「BCC (Updated email archiving system) [」の節を参照してください](#updated-email-archiving-system--bcc-) 。

## メール・アーカイブのアクティブ化（オンプレミス） {#activating-email-archiving--on-premise-}

Adobe Campaignがオンプレミスでインストールされている場合にBCC電子メールアーカイブをアクティブにするには、次の手順に従います。

### ローカルフォルダ {#local-folder}

BCC電子メールアドレスに送信済みの電子メールを転送できるようにするには、送信済みの電子メールの正確な生コピーを.emlファイルとしてローカルフォルダに保存する必要があります。

ローカルフォルダーのパスは、設定の **config-`<instance>`.xmlファイルで指定する必要があります** 。 次に例を示します。

```
<mta dataLogPath="C:\emails">
```

>[!NOTE]
>
>セキュリティ設定で **dataLogPathパラメーターを使用して定義されたフォルダーへのアクセスが許可されていることを確認するのは、プロジェクトを導入するチームの責任** です。

フルパスは次のとおりです。 **`<datalogpath>  YYYY-MM-DDHHh`**. 日時はMTAサーバーの時計(UTC)に従って設定されます。 次に例を示します。

```
C:\emails\2018-12-02\13h
```

アーカイブファイル名は、電 **`<deliveryid>-<broadlogid>.eml`** 子メールのステータスが異なる場合に表示されま **[!UICONTROL Sent]**&#x200B;す。 ステータスがに変更され **[!UICONTROL Sent]**&#x200B;ると、ファイル名がになりま **`<deliveryid>-<broadlogid>-sent.eml`**&#x200B;す。 次に例を示します。

```
C:\emails\2018-12-02\13h\4012-8040-sent.eml
```

>[!NOTE]
>
>ミッドソーシングインスタンスでは、アーカイブ済み電子メールのディレクトリはミッドソーシングサーバー上にあります。
>
>deliveryIDとbroadlogIDは、電子メールのステータスが送信されない場合に、ミッドソーシングサーバーから送信されます。 ステータスがに変更され **[!UICONTROL Sent]**&#x200B;ると、これらのIDはマーケティングサーバーから取得されます。

### パラメーター {#parameters}

ローカルフォルダーパスを定義したら、 **config-fileで必要に応じて次の要素を追加し、編集し`<instance name>.xml`**ます。 デフォルト値は次のとおりです。

```
<archiving autoStart="false" compressionFormat="0" compressBatchSize="10000"
           archivingType="0" expirationDelay="2" purgeArchivesDelay="7"
           pollDelay="600" acquireLimit="5000" smtpNbConnection="2"/>
```

* **compressionFormat**:.emlファイルを圧縮する際に使用する形式。 使用可能な値は次のとおりです。

   **0**:no compression（デフォルト値）

   **1**:圧縮（.zip形式）

* **compressBatchSize**:アーカイブ（.zipファイル）に追加された.emlファイルの数。
* **archivingType**:アーカイブ戦略を使用します。 使用可能な値は次のとおりです。

   **0**:送信された電子メールの生のコピーは.eml形式でdataLogPath **** （デフォルト値）に保存されます。 ファイルのアーカイブコピ **`<deliveryid>-<broadlogid>-sent.eml`** ーがdataLogPath/archivesフォルダー **に保存されます** 。 送信された電子メールのファイルパスがになりま **`<datalogpath>archivesYYYY-MM-DDHHh <deliveryid>-<broadlogid>-sent.eml`**&#x200B;す。

   **1**:送信された電子メールの生のコピーは.eml形式で **dataLogPath** フォルダーに保存され、SMTP経由でBCC電子メールアドレスに送信されます。 電子メールのコピーがBCCアドレスに送信されると、アーカイブファイル名がにな **`<deliveryid>-<broadlogid>-sent-archived.eml`** り、そのファイルが **dataLogPath/archivesフォルダーに移動されます** 。 次に、送信済みおよびBCCアーカイブ済みの電子メールファイルのパスを示しま **`<datalogpath>archivesYYYY-MM-DDHHh<deliveryid>- <broadlogid>-sent-archived.eml`**&#x200B;す。

* **expirationDelay**:アーカイブ用に保存される.emlファイルの日数。 その後、圧縮用にdataLogPath/archivesフォルダーに自 **動的に移動されます** 。 デフォルトでは、.emlファイルは2日後に有効期限が切れます。
* **purgeArchivesDelay**:datalogpath/folderにアーカイブが保存され **る日数`<archives>`**。 その期間が過ぎると、それらは完全に削除されます。 削除は、MTAが開始されると開始されます。 デフォルトでは、7日ごとに実行されます。
* **pollDelay**:datalogpathフォルダーに新しく送信される電子メールの受信頻度（秒） **を確認します** 。 例えば、このパラメーターを60に設定した場合、アーカイブ処理は **`<date and time>`**dataLogPath/フォルダー内の.emlファイルを毎分処理し、必要に応じて削除を適用し、BCCアドレスに電子メールコピーを送信し、アーカイブ済みファイルを圧縮します。
* **acquireLimit**:polldelayパラメーターに従ってアーカイブ処理が再適用される前に一度に処理された.emlファ **イルの** 数。 例えば、pollDelayパラメーターが60に設定されている間に **acquireLimit****** パラメーターを100に設定した場合、1分あたり100個の.emlファイルが処理されます。
* **smtpNbConnection**:bcc電子メールアドレスへのSMTP接続の数。

電子メール送信のスループットに従って、これらのパラメーターを必ず調整してください。 例えば、MTAが1時間に30,000通の電子メールを送信する設定では、 **pollDelay** パラメーターを600に設定し、 **acquireLimit** パラメーターを5000に設定し、 **smtpNbConnectionパラメーターを2に設定できます** 。 つまり、2つのSMTP接続を使用して、10分ごとに5,000通の電子メールがBCCアドレスに送信されます。

## BCC電子メールアドレスの設定（オンプレミス） {#configuring-the-bcc-email-address--on-premise-}

>[!CAUTION]
>
>プライバシー上の理由から、BCC電子メールは、個人を特定できる情報(PII)を安全に保存できるアーカイブ・システムで処理する必要があります。

config — ファ **イルで、`<instance name>.xml`**次のパラメーターを使用して、保存されたファイルの転送先となるSMTP電子メールサーバーを定義します。

```
<archiving smtpBccAddress="" smtpEnableTLS="false" smtpRelayAddress="" smtpRelayPort="25"/>
```

* **smtpBccAddress**:アーカイブ先
* **smtpEnableTLS**:保護されたSMTP接続（TLS/SSLプロトコル）の使用
* **smtpRelayAddress**:使用するリレーアドレス
* **smtpRelayPort**:使用する中継ポート

>[!NOTE]
>
>SMTPリレーを使用している場合、リレーによって行われた電子メールに対する変更はアーカイブ処理では考慮されません。
>
>また、リレーは、未送信の **[!UICONTROL Sent]** 電子メールを含むすべての電子メールにステータスを割り当てます。 したがって、すべてのメッセージはアーカイブされます。

## BCC（メール・アーカイブ・システム）の更新 {#updated-email-archiving-system--bcc-}

>[!CAUTION]
>
>電子メールアーカイブシステム(BCC)は、Adobe Campaign 17.2（ビルド8795）で変更されました。 古いビルドからアップグレードする場合で、既に電子メールアーカイブ機能を使用していた場合は、新しい電子メールアーカイブシステム(BCC)に手動でアップグレードする必要があります。

これを行うには、ファイルに次の変更を加え **`config-<instance>.xml`** ます。

1. ノードから **zipPath** パラメーターを削除 **`<archiving>`** します。
1. 必要に応じて、 **compressionFormatパラメー** ターを **** 1に設定します。
1. archivingTypeパラメ **ーターを** 1に設 **定します**。

電子メールBCCを設定したら、配信テンプレートまたは配信 **[!UICONTROL Archive emails]** でオプションを選択していることを確認します。 For more on this, see [this section](../../delivery/using/sending-messages.md#archiving-emails).

## ベストプラクティス{#best-practices}

* **BCCアドレスメールボックス**:mtaから送信されるすべての電子メールをアーカイブするのに十分な受信容量があることを確認します。
* **MTAの相互化**:bccアーカイブ機能は、MTAレベルで機能します。 MTAから送信されるすべての電子メールを複製できます。 MTAは、複数のインスタンス（開発、テスト、実稼動など）または複数のクライアント（ミッドソーシング環境）にまたがって相互化できるので、この機能を設定するとセキュリティに影響します。

   * MTAを複数のクライアントと共有し、そのうちの1つでこのオプションがアクティブになっている場合、このクライアントは同じMTAを共有する他のクライアントの電子メールにすべてアクセスします。 このような状況を避けるには、クライアントごとに異なるMTAを使用します。
   * 1つのクライアントに対して複数のインスタンス（開発、テスト、実稼動）で同じMTAを使用する場合、3つのインスタンスすべてから送信されたメッセージは、dataLogPathオプションで複製されます。

* **接続ごとの電子メール**:BCC電子メールのアーカイブは、接続を開き、その接続を通じてすべての電子メールを送信しようとすることで動作します。 アドビでは、社内の技術担当者に対し、特定の接続で受け入れられる電子メールの数を確認することをお勧めします。 この数を増やすと、BCCのスループットに大きな影響を与える可能性があります。
* **BCC送信IP**:現在、BCC電子メールは通常のMTAプロキシを通じて送信されません。 代わりに、MTAサーバーから宛先の電子メールサーバーへの直接接続が開かれます。 つまり、電子メールサーバーの設定に応じて、ネットワーク上の追加のIPをホワイトリストに登録する必要が生じる場合があります。

