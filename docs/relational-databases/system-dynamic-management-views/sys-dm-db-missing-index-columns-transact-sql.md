---
title: sys.dm_db_missing_index_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns_TSQL
- sys.dm_db_missing_index_columns
- dm_db_missing_index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_columns dynamic management function
- missing indexes feature [SQL Server], sys.dm_db_missing_index_columns dynamic management function
ms.assetid: 3b24e5ed-0c79-47e5-805c-a0902d0aeb86
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 38d21e20ec158ea316caf6acd17f7225c8d3a49d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002653"
---
# <a name="sysdmdbmissingindexcolumns-transact-sql"></a>sys.dm_db_missing_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  空間インデックスを除く、インデックスのないデータベース テーブル列に関する情報を返します。 **sys.dm_db_missing_index_columns**は動的管理関数です。  

## <a name="syntax"></a>構文  
  
```  
  
sys.dm_db_missing_index_columns(index_handle)  
```  
  
## <a name="arguments"></a>引数  
 *index_handle*  
 不足インデックスを一意に識別する整数です。 次の動的管理オブジェクトから取得できます。  
  
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)  
  
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|列の ID です。|  
|**column_name**|**sysname**|テーブル列の名前。|  
|**column_usage**|**varchar(20)**|クエリで列の使用方法です。 使用可能な値とその説明のとおり。<br /><br /> 等しいかどうか。列は、フォームの等しいかどうかを表す述語に役立ちます。 <br />                        *table.column* = *constant_value*<br /><br /> 非等値:たとえば、非等値を表す述語にフォームの述語貢献する列: *table.column* > *constant_value*します。 "=" 以外の比較演算子はすべて、不等値を表します。<br /><br /> 次のとおり列は、述語の評価には使用されませんが、クエリをカバーするなどの理由により使用されます。|  
  
## <a name="remarks"></a>コメント  
 によって返される情報**sys.dm_db_missing_index_columns**クエリが、クエリ オプティマイザーによって最適化されて永続化されていないときに更新されます。 欠落インデックスの情報が保持されるのは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の再起動までです。 欠落インデックスの情報を、サーバーの再利用後も保持する場合は、データベース管理者が情報のバックアップ コピーを定期的に作成する必要があります。  
  
## <a name="transaction-consistency"></a>トランザクションの一貫性  
 トランザクションでテーブルを作成または削除する場合、削除されたオブジェクトに関する欠落インデックス情報を含む行は、トランザクションの一貫性を保持するためこの動的管理オブジェクトから削除されます。  
  
## <a name="permissions"></a>アクセス許可  
 この動的管理関数をクエリするには、VIEW SERVER STATE 権限、または VIEW SERVER STATE が暗黙的に与えられる権限が許可されている必要があります。  
  
## <a name="examples"></a>使用例  
 に対してクエリを実行する次の使用例、`Address`テーブルが表示され、クエリを使用してを実行し、`sys.dm_db_missing_index_columns`動的管理ビューは、インデックスのないテーブルの列を返すにします。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode  
FROM Person.Address  
WHERE StateProvinceID = 9;  
GO  
SELECT mig.*, statement AS table_name,  
    column_id, column_name, column_usage  
FROM sys.dm_db_missing_index_details AS mid  
CROSS APPLY sys.dm_db_missing_index_columns (mid.index_handle)  
INNER JOIN sys.dm_db_missing_index_groups AS mig ON mig.index_handle = mid.index_handle  
ORDER BY mig.index_group_handle, mig.index_handle, column_id;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
