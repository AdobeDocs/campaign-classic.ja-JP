---
product: campaign
title: TLS 1.0 および 1.1 のサポートの提供終了（EOL）
description: TLS 1.0 および 1.1 のサポートの提供終了（EOL）
feature: Technote
audience: delivery
content-type: reference
topic-tags: tracking-messages
hide: true
hidefromtoc: true
exl-id: e18d43b6-2a77-4881-85e7-ca36248d4634
source-git-commit: 19b40f0b827c4b5b7b6484fe4953aebe61d00d1d
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 100%

---

# TLS 1.0 および 1.1 のサポートの提供終了（EOL）{#eol-tls-support}



アドビでは、Transport Layer Security（TLS）1.2 プロトコルに準拠していないユーザーシステムとクライアントシステムをサポートしなくなりました。古いバージョンの TLS を引き続き使用すると、すべてのアドビ製品およびサービスにアクセスできなくなる可能性があります。

## このページが表示される理由

「**このページを表示できません**」というメッセージが表示された場合は、アクセスしようとしているアドビアプリ、web ページまたはサービスに、web ブラウザー、オペレーティングシステムまたはアプリとのより安全なネットワーク接続が必要であることを意味しています。ユーザーシステムとアドビアプリおよび web サービスの間の安全なネットワーク通信およびデータ交換には、**TLS 1.2** を使用する必要があります。

アドビでは、TLS の下位バージョン（TLS 1.0 および 1.1 を含む）のサポートを廃止しました。TLS 1.2 プロトコルに関する技術的な詳細については、 [よくある質問](#faq)を参照してください。

## サービスを再開するためにできること

最新の web ブラウザーでは TLS 1.2 をサポートしています。ブラウザーをアップグレードすると、これらのアプリやサービスにアクセスできるようになります。

次の一般的なブラウザーのいずれかをダウンロードしてインストールします。

* [Google Chrome](https://www.google.com/chrome/)
* [Apple Safari](https://www.apple.com/safari/)
* [Firefox](https://www.mozilla.org/ja-JP/firefox/new/)
* [Microsoft Edge](https://www.microsoft.com/ja-jp/edge)

別のブラウザーを使用している場合は、TLS 1.2 がサポートされていることを確認します。

オペレーティングシステムとアプリケーションフレームワークでも TLS 1.2 がサポートされている必要があります。ブラウザーをアップグレードしても問題が解決しない場合は、コンピューターが [Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)に記載されている必要システム構成を満たしていることを確認します。

## よくある質問{#faq}

* **Transport Layer Security（TLS）とは何ですか？**

  [Transport Layer Security](https://ja.wikipedia.org/wiki/Transport_Layer_Security)（TLS）は、通信する 2 つのアプリケーション間でプライバシーとデータの整合性を確保するセキュリティプロトコルです。ネットワークを通じてデータを安全に交換する必要がある web ブラウザーやその他のアプリケーションに広くデプロイされています。

  プロトコル仕様に従い、TLS には、TLS レコードプロトコルと TLS ハンドシェイクプロトコルの 2 つのレイヤーが含まれています。レコードプロトコルは、接続のセキュリティを提供します。ハンドシェイクプロトコルを使用すると、サーバーとクライアントは互いを認証し、データ交換の前に暗号化アルゴリズムと暗号化キーをネゴシエートできます。

* **どのような影響がありますか？**

  アドビのセキュリティコンプライアンス標準では、2018年5月をもって古いプロトコルを廃止し、最新バージョンとして TLS 1.2 を使用することが義務付けられています。システムが TLS 1.2 に準拠していない場合、一部のアドビアプリおよびサービスへのアクセスが制限されます。

* **TLS はどのような影響を与えますか？**

  安全なネットワーク接続を通じてのみ、一部のアドビアプリおよびサービスを利用できます。TLS は、ブラウザーとこれらのアプリおよび web サービスとの接続が安全で信頼できることを保証するのに役立ちます。

  新しいブラウザーとオペレーティングシステムがリリースされると、セキュリティ標準がアップグレードされ、より高いレベルのプライバシーとデータ整合性が保証されます。ただし、これらのブラウザーや OS の古いバージョンは、最新の標準に対応するように更新されていません。

  許容可能なセキュリティレベルが上がると、これらの古い、安全性の低いブラウザーバージョンやアプリケーションは取り残されます。

  安全なサイトに接続できるようにするには、OS とブラウザーのバージョンを更新します。

* **TLS はハッカーに対して脆弱ですか？**

  古い暗号化方式を使用した TLS 1.0 に対する攻撃が文書化されており、古いバージョンは TLS 1.2 よりも脆弱です。詳しくは、「TLS/SSL の既知の脆弱性」を参照してください。

* **アドビが TLS 1.0 および 1.1 のサポートを無効にしているのはなぜですか？**

  アドビには、古いプロトコルのサポートを無効にすることを義務付けているセキュリティコンプライアンス標準があります。そのような標準の 1 つが、PCI（ペイメントカード業界）へのコンプライアンスを保証します。PCI 適応サーバーは、安全な環境を維持するために、クレジットカード情報の受け付け、処理、保存または送信を行う組織の設置を求める一連のセキュリティ標準です。

  PCI コンプライアンスでは、2018年5月をもって TLS 1.1 以降の使用が義務付けられています。

* **アドビが TLS 1.1 または TLS 1.0 の使用を許可するのではなく、TLS 1.2 の使用を義務付けているのはなぜですか？**

  アドビのアプリと web サービスに対するほとんどのリクエストは、TLS 1.2 準拠のユーザーシステムから発信され、TLS 1.1 システムからのトラフィックは少なくなっています。

  アドビは TLS 1.2 に移行したので、アドビのアプリや web サービスには、より安全にアクセスできるようになりました。

* **旧バージョンの TLS を使用できるのはいつまでですか？**

  アドビでは、セキュリティの脆弱性にさらされることを避けるために、旧バージョンの使用を速やかに中止することをお勧めします。詳しくは、アドビカスタマーケアまたはカスタマーサクセスマネージャーにお問い合わせください。

* **TLS 1.2 に対応するように設定されていないブラウザーを使用すると、どのようなエラーメッセージが表示されますか？**

  使用しているブラウザーによって異なります。[Campaign 互換性マトリックス](../../rn/using/compatibility-matrix.md)に記載されているすべてのブラウザーは、TLS 1.2 を使用するように設定されています。リストに記載されていないブラウザーまたはバージョンを使用している場合は、ブラウザーを更新します。

  アドビでは、SSL 通信レイヤーによって生成されるエラーメッセージを制御しません。ブラウザーは、アドビのアプリやサービスに接続する前にこれらのメッセージを生成します。Windows 7 上の Internet Explorer 11 で発生する可能性のあるエラーの例を以下に示します。

  ![](assets/do-not-translate/page-not-displayed.png)

  TLS 1.2 は Internet Explorer 11 でデフォルトで有効になっていますが、無効になっている場合は、有効にすることができます。この場合、他の選択肢を使用する代わりに、詳細設定ダイアログで TLS 1.2 を有効にします。次のようなその他のエラーも発生する場合があります。

   * サービスに接続できません
   * サービスを利用できません
   * 接続中にエラーが発生しました
