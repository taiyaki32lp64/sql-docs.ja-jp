---
title: dm_os_hosts (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_hosts_TSQL
- dm_os_hosts
- dm_os_hosts_TSQL
- sys.dm_os_hosts
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_hosts dynamic management view
ms.assetid: a313ff3b-1fe9-421e-b94b-cea19c43b0e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: e4ff3e25accf5c499afb5e306a0eec206f6b3f82
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982552"
---
# <a name="sysdm_os_hosts-transact-sql"></a>sys.dm_os_hosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに現在登録されているすべてのホストを返します。 このビューでは、ホストで使用されているリソースも返されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_hosts**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**host_address**|**varbinary(8)**|ホスト オブジェクトの内部メモリ アドレス。|  
|**型**|**nvarchar(60)**|ホストされるコンポーネントの種類。 例:<br /><br /> SOSHOST_CLIENTID_SERVERSNI = SQL Server ネイティブ インターフェイス<br /><br /> SOSHOST_CLIENTID_SQLOLEDB = SQL Server Native Client OLE DB プロバイダー<br /><br /> SOSHOST_CLIENTID_MSDART = Microsoft Data Access Run Time|  
|**name**|**nvarchar(32)**|ホストの名前。|  
|**enqueued_tasks_count**|**int**|ホストによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のキューに挿入されたタスクの合計数。|  
|**active_tasks_count**|**int**|ホストによってキューに挿入されたタスクのうち、現在実行中のタスクの数。|  
|**completed_ios_count**|**int**|ホスト経由で発行され、完了した I/O の合計数。|  
|**completed_ios_in_bytes**|**bigint**|ホスト経由で完了した I/O の合計バイト数。|  
|**active_ios_count**|**int**|現在完了を待機しているホストに関連する I/O 要求の合計数。|  
|**default_memory_clerk_address**|**varbinary(8)**|ホストに関連付けられているメモリ クラーク オブジェクトのメモリ アドレス。 詳細については、「 [sys &#40;. dm_os_memory_clerks transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)」を参照してください。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の実行可能なコンポーネント以外の OLE DB プロバイダーなどのコンポーネントが、メモリを割り当てたりノンプリエンプティブなスケジュールに参加することが許可されます。 これらのコンポーネントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によってホストされ、これらのコンポーネントによって割り当てられるすべてのリソースが追跡されます。 ホスティングによって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の外部コンポーネントで使用されるリソースをより正確に把握できます。  
  
## <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|[リレーションシップ]|  
|----------|--------|------------------|  
|sys.dm_os_hosts. default_memory_clerk_address|sys.dm_os_memory_clerks. memory_clerk_address|1対1|  
|sys.dm_os_hosts. host_address|sys.dm_os_memory_clerks. host_address|1対1|  
  
## <a name="examples"></a>使用例  
 次の例では、ホストされるコンポーネントによって使用されているメモリの総量を調べます。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。|  
  
```  
SELECT h.type, SUM(mc.pages_kb) AS commited_memory  
FROM sys.dm_os_memory_clerks AS mc   
INNER JOIN sys.dm_os_hosts AS h   
    ON mc.memory_clerk_address = h.default_memory_clerk_address  
GROUP BY h.type;  
```  
  
## <a name="see-also"></a>参照  

 [dm_os_memory_clerks &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


