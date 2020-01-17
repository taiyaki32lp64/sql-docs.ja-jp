---
title: sys.trace_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.trace_columns
- trace_columns
- trace_columns_TSQL
- sys.trace_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trace_columns catalog view
ms.assetid: 5c48eb09-9e9b-45dd-b151-ca39b026ece5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bda45d55505356594f23a8bb1ece2e95153206a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022656"
---
# <a name="systracecolumns-transact-sql"></a>sys.trace_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sys.trace_columns**カタログ ビューには、すべてのトレース イベント列の一覧が含まれています。 これらの列がの指定したバージョンは変更しないでください、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]します。  
  
 サポートされているトレース イベントの完全な一覧を参照してください。 [SQL Server Event Class Reference](../../relational-databases/event-classes/sql-server-event-class-reference.md)します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 拡張イベント カタログ ビューを代わりに使用します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**trace_column_id**|**smallint**|この列の一意の ID。|  
|**name**|**nvarchar(128)**|この列の一意の名前。 このパラメーターはローカライズされません。|  
|**type_name**|**nvarchar(128)**|データは、この列の名前を入力します。|  
|**max_size**|**int**|この列のバイト単位の最大データ サイズ。|  
|**is_filterable**|**bit**|フィルターの指定に列を使用できるかどうか。<br /><br /> 0 = false<br /><br /> 1 = true|  
|**is_repeatable**|**bit**|"繰り返し列" のデータで列を参照できるかどうか。<br /><br /> 0 = false<br /><br /> 1 = true|  
|**is_repeated_base**|**bit**|繰り返しデータを参照する一意のキーとして、この列を使用できるかどうか。<br /><br /> 0 = false<br /><br /> 1 = true|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [sys.traces &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-traces-transact-sql.md)   
 [sys.trace_categories &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-categories-transact-sql.md)   
 [sys.trace_events &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-events-transact-sql.md)   
 [sys.trace_event_bindings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-event-bindings-transact-sql.md)   
 [sys.trace_subclass_values &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-trace-subclass-values-transact-sql.md)  
  
  
