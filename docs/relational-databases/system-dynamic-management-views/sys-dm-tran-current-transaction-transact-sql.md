---
title: sys.dm_tran_current_transaction (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_current_transaction
- sys.dm_tran_current_transaction_TSQL
- dm_tran_current_transaction_TSQL
- dm_tran_current_transaction
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_current_transaction dynamic management view
ms.assetid: 75d5697d-b390-4963-99b8-fa0b4244a40c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4d1817910457d9d4e46dd1f923058ce98f02f51e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262630"
---
# <a name="sysdmtrancurrenttransaction-transact-sql"></a>sys.dm_tran_current_transaction (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  現在のセッションでトランザクションの状態情報を表示する 1 つの行を返します。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_tran_current_transaction**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_tran_current_transaction  
```  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|現在のスナップショットのトランザクション ID。|  
|**transaction_sequence_num**|**bigint**|レコードのバージョンを生成するトランザクションのシーケンス番号。|  
|**transaction_is_snapshot**|**bit**|スナップショット分離の状態。 トランザクションがスナップショット分離に基づいて開始された場合、この値は 1 です。 それ以外の場合、値は 0 です。|  
|**first_snapshot_sequence_num**|**bigint**|スナップショットが取得されたときにアクティブだったトランザクションの最小トランザクション シーケンス番号。 実行には、スナップショット トランザクションは、その時点でアクティブなトランザクションのすべてのスナップショットを取得します。 スナップショット トランザクションの場合は、この列には、0 が表示されます。|  
|**last_transaction_sequence_num**|**bigint**|グローバル シーケンス番号。 この値は、システムにより生成された最後のトランザクション シーケンス番号を表します。|  
|**first_useful_sequence_num**|**bigint**|グローバル シーケンス番号。 この値は、行バージョンをバージョン ストアに保持する必要があるトランザクションの、最も古いトランザクション シーケンス番号を表します。 以前のトランザクションによって作成された行のバージョンを削除することができます。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   
  
## <a name="examples"></a>使用例  
 次の例では、4 つの同時実行トランザクションが存在するテスト シナリオを使用します。これらのトランザクションはそれぞれトランザクション シーケンス番号 (XSN) で識別され、ALLOW_SNAPSHOT_ISOLATION オプションと READ_COMMITTED_SNAPSHOT オプションが ON に設定されているデータベース内で実行されます。 実行されるトランザクションは次のとおりです。  
  
-   XSN-57。SERIALIZABLE 分離での更新操作です。  
  
-   Xsn-58 では、xsn-57 と同じです。  
  
-   Xsn-59 では、スナップショット分離下で選択操作です。  
  
-   Xsn-60 では、xsn-59 と同じです。  
  
 次のクエリは、各トランザクションのスコープ内で実行されます。  
  
```  
SELECT   
    transaction_id  
   ,transaction_sequence_num  
   ,transaction_is_snapshot  
   ,first_snapshot_sequence_num  
   ,last_transaction_sequence_num  
   ,first_useful_sequence_num  
  FROM sys.dm_tran_current_transaction;  
```  
  
 ここでは、xsn-59 の結果です。  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9387                 59                       1                         
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
57                               61                        
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 出力は、xsn-59 がスナップショット トランザクション xsn-59 の開始時にアクティブだった最初のトランザクションとして xsn-57 を使用するを示します。 つまり、XSN-59 では、トランザクション シーケンス番号が XSN-57 より低いトランザクションによってコミットされたデータが読み取られます。  
  
 Xsn-57 の結果を次に示します。  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9295                 57                       0  
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
NULL                        61  
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 Xsn-57 がスナップショット トランザクションではないため`first_snapshot_sequence_num`は`NULL`します。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


