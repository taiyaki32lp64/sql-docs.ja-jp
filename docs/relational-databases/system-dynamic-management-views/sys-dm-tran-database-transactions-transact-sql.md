---
title: dm_tran_database_transactions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_database_transactions
- sys.dm_tran_database_transactions_TSQL
- dm_tran_database_transactions_TSQL
- sys.dm_tran_database_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_database_transactions dynamic management view
ms.assetid: 82a44295-4cbc-4a5b-891a-8ebaf307b8f5
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a01dc7df9a8269190ae1c1c3cf05de3adaecc662
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982311"
---
# <a name="sysdm_tran_database_transactions-transact-sql"></a>dm_tran_database_transactions (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  データベースレベルでのトランザクションに関する情報を返します。  
  
> [!NOTE]  
>  [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]からこの DMV を呼び出すには、「 **sys. dm_pdw_nodes_tran_database_transactions**」という名前を使用します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|データベース レベルではなくインスタンス レベルのトランザクションの ID。 インスタンス内のすべてのデータベースでのみ一意ですが、すべてのサーバーインスタンスで一意であるとは限りません。|  
|database_id|**int**|トランザクションが関連付けられているデータベースの ID。|  
|database_transaction_begin_time|**datetime**|データベースがトランザクションに参加した時刻。 具体的には、トランザクションのデータベース内の最初のログレコードの時刻になります。|  
|database_transaction_type|**int**|1 = 読み取り/書き込みトランザクション<br /><br /> 2 = 読み取り専用トランザクション<br /><br /> 3 = システムトランザクション|  
|database_transaction_state|**int**|1 = トランザクションは初期化されていません。<br /><br /> 3 =  トランザクションは初期化されていますが、ログ レコードが生成されていません。<br /><br /> 4 = トランザクションによってログレコードが生成されました。<br /><br /> 5 = トランザクションは準備済みです。<br /><br /> 10 = トランザクションはコミットされています。<br /><br /> 11 = トランザクションはロールバックされました。<br /><br /> 12 = トランザクションはコミット中です。 (ログレコードは生成されていますが、具体化または永続化されていません)。|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> トランザクションのデータベースで生成されたログレコードの数。|  
|database_transaction_replicate_record_count|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> レプリケートされたトランザクションのデータベースで生成されたログレコードの数。|  
|database_transaction_log_bytes_used|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> トランザクションのデータベースログ内でこれまでに使用されたバイト数。|  
|database_transaction_log_bytes_reserved|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> トランザクションのデータベース ログ内で使用するために予約されたバイト数。|  
|database_transaction_log_bytes_used_system|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> トランザクションの代用となるシステム トランザクションのデータベース ログ内でこれまでに使用されたバイト数。|  
|database_transaction_log_bytes_reserved_system|**int**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> トランザクションに代わってシステムトランザクションのデータベースログで使用するために予約されているバイト数。|  
|database_transaction_begin_lsn|**numeric(25,0)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> データベース ログ内のトランザクションに対する、開始レコードのログ シーケンス番号 (LSN)。|  
|database_transaction_last_lsn|**numeric(25,0)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> データベース ログ内のトランザクションに対して、最後に記録されたレコードの LSN。|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> データベース ログ内のトランザクションに対する、最後のセーブポイントの LSN。|  
|database_transaction_commit_lsn|**numeric(25,0)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> データベースログ内のトランザクションのコミットログレコードの LSN。|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> 最後にロールバックされた LSN。 ロールバックが行われない場合、値は MaxLSN になります。|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> 元に戻す次のレコードの LSN。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]では、`VIEW SERVER STATE` のアクセス許可が必要です。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、データベースの `VIEW DATABASE STATE` アクセス許可が必要です。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard レベルと Basic レベルでは、**サーバー管理**者または**Azure Active Directory 管理者**アカウントが必要です。   

## <a name="see-also"></a>参照  
 [dm_tran_active_transactions &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [dm_tran_session_transactions &#40;transact-sql&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


