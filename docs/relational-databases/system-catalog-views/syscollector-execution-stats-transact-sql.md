---
title: syscollector_execution_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_stats
- syscollector_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_execution_stats view
- data collector view
ms.assetid: 23e35ac5-fbbf-4922-970c-f4fac44c1263
author: stevestein
ms.author: sstein
ms.openlocfilehash: bca1d879c0988ffb48eb5ae2fd080b1133e24339
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060327"
---
# <a name="syscollectorexecutionstats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  コレクション セットまたはパッケージのタスクの実行に関する情報を提供します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|各コレクション セットの実行を識別します。 このビューを他の詳細なログを結合するために使用します。 NULL 値は許可されません。|  
|**task_name**|**nvarchar(128)**|コレクションの名前は、設定またはこの情報はタスクをパッケージ化します。 NULL 値は許可されません。|  
|**execution_row_count_in**|**int**|データ フローの最初に処理された行の数。 NULL 値が許可されます。|  
|**execution_row_count_out**|**int**|データ フローの最後に処理される行数です。 NULL 値が許可されます。|  
|**execution_row_count_errors**|**int**|データ フロー中に失敗した行数です。 NULL 値が許可されます。|  
|**execution_time_ms**|**int**|タスクが完了するために必要な時間 (ミリ秒単位)。 NULL 値が許可されます。|  
|**log_time**|**datetime**|この情報が記録された時刻。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
 に対する SELECT 権限が必要です**dc_operator**します。  
  
## <a name="see-also"></a>関連項目  
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [データ コレクターのビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
