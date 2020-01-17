---
title: dm_os_memory_cache_counters (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_counters_TSQL
- dm_os_memory_cache_counters_TSQL
- sys.dm_os_memory_cache_counters
- dm_os_memory_cache_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_counters dynamic management view
ms.assetid: ca7bd036-d661-4c17-b00a-e1a975bd8932
author: stevestein
ms.author: sstein
ms.openlocfilehash: 755e0cdbf5bff5bcd9c048a2f77918dc9a6eb2a3
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982527"
---
# <a name="sysdm_os_memory_cache_counters-transact-sql"></a>dm_os_memory_cache_counters (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、キャッシュのヘルスのスナップショットを返します。 **dm_os_memory_cache_counters**は、割り当てられたキャッシュエントリ、その使用、およびキャッシュエントリのメモリのソースに関する実行時の情報を提供します。  
  
> **注:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_memory_cache_counters**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary (8)**|特定のキャッシュに関連付けられているカウンターのアドレス (主キー) を示します。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|キャッシュの名前を指定します。 NULL 値は許可されません。|  
|**型**|**nvarchar(60)**|このエントリに関連付けられているキャッシュの型を示します。 NULL 値は許可されません。|  
|**single_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> 割り当てられた単一ページメモリの量 (kb 単位)。 これは、単一ページアロケーターを使用して割り当てられたメモリの量です。 キャッシュ用にバッファー プールから直接取得された 8 KB ページを表します。 NULL 値は許可されません。|  
|**pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> キャッシュに割り当てられたメモリの量 (kb 単位) を指定します。 NULL 値は許可されません。|  
|**multi_pages_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> 割り当てられている複数ページ メモリの量 (KB 単位)。 メモリ ノードの複数ページ アロケーターを使用することによって割り当てられるメモリの量です。 このメモリは、バッファー プール外に割り当てられ、メモリ ノードの仮想アロケーターを利用します。 NULL 値は許可されません。|  
|**pages_in_use_kb**|**bigint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> キャッシュで割り当てられて使用されているメモリの量 (kb 単位) を指定します。 NULL 値が許可されます。  `USERSTORE_<*>` 型のオブジェクトの値は追跡されません。  これらについては NULL が報告されます。|  
|**single_pages_in_use_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> 使用されている単一ページ メモリの量 (KB 単位)。 NULL 値が許可されます。 USERSTORE_\<* > 型のオブジェクトの場合、この情報は追跡されず、これらの値は NULL になります。|  
|**multi_pages_in_use_kb**|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]<br /><br /> 使用されている複数ページメモリの量 (kb 単位)。 NULLABLE. USERSTORE_\<* > 型のオブジェクトの場合、この情報は追跡されず、これらの値は NULL になります。|  
|**entries_count**|**bigint**|キャッシュ内のエントリの数を示します。 NULL 値は許可されません。|  
|**entries_in_use_count**|**bigint**|キャッシュ内の使用されているエントリの数を示します。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
  [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


