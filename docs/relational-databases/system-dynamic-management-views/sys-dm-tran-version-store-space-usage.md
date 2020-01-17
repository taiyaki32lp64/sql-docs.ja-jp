---
title: sys.dm_tran_version_store_space_usage (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 04/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_space_usage_TSQL
- sys.dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage
- dm_tran_version_store_space_usage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store_space_usage dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: savjani
ms.author: pariks
manager: ajayj
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a4fac732f784a401206f37fb2af9d3d8e0688ba
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262662"
---
# <a name="sysdmtranversionstorespaceusage-transact-sql"></a>sys.dm_tran_version_store_space_usage (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-2016sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2016sp2-asdb-xxxx-xxx-md.md)]

各データベースのバージョン ストア レコードで使われている tempdb の領域の合計を表示するテーブルを返します。 **sys.dm_tran_version_store_space_usage**効率的でが高く低コストの個別のバージョン ストア レコードを移動しないと返しますデータベースごとに tempdb で消費されるバージョン ストア領域の集計を実行します。
  
バージョン管理された各レコードは、いくつかの追跡または状態情報と共に、バイナリ データとして格納されます。 データベース テーブル内のレコードと同様、バージョン ストア レコードは 8,192 バイトのページに格納されます。 レコードが 8,192 バイトを超える場合は、2 つのレコードに分割されます。  
  
バージョン レコードはバイナリであるため、異なるデータベース照合順序の異なる問題はありません。 使用**sys.dm_tran_version_store_space_usage** tempdb のサイズの SQL Server インスタンスのデータベース バージョン ストア領域の使用量に基づくを監視して計画します。
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|データベースのデータベース ID。|  
|**reserved_page_count**|**bigint**|Tempdb のバージョンで予約済みページの合計数は、データベースのレコードを格納します。|  
|**reserved_space_kb**|**bigint**|バージョンの tempdb のキロバイト単位で使用される領域の合計は、データベースのレコードを格納します。|  
  
## <a name="permissions"></a>アクセス許可  
[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   

## <a name="examples"></a>使用例  
内の各データベースのバージョン ストアによって、tempdb で消費される領域を決定する、次のクエリを使用できます、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンス。 
  
```sql  
SELECT 
  DB_NAME(database_id) as 'Database Name',
  reserved_page_count,
  reserved_space_kb 
FROM sys.dm_tran_version_store_space_usage;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Database Name            reserved_page_count reserved_space_kb  
------------------------ -------------------- -----------  
msdb                      0                    0             
AdventureWorks2016        10                   80             
AdventureWorks2016DW      0                    0             
WideWorldImporters        20                   160             
```
 
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
