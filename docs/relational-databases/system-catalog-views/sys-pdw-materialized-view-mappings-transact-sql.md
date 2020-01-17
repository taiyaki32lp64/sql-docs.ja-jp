---
title: pdw_materialized_view_mappings (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: d548291653b589d973c9c21813690a61a0fdb7ba
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729825"
---
# <a name="syspdw_materialized_view_mappings-transact-sql"></a>pdw_materialized_view_mappings (Transact-sql)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

具体化されたビューを object_id によって内部オブジェクト名と結び付けます。

列 physical_name および object_id は、このカタログビューのキーを形成します。
  
|列名|[データ型]|[説明]|  
|-----------------|---------------|-----------------|  
|physical_name |**nvarchar(36)**|具体化されたビューの物理名。|  
|object_id  |**int**|具体化されたビューのオブジェクト ID。 「 [Sys (transact-sql)](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql?view=azure-sqldw-latest)」を参照してください。| 

## <a name="permissions"></a>アクセス許可

VIEW DATABASE STATE 権限が必要です。
  
## <a name="see-also"></a>参照

[具体化されたビューを使用したパフォーマンス チューニング](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse and Parallel Data Warehouse Catalog Views (SQL Data Warehouse および Parallel Data Warehouse のカタログ ビュー)](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[System views supported in Azure SQL Data Warehouse (Azure SQL Data Warehouse でサポートされるシステム ビュー)](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[T-SQL statements supported in Azure SQL Data Warehouse (Azure SQL Data Warehouse でサポートされる T-SQL ステートメント)](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements) 
