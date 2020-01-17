---
title: SQL Server、Database Replica | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 89d2da02b841edd85d58798ca4c7c1745332d536
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093646"
---
# <a name="sql-server-database-replica"></a>SQL Server、データベース レプリカ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:Database Replica** パフォーマンス オブジェクトには、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の AlwaysOn 可用性グループのセカンダリ データベースに関する情報を報告するパフォーマンス カウンターが含まれています。 このオブジェクトは、セカンダリ レプリカをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでのみ有効です。  
  
|カウンター名|[説明]|表示|  
|------------------|-----------------|--------------|  
|**受信ファイル バイト数/秒**|セカンダリ データベースのセカンダリ レプリカが最近 1 秒間に受信した FILESTREAM データの量。|セカンダリ レプリカ|  
|**ログ適用保留キュー**|データベース レプリカへの適用を待機しているログ ブロックの数。|セカンダリ レプリカ|
|**ログ適用準備完了キュー**|データベース レプリカへの適用を待機中で準備が完了しているログ ブロックの数。|セカンダリ レプリカ|
|**受信ログ バイト数/秒**|データベースのセカンダリ レプリカが最近 1 秒間に受信したログ レコードの量。|セカンダリ レプリカ|  
|**Log remaining for undo**|元に戻すフェーズを完了するためのログの残量 (KB 単位)。|セカンダリ レプリカ|  
|**Log Send Queue**|まだセカンダリ レプリカに送信されていない、プライマリ データベースのログ ファイル内のログ レコードの量 (KB 単位)。 この値は、プライマリ レプリカからセカンダリ レプリカに送信されます。 セカンダリに送信される FILESTREAM ファイルはキューのサイズに含まれません。|セカンダリ レプリカ|  
|**Mirrored Write Transaction/sec**|最後の 1 秒間に、プライマリ データベースに書き込まれたトランザクションのうち、ログがセカンダリ データベースに送信されるまでコミットを待機したトランザクションの数。|プライマリ レプリカ|  
|**Recovery Queue**|まだ再実行されていないセカンダリ レプリカのログ ファイル内のログ レコードの量。|セカンダリ レプリカ|  
|**Redo blocked/sec**|再実行スレッドがデータベースのリーダーで保持されているロックでブロックされた回数。|セカンダリ レプリカ|  
|**Redo Bytes Remaining**|元に戻すフェーズを完了するために再実行されるログの残量 (KB 単位)。|セカンダリ レプリカ|  
|**再適用バイト数/秒**|セカンダリ データベースで最近 1 秒間に再実行されたログ レコードの量。|セカンダリ レプリカ|  
|**Total Log requiring undo**|元に戻す必要のあるログの合計 KB 数。|セカンダリ レプリカ|  
|**Transaction Delay**|現在の全トランザクションに対する終了していないコミットの確認を待機中に生じた遅延 (ミリ秒単位)。 *Mirrored Write Transaction/sec* で割ると、*平均の Transaction Delay* が得られます。 詳細については、「[SQL Server 2012 AlwaysOn – Part 12 – Performance Aspects and Performance Monitoring II](https://blogs.msdn.microsoft.com/saponsqlserver/2013/04/24/sql-server-2012-alwayson-part-12-performance-aspects-and-performance-monitoring-ii/)」 (SQL Server 2012 AlwaysOn – パート 12 – パフォーマンスの性質およびパフォーマンスの監視 II) を参照してください。|プライマリ レプリカ|  
  
## <a name="see-also"></a>参照
  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、Availability Replica](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [SQL Server、Databases オブジェクト](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  