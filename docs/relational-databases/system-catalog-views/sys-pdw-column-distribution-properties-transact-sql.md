---
title: pdw_column_distribution_properties (Transact-sql)
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5b71df1a25a9cd8480f23dc104792ad8f3e70f35
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401692"
---
# <a name="syspdw_column_distribution_properties-transact-sql"></a>pdw_column_distribution_properties (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  列の分布情報を保持します。  
  
|列名|データ型|説明|Range|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**通り**|列が所属するオブジェクトの ID。||  
|**column_id**|**通り**|列の ID。||  
|**distribution_ordinal**|**tinyint**|分布のセット内の序数 (1 から始まる)。|0 = ディストリビューション列ではありません。 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]この列を使用して、親テーブルを配布します。|  
  
## <a name="see-also"></a>参照  
 [SQL Data Warehouse および並列データウェアハウスのカタログビュー](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
