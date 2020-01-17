---
title: sys.dm_exec_valid_use_hints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c6fcaa491f7d42e255ed329a8e16798437aa2c7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936790"
---
# <a name="sysdmexecvalidusehints-transact-sql"></a>sys.dm_exec_valid_use_hints (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

返します[USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint)ヒント名がサポートされています。 行ごとに 1 つのヒント名が一覧表示します。  
  
この DMV を使用して、USE HINT 表記法でサポートされているすべてのヒントの一覧を参照してください。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|NAME|**sysname**|ヒントの名前。|

参照してください[クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)の各ヒントについて説明します。

導入された[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]SP1。
  
## <a name="see-also"></a>関連項目  
    
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [データベース関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

