---
product: campaign
title: SFTP サーバーの使用
description: SFTP サーバーのベストプラクティスとトラブルシューティングの詳細を説明します
badge-v7: label="v7" type="Informative" tooltip="Applies to Campaign Classic v7"
badge-v8: label="v8" type="Positive" tooltip="Also applies to Campaign v8"
audience: platform
content-type: reference
topic-tags: importing-and-exporting-data
exl-id: d585a5d4-ea33-43c8-aa37-4d892025374a
source-git-commit: 4661688a22bd1a82eaf9c72a739b5a5ecee168b1
workflow-type: ht
source-wordcount: '1159'
ht-degree: 100%

---

# SFTP サーバーのベストプラクティスとトラブルシューティング {#sftp-server-usage}



## SFTP サーバーのグローバルな推奨事項 {#global-recommendations}

ETL のためのファイルやデータを管理する際、これらのファイルはアドビがホストする SFTP サーバー上に保存されます。SFTP サーバーを使用する場合は、次の推奨事項に従ってください。

* パスワードが期限切れになるのを避けるために、パスワード認証ではなく、キーベースの認証を使用します（パスワードの有効期間は 90 日間です）。さらに、キーベースの認証では、複数のエンティティを管理する場合などに、複数のキーを生成できます。一方、パスワード認証では、管理しているすべてのエンティティとパスワードを共有する必要があります。

   サポートされているキーの形式は、SSH-2 RSA 2048 です。キーは、PyTTY（Windows）や ssh-keygen（Unix）などのツールを使用して生成できます。[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)を通じてアドビサポートチームに公開鍵を提供して Campaign サーバーにアップロードしてもらう必要があります。

* SFTP アップロードやワークフローでバッチ処理を使用します。

* エラー／例外を処理します。

* デフォルトでは、作成したすべてのフォルダーは自分の識別子に対してのみ読み取り／書き込みモードになります。Campaign からアクセスする必要のあるフォルダーを作成する場合は、グループ全体に対して読み取り／書き込み権限を付与するように必ず設定します。そうしないと、同じグループ内の別の識別子でワークフローが実行された場合に、セキュリティ上の理由により、ファイルを作成または削除できないことがあります。

* SFTP 接続を開始しようとしているパブリック IP は、Campaign インスタンスの許可リストに登録されている必要があります。許可リストへの IP アドレスの追加は、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)を通じて依頼できます。

## データベース使用のベストプラクティス {#sftp-server-best-practices}

SFTP サーバーは、ファイルの保持や削除を制御できる一時的なストレージスペースとなるように設計されています。

この領域の使用または監視が適切におこなわれないと、サーバー上の使用可能な物理領域がすぐにいっぱいになって、その後のアップロードでファイルが切り捨てられる可能性があります。スペースがいっぱいになると、自動パージがトリガーされ、SFTP ストレージから一番古いファイルが消去されることがあります。

こうした問題を回避するために、アドビでは以下のベストプラクティスに従うことをお勧めします。

>[!NOTE]
>
>インスタンスが AWS でホストされている場合、Campaign Classic [コントロールパネル](https://experienceleague.adobe.com/docs/control-panel/using/sftp-management/sftp-storage-management.html?lang=ja)で SFTP サーバーストレージを監視できます。インスタンスが AWS でホストされているかどうかを確認するには、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/faq.html?lang=ja)に記載されている手順に従います。
>
>コントロールパネルは、すべての管理者ユーザーがアクセスできます。 ユーザーに管理者アクセス権を付与する手順については、[このページ](https://experienceleague.adobe.com/docs/control-panel/using/discover-control-panel/managing-permissions.html?lang=ja#discover-control-panel)で詳しく説明しています。
>
>インスタンスは、[最新の GA ビルド](../../rn/using/rn-overview.md)でアップグレードされている必要があります。バージョンを確認する方法については、[この節](../../platform/using/launching-adobe-campaign.md#getting-your-campaign-version)を参照してください。

* サーバーのサイズ機能は、ライセンスによって異なります。いずれの場合でも、最小限のデータを保持し、必要な期間だけデータを保持します（最長で 15 日）。

* データを適切に削除するには、ワークフローを使用します（データを消費しているワークフローから保持を管理）。

* 時々 SFTP にログインして、問題がないか直接確認します。

* SFTP のディスク管理は、基本的に管理者の責任となります。

## 外部 SFTP サーバーの使用 {#external-SFTP-server}

独自の SFTP サーバーを使用する場合は、できるだけ上記の推奨事項に従ってください。

また、Campaign Classic で外部 SFTP サーバーへのパスを指定する場合、パスの構文は SFTP サーバーのオペレーティングシステムによって異なります。

* SFTP サーバーが **Windows** 上にある場合は、常に相対パスを使用します。
* STP サーバーが **Linux** 上にある場合は、ホームからの相対パス（「～/」で始まるパス）か絶対パス（「/」で始まるパス）を常に使用します。

## アドビがホストする SFTP サーバーとの接続に関する問題 {#sftp-server-troubleshooting}

アドビがホストする SFTP サーバーとの接続で問題が発生した場合は、以下を確認し、[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)を通じてその情報をアドビサポートチームに提供します。

1. インスタンスが実行中であることを確認します。そのためには、ブラウザーを開き、インスタンスの **[!UICONTROL /r/test]** エンドポイントに対して **[!UICONTROL GET]** 呼び出しをおこないます。

   ```
   https://instanceUrl/r/test
   ```

   インスタンスが実行中である場合は、次のタイプの応答が返されます。

   ```
   <redir status='OK' date='YYYY-MM-DD HH:MM:SS' build='XXXX' instance='instance-name'
   sourceIP='AAA.BB.CCC.DD' host='instanceUrl' localHost='instance-name'/>
   ```

   いずれの場合も、サポートチケットでコマンドの応答を提供してください。

1. SFTP 接続を開始しようとしているサイトでアウトバウンドポート 22 が開いているかどうかを確認します。それには、次のコマンドを使用します。

   ```
   bash-3.2$ nc -vz <SFTP_URL> 22
   # Replace the SFTP_URL with actual SFTP instance URL
   # If the port 22 is opened you will see output similar to the below one
   # for e.g. the  output for the command on myCompany-stage-sftp.neolane.net after ssh-out, will give
   bash-3.2$ nc -vz myCompagny-stage-sftp.neolane.net 22
   myCompany-stage-sftp.neolane.net [AAA.BBB.CCC.D] 22 (ssh) open
   ```

   >[!NOTE]
   >
   >Netcat ツールを使用すると、様々なオペレーティングシステムでネットワーク接続を簡単に管理できます（[https://eternallybored.org/misc/netcat/](https://eternallybored.org/misc/netcat/) を参照）。

   ポートが開いていない場合は、接続元でアウトバウンド接続を開いてから、もう一度やり直してください。接続の問題が解消されない場合は、コマンドの出力を添えて[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)チームに連絡してください。

1. SFTP 接続を開始しようとしているパブリック IP が、許可リストへの登録のためにアドビサポートに提供した IP であることを確認します。
1. パスワードベースの認証を使用している場合は、パスワードの有効期限が切れている可能性があります（パスワードの有効期間は 90 日間です）。そのため、キーベースの認証を使用することを強くお勧めします（[SFTP サーバーのベストプラクティス](#sftp-server-best-practices)を参照）。
1. キーベースの認証を使用している場合は、使用しているキーとインスタンス設定用に[アドビカスタマーケア](https://helpx.adobe.com/jp/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html)チームに提供したキーが同じであることを確認します。
1. FileZilla または同等の FTP ツールを使用している場合は、サポートチケットで接続ログの詳細を提供してください。

## 「ホスト名を解決できませんでした」エラー

この節では、Campaign Classic から FTP サーバーに接続した後に「ホスト名を解決できませんでした」というエラーが発生した場合に実行する確認および操作について説明します。

ワークフロージャーナルには、次のログが表示されます。

```
16/05/2016 12:49:03    fileTransfer    Upload error in cURL
16/05/2016 12:49:03    fileTransfer    Couldn't resolve host name
16/05/2016 12:49:03    fileTransfer    Couldn't resolve host name
16/05/2016 12:49:03    fileTransfer    Starting transfer of '/usr/local/neolane/nl6/var/williamreed/export/Recipients' to 'ftp://213.253.61.250/Recipients'
16/05/2016 12:49:03    fileTransfer    1 file(s) to transfer
```

このエラーは、FileZilla または WinSCP を使用して FTP 経由で接続できる状態で、ワークフローから FTP サーバーに接続してサーバーからファイルをダウンロードしようとすると発生します。

このエラーは、FTP サーバーのドメイン名が正しく解決されなかったことを示します。トラブルシューティングには、次の手順を実行します。

1. **DNS サーバー設定**&#x200B;のトラブルシューティング

   1. サーバー名がローカル DNS サーバーに追加されているかどうかを確認します。
   1. 追加されている場合、Adobe Campaign サーバーで次のコマンドを実行して IP アドレスを取得します。

      `nslookup <server domain name>`

      これにより、FTP サーバーが動作しており、Adobe Campaign アプリケーションサーバーから到達可能であることが確認されます。

1. **セッションログ**&#x200B;のトラブルシューティング

   1. ワークフローで、「[ファイル転送](../../workflow/using/file-transfer.md)」アクティビティをダブルクリックします。
   1. 「**[!UICONTROL ファイル転送]**」タブに移動し、「**[!UICONTROL 詳細設定パラメーター]**」をクリックします。
   1. 「**[!UICONTROL セッションログを表示]**」オプションをオンにします。

      ![](assets/sftp-error-display-logs.png)

   1. 「監査」ワークフローに移動し、ログに「ホスト名を解決できませんでした」というエラーが表示されるかどうかを確認します。

1. SFTP サーバーがアドビでホストされている場合は、カスタマーケアに問い合わせて、IP が許可リストに追加されているかどうかを確認します。

   それ以外の場合は、次を確認します。

   * パスワードに「@」が含まれていない。パスワードに「@」が含まれている場合、接続に失敗します。
   * Adobe Campaign アプリケーションサーバーと SFTP サーバー間の通信を妨げる可能性のあるファイアウォールの問題がない。
   * キャンペーンサーバーから SFTP に対して tracert および telnet コマンドを実行し、接続に問題があるかどうかを確認します。
   * 通信プロトコルの問題がない。
   * ポートが開いている。
