---
title: 'SQL Server: Memory Manager オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Manager
- Memory Manager object
ms.assetid: dbf49000-eeb0-4e9c-a361-5092363920dc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 822cb494b7dce35ea965a2a53cab36785a38bc75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250629"
---
# <a name="sql-server-memory-manager-object"></a>SQL Server: Memory Manager オブジェクト
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **Memory Manager** オブジェクトには、全体的なサーバー メモリの使用状況を監視するためのカウンターが用意されています。 全体的なサーバー メモリの使用状況を監視して、ユーザーの利用状況やリソースの使用状況を計測すると、パフォーマンスのボトルネックを突き止めるのに役立つ可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで使用されるメモリを監視すると、次のことを判断する際に役立ちます。  
  
-   ボトルネックの発生原因が、頻繁にアクセスされるデータをキャッシュに格納するための物理メモリ不足によるものかどうか。 メモリが不足している場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではディスクからデータを取得する必要があります。  
  
-   メモリを増設したり、データ キャッシュや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部構造により多くのメモリを使用できるように設定することで、クエリのパフォーマンスを向上できるかどうか。  
  
## <a name="memory-manager-counters"></a>Memory Manager カウンター  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Manager** カウンターについて説明します。  
  
|SQL Server Memory Manager カウンター|説明|  
|----------------------------------------|-----------------|  
|**Connection Memory (KB)**|接続を維持するためにサーバーが使用している動的メモリの合計サイズを指定します。|  
|**Database Cache Memory (KB)**|サーバーがデータベース ページ キャッシュに現在使用しているメモリの量を指定します。|  
|**Free Memory (KB)**|サーバーによって使用されていないコミット済みのメモリの量を指定します。|  
|**Granted Workspace Memory (KB)**|ハッシュ、並べ替え、一括コピー、インデックス作成などの操作を実行しているプロセスに現在割り当てられているメモリの合計サイズを指定します。|  
|**Lock Blocks**|サーバーで使用中のロック ブロックの現在数 (定期的に更新されます) を指定します。 ロック ブロックは、テーブル、ページ、行など、ロックされている個々のリソースを表します。|  
|**Lock Blocks Allocated**|現在割り当てられているロック ブロック数を指定します。 サーバー起動時に割り当てられるロック ブロック数と、割り当てられるロック所有者ブロックの数は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** 構成オプションによって決まります。 より多くのロック ブロックが必要な場合は、値が大きくなります。|  
|**Lock Memory (KB)**|ロックのためにサーバーが使用している動的メモリの合計サイズを指定します。|  
|**Lock Owner Blocks**|サーバーで使用中のロック所有者ブロックの現在数 (定期的に更新されます) を指定します。 ロック所有者ブロックは、各スレッドがオブジェクトに設定したロックの所有権を表します。 たとえば、3 つのスレッドがそれぞれ、ページに共有 (S) ロックを所有している場合は、3 つのロック所有者ブロックがあります。|  
|**Lock Owner Blocks Allocated**|現在割り当てられているロック所有者ブロック数を指定します。 サーバー起動時に割り当てられるロック所有者ブロック数と、割り当てられるロック ブロック数は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** 構成オプションによって決まります。 より多くのロック所有者ブロックが必要な場合は、値が動的に大きくなります。|  
|**Maximum Workspace Memory (KB)**|ハッシュ、並べ替え、一括コピー、インデックス作成などの操作を実行しているプロセスが使用できるメモリの最大サイズを示します。|  
|**Memory Grants Outstanding**|ワークスペース メモリを取得できたプロセスの総数を指定します。|  
|**Memory Grants Pending**|ワークスペース メモリ許可を待機しているプロセスの総数を指定します。|  
|**Optimizer Memory (KB)**|サーバーがクエリの最適化のために使用している動的メモリの合計サイズを指定します。|  
|**Reserved Server Memory (KB)**|将来の使用のためにサーバーが予約しているメモリの量を示します。 このカウンターは、 **[Granted Workspace Memory (KB)]** に表示される、最初に許可された現在の未使用メモリ量を示します。|  
|**SQL Cache Memory (KB)**|サーバーが動的 SQL キャッシュのために使用している動的メモリの合計サイズを指定します。|  
|**Stolen Server Memory (KB)**|サーバーがデータベース ページ以外に使用しているメモリの量を指定します。|  
|**Target Server Memory (KB)**|サーバーが使用できるメモリの最適な量を示します。|  
|**Total Server Memory (KB)**|Memory Manager を使用してサーバーがコミットしたメモリの量を指定します。|  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server: Buffer Manager オブジェクト](sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
