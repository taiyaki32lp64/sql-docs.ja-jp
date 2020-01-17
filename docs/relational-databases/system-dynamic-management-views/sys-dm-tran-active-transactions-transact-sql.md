---
title: sys.dm_tran_active_transactions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_transactions
- sys.dm_tran_active_transactions_TSQL
- dm_tran_active_transactions_TSQL
- dm_tran_active_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_transactions dynamic management view
ms.assetid: 154ad6ae-5455-4ed2-b014-e443abe2c6ee
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 138a44184276e1eecc524747ad801df7a8991482
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262679"
---
# <a name="sysdmtranactivetransactions-transact-sql"></a>sys.dm_tran_active_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのトランザクションに関する情報を返します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_tran_active_transactions**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|データベース レベルではなくインスタンス レベルのトランザクションの ID。 インスタンス内のすべてのデータベース間でユニークであるが、すべてのサーバー インスタンス間で一意ではありません。|  
|NAME|**nvarchar(32)**|トランザクション名。 トランザクションがマークされている場合、この名前が上書きされます。マークされた名前がトランザクション名と置き換わります。|  
|transaction_begin_time|**datetime**|トランザクションの開始時刻。|  
|transaction_type|**int**|トランザクションのタイプ。<br /><br /> 1 = 読み取り/書き込みトランザクション<br /><br /> 2 = 読み取り専用トランザクション<br /><br /> 3 = システム トランザクション<br /><br /> 4 = 分散トランザクション|  
|transaction_uow|**uniqueidentifier**|トランザクション単位の分散トランザクションの作業 (UOW) 識別子。 MS DTC では UOW 識別子を使って分散トランザクションが処理されます。|  
|transaction_state|**int**|0 = トランザクションが完全に初期化されていません。<br /><br /> 1 = トランザクションは初期化されていますが、開始されていません。<br /><br /> 2 = トランザクションはアクティブです。<br /><br /> 3 = トランザクションは終了しました。 これは、読み取り専用トランザクションに使用されます。<br /><br /> 4 = コミット分散トランザクションの処理が開始されました。 これは、分散トランザクションのみに使用されます。 分散トランザクションはまだアクティブですが、追加の処理は行えません。<br /><br /> 5 = トランザクションは準備された状態で解決を待機しています。<br /><br /> 6 = トランザクションはコミットされました。<br /><br /> 7 = トランザクションはロールバック中です。<br /><br /> 8 = トランザクションはロールバックされています。|  
|transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_state|**int**|**適用対象**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (初回のリリースから[現在のリリース](https://go.microsoft.com/fwlink/p/?LinkId=299659))。<br /><br /> 1 = アクティブ<br /><br /> 2 = PREPARED<br /><br /> 3 = COMMITTED<br /><br /> 4 = 中止<br /><br /> 5 = 回復|  
|dtc_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|dtc_isolation_level|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|filestream_transaction_id|**varbinary (128)**|**適用対象**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] (初回のリリースから[現在のリリース](https://go.microsoft.com/fwlink/p/?LinkId=299659))。<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="see-also"></a>関連項目  
 [sys.dm_tran_session_transactions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [sys.dm_tran_database_transactions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


