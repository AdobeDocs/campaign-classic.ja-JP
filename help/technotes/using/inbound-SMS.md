---
product: campaign
title: ミッドソーシングインフラストラクチャに対するインバウンド SMS ワークフローアクティビティ
description: ミッドソーシングインフラストラクチャに対するインバウンド SMS ワークフローアクティビティ
feature: Technote, SMS
badge-v7-only: label="v7" type="Informative" tooltip="Campaign Classic v7 にのみ適用されます"
source-git-commit: de57e7aec255ab2995d1a758642e6a73cafa91b3
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 2%

---

# ミッドソーシングインフラストラクチャに対するインバウンド SMS ワークフローアクティビティ {#inbound-sms}

## 制限事項 {#limitations}

* この使用例は、ミッドソーシングインスタンスから inSMS データを収集するマーケティングインスタンスにのみ当てはまります。
* ミッドソーシングインスタンスにこの使用例を実装しないでください。
* 外部ミッドソーシングアカウントあたり 1 つのカスタムワークフローのみ。

## 実装 {#implementation}

1. 拡張機能を `nms:inSMS` スキーマをマーケティングインスタンス上に配置する必要があります。 拡張機能により、新しい属性が `nms:inSMS` スキーマを作成し、ミッドソーシングインスタンスからの inSMS レコードのプライマリキーを追跡します。

   ```
   <element img="nms:miniatures/mini-sms.png" label="Incoming SMS"
          labelSingular="Incoming SMS" name="inSMS">
   <dbindex name="midInSMSId" unique="false">
     <keyfield xpath="@extAccount-id"/>
     <keyfield xpath="@midInSMSId"/>
   </dbindex>
   
   <attribute label="External Mid SMS ID" name="midInSMSId" type="long"/>
   </element>
   ```

1. スキーマに加えた変更を適用するには、データベース更新ウィザードを起動します。 このウィザードには、 **ツール** > **詳細** > **データベース構造を更新**. データベースの物理構造が論理的な記述と一致するかどうかを確認し、SQL 更新スクリプトを実行します。 [詳細情報](../../configuration/using/updating-the-database-structure.md)

1. 次を含むワークフローを停止してバックアップします： **インバウンド SMS アクティビティ**.

   対応するオプションポインタを次の形式でバックアップします。 `SMS_MO_INDEX_{internal name of the workflow}_{name of the insms workflow activity}_{internal name of the external account to access the mid}`.

[バックアップの詳細を表示](../../production/using/backup.md)

1. (**オプション**) 既に「スケジューラー」アクティビティを使用している場合は、ワークフローを開き、次のように再設定します。

   1. 現在の設定を **スケジュール** 」タブから **インバウンド SMS** 外部へのアクティビティ **スケジューラ** アクティビティ。

   1. 現在の設定を **スケジュール** タブ **インバウンド SMS** アクティビティ。

      ![](assets/inbound_sms_1.png)

1. を更新します。 **インバウンド SMS** カスタムスクリプト。

   下のブロックを置き換えます。 このスクリプトは、以前にこのコードをカスタマイズした場合に異なる場合があります。

   ```
   var lastSynchKey = getOption('SMS_MO_INDEX_WKF1105_inSmsUS_smsmidus');
   
   var smsId = application.getNewIds(1);
   
   xtk.session.Write(<inSMS xtkschema="nms:inSMS" _operation="insert"
       id={smsId}
       origin={smsMessage.origin}
       message={smsMessage.message}
       providerId={smsMessage.messageId}/>);
   
   return 2;
   ```

   次の新しいカスタムスクリプトを使用して、ミッドソーシングレコードのプライマリキーとマーケティング SMS ルーティングの外部アカウント ID を組み合わせ、複合キーに基づいて inSMS データを更新します。

   ```
   // please enter real external account ID to replace <EXTERNAL ACCOUNT ID>
   var iExtAccountId=<EXTERNAL_ACCOUNT_ID>;
   // make sure to keep the following elements in the custom script (the rest is optional and custom code can be added): _operation="insertOrUpdate", _key="@midInSMSId,@extAccount-id", midInSMSId={smsMessage.id}, inSms.@["extAccount-id"] = iExtAccountId;, var inSms = <inSMS xtkschema="nms:inSMS" _operation="insertOrUpdate"
   
               _key="@midInSMSId,@extAccount-id"
               midInSMSId={smsMessage.id}
               message={smsMessage.message}
               origin={smsMessage.origin}
               providerId={smsMessage.providerId}
               alias={smsMessage.alias}
               messageDate = {smsMessage.messageDate}
               receivalDate = {smsMessage.receivalDate}
               deliveryDate = {smsMessage.deliveryDate}
               largeAccount = {smsMessage.largeAccount}
               countryCode = {smsMessage.countryCode}
               operatorCode = {smsMessage.operatorCode}
               linkedSmsId={smsMessage.linkedSmsId}
               separator = {smsMessage.separator}/>
   inSms.@["extAccount-id"] = iExtAccountId;
   
   xtk.session.Write(inSms);
   
   return 2;
   ```

1. インバウンド SMS の高度な初期化スクリプトを次のスクリプトで更新します。

   スクリプトは、プライマリキーポインタを 24 時間前にリセットします。 ワークフローは、過去 24 時間以内にミッドソーシングインスタンスからすべての inSMS データの再処理を試み、見つからないデータをマーケティングインスタンスに追加します。

   ```
   // please enter real external account ID to replace <EXTERNAL_ACCOUNT_ID>
   // please enter real pointer option name to replace '<POINTER_OPTION_NAME>'
   // OPTION NAME format: SMS_MO_INDEX_{internal name of the workflow}_inSms_{internal name of the external account to access the mid}
   
   var queryDef = xtk.queryDef.create(
       <queryDef operation="getIfExists" schema="nms:inSMS" lineCount="1">
       <select>
           <node expr="@midInSMSId" alias="@midInSMSId"/>
       </select>
       <where>
           <condition expr="@midInSMSId != 0"/>
           <condition expr={"@created > SubHours(GetDate(), 24)"}/>
           <condition expr={"[@extAccount-id]=<EXTERNAL_ACCOUNT_ID>"}/>
       </where>
       <orderBy>
           <node expr="@midInSMSId"/>
       </orderBy>
       </queryDef>);
   
   var res = parseInt(queryDef.ExecuteQuery().@midInSMSId.toString());
   
   if( !isNaN(res) )
   setOption('<POINTER_OPTION_NAME>', res);
   ```

   >[!WARNING]
   >
   > * 複数の SMS ルーティングアカウントが同じミッドソーシングインスタンスにリンクされている場合、ミッドソーシングインスタンスごとに 1 つのワークフローのみが許可されます。
   > * 任意の外部アカウント ID を使用できます。 外部キーの役割は、ミッドソーシング SMS ID が他のミッドソーシングインスタンスと同一である可能性がある、異なるミッドソーシングサーバーが関与するシナリオで、データの紐付けの整合性を維持することです。
   > * ミッドソーシングインスタンスごとに複数の inSMS ワークフローがある場合、外部アカウント ID が異なる間、ミッドソーシング SMS ID は変わらないので、データの重複が発生する可能性があります。

1. 保存して、ワークフローを再起動します。


