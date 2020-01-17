---
title: MSdbms_datatype_mapping (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdbms_datatype_mapping_TSQL
- MSdbms_datatype_mapping
dev_langs:
- TSQL
helpviewer_keywords:
- MSdbms_datatype_mapping system table
ms.assetid: 13289a0b-dfb0-4771-ad80-4c5f83cded99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a1042bb3aa7b6113121693cc66440ebbf81ce1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907542"
---
# <a name="msdbms_datatype_mapping-transact-sql"></a>MSdbms_datatype_mapping (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSdbms_datatype_mapping**テーブルには、マップ先 DBMS での 1 つまたは複数の特定のデータ型を元のデータベース管理システム (DBMS) でのデータ型から使用可能なデータ型のマッピングが含まれています。 このテーブルに格納されます、 **msdb**データベースにあり、異種データベース レプリケーションに使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**datatype_mapping_id**|**int**|個々のデータ型マッピングを一意に識別します。|  
|**map_id**|**int**|ソースのデータ型を識別します。|  
|**dest_datatype_id**|**int**|変換先のデータ型を識別します。|  
|**dest_precision**|**bigint**|値が NULL の場合、有効桁数が使用されないことに、変換先のデータ型の有効桁数と値の定義 **-1**ソースのデータ型の有効桁数が使用されることを意味します。|  
|**dest_scale**|**int**|NULL の値は、小数点以下桁数が使用されていない場合、変換先のデータ型の小数点以下桁数の値を定義します **-1**ソースのデータ型の小数点以下桁数が使用されていることを意味します。|  
|**dest_length**|**bigint**|値が NULL の場合、長さが使用されないことに、変換先のデータ型の長さと値の定義 **-1**ソースのデータ型の長さを使用することを意味します。|  
|**dest_nullable**|**bit**|かどうか、変換先の列のマッピングで NULL 値が許容が値が NULL の場合、この定義が必要ないことを示します。|  
|**dest_createparams**|**int**|長さ、精度、およびスケールの組み合わせを表すビットマップを含む各データ型の適用のとおりです。<br /><br /> **0x1** = 有効桁数。<br /><br /> **0x2**スケールを = です。<br /><br /> **0x4**長さを = です。|  
  
## <a name="see-also"></a>関連項目  
 [異種データベース レプリケーション](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Oracle パブリッシャーのデータ型マッピングの指定](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [レプリケーション テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [レプリケーション ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
