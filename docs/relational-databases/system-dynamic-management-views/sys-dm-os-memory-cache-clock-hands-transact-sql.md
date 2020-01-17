---
title: sys.dm_os_memory_cache_clock_hands (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_cache_clock_hands_TSQL
- dm_os_memory_cache_clock_hands
- dm_os_memory_cache_clock_hands_TSQL
- sys.dm_os_memory_cache_clock_hands
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_cache_clock_hands dynamic management view
ms.assetid: 0660eddc-691c-425f-9d43-71151d644de7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 783f985810b44673c6a6566caa6e89ff655670e0
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265789"
---
# <a name="sysdmosmemorycacheclockhands-transact-sql"></a>sys.dm_os_memory_cache_clock_hands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定のキャッシュ クロックに関する各ハンドの状態を返します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_memory_cache_clock_hands**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**cache_address**|**varbinary(8)**|クロックに関連付けられたキャッシュのアドレス。 NULL 値は許可されません。|  
|**name**|**nvarchar (256)**|キャッシュの名前。 NULL 値は許可されません。|  
|**type**|**nvarchar(60)**|キャッシュ ストアの種類。 同じ種類のキャッシュが複数存在することが可能です。 NULL 値は許可されません。|  
|**clock_hand**|**nvarchar(60)**|ハンドの種類。 これは、次のいずれかです。<br /><br /> 外部リンク<br /><br /> Internal<br /><br /> NULL 値は許可されません。|  
|**clock_status**|**nvarchar(60)**|クロックの状態です。 これは、次のいずれかです。<br /><br /> 中断<br /><br /> 実行中<br /><br /> NULL 値は許可されません。|  
|**rounds_count**|**bigint**|エントリを削除するため、キャッシュ経由で行われたスイープの数。 NULL 値は許可されません。|  
|**removed_all_rounds_count**|**bigint**|すべてのスイープで削除されたエントリの数。 NULL 値は許可されません。|  
|**updated_last_round_count**|**bigint**|前回のスイープ中に更新されたエントリの数。 NULL 値は許可されません。|  
|**removed_last_round_count**|**bigint**|前回のスイープ中に削除されたエントリの数。 NULL 値は許可されません。|  
|**last_tick_time**|**bigint**|最後に、クロック ハンドの移動をミリ秒単位。 NULL 値は許可されません。|  
|**round_start_time**|**bigint**|前回のスイープの時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|**last_round_start_time**|**bigint**|合計時間 (ミリ秒)、前回のラウンドの完了に、クロックでかかります。 NULL 値は許可されません。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="remarks"></a>コメント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリ キャッシュと呼ばれる構造体でメモリ内の情報を格納します。 キャッシュには、データ、インデックス エントリ、コンパイル済みプロシージャ プランなど、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に関するさまざまな種類の情報が格納されます。 情報を再作成を避けるためには、保持されるメモリがキャッシュ可能な限りおよび利用するのには古すぎる場合、またはメモリ領域が新しい情報が必要なときに通常、キャッシュから削除します。 古い情報を削除する処理は、メモリ スイープと呼ばれます。 メモリ スイープは、頻繁にアクティビティしますが、継続的ないません。 メモリ キャッシュのスイープはクロック アルゴリズムによって制御され、 1 つのクロック ハンドと呼ばれるいくつかのメモリ スイープを制御できます。 メモリ キャッシュのクロック ハンドは、メモリ スイープの手の 1 つの現在の場所です。  

## <a name="see-also"></a>関連項目  
 [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
 [sys.dm_os_memory_cache_counters &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)
  

