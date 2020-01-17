---
title: sys.dm_os_memory_brokers (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
author: stevestein
ms.author: sstein
ms.openlocfilehash: a8e131e2550ffa5078df5e284898ffe936128b7e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265875"
---
# <a name="sysdmosmemorybrokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  内部的な割り当て[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリ マネージャー。 プロセス メモリ カウンター間の差を追跡**sys.dm_os_process_memory**内部カウンターは、外部コンポーネントからメモリ使用量を示すことができます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メモリ領域です。  
  
 メモリ ブローカー内のさまざまなコンポーネント間のメモリ割り当てを適切に配分[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]現在と予想される使用量に基づきます。 メモリ ブローカーは割り当てを実行しません。 だけ、配布を計算するための割り当てを追跡します。  
  
 次の表は、メモリ ブローカーに関する情報を示しています。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_os_memory_brokers**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|リソース ガバナー プールに関連付けられているリソース プールの ID。|  
|**memory_broker_type**|**nvarchar(60)**|メモリ ブローカーの種類。 現在は、次の 3 つの種類でのメモリ ブローカーの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]とその説明の下に表示されています。<br /><br /> **MEMORYBROKER_FOR_CACHE** :使用するために割り当てられているメモリ (バッファー プールではないキャッシュ) のオブジェクトがキャッシュされます。<br /><br /> **MEMORYBROKER_FOR_STEAL** :バッファー プールから盗用されたメモリ。 現在の所有者が解放されるまでにも、このメモリは他のコンポーネントで再利用のご利用いただけません。<br /><br /> **MEMORYBROKER_FOR_RESERVE** :メモリの現在の要求を実行することによって将来使用するために予約されています。|  
|**allocations_kb**|**bigint**|この種類のブローカーに割り当てられているキロバイト (KB) 単位でのメモリの量。|  
|**allocations_kb_per_sec**|**bigint**|1 秒あたりのキロバイト (KB) のメモリ割り当ての数です。 この値は、メモリの割り当て解除の場合は負であることができます。|  
|**predicted_allocations_kb**|**bigint**|ブローカーによるメモリの予想割り当て量。 これは、メモリの使用パターンに基づきます。|  
|**target_allocations_kb**|**bigint**|推奨されるメモリ割り当て量 (KB 単位)。現在の設定とメモリの使用パターンに基づいて決定されます。 このブローカーを拡大またはこの番号を縮小する必要があります。|  
|**future_allocations_kb**|**bigint**|次の数秒間で行われますキロバイト (KB) 単位での割り当ての予測数。|  
|**overall_limit_kb**|**bigint**|キロバイト (KB)、ブローカーが割り当てられるメモリの最大量。|  
|**last_notification**|**nvarchar(60)**|メモリ使用量の推奨値。現在の設定と使用パターンに基づいて決定されます。 有効な値は次のとおりです。<br /><br /> 拡大<br /><br /> 縮小<br /><br /> 安定版|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="see-also"></a>関連項目  

  [SQL Server オペレーティング システム関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


