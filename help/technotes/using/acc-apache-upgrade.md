---
product: campaign
title: テクニカルノート — Adobe Campaign - Apache バージョンのセキュリティアップデート
description: Adobe Campaign - Apache バージョンのセキュリティの更新
hide: true
hidefromtoc: true
source-git-commit: 41aa16e3ac6f150b9a048a22729b4cc4b9ccc10a
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 6%

---

# Adobe Campaign - Apache バージョンのセキュリティの更新 {#apache-update}

Campaign Classicはサードパーティのツールと連携し、サポート対象のバージョンのみを実装し、最新の修正および改善を活用するために、定期的に互換性が更新されています。

Adobe Campaignには、HTTP を介してアプリケーションサーバーのエントリポイントとして機能し、Apache Web サーバーと統合される Apache Tomcat が含まれています。 Apache Software Foundation は、Apache HTTP Server 2.4.53 をリリースしました。このバージョンは、リモート攻撃者が影響を受けるシステムを制御できる可能性のある脆弱性に対処します。 詳しくは、 [Apache 2.4.53 のリリース](https://downloads.apache.org/httpd/Announcement2.4.html){target=&quot;_blank&quot;}。

Adobe Campaignチームは、次の手順で Apache バージョンセキュリティアップグレードアクティビティを実行します。 **2022 年 5 月 31 日** この Apache の脆弱性を軽減し、インスタンス環境のセキュリティを高めるため。 このアップグレードは、脆弱なバージョンの Apache HTTP Server で動作するすべてのManaged Servicesのお客様に適用されます。 影響を受けた場合、Adobeは既に連絡を受けて、このアップグレードに関する通知を受け取ります。

このアップグレードは、通常の営業時間外に自動的に実行され、中断することなく Campaign サービスを引き続き使用できるようになります。

実稼動以外のインスタンスは、アドビが実稼動インスタンスをアップグレードする前に、アドビのチームが最初にアップグレードします。 これはAdobeが所有する自動アップグレードプロセスなので、お客様側から必要なアクションはありません。 ただし、問題が発生した場合は、 [Adobeカスタマーケア](https://experienceleague.adobe.com/?support-solution=Campaign#support).


>[!NOTE]
>このアップグレードを行うには、Apache Web サーバーを再起動する必要があります。 ダウンタイムは、以下に示す時間枠内で 10 分を超えることはありません。

## よくある質問 {#apache-faq}

* **これが必須のアップグレードなのはなぜですか？**

   現在の Apache バージョンは脆弱で、セキュリティ上の脅威が発生する可能性があります。 セキュリティ上のリスクに対処するために、Campaign インスタンスを適用可能な最新の Apache バージョンにアップグレードすることが重要です。


* **セキュリティのアップグレードを対象としているのは、どのお客様ですか？**

   古い Apache バージョンで実装された Campaign 環境を使用しているすべてのお客様は、適用可能な最新の Apache バージョンにアップグレードされます。

* **予想されるダウンタイムはどれくらいですか？**

   予想されるダウンタイムは 10 分未満です。


* **このセキュリティアップグレードに関して、お客様に必要なアクションはありますか？**

   セキュリティアップグレードは自動的に実行されるので、アクションは必要ありません。


* **顧客が実行する必要がある検証は何ですか？**

   このセキュリティアップグレードでは、特定のテストは必要ありません。 問題が見つかった場合は、 [Adobeカスタマーケア](https://experienceleague.adobe.com/?support-solution=Campaign#support)


* **スケジュールされたセキュリティアップグレードスロットに対する日時の変更をリクエストできますか？**

   これはセキュリティの修正なので、既存のスケジュールに適応することを強くお勧めします。


その他の質問については、[アドビカスタマーケア](https://experienceleague.adobe.com/?support-solution=Campaign#support)にお問い合わせください。
