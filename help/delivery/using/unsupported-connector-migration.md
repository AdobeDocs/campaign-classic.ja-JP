---
product: campaign
title: サポートされていない SMS コネクタの移行
description: サポートされていない SMS コネクタの拡張汎用 SMPP コネクタへの移行
feature: SMS, Upgrade
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
hidefromtoc: true
exl-id: 60acf80c-8506-410b-ab2c-4f67a5677b43
source-git-commit: 3a9b21d626b60754789c3f594ba798309f62a553
workflow-type: ht
source-wordcount: '643'
ht-degree: 100%

---

# サポートされていない SMS コネクタの、拡張された汎用 SMPP コネクタへの移行{#unsupported-connector-migration}



リリース 20.2 の時点で、従来のコネクタは非推奨（廃止予定）となっています。 このドキュメントは、古いシステムでまだ動作中のコネクタを推奨の SMPP コネクタに移行する際に役立ちます。

>[!CAUTION]
>
>この移行は必須ではありませんが、推奨されています。この移行により、サポートされている最新バージョンのソフトウェアでの実行が保証されます。

## SMS コネクタについて {#about-sms-connectors}

次のコネクタは、リリース 20.2 で非推奨となりました。

* **[!UICONTROL 一般的な SMPP]**（バイナリモードをサポートする SMPP バージョン 3.4）
* **[!UICONTROL Sybase365]** （SAP SMS 365）
* **[!UICONTROL CLX Communications]**
* **[!UICONTROL Tele2]**
* **[!UICONTROL O2]**
* **[!UICONTROL iOS]**

非推奨の機能は引き続き使用可能でサポートされますが、それ以上強化されることはありません。 **[!UICONTROL 拡張された汎用 SMPP]** コネクタの使用をお勧めします。

非推奨および削除された機能の詳細については、[こちらのページ](../../rn/using/deprecated-features.md)を参照してください。

古い SMS コネクタは、Web プロセスに過大な負荷をかける Java SMS コネクタを使用しています。 新しい&#x200B;**[!UICONTROL 拡張された汎用 SMPP]** コネクタに移行すると、この負荷をサポートできる MTA に負荷が移動します。

## 拡張された汎用 SMPP コネクタへの移行 {#migrating-extended-generic-smpp}

>[!CAUTION]
>
>パラメーターの移行が可能な場合でも、**[!UICONTROL 拡張された汎用 SMPP]** コネクタを設定するには、残りのパラメーターの入力に必要な情報を提供するプロバイダーとの連携が必要です。 詳しくは、[こちらのページ](sms-protocol.md)を参照してください。

まず、新しい「**[!UICONTROL 拡張された汎用 SMPP]**」外部アカウントを作成する必要があります。その後、場合によっては一部のパラメータを移行できます。 詳細な手順については、[こちらのページ](sms-set-up.md#creating-an-smpp-external-account)を参照してください。

新しく作成した「**[!UICONTROL 拡張された汎用 SMPP]**」外部アカウントの「**[!UICONTROL モバイル]**」タブから、以前のコネクタに応じてパラメーターを入力する必要があります。

### 汎用コネクタから {#from-generic-connector}

**[!UICONTROL 汎用]**&#x200B;コネクタを選択する場合は、それぞれの状況に適応するカスタム JavaScript コネクタが必要です。

このコネクタが既に SMPP プロトコルを使用していることがわかっている場合は、**[!UICONTROL 拡張された汎用 SMPP]** コネクタに移行できます。 そうでない場合は、プロバイダーに SMPP プロトコルをサポートしているかどうかを確認し、コンサルタントの助けを借りて新しいコネクタを設定します。

**[!UICONTROL 汎用]**&#x200B;コネクタから、新しく作成した「**[!UICONTROL 拡張された SMPP]**」アカウントに移行できます。

![](assets/smpp_generic.png)

「**[!UICONTROL 接続設定]**」タブで以下を設定します。

* **[!UICONTROL アカウント]**
* **[!UICONTROL パスワード]**
* **[!UICONTROL サーバー]**
* **[!UICONTROL ポート]**

### 汎用 SMPP コネクタから {#from-generic-smpp-connector}

**[!UICONTROL 汎用 SMPP]** コネクタから、新しく作成した「**[!UICONTROL 拡張された汎用 SMPP]**」アカウントに移行できます。

![](assets/smpp_generic_2.png)

「**[!UICONTROL 接続設定]**」タブで以下を設定します。

* **[!UICONTROL アカウント]**
* **[!UICONTROL パスワード]**
* **[!UICONTROL サーバー]**
* **[!UICONTROL ポート]**
* **[!UICONTROL システムタイプ]**

「**[!UICONTROL SMPP チャネル設定]**」タブで以下を設定します。 

* **[!UICONTROL ソース番号]**
* **[!UICONTROL ソース NPI]**
* **[!UICONTROL 宛先の NPI]**
* **[!UICONTROL ソース TON]**
* **[!UICONTROL 送信先 TON]**

「**[!UICONTROL エンコードのマッピング]**」タブで以下を設定します。 

* **[!UICONTROL アウントバウンド SMS のコーディング]**

「**[!UICONTROL SMSC 特異性]**」タブで以下を設定します。 

* **[!UICONTROL 送信時のコーディング]**&#x200B;は **[!UICONTROL MT 確認の ID フォーマット]**&#x200B;に対応
* **[!UICONTROL 受信時のコーディング]**&#x200B;は **[!UICONTROL SR の ID のフォーマット]**&#x200B;に対応

### Sybase365 コネクタから {#from-sybase}

**[!UICONTROL Sybase365]** コネクタから、新しく作成した「**[!UICONTROL 拡張された汎用 SMPP]**」アカウントに移行できます。

![](assets/smpp_3.png)

「**[!UICONTROL 接続設定]**」タブで以下を設定します。 

* **[!UICONTROL アカウント]**
* **[!UICONTROL パスワード]**
* **[!UICONTROL サーバー]**
* **[!UICONTROL ポート]**
* **[!UICONTROL システムタイプ]**

### CLX コネクタから {#from-clx}

**[!UICONTROL CLX]** コネクタから、新しく作成した「**[!UICONTROL 拡張された汎用 SMPP]**」アカウントに移行できます。

![](assets/smpp_4.png)

「**[!UICONTROL 接続設定]**」タブで以下を設定します。 

* **[!UICONTROL アカウント]**
* **[!UICONTROL パスワード]**
* **[!UICONTROL サーバー]**
* **[!UICONTROL ポート]**
* **[!UICONTROL システムタイプ]**

「**[!UICONTROL SMPP チャネル設定]**」タブで以下を設定します。 

* **[!UICONTROL ソース番号]**

「**[!UICONTROL SMSC 特異性]**」タブで以下を設定します。 

* **[!UICONTROL 送信時のコーディング]**&#x200B;は **[!UICONTROL MT 確認の ID フォーマット]**&#x200B;に対応
* **[!UICONTROL 受信時のコーディング]**&#x200B;は **[!UICONTROL SR の ID のフォーマット]**&#x200B;に対応

### Tele2 コネクタから {#from-tele2}

**[!UICONTROL Tele2]** コネクタから、新しく作成した「**[!UICONTROL 拡張された汎用 SMPP]**」アカウントに移行できます。

![](assets/smpp_6.png)

「**[!UICONTROL 接続設定]**」タブで以下を設定します。 

* **[!UICONTROL アカウント]**
* **[!UICONTROL パスワード]**
* **[!UICONTROL サーバー]**
* **[!UICONTROL ポート]**
* **[!UICONTROL システムタイプ]**

「**[!UICONTROL SMPP チャネル設定]**」タブで以下を設定します。 

* **[!UICONTROL ソース番号]**
* **[!UICONTROL ソース NPI]**
* **[!UICONTROL 宛先の NPI]**
* **[!UICONTROL ソース TON]**

「**[!UICONTROL エンコードのマッピング]**」タブで以下を設定します。 

* **[!UICONTROL アウントバウンド SMS のコーディング]**

### O2 コネクタから {#from-O2}

**[!UICONTROL O2]** コネクタから、新しく作成した「**[!UICONTROL 拡張された汎用 SMPP]**」アカウントに移行できます。

![](assets/smpp_5.png)

「**[!UICONTROL 接続設定]**」タブで以下を設定します。 

* **[!UICONTROL アカウント]**
* **[!UICONTROL パスワード]**
* **[!UICONTROL サーバー]**
* **[!UICONTROL ポート]**
* **[!UICONTROL システムタイプ]**

「**[!UICONTROL SMPP チャネル設定]**」タブで以下を設定します。 

* **[!UICONTROL ソース番号]**
* **[!UICONTROL ソース NPI]**
* **[!UICONTROL 宛先の NPI]**
* **[!UICONTROL ソース TON]**
* **[!UICONTROL 送信先 TON]**
