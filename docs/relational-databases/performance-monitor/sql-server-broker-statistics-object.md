---
title: 'SQL Server: Broker Statistics オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 77a6174931924c30b8d482c0bd5d3f4a358f4a10
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987013"
---
# <a name="sql-server-broker-statistics-object"></a>SQL Server: Broker Statistics オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQLServer:Broker Statistics パフォーマンス オブジェクトには、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] のインスタンスに関する [!INCLUDE[ssDE](../../includes/ssde-md.md)]の一般的な情報を報告するパフォーマンス カウンターが含まれています。 次の表は、このオブジェクトに含まれているカウンターの一覧です。  
  
|SQL Server Broker Statistics カウンター|[説明]|  
|-------------------------------------------|-----------------|  
|**Activation Errors Total**|[!INCLUDE[ssSB](../../includes/sssb-md.md)] アクティブ化ストアド プロシージャがエラーで終了した回数。|  
|**Broker Transaction Rollbacks**|SEND や RECEIVE など [!INCLUDE[ssSB](../../includes/sssb-md.md)]に関連する DML ステートメントを含んでいるトランザクションのうち、ロールバックされたトランザクションの数。|  
|**Corrupted Messages Total**|インスタンスが受信した破損メッセージの数。|  
|**Dequeued Transmission Msgs/sec**|1 秒あたりに [!INCLUDE[ssSB](../../includes/sssb-md.md)] 転送キューから削除されたメッセージの数。|  
|**Dialog Timer Event Count**|ダイアログ プロトコル層内でアクティブなタイマーの行数。 この数はアクティブなダイアログの数と同じです。|  
|**Dropped Messages Total**|インスタンスが受信し、キューに配布できなかったメッセージの数。|  
|**Enqueued Local Messages Total**|インスタンスのキューに格納されたメッセージの数。ネットワーク経由以外でキューに格納されたメッセージのみをカウントします。|  
|**Enqueued Local Messages/sec**|1 秒あたりにインスタンスのキューに格納されたメッセージの数。ネットワーク経由以外でキューに格納されたメッセージのみをカウントします。|  
|**Enqueued Messages Total**|インスタンスのキューに格納されたメッセージの総数。|  
|**Enqueued Messages/sec**|1 秒あたりにインスタンスのキューに格納されたメッセージの数。 これには、すべての優先度レベルのメッセージが含まれます。|  
|**Enqueued P1 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 1 のメッセージの数。|  
|**Enqueued P2 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 2 のメッセージの数。|  
|**Enqueued P3 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 3 のメッセージの数。|  
|**Enqueued P4 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 4 のメッセージの数。|  
|**Enqueued P5 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 5 のメッセージの数。|  
|**Enqueued P6 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 6 のメッセージの数。|  
|**Enqueued P7 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 7 のメッセージの数。|  
|**Enqueued P8 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 8 のメッセージの数。|  
|**Enqueued P9 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 9 のメッセージの数。|  
|**Enqueued P10 Msgs/sec**|1 秒あたりにインスタンスのキューに格納された優先度 10 のメッセージの数。|  
|**Enqueued Transmission Msgs/sec**|1 秒あたりに [!INCLUDE[ssSB](../../includes/sssb-md.md)] 転送キューに格納されたメッセージの数。|  
|**Enqueued Transport Msg Frag Tot**|インスタンスのキューに格納されたメッセージ フラグメントの数。ネットワーク経由でキューに格納されたメッセージのみをカウントします。|  
|**Enqueued Transport Msg Frags/sec**|1 秒あたりにインスタンスのキューに格納されたメッセージ フラグメントの数。|  
|**Enqueued Transport Msgs Total**|インスタンスのキューに格納されたメッセージの数。ネットワーク経由でキューに格納されたメッセージのみをカウントします。|  
|**Enqueued Transport Msgs/sec**|1 秒あたりにインスタンスのキューに格納されたメッセージの数。ネットワーク経由でキューに格納されたメッセージのみをカウントします。|  
|**Forwarded Messages Total**|このコンピューターにより転送された [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージの総数。|  
|**Forwarded Messages/sec**|このコンピューターにより 1 秒あたりに転送されたメッセージの数。|  
|**Forwarded Msg Byte Total**|このコンピューターにより転送されたメッセージの合計サイズ (バイト単位)。|  
|**Forwarded Msg Bytes/sec**|このコンピューターにより 1 秒あたりに転送されたメッセージの合計サイズ (バイト単位)。|  
|**Forwarded Msg Discarded Total**|転送するためにこのコンピューターで受信したメッセージのうち、正常に転送できなかったメッセージの数。|  
|**Forwarded Msg Discarded/sec**|転送するためにこのコンピューターで受信したメッセージのうち、1 秒あたりに正常に転送できなかったメッセージの数。|  
|**Forwarded Pending Msg Bytes**|現在転送を待機しているメッセージの合計サイズ。|  
|**Forwarded Pending Msg Count**|現在転送を待機しているメッセージの総数。|  
|**SQL RECEIVE Total**|処理された [!INCLUDE[tsql](../../includes/tsql-md.md)] の RECEIVE ステートメントの総数。|  
|**SQL RECEIVEs/sec**|1 秒あたりに処理された [!INCLUDE[tsql](../../includes/tsql-md.md)] の RECEIVE ステートメントの数。|  
|**SQL SEND Total**|実行された [!INCLUDE[tsql](../../includes/tsql-md.md)] の SEND ステートメントの総数。|  
|**SQL SENDs/sec**|1 秒あたりに実行された [!INCLUDE[tsql](../../includes/tsql-md.md)] の SEND ステートメントの数。|  
  
## <a name="see-also"></a>参照  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
