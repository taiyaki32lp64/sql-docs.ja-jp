---
title: dm_os_memory_clerks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_memory_clerks
- sys.dm_os_memory_clerks
- dm_os_memory_clerks_TSQL
- sys.dm_os_memory_clerks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_clerks dynamic management view
ms.assetid: 1d556c67-5c12-46d5-aa8c-7ec1bb858df7
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 97805251e309132892fb94db63a308b10657daff
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983097"
---
# <a name="sysdm_os_memory_clerks-transact-sql"></a>sys.dm_os_memory_clerks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで現在アクティブなすべてのメモリクラークのセットを返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_memory_clerks**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**memory_clerk_address**|**varbinary(8)**|メモリ クラークの一意のメモリ アドレスを指定します。 これは主キー列です。 NULL 値は許可されません。|  
|**型**|**nvarchar(60)**|メモリ クラークの種類を指定します。 各クラークには、CLR Clerks MEMORYCLERK_SQLCLR などの特定の種類があります。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|このメモリ クラークに内部的に割り当てられた名前を指定します。 コンポーネントには、特定の種類の複数のメモリ クラークを作成できます。 同じ種類のメモリ クラークを識別するために、コンポーネントで特定の名前を選択して使用することもできます。 NULL 値は許可されません。|  
|**memory_node_id**|**smallint**|メモリ ノードの ID を指定します。 Null 値は許容されません。|  
|**single_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|  
|**pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> このメモリ クラークに割り当てられたページ メモリの量を KB 単位で指定します。 NULL 値は許可されません。|  
|**multi_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> 割り当てられた複数ページ メモリの量 (KB 単位)。 これは、メモリノードの複数ページアロケーターを使用して割り当てられたメモリの量です。 このメモリは、バッファー プール外に割り当てられ、メモリ ノードの仮想アロケーターを利用します。 NULL 値は許可されません。|  
|**virtual_memory_reserved_kb**|**bigint**|メモリ クラークによって予約済みの仮想メモリの量を指定します。 NULL 値は許可されません。|  
|**virtual_memory_committed_kb**|**bigint**|メモリ クラークによってコミット済みの仮想メモリの量を指定します。 コミット済みのメモリ量は、予約済みのメモリ量よりも常に少ない状態である必要があります。 NULL 値は許可されません。|  
|**awe_allocated_kb**|**bigint**|物理メモリでロックされ、オペレーティング システムによってページ アウトされないメモリの量を KB 単位で指定します。 NULL 値は許可されません。|  
|**shared_memory_reserved_kb**|**bigint**|メモリ クラークによって予約済みの共有メモリの量を指定します。 共有メモリおよびファイル マッピングで使用するために予約されるメモリの量です。 NULL 値は許可されません。|  
|**shared_memory_committed_kb**|**bigint**|メモリ クラークによってコミット済みの共有メモリの量を指定します。 NULL 値は許可されません。|  
|**page_size_in_bytes**|**bigint**|このメモリ クラークのページ割り当ての粒度を指定します。 NULL 値は許可されません。|  
|**page_allocator_address**|**varbinary(8)**|ページ アロケーターのアドレスを指定します。 このアドレスは、メモリクラークに対して一意であり、 **dm_os_memory_objects**で使用して、この clerk にバインドされているメモリオブジェクトを見つけることができます。 NULL 値は許可されません。|  
|**host_address**|**varbinary(8)**|このメモリ クラークのホストのメモリ アドレスを指定します。 詳細については、「 [sys &#40;. dm_os_hosts transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)」を参照してください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client などのコンポーネントは、ホストインターフェイスを介して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリリソースにアクセスします。<br /><br /> 0x00000000 = メモリ クラークは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に属します。<br /><br /> NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory manager は、3層階層で構成されます。 一番下の階層は、メモリ ノードです。 中間レベルの階層は、メモリ クラーク、メモリ キャッシュ、およびメモリ プールから成ります。 最上位の階層はメモリ オブジェクトから成ります。 これらのオブジェクトは、一般的に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでメモリを割り当てる場合に使用されます。  
  
 メモリ ノードでは、低レベルのアロケーター用インターフェイスおよび実装が用意されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内部では、メモリ クラークのみがメモリ ノードにアクセスできます。 メモリ クラークは、メモリ ノードのインターフェイスにアクセスしてメモリを割り当てます。 また、メモリ ノードは、診断用のクラークを使用して、割り当てられたメモリを追跡します。 メモリを大量に割り当てるコンポーネントはすべて、独自のメモリ クラークを作成し、クラークのインターフェイスを使用してすべてのメモリを割り当てる必要があります。 通常、コンポーネントは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に、それぞれに対応したクラークを作成します。  
  
## <a name="see-also"></a>参照  

 [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [dm_exec_query_memory_grants &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [dm_exec_sql_text &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
  
  


