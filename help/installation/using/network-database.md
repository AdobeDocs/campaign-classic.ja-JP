---
product: campaign
title: ネットワーク、データベース、SSL/TLS
description: ネットワーク、データベース、SSL/TLS設定のベストプラクティスについて詳しく見る
feature: Installation, Instance Settings
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
exl-id: 2a66dfaa-7fff-48de-bdd4-62f3ebfbab19
source-git-commit: c262c27e75869ae2e4bd45642f5a22adec4a5f1e
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 41%

---

# ネットワーク、データベース、SSL/TLS {#network-database}

## ネットワーク設定

オンプレミスタイプのアーキテクチャをデプロイする際に確認すべき非常に重要なことは、[ ネットワーク設定](../../installation/using/network-configuration.md)です。 Tomcat サーバーがサーバーの外部から直接アクセスできないことを確認します。

* 外部 IP の Tomcat ポート（8080）を閉じます（localhost では動作する必要があります）。
* 標準 HTTP ポート（80）を Tomcat ポート（8080）にマッピングしないようにします。

可能な場合は、POP3SではなくPOP3 （またはTLS経由のPOP3）という安全なチャネルを使用してください。

## データベース

データベースエンジンセキュリティのベストプラクティスを適用する必要があります。

## SSL/TLS設定

証明書を確認するには、opensslを使用します。 アクティブな暗号をチェックするには、nmap を使用します。

```
#!/bin/sh
#
# usage: testSSL.sh remote.host.name [port]
#
REMHOST=$1
REMPORT=${2:-443}
 
echo |\
openssl s_client -connect ${REMHOST}:${REMPORT} -servername ${REMHOST} 2>&1 |\
sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' |\
openssl x509 -noout -subject -dates
   
nmap --script ssl-enum-ciphers -p ${REMPORT} ${REMHOST}
```

また、[sslyze](https://github.com/nabla-c0d3/sslyze/releases) Python スクリプトを使用すると、両方の処理ができます。

```
python sslyze.py --sslv2 --sslv3 --tlsv1 --reneg --resum --certinfo=basic --hide_rejected_ciphers --sni=SNI myserver.com
```
