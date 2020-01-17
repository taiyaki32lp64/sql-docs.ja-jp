---
title: sys.dm_tran_active_snapshot_database_transactions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_active_snapshot_database_transactions_TSQL
- dm_tran_active_snapshot_database_transactions
- sys.dm_tran_active_snapshot_database_transactions
- dm_tran_active_snapshot_database_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_snapshot_database_transactions dynamic management view
ms.assetid: 55b83f9c-da10-4e65-9846-f4ef3c0c0f36
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a17fb16130aea073c7a878334ac78b0347267b6b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262700"
---
# <a name="sysdmtranactivesnapshotdatabasetransactions-transact-sql"></a>sys.dm_tran_active_snapshot_database_transactions (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスでは、この動的管理ビューが生成または行のバージョンにアクセスする可能性のあるすべてのアクティブなトランザクションの仮想テーブルを返します。 トランザクションは、次の条件を 1 つ以上満たします。  
  
-   ALLOW_SNAPSHOT_ISOLATION データベース オプションと READ_COMMITTED_SNAPSHOT データベース オプションのいずれかまたは両方が ON に設定されている場合、  
  
    -   スナップショット分離レベルまたは行のバージョン管理を使用する read committed 分離レベルで実行されているトランザクションごとに 1 つの行があります。  
  
    -   現在のデータベースに行バージョンを作成するトランザクションごとに、1 行のデータが存在する。 たとえば、トランザクションは、更新または現在のデータベース内の行を削除するで行バージョンを生成します。  
  
-   トリガーが起動される場合、トリガーが実行されるトランザクションごとに 1 行のデータが存在する。  
  
-   オンライン インデックス処理中に、インデックスを作成しているトランザクションごとに 1 行のデータが存在する。  
  
-   複数のアクティブな結果セット (MARS) セッションを有効にすると、行のバージョンにアクセスしているトランザクションごとに 1 つの行があります。  
  
 この動的管理ビューでは、システム トランザクションは含まれません。  
  
> [!NOTE]  
>  これから[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]または[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]、名前を使用して、 **sys.dm_pdw_nodes_tran_active_snapshot_database_transactions**します。  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.dm_tran_active_snapshot_database_transactions  
```  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|トランザクションに割り当てられている一意な識別番号。 トランザクション ID は、主にロック操作でトランザクションを識別するために使用します。|  
|**transaction_sequence_num**|**bigint**|トランザクション シーケンス番号。 これは、開始時にトランザクションに割り当てられている一意のシーケンス番号です。 バージョン レコードを生成せず、スナップショット スキャンを行わないトランザクションには、トランザクション シーケンス番号は割り当てられません。|  
|**commit_sequence_num**|**bigint**|トランザクションが完了 (コミットまたは停止) したことを示すシーケンス番号。 アクティブなトランザクションは、値は NULL です。|  
|**is_snapshot**|**int**|0 = スナップショット分離トランザクションではありません。<br /><br /> 1 = スナップショット分離トランザクションです。|  
|**session_id**|**int**|トランザクションを開始したセッションの ID。|  
|**first_snapshot_sequence_num**|**bigint**|スナップショットが取得されたときにアクティブだったトランザクションの最小トランザクション シーケンス番号。 実行には、スナップショット トランザクションは、その時点でアクティブなトランザクションのすべてのスナップショットを取得します。 スナップショット トランザクションの場合は、この列には、0 が表示されます。|  
|**max_version_chain_traversed**|**int**|トランザクション全体で一貫性のあるバージョンを検索するためにスキャンされるバージョン チェーンの最大長。|  
|**average_version_chain_traversed**|**real**|スキャンされるバージョン チェーン内の行バージョンの平均数。|  
|**elapsed_time_seconds**|**bigint**|トランザクションからの経過時間は、そのトランザクション シーケンス番号を取得します。|  
|**pdw_node_id**|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> この配布であるノードの識別子。|  
  
## <a name="permissions"></a>アクセス許可

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="remarks"></a>コメント  
 **sys.dm_tran_active_snapshot_database_transactions**トランザクション シーケンス番号 (XSN) が割り当てられているトランザクションを報告します。 トランザクションは、バージョン ストアを最初にアクセスした場合は、XSN が割り当てられます。 行のバージョン管理を使用するスナップショット分離または READ COMMITTED 分離が有効なデータベースにおいて、XSN がトランザクションに割り当てられるときの例を次に示します。  
  
-   トランザクションが serializable 分離レベルで実行している場合は、トランザクションが最初に作成される行バージョンを原因となる、更新操作などのステートメントを実行するときに XSN が割り当てられます。  
  
-   トランザクションがスナップショット分離下で実行している場合、データ操作言語 (DML) ステートメント、SELECT 操作などが実行されたときに XSN が割り当てられます。  
  
 トランザクション シーケンス番号は、[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスでトランザクションが開始されるたびに増分されます。  
  
## <a name="examples"></a>使用例  
 次の例では、4 つの同時実行トランザクションが存在するテスト シナリオを使用します。これらのトランザクションはそれぞれトランザクション シーケンス番号 (XSN) で識別され、ALLOW_SNAPSHOT_ISOLATION オプションと READ_COMMITTED_SNAPSHOT オプションが ON に設定されているデータベース内で実行されます。 実行されるトランザクションは次のとおりです。  
  
-   XSN-57。SERIALIZABLE 分離での更新操作です。  
  
-   Xsn-58 では、xsn-57 と同じです。  
  
-   Xsn-59 がスナップショット分離下で選択の操作  
  
-   Xsn-60 では、同じ xsn-59 とします。  
  
 次のクエリを実行します。  
  
```  
SELECT   
    transaction_id,  
    transaction_sequence_num,  
    commit_sequence_num,  
    is_snapshot session_id,  
    first_snapshot_sequence_num,  
    max_version_chain_traversed,  
    average_version_chain_traversed,  
    elapsed_time_seconds  
  FROM sys.dm_tran_active_snapshot_database_transactions;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_id  transaction_sequence_num  commit_sequence_num  
--------------  ------------------------  -------------------  
9295            57                        NULL  
9324            58                        NULL  
9387            59                        NULL  
9400            60                        NULL  
  
is_snapshot  session_id   first_snapshot_sequence_num  
-----------  -----------  ---------------------------  
0            54           0  
0            53           0  
1            52           57  
1            51           57  
  
max_version_chain_traversed  average_version_chain_traversed  
---------------------------  -------------------------------  
0                            0  
0                            0  
1                            1  
1                            1  
  
elapsed_time_seconds  
--------------------  
419  
397  
359  
333  
```  
  
 次の情報の評価の結果を**sys.dm_tran_active_snapshot_database_transactions**:  
  
-   XSN-57:このトランザクションがスナップショット分離で実行されていないため、`is_snapshot`値と`first_snapshot_sequence_num`は`0`します。 `transaction_sequence_num` 1 つまたは両方 ALLOW_SNAPSHOT_ISOLATION または READ_COMMITTED_SNAPSHOT データベース オプションが ON であるため、このトランザクションにトランザクション シーケンス番号が割り当てられていることを示します。  
  
-   XSN-58:このトランザクションがスナップショット分離下で実行されていないと、xsn-57 と同じ情報が適用されます。  
  
-   XSN-59:これは、スナップショット分離で実行されている最初のアクティブなトランザクションです。 示すとおり、このトランザクションは、xsn-57 より前にコミットされたデータを読み取ります`first_snapshot_sequence_num`します。 このトランザクションの出力では、1 行にスキャンされるバージョン チェーンの最大長が `1` で、アクセスした行ごとに平均で `1` つのバージョンがスキャンされていることも示されています。 これは、トランザクション XSN-57、XSN-58、および XSN-60 では行が変更されずコミットされていないことを表します。  
  
-   XSN-60:これは、2 番目のスナップショット分離下で実行されているトランザクションです。 出力では、XSN-59 と同じ情報が示されます。  
  
## <a name="see-also"></a>関連項目  
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


