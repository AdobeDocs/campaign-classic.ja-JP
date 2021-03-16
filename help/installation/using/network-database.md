---
solution: Campaign Classic
product: campaign
title: ネットワーク、データベース、SSL／TLS
description: ネットワーク、データベース、SSL/TLS設定のベストプラクティスの詳細を説明します。
audience: installation
content-type: reference
topic-tags: prerequisites-and-recommendations-
translation-type: tm+mt
source-git-commit: 63b2e6b95812f1649e636580984a1f0dcc9c5c53
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 54%

---


# ネットワーク、データベース、SSL／TLS {#network-database}

## ネットワーク設定

オンプレミスタイプのアーキテクチャを導入する際に確認する必要がある重要な点は、[ネットワーク設定](../../installation/using/network-configuration.md)です。 Tomcat サーバーに外部から直接アクセスできないことを確認します。

* 外部 IP の Tomcat ポート（8080）を閉じます（localhost では動作する必要があります）。
* 標準 HTTP ポート（80）を Tomcat ポート（8080）にマッピングしないようにします。

可能な場合は、次の安全なチャネルを使用します。POP3はPOP3（またはTLS上のPOP3）の代わりにPOP3Sを使用します。

## データベース

データベースエンジンのセキュリティに関するベストプラクティスを適用する必要があります。

## SSL/TLSの設定

証明書をチェックするには、OpenSSL を使用します。アクティブな暗号をチェックするには、nmap を使用します。

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
