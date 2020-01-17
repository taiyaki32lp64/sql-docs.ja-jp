---
title: SQL Server、Availability Replica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6269474edbde55f1ebf506bfbd5599f5c3287bc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250791"
---
# <a name="sql-server-availability-replica"></a>SQL Server、Availability Replica
  **SQLServer:Availability Replica** パフォーマンス オブジェクトには、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の AlwaysOn 可用性グループの可用性レプリカに関する情報を報告するパフォーマンス カウンターが含まれています。 可用性レプリカのパフォーマンス カウンターはすべてプライマリ レプリカとセカンダリ レプリカの両方に適用され、送信/受信カウンターによってローカル レプリカの状態が示されます。 ほとんどの場合、プライマリ レプリカがデータの大部分を送信し、セカンダリ レプリカがデータを受信します。 ただし、セカンダリ レプリカは、ACK と他のバックグラウンド トラフィックをプライマリ レプリカに送信します。 可用性レプリカでは、ローカル レプリカの現在のロール (プライマリまたはセカンダリ) に応じて一部のカウンターが値 0 を示します。  
  
|カウンター名|説明|  
|------------------|-----------------|  
|**レプリカからの受信バイト数/秒**|可用性レプリカから 1 秒あたりに受信したバイト数。 ユーザーによる更新のないデータベースでも、ping と状態の更新でネットワーク トラフィックが発生します。|  
|**レプリカへの送信バイト数/秒**|リモート可用性レプリカに 1 秒あたりに送信されたバイト数。 プライマリ レプリカの場合、これはセカンダリ レプリカに送信されたバイト数です。 セカンダリ レプリカの場合、これはプライマリ レプリカに送信されたバイト数です。|  
|**トランスポートへの送信バイト数/秒**|リモート可用性レプリカにネットワーク経由で 1 秒あたりに送信された実際のバイト数。 プライマリ レプリカの場合、これはセカンダリ レプリカに送信されたバイト数です。 セカンダリ レプリカの場合、これはプライマリ レプリカに送信されたバイト数です。|  
|**Flow Control Time (ms/sec)**|最後の 1 秒間にログ ストリーム メッセージが送信フロー制御を待機した時間のミリ秒数。|  
|**フロー制御/秒**|最後の 1 秒間に開始されたフロー制御の回数。 **Flow Control Time (ms/sec)** を **Flow Control/sec** で除算すると、平均待機時間が算出されます。|  
|**レプリカからの受信/秒**|レプリカから 1 秒あたりに受信した AlwaysOn メッセージの数。|  
|**再送信メッセージ/秒**|最後の 1 秒間に再送された AlwaysOn メッセージの数。|  
|**レプリカへの送信/秒**|この可用性レプリカに 1 秒あたりに送信された AlwaysOn メッセージの数。|  
|**トランスポートへの送信/秒**|リモート可用性レプリカにネットワーク経由で 1 秒あたりに送信された実際の AlwaysOn メッセージ数。 プライマリ レプリカの場合、これはセカンダリ レプリカに送信されたメッセージ数です。 セカンダリ レプリカの場合、これはプライマリ レプリカに送信されたメッセージ数です。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server、Database Replica](sql-server-database-replica.md)   
 [AlwaysOn 可用性グループ (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
