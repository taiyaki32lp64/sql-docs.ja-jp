---
title: sys.dm_tran_session_transactions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_session_transactions
- sys.dm_tran_session_transactions
- sys.dm_tran_session_transactions_TSQL
- dm_tran_session_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_session_transactions dynamic management view
ms.assetid: c7157491-58c2-49fe-87d7-0c9723113adf
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 148cab2122a907c138a2bd74c5f3403d231e2793
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262670"
---
# <a name="sysdmtransessiontransactions-transact-sql"></a>sys.dm_tran_session_transactions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  関連付けられているトランザクションやセッションの相関関係情報を返します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_tran_session_transactions**します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|session_id|**int**|トランザクションを実行中のセッションの ID。|  
|transaction_id|**bigint**|トランザクションの ID。|  
|transaction_descriptor|**binary(8)**|使用されるトランザクション識別子[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クライアント ドライバーと通信するとき。|  
|enlist_count|**int**|トランザクションの処理中のセッションにアクティブな要求の数。|  
|is_user_transaction|**bit**|1 = ユーザーの要求によって開始されたトランザクション。<br /><br /> 0 = システム トランザクション。|  
|is_local|**bit**|1 = ローカル トランザクション。<br /><br /> 0 = 分散トランザクションまたはバインドされたセッションが参加しているトランザクションです。|  
|is_enlisted|**bit**|1 = 参加している分散トランザクション。<br /><br /> 0 = 参加している分散トランザクションではない。|  
|is_bound|**bit**|1 = トランザクションは、バインドされたセッションを介したセッションでアクティブです。<br /><br /> 0 = トランザクションは、バインドされたセッションを介したセッションでアクティブではありません。|  
|open_transaction_count||各セッションの開いているトランザクションの数。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="remarks"></a>コメント  
 バインドされたセッションと分散トランザクションでは、トランザクションで複数の 1 つのセッションが実行されている可能性があります。 このような場合、sys.dm_tran_session_transactions では、同じ transaction_id を持つ複数の行が表示されます。つまり、トランザクションが実行中のセッションごとに 1 行ずつ表示されます。  
  
 複数のアクティブな結果セット (MARS) を使用する自動コミット モードで複数の要求を実行すると、1 つのセッションに複数のアクティブなトランザクションを含めることができます。 このような場合、sys.dm_tran_session_transactions では、同じ session_id を持つ複数の行が表示されます。つまり、そのセッションで実行中のトランザクションごとに 1 行ずつ表示されます。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


