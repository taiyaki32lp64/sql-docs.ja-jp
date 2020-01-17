---
title: sys.dm_os_process_memory (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_process_memory_TSQL
- dm_os_process_memory_TSQL
- dm_os_process_memory
- sys.dm_os_process_memory
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_process_memory dynamic management view
ms.assetid: e838130c-95d4-4605-9e3b-eb0ab71cd250
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fcbab4d5dc1bbc86fe9083e9c3407749040a0023
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265701"
---
# <a name="sysdmosprocessmemory-transact-sql"></a>sys.dm_os_process_memory (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス空間から生じる大半のメモリ割り当ては、こうした割り当ての追跡と管理を可能にするインターフェイスを通じて制御されます。 ただし、メモリ割り当てが、内部のメモリ管理ルーチンをバイパスする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アドレス空間で実行される場合もあります。 値は、ベースとなるオペレーティング システムを通じて取得されます。 操作することがない内部メソッドによって[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、調整を行うロックされている場合、またはサイズの大きいページの割り当てを除く。  
  
 すべてには、キロバイト (KB) のサイズが示されているメモリを示す値が返されます。 列**total_virtual_address_space_reserved_kb**の複製である**virtual_memory_in_bytes**から**sys.dm_os_sys_info**します。  
  
 次の表は、プロセス アドレス空間の全体像を表したものです。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_process_memory**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**physical_memory_in_use_kb**|**bigint**|オペレーティング システムから報告されたプロセス ワーキング セットに、ラージ ページ API を使用して追跡された割り当てを加えた値 (KB 単位) を示します。 Null を許容しません。|  
|**large_page_allocations_kb**|**bigint**|ラージ ページ Api を使用して割り当てられた物理メモリを指定します。 Null を許容しません。|  
|**locked_page_allocations_kb**|**bigint**|メモリでロックされているメモリ ページを指定します。 Null を許容しません。|  
|**total_virtual_address_space_kb**|**bigint**|仮想アドレス空間のユーザー モード領域の合計サイズを示します。 Null を許容しません。|  
|**virtual_address_space_reserved_kb**|**bigint**|プロセスによって予約されている仮想アドレス空間の総量を示します。 Null を許容しません。|  
|**virtual_address_space_committed_kb**|**bigint**|コミットまたは物理ページへのマップが済んでいる予約済みの仮想アドレス領域の量を示します。 Null を許容しません。|  
|**virtual_address_space_available_kb**|**bigint**|現在利用可能な仮想アドレス空間の量を示します。 Null を許容しません。<br /><br /> **注:** 割り当ての粒度未満の空き領域が存在できます。 これらの領域は割り当てに利用できません。|  
|**page_fault_count**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセスに起因するページ違反の数を示します。 Null を許容しません。|  
|**memory_utilization_percentage**|**int**|ワーキング セットのコミット済みメモリの割合を指定します。 Null を許容しません。|  
|**available_commit_limit_kb**|**bigint**|プロセスによってコミット可能なメモリの量を示します。 Null を許容しません。|  
|**process_physical_memory_low**|**bit**|プロセスが物理メモリの不足の通知に応答していることを示します。 Null を許容しません。|  
|**process_virtual_memory_low**|**bit**|仮想メモリの不足の状態が検出されたことを示します。 Null を許容しません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


