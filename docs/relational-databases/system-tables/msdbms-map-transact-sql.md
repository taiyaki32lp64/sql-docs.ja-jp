---
title: MSdbms_map (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_map
- MSdbms_map_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_map system table
ms.assetid: df67e691-3a50-450a-99c5-8c4a041749ae
author: stevestein
ms.author: sstein
ms.openlocfilehash: fffa30d0e252392c41cee34c1875b12b5b7a53b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907491"
---
# <a name="msdbms_map-transact-sql"></a>MSdbms_map (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_map**テーブルには、元とコピー先の DBMS の組の既定の変換先データ型の情報へのリンクだけでなく、ソース データの型情報が含まれています。 このテーブルに格納されます、 **msdb**データベース、異種パブリッシングに使用されます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**map_id**|**int**|データ型のマッピングを一意に識別します。|  
|**src_dbms_id**|**int**|指定することで、マップ元 DBMS を識別します。 その**dbms_id**で、 [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)テーブル。|  
|**dest_dbms_id**|**int**|指定することで、マップ先 DBMS を識別します。 その**dbms_id**で、 [MSdbms](../../relational-databases/system-tables/msdbms-transact-sql.md)テーブル。|  
|**src_datatype_id**|**int**|識別、 **datatype_id**から、 [MSdbms_datatype](../../relational-databases/system-tables/msdbms-datatype-transact-sql.md)テーブルのソース データの種類。|  
|**src_len_min**|**bigint**|マップ元 DBMS におけるデータ型の最小の長さ。値 NULL は長さが使用されないことを示します。|  
|**src_len_max**|**bigint**|マップ元 DBMS で NULL 値が長さが使用されないことを示すにおけるデータ型の最大長。|  
|**src_prec_min**|**bigint**|マップ元 DBMS で NULL 値が有効桁数が使用されないことを示すにおけるデータ型の最小有効桁数。|  
|**src_prec_max**|**bigint**|マップ元 DBMS で NULL 値が有効桁数が使用されないことを示すにおけるデータ型の最大有効桁数。|  
|**src_scale_min**|**int**|マップ元 DBMS で NULL 値がスケールが使用されないことを示すにおけるデータ型の最小のスケール。|  
|**src_scale_max**|**int**|マップ元 DBMS におけるデータ型の最大小数点以下桁数。値 NULL は小数点以下桁数が使用されないことを示します。|  
|**src_nullable**|**bit**|かどうか、変換先の列のマッピングで NULL 値が許容が値が NULL の場合、この定義が必要ないことを示します。|  
|**default_datatype_mapping_id**|**int**|指定することで、既定のデータ型マッピングを識別します。 その**map_id**テーブル[MSdbms_datatype_mapping](../../relational-databases/system-tables/msdbms-datatype-mapping-transact-sql.md)します。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
