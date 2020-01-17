---
title: dm_os_waiting_tasks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_waiting_tasks
- sys.dm_os_waiting_tasks_TSQL
- dm_os_waiting_tasks_TSQL
- sys.dm_os_waiting_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_waiting_tasks dynamic management view
ms.assetid: ca5e6844-368c-42e2-b187-6e5f5afc8df3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c0a89a48fa960812ee955cd3b7ecb30069161f61
ms.sourcegitcommit: aece9f7db367098fcc0c508209ba243e05547fe1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72260379"
---
# <a name="sysdm_os_waiting_tasks-transact-sql"></a>sys.dm_os_waiting_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  あるリソースで待機しているタスクの待機キューに関する情報を返します。 タスクの詳細については、「[スレッドおよびタスクアーキテクチャガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。
   
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_waiting_tasks**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**waiting_task_address**|**varbinary(8)**|待機中のタスクのアドレス。|  
|**session_id**|**smallint**|タスクに関連付けられているセッションの ID。|  
|**exec_context_id**|**int**|タスクに関連付けられている実行コンテキストの ID。|  
|**wait_duration_ms**|**bigint**|この待機の種類の合計待機時間 (ミリ秒単位)。 この時間には**signal_wait_time**が含まれます。|  
|**wait_type**|**nvarchar(60)**|待機の種類の名前。|  
|**resource_address**|**varbinary(8)**|タスクが待機しているリソースのアドレス。|  
|**blocking_task_address**|**varbinary(8)**|このリソースを現在保持しているタスク|  
|**blocking_session_id**|**smallint**|要求をブロックしているセッションの ID。 この列が NULL の場合は、要求がブロックされていないか、ブロックしているセッションのセッション情報が使用または識別できません。<br /><br /> -2 = ブロックしているリソースは、孤立した分散トランザクションが所有しています。<br /><br /> -3 = ブロックしているリソースは、遅延復旧トランザクションによって所有されています。<br /><br /> -4 = 内部ラッチの状態遷移のため、ブロックしているラッチの所有者のセッション ID を特定できませんでした。|  
|**blocking_exec_context_id**|**int**|ブロックしているタスクの実行コンテキストの ID。|  
|**resource_description**|**nvarchar(3072)**|消費されているリソースの説明。 詳細については、以下の説明を参照してください。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="resource_description-column"></a>resource_description 列  
 Resource_description 列には、次の有効な値があります。  
  
 **スレッドプールリソース所有者:**  
  
-   threadpool id=scheduler\<hex-address>  
  
 **並列クエリリソース所有者:**  
  
-   exchangeEvent id = {Port |パイプ}\<16 進数アドレス > WaitType =\<exchange-待機の種類 > nodeId =\<exchange-ノード id >  
  
 **Exchange-wait-type:**  
  
-   e_waitNone  
  
-   e_waitPipeNewRow  
  
-   e_waitPipeGetRow  
  
-   e_waitSynchronizeConsumerOpen  
  
-   e_waitPortOpen  
  
-   e_waitPortClose  
  
-   e_waitRange  
  
 **リソース所有者のロック:**  
  
-   \<の種類に固有の説明 > id = ロック\<ロック-16 進数 > mode =\<mode > associatedObjectId =\<関連付けられた .obj-id >  
  
     **\<種類固有の説明 > は次のようになります。**  
  
    -   データベースの場合: databaselock subresource =\<databaselock-subresource > dbid =\<db id >  
  
    -   ファイルの場合: filelock fileid =\<ファイル id > subresource =\<filelock-subresource > dbid =\<db id >  
  
    -   オブジェクトの場合: objectlock lockPartition =\<ロックパーティション id > objid =\<obj-id > subresource =\<objectlock-subresource > dbid =\<db-id >  
  
    -   ページの場合: pagelock fileid =\<ファイル id > ページ id =\<ページ id > dbid =\<db id > subresource =\<pagelock-subresource >  
  
    -   キーの場合: キーロック hobtid =\<hobt > dbid =\<db id >  
  
    -   エクステントの場合: extentlock fileid =\<ファイル id > ページ id =\<ページ id > dbid =\<db id >  
  
    -   RID の場合: ridlock fileid =\<ファイル id > ページ id =\<ページ id > dbid =\<db id >  
  
    -   アプリケーションの場合: applicationlock hash =\<hash > databasePrincipalId =\<ロール id > dbid =\<db id >  
  
    -   メタデータの場合: metadatalock subresource =\<metadata-subresource > classid =\<metadatalock > dbid =\<db id >  
  
    -   HOBT の場合: hobtlock hobtid =\<HOBT > subresource =\<HOBT-subresource > dbid =\<db-id >  
  
    -   ALLOCATION_UNIT の場合: allocunitlock hobtid =\<hobt > subresource =\<alloc-UNIT-subresource > dbid =\<db id >  
  
     **\<モード > は次のようになります。**  
  
     Sch-m-S、Sch-m、S、U、X、IS、IU、IX、SIU、6、UIX、BU、範囲-S、範囲-U、RangeI-N、RangeI-S、RangeI-U、RangeI-X、RangeX-、RangeX-U、RangeX-X  
  
 **外部リソース所有者:**  
  
-   External ExternalResource=\<wait-type>  
  
 **汎用リソース所有者:**  
  
-   TransactionMutex Transactionmutex Workspace =\<ワークスペース id >  
  
-   Mutex  
  
-   CLRTaskJoin  
  
-   CLRMonitorEvent  
  
-   CLRRWLockEvent  
  
-   resourceWait  
  
 **ラッチリソース所有者:**  
  
-   \<db-id>:\<file-id>:\<page-in-file>  
  
-   \<GUID>  
  
-   \<latch-class> (\<latch-address>)  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   
 
## <a name="example"></a>例
この例では、ブロックされているセッションを識別します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを実行します。

```sql
SELECT * FROM sys.dm_os_waiting_tasks 
WHERE blocking_session_id IS NOT NULL; 
``` 
  
## <a name="see-also"></a>参照  
[オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)      
[スレッドおよびタスクのアーキテクチャ ガイド](../../relational-databases/thread-and-task-architecture-guide.md)     
   
 
