---
title: Broker:Remote Message Ack イベント クラス | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1992d071079e5ecb1912abb1014becca35a339b7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67999617"
---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack イベント クラス

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **がメッセージの受信確認を送信または受信するときに、** Broker:Remote Message Ack [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントが生成されます。  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Broker:Remote Message Ack イベント クラスのデータ列  
  
|データ列|型|[説明]|列番号|フィルターの適用|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスへの接続を作成したクライアント アプリケーションの名前。 この列には、プログラムの表示名ではなく、アプリケーションによって渡された値が格納されます。|10|はい|  
|**BigintData1**|**bigint**|受信確認を含むメッセージのシーケンス番号。|52|いいえ|  
|**BigintData2**|**bigint**|受信確認されているメッセージのシーケンス番号。|53|いいえ|  
|**ClientProcessID**|**int**|クライアント アプリケーションが実行されているプロセスに対し、ホスト コンピューターによって割り当てられた ID。 クライアントでクライアント プロセス ID が指定されると、このデータ列が作成されます。|9|はい|  
|**DatabaseID**|**int**|USE *database* ステートメントで指定されているデータベースの ID。 特定のインスタンスについて USE *database* ステートメントが実行されていない場合は既定のデータベースの ID となります。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、 **ServerName** データ列がトレースにキャプチャされ、そのサーバーが利用可能な場合、データベースの名前が表示されます。 データベースに対応する値は、DB_ID 関数を使用して特定します。|3|はい|  
|**EventClass**|**int**|キャプチャされたイベント クラスの種類。 **Broker:Message Ack** の場合は、常に **149**です。|27|いいえ|  
|**EventSequence**|**int**|このイベントのシーケンス番号。|51|いいえ|  
|**EventSubClass**|**nvarchar**|イベント サブクラスの種類です。各イベント クラスについての詳細な情報を提供します。 この列は次の値を含むことができます。<br /><br /> **Message With Acknowledgement Sent**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] は、通常のシーケンス番号付きメッセージの一部として受信確認を送信しました。<br /><br /> **Acknowledgement Sent**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] は、通常のシーケンス番号付きメッセージとは別に受信確認を送信しました。<br /><br /> **Message With Acknowledgement Received**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] は、通常のシーケンス番号付きメッセージの一部として受信確認を受信しました。<br /><br /> **Acknowledgement Received**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] は、シーケンス番号付きメッセージとは別に受信確認を受信しました。|21|はい|  
|**GUID**|**uniqueidentifier**|ダイアログのメッセージ交換 ID。 この ID はメッセージの一部として転送され、メッセージ交換の両側で共有されます。|54|いいえ|  
|**HonorBrokerPriority**|**Int**|データベースの HONOR_BROKER_PRIORITY オプションの現在の値。0 = オフ、1 = オン。|32|はい|  
|**HostName**|**nvarchar**|クライアントが実行しているコンピューターの名前。 このデータ列には、クライアントがホスト名を指定している場合にデータが格納されます。 ホスト名を指定するには、HOST_NAME 関数を使用します。|8|はい|  
|**IntegerData**|**int**|受信確認を含むメッセージのフラグメント番号。|25|いいえ|  
|**IntegerData2**|**int**|受信確認の対象となるメッセージのフラグメント番号。|55|いいえ|  
|**IsSystem**|**int**|イベントがシステム プロセスとユーザー プロセスのどちらで発生したか。<br /><br /> 0 = ユーザー<br /><br /> 1 = システム|60|いいえ|  
|**LoginSid**|**image**|ログイン ユーザーのセキュリティ ID 番号 (SID)。 各 SID はサーバーのログインごとに一意です。|41|はい|  
|**NTDomainName**|**nvarchar**|ユーザーが属している Windows ドメイン。|7|はい|  
|**NTUserName**|**nvarchar**|このイベントが生成された接続を所有するユーザーの名前。|6|はい|  
|**[Priority]**|**int**|メッセージ交換の優先度レベル。|5|はい|  
|**RoleName**|**nvarchar**|メッセージの受信確認を行ったインスタンスのロール。 **initiator** または **target**のいずれかです。|38|いいえ|  
|**ServerName**|**nvarchar**|トレースしている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|26|いいえ|  
|**SPID**|**int**|クライアントに関連付けられているプロセスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって割り当てられているサーバー プロセス ID。|12|はい|  
|**StartTime**|**datetime**|イベントの開始時刻 (取得できた場合)。|14|はい|  
|**StarvationElevation**|**int**|メッセージ交換に設定された優先度より高い優先度でメッセージが送信されたかどうか。0 = false、1 = true。|33|はい|  
|**TransactionID**|**bigint**|トランザクションに対してシステムが割り当てた ID。|4|いいえ|  
  
  
