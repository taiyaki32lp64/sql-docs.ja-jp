---
title: pdw_materialized_view_column_distribution_properties (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d62b0e25-3226-4f87-a10a-b3a0d9555e19
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 934b1ed84aa7391ad8cf47e463dd38b37408ec00
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401662"
---
# <a name="syspdw_materialized_view_column_distribution_properties-transact-sql"></a>pdw_materialized_view_column_distribution_properties (Transact-sql) 

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

具体化されたビューの列の分布情報を表示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|object_id|**通り**|列が所属するオブジェクトの ID。 |  
|column_id|**通り**|列の ID。|  
|distribution_ordinal|**tinyint**|0 = ディストリビューション列ではありません。</br> 1 = SQL Data Warehouse は、この列を使用して具体化されたビューを分散しています。|
 
## <a name="permissions"></a>アクセス許可 

VIEW DATABASE STATE 権限が必要です。

## <a name="see-also"></a>参照

[具体化されるビューを使用したパフォーマンスチューニング](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[SELECT &#40;Transact-sql&#41;として具体化されるビューを作成する](/sql/t-sql/statements/create-materialized-view-as-select-transact-sql?view=azure-sqldw-latest)   
[具体化ビュー &#40;Transact-sql&#41;の変更](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)   
[Transact-sql&#41;について説明 &#40;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[pdw_materialized_view_distribution_properties &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[pdw_materialized_view_mappings &#40;Transact-sql&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-sql&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Azure SQL Data Warehouse でサポートされているシステムビュー](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Azure SQL Data Warehouse でサポートされている t-sql ステートメント](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
