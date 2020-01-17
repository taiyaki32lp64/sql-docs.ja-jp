---
title: 'SQL Server: Broker - DBM Transport オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 8a6a8bc83c1842676220f384d39179c74c47a336
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987067"
---
# <a name="sql-server-broker---dbm-transport-object"></a>SQL Server: Broker - DBM Transport オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Broker / DBM Transport** パフォーマンス オブジェクトには、Service Broker とデータベース ミラーリングに関するネットワーク情報を報告するパフォーマンス カウンターが含まれています。 次の表は、このオブジェクトに含まれているカウンターを示します。  
  
|SQL Server: Broker / DBM Transport カウンター|[説明]|  
|------------------------------------------------|-----------------|  
|**Current Bytes for Recv I/O**|現在実行中のトランスポート受信操作で読み取るバイト数を報告します。|  
|**Current Bytes for Send I/O**|ネットワーク経由で送信処理中のメッセージ フラグメントに含まれるバイト数を報告します。|  
|**Current Msg Frags for Send I/O**|ネットワーク経由で送信処理中のメッセージ フラグメントの総数を報告します。|  
|**Message Fragment P1 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 1 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P2 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 2 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P3 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 3 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P4 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 4 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P5 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 5 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P6 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 6 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P7 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 7 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P8 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 8 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P9 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 9 のメッセージ フラグメント数を報告します。|  
|**Message Fragment P10 Sends/sec**|ネットワーク経由で 1 秒あたりに送信された優先度 10 のメッセージ フラグメント数を報告します。|  
|**Message Fragment Receives/sec**|ネットワーク経由で 1 秒あたりに受信したメッセージ フラグメント数を報告します。|   
|**Message Fragment Sends/sec**|ネットワーク経由で 1 秒あたりに送信されたすべての優先度のメッセージ フラグメント数を報告します。|  
|**Msg Fragment Recv Size Avg**|ネットワーク経由で受信したメッセージ フラグメントの平均サイズを報告します。|  
|**Msg Fragment Recv Size Avg Base**|内部使用のみです。| 
|**Msg Fragment Send Size Avg**|ネットワーク経由で送信されたメッセージ フラグメントの平均サイズを報告します。|  
|**Msg Fragment Send Size Avg Base**|内部使用のみです。|
|**Open Connection Count**|Service Broker が現在開いているネットワーク接続の数を報告します。|  
|**Pending Bytes for Recv I/O**|ネットワークからの受信後、まだキューへの配置も破棄も行われていないメッセージ フラグメントに含まれるバイト数を報告します。|  
|**Pending Bytes for Send I/O**|ネットワーク経由での送信準備が整ったメッセージ フラグメント内の合計バイト数を報告します。|  
|**Pending Msg Frags for Recv I/O**|ネットワークからの受信後、まだキューへの配置も破棄も行われていないメッセージ フラグメントの数を報告します。|  
|**Pending Msg Frags for Send I/O**|ネットワーク経由での送信準備が整ったメッセージ フラグメントの総数を報告します。|  
|**Receive I/O bytes/sec**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で 1 秒あたりに受信したバイト数を報告します。|  
|**Receive I/O Bytes Total**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で受信した合計バイト数を報告します。|  
|**Receive I/O Len Avg**|トランスポート受信操作の平均バイト数を報告します。|  
|**Receive I/O Len Avg Base**|内部使用のみです。|
|**Receive I/Os/sec**|Service Broker / DBM トランスポート層が 1 秒あたりに完了したトランスポート受信 I/O 操作の数を報告します。 1 つのトランスポート受信操作には、複数のメッセージ フラグメントが含まれている可能性があることに注意してください。|  
|**Recv I/O Buffer Copies bytes/sec**|トランスポート受信 I/O 操作でバッファー フラグメントをメモリに移動しなければならなかった割合。|
|**Recv I/O Buffer Copies Count**|トランスポート受信 I/O 操作でバッファー フラグメントをメモリに移動しなければならなかった回数。| 
|**Send I/O bytes/sec**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で 1 秒あたりに送信したバイト数を報告します。|   
|**Send I/O Bytes Total**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で送信した合計バイト数を報告します。| 
|**Send I/O Len Avg**|各トランスポート送信操作の平均サイズをバイト単位で報告します。 1 つのトランスポート送信操作には、複数のメッセージ フラグメントが含まれている可能性があることに注意してください。|  
|**Send I/O Len Avg Base**|内部使用のみです。|
|**Send I/Os/sec**|1 秒あたりに完了したトランスポート送信 I/O 操作の数を報告します。 1 つのトランスポート送信操作には、複数のメッセージ フラグメントが含まれている可能性があることに注意してください。|  
  
## <a name="see-also"></a>参照  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
