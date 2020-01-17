---
title: sys.function_order_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: stevestein
ms.author: sstein
ms.openlocfilehash: a2a51cc56b37325d760ca77f014594496c8ab6b5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122747"
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列の一部であるごとに 1 行を返します、**順序**列ごと言語ランタイム (CLR) テーブル値関数の式を指定します。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|順序が定義されているオブジェクト (CLR テーブル値関数) の ID です。|  
|**order_column_id**|**int**|順序列の ID です **order_column_id**内でのみ一意です**object_id**します。<br /><br /> **order_column_id**順序付けにおけるこの列の位置を表します。|  
|**column_id**|**int**|内の列の ID **object_id**します。<br /><br /> **column_id**内でのみ一意です**object_id**します。|  
|**is_descending**|**bit**|1 = 順序列には、降順の並べ替え方向。<br /><br /> 0 = 順序列には昇順の並べ替え方向。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
