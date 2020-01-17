---
title: SQL Server、ブローカーおよび DBM トランスポート オブジェクト |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b0347c7f7e19ae5500f8c5be100ef2d0dc663784
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250729"
---
# <a name="sql-server-broker-and-dbm-transport-object"></a>SQL Server の Broker および DBM Transport オブジェクト
  **Broker / DBM Transport** パフォーマンス オブジェクトには、Service Broker とデータベース ミラーリングに関するネットワーク情報を報告するパフォーマンス カウンターが含まれています。 次の表は、このオブジェクトに含まれているカウンターを示します。  
  
|SQL Server: Broker / DBM Transport カウンター|説明|  
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
|**メッセージ フラグメント送信サイズの平均**|ネットワーク経由で送信されたメッセージ フラグメントの平均サイズを報告します。|  
|**Message Fragment Sends/sec**|ネットワーク経由で 1 秒あたりに送信されたすべての優先度のメッセージ フラグメント数を報告します。|  
|**受信メッセージ フラグメントの数/秒**|ネットワーク経由で 1 秒あたりに受信したメッセージ フラグメント数を報告します。|  
|**Msg Fragment Recv Size Avg**|ネットワーク経由で受信したメッセージ フラグメントの平均サイズを報告します。|  
|**Open Connection Count**|Service Broker が現在開いているネットワーク接続の数を報告します。|  
|**Pending Bytes for Recv I/O**|ネットワークからの受信後、まだキューへの配置も破棄も行われていないメッセージ フラグメントに含まれるバイト数を報告します。|  
|**Pending Bytes for Send I/O**|ネットワーク経由での送信準備が整ったメッセージ フラグメント内の合計バイト数を報告します。|  
|**Pending Msg Frags for Recv I/O**|ネットワークからの受信後、まだキューへの配置も破棄も行われていないメッセージ フラグメントの数を報告します。|  
|**Pending Msg Frags for Send I/O**|ネットワーク経由での送信準備が整ったメッセージ フラグメントの総数を報告します。|  
|**Receive I/O Bytes Total**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で受信した合計バイト数を報告します。|  
|**Receive I/O bytes/sec**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で 1 秒あたりに受信したバイト数を報告します。|  
|**Receive I/O Len Avg**|トランスポート受信操作の平均バイト数を報告します。|  
|**受信 I/o 数/秒**|Service Broker / DBM トランスポート層が 1 秒あたりに完了したトランスポート受信 I/O 操作の数を報告します。 1 つのトランスポート受信操作には、複数のメッセージ フラグメントが含まれている可能性があることに注意してください。|  
|**Send I/O Bytes Total**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で送信した合計バイト数を報告します。|  
|**Send I/O bytes/sec**|Service Broker のエンドポイントとデータベース ミラーリングのエンドポイントで、ネットワーク経由で 1 秒あたりに送信したバイト数を報告します。|  
|**Send I/O Len Avg**|各トランスポート送信操作の平均サイズをバイト単位で報告します。 1 つのトランスポート送信操作には、複数のメッセージ フラグメントが含まれている可能性があることに注意してください。|  
|**Send I/Os/sec**|1 秒あたりに完了したトランスポート送信 I/O 操作の数を報告します。 1 つのトランスポート送信操作には、複数のメッセージ フラグメントが含まれている可能性があることに注意してください。|  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_broker_forwarded_messages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql)   
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
