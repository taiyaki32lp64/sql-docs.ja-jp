---
title: cdc.captured_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.captured_columns
- cdc.captured_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.captured_columns
ms.assetid: 7bb4d408-d764-4ef6-802c-f271c8d39c2a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 96927e2c0a773674cbc4b8dabee804870d6559e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119258"
---
# <a name="cdccapturedcolumns-transact-sql"></a>cdc.captured_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  キャプチャ インスタンスで追跡されている各列に対して 1 つの行を返します。 既定では、ソース テーブルのすべての列がキャプチャされます。 ただし、列リストを指定することで、ソース テーブルでの変更データ キャプチャが有効になっているときに列を含めたり除外したりできます。 詳細については、次を参照してください。 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)します。  
  
 お勧めする**直接システム テーブルを照会できません**します。 代わりに、実行、 [sys.sp_cdc_get_source_columns](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)ストアド プロシージャ。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|キャプチャされた列が属するソース テーブルの ID です。|  
|**column_name**|**sysname**|キャプチャされた列の名前です。|  
|**column_id**|**int**|ソース テーブル内のキャプチャされた列の ID です。|  
|**column_type**|**sysname**|キャプチャされた列の型です。|  
|**column_ordinal**|**int**|変更テーブル内での (1 から始まる) 列序数です。 変更テーブル内のメタデータ列は除外されます。 序数 1 は、キャプチャされた最初の列に割り当てられます。|  
|**is_computed**|**bit**|キャプチャされた列がソース テーブル内で計算列であることを示します。|  
  
## <a name="see-also"></a>参照  
 [cdc.change_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
