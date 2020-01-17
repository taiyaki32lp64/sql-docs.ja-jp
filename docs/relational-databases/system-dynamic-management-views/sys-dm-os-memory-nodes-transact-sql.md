---
title: dm_os_memory_nodes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_nodes_TSQL
- sys.dm_os_memory_nodes
- sys.dm_os_memory_nodes_TSQL
- dm_os_memory_nodes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_nodes dynamic management view
ms.assetid: bf4032fe-7db1-40e9-a62e-d69cebff4b44
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6f68524b2713b9d662c9e9ed0950334ea0a94ece
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983128"
---
# <a name="sysdm_os_memory_nodes-transact-sql"></a>sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部の割り当てでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory manager が使用されます。 **Dm_os_process_memory**と内部カウンターのプロセスメモリカウンターの差を追跡すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ領域内の外部コンポーネントからのメモリ使用を示すことができます。  
  
 ノードは、物理 NUMA メモリ ノードごとに作成されます。 これらは、 **dm_os_nodes**の CPU ノードとは異なる場合があります。  
  
 Windows メモリ割り当てルーチンを介して直接実行された割り当ては追跡されません。 次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory manager インターフェイスを使用した場合にのみ実行されるメモリ割り当てに関する情報を示しています。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_memory_nodes**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|メモリノードの ID を指定します。 **Dm_os_memory_clerks**の**memory_node_id**に関連付けられています。 Null 値は許容されません。|  
|**virtual_address_space_reserved_kb**|**bigint**|仮想アドレス予約の数 (kb 単位) を示します。これは、コミットされていないか、物理ページにマップされていません。 Null 値は許容されません。|  
|**virtual_address_space_committed_kb**|**bigint**|コミットまたは物理ページにマップされた仮想アドレスの量を KB 単位で指定します。 Null 値は許容されません。|  
|**locked_page_allocations_kb**|**bigint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によってロックされている物理メモリの量を KB 単位で指定します。 Null 値は許容されません。|  
|**single_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> このノードで実行されているスレッドによって1ページアロケーターを使用して割り当てられたコミット済みメモリの量 (KB 単位)。 このメモリは、バッファープールから割り当てられます。 この値は、割り当て要求が実行された場所を示します。割り当て要求が満たされた物理的な場所ではありません。|  
|**pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> メモリ マネージャー ページ アロケーターによってこの NUMA ノードから割り当てられる、コミット済みのメモリ量 (KB 単位) を指定します。 Null 値は許容されません。|  
|**multi_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> このノード上で実行されているスレッドが複数ページ アロケーターを使って割り当てたコミット済みのメモリ量 (KB 単位)。 このメモリは、バッファー プール外から割り当てられます。 この値は、割り当て要求が実行された場所を示します。割り当て要求が満たされた物理的な場所ではありません。|  
|**shared_memory_reserved_kb**|**bigint**|このノードから予約されている共有メモリの量を KB 単位で指定します。 Null 値は許容されません。|  
|**shared_memory_committed_kb**|**bigint**|このノードでコミットされた共有メモリの量 (KB 単位) を指定します。 Null 値は許容されません。|  
|**cpu_affinity_mask**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 内部使用のみです。 Null 値は許容されません。|  
|**online_scheduler_mask**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 内部使用のみです。 Null 値は許容されません。|  
|**processor_group**|**smallint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 内部使用のみです。 Null 値は許容されません。|  
|**foreign_committed_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 他のメモリノードからコミットされたメモリの量を KB 単位で指定します。 Null 値は許容されません。|  
|**target_kb** |**bigint** |**適用対象**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> メモリノードのメモリ目標を KB 単位で指定します。 |   
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
  [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


