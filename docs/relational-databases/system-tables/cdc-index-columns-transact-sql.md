---
title: cdc.index_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 69ed86e55cadf6c594ca764874bc1257c6d1a9a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035344"
---
# <a name="cdcindexcolumns-transact-sql"></a>cdc.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  変更テーブルに関連付けられた各インデックス列について、対応する 1 行を返します。 インデックス列は、変更データ キャプチャ時に、ソース テーブル内の行を一意に識別するために使用されます。 既定では、ソース テーブルの主キー列が含まれます。 ただし、ソース テーブルに対して変更データ キャプチャを有効にする際、ソース テーブルの一意のインデックスが指定された場合は、代わりにそのインデックスの列が使用されます。 差分変更の追跡を有効にする場合は、ソース テーブルに主キーまたは一意のインデックスが必要です。 詳細については、次を参照してください。 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)します。  
  
 システム テーブルに対して直接クエリを実行することは、できるだけ避けてください。 代わりに、実行、 [sys.sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)ストアド プロシージャ。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|変更テーブルの ID です。|  
|**column_name**|**sysname**|インデックス列の名前。|  
|**index_ordinal**|**tinyint**|インデックス内の列の 1 から始まる序数。|  
|**column_id**|**int**|ソース テーブル内の列の ID です。|  
  
## <a name="see-also"></a>参照  
 [cdc.change_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
