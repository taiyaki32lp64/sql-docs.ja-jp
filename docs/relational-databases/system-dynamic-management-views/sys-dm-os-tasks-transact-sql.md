---
title: dm_os_tasks (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_tasks
- sys.dm_os_tasks_TSQL
- dm_os_tasks_TSQL
- dm_os_tasks
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_tasks dynamic management view
ms.assetid: 180a3c41-e71b-4670-819d-85ea7ef98bac
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 086065aa79ca6fba7ad84e5b7e7f99f6f462f7dd
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74164898"
---
# <a name="sysdm_os_tasks-transact-sql"></a>sys.dm_os_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスでアクティブになっているタスクごとに1行の値を返します。 タスクは、SQL Server での実行の基本単位です。 タスクの例としては、クエリ、ログイン、ログアウト、およびゴーストクリーンアップアクティビティ、チェックポイントアクティビティ、ログライター、並列再実行アクティビティなどのシステムタスクがあります。 タスクの詳細については、「[スレッドおよびタスクアーキテクチャガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。
  
> [!NOTE]  
> [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_os_tasks**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|オブジェクトのメモリ アドレス。|  
|**task_state**|**nvarchar(60)**|タスクの状態です。 次のいずれかになります。<br /><br /> PENDING: ワーカー スレッドを待機しています。<br /><br /> RUNNABLE: 実行可能ですが、クォンタムの受信を待機しています。<br /><br /> RUNNING: スケジューラで現在実行中です。<br /><br /> SUSPENDED: ワーカーがありますが、イベントを待機しています。<br /><br /> DONE: 完了しました。<br /><br /> SPINLOOP: スピンロックで停止しています。|  
|**context_switches_count**|**int**|タスクによって完了されたスケジューラ コンテキスト スイッチの数。|  
|**pending_io_count**|**int**|タスクによって実行された物理 I/O の数。|  
|**pending_io_byte_count**|**bigint**|タスクによって実行された I/O の総バイト数。|  
|**pending_io_byte_average**|**int**|タスクによって実行された I/O の平均バイト数。|  
|**scheduler_id**|**int**|親スケジューラの ID。 タスクのスケジューラ情報に対するハンドルです。 詳細については、「 [sys &#40;. dm_os_schedulers transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)」を参照してください。|  
|**session_id**|**smallint**|タスクに関連付けられているセッションの ID。|  
|**exec_context_id**|**int**|タスクに関連付けられている実行コンテキスト ID。|  
|**request_id**|**int**|タスクの要求の ID。 詳細については、「 [sys &#40;. dm_exec_requests transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)」を参照してください。|  
|**worker_address**|**varbinary(8)**|タスクを実行しているワーカーのメモリ アドレス。<br /><br /> NULL = タスクがワーカーの実行待ちとなっているか、完了したばかりであることを表します。<br /><br /> 詳細については、「 [sys &#40;. dm_os_workers transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)」を参照してください。|  
|**host_address**|**varbinary(8)**|ホストのメモリ アドレス。<br /><br /> 0 = ホストがタスクの作成に使用されなかったことを表します。 このタスクの作成に使用されたホストを特定する場合に役立ちます。<br /><br /> 詳細については、「 [sys &#40;. dm_os_hosts transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-hosts-transact-sql.md)」を参照してください。|  
|**parent_task_address**|**varbinary(8)**|オブジェクトの親であるタスクのメモリ アドレス。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="examples"></a>使用例  
  
### <a name="a-monitoring-parallel-requests"></a>A. 並列要求を監視する  
 並列で実行される要求の場合は、(\<**session_id**>、\<**request_id**>) の同じ組み合わせに対して複数の行が表示されます。 次のクエリを使用して、すべてのアクティブな要求に対する[並列処理の最大限度を構成するサーバー構成オプション](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)を検索します。  
  
> [!NOTE]  
>  **Request_id**は、セッション内で一意です。  
  
```  
SELECT  
    task_address,  
    task_state,  
    context_switches_count,  
    pending_io_count,  
    pending_io_byte_count,  
    pending_io_byte_average,  
    scheduler_id,  
    session_id,  
    exec_context_id,  
    request_id,  
    worker_address,  
    host_address  
  FROM sys.dm_os_tasks  
  ORDER BY session_id, request_id;  
```  
  
### <a name="b-associating-session-ids-with-windows-threads"></a>b. セッション ID を Windows のスレッドに関連付ける  
 次のクエリを使用して、セッション ID を Windows スレッド ID に関連付けることができます。 これにより、Windows パフォーマンス モニターでスレッドのパフォーマンスを監視できます。 このクエリでは、休止しているセッションの情報は返されません。  
  
```  
SELECT STasks.session_id, SThreads.os_thread_id  
  FROM sys.dm_os_tasks AS STasks  
  INNER JOIN sys.dm_os_threads AS SThreads  
    ON STasks.worker_address = SThreads.worker_address  
  WHERE STasks.session_id IS NOT NULL  
  ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>参照  
[オペレーティングシステム関連の動的管理ビュー &#40;の SQL Server transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)    
[スレッドおよびタスクのアーキテクチャ ガイド](../../relational-databases/thread-and-task-architecture-guide.md)     
  


