---
title: sys.dm_db_session_space_usage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_session_space_usage_TSQL
- dm_db_session_space_usage
- sys.dm_db_session_space_usage
- sys.dm_db_session_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_session_space_usage dynamic management view
ms.assetid: a67a6045-8e14-460a-9fe3-912b846c08c1
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5e4febf0882f57f7d1545f86cbe4c65e322226dc
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263969"
---
# <a name="sysdm_db_session_space_usage-transact-sql"></a>sys.dm_db_session_space_usage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  ページ割り当てし、解放は、データベースの各セッションでの数を返します。  
  
> [!NOTE]  
>  このビューはのみに適用できる、 [tempdb データベース](../../relational-databases/databases/tempdb-database.md)します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_db_session_space_usage**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**smallint**|セッション ID。<br /><br /> **session_id**マップ**session_id**で[sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)します。|  
|**database_id**|**smallint**|データベース ID。|  
|**user_objects_alloc_page_count**|**bigint**|予約された、またはこのセッションでユーザー オブジェクトに割り当てられたページ数。|  
|**user_objects_dealloc_page_count**|**bigint**|セッションで、ユーザー オブジェクトへの割り当てが解除され、予約されなくなったページの数。|  
|**internal_objects_alloc_page_count**|**bigint**|セッションで、内部オブジェクトに予約された、または割り当てられたページの数。|  
|**internal_objects_dealloc_page_count**|**bigint**|割り当てを解除し、内部オブジェクト用にこのセッションで不要になった予約ページ数。|  
|**user_objects_deferred_dealloc_page_count**|**bigint**|遅延割り当て解除のマークされているページ数。<br /><br /> **注:** サービス パックで導入された[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]と[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]します。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="remarks"></a>コメント  
 IAM ページは、このビューでレポートされる割り当てや割り当て解除の数には含まれません。  
  
 ページ カウンターはセッションの開始時に 0 に初期化されます。 このカウンターによって、セッションで完了したタスクに割り当てられた、または割り当て解除されたページの合計数が記録されます。 カウンターはタスクが終了したときにだけ更新され、実行中のタスクは反映されません。  
  
 セッションは、複数の要求を同時にアクティブに持つことができます。 要求が並列クエリの場合、複数のスレッドやタスクを開始できます。  
  
 セッション、要求、およびタスクの詳細については、[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)、 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)、および [sys.dm_os_tasks と組み合わせます&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md) を参照してください。  
  
## <a name="user-objects"></a>ユーザー オブジェクト  
 次のオブジェクトは、ユーザー オブジェクト ページ カウンターに含まれます。  
  
-   ユーザー定義テーブルとインデックス  
  
-   システム テーブルとインデックス  
  
-   グローバル一時テーブルとインデックス  
  
-   ローカル一時テーブルとインデックス  
  
-   テーブル変数  
  
-   テーブル値関数で返されるテーブル  
  
## <a name="internal-objects"></a>内部オブジェクト  
 内部オブジェクトにのみ含まれる**tempdb**します。 次のオブジェクトは、内部オブジェクト ページ カウンターに含まれます。  
  
-   カーソルまたはスプール操作と一時的なラージ オブジェクト (LOB) ストレージ用の作業テーブル  
  
-   ハッシュ結合などの操作用の作業ファイル  
  
-   並べ替え実行結果  
  
## <a name="physical-joins"></a>物理結合  
 ![Sys.dm_db_session_space_usage の物理結合](../../relational-databases/system-dynamic-management-views/media/join-dm-db-session-space-usage-1.gif "sys.dm_db_session_space_usage の物理への参加")  
  
## <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|リレーションシップ|  
|----------|--------|------------------|  
|dm_db_session_space_usage.session_id|dm_exec_sessions.session_id|一対一|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sys.dm_os_tasks と組み合わせます&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_db_task_space_usage &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)   
 [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
  



