---
title: pdw_table_distribution_properties (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 43974e2ae8becb5ad24daf0c52246a71c890bce2
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822165"
---
# <a name="syspdw_table_distribution_properties-transact-sql"></a>pdw_table_distribution_properties (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  テーブルの分布情報を保持します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**通り**|プロパティが指定されたテーブルの ID。||  
|**distribution_policy**|**tinyint**|0 = 未定義<br /><br /> 1 = なし<br /><br /> 2 = ハッシュ<br /><br /> 3 = レプリケート<br /><br /> 4 = ROUND_ROBIN||  
|**distribution_policy_desc**|**nvarchar (60)**|UNDEFINED、NONE、HASH、REPLICATE、ROUND_ROBIN|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]ハッシュ、ROUND_ROBIN、またはレプリケートを返します。|  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
