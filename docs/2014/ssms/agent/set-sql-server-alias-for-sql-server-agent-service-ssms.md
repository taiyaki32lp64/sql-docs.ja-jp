---
title: トレース フィルターの設定 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 7b976a84-7381-43a6-a828-ba83ada71cbe
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6e3ecc4b125d226fc2cdf6dbe241e0ce017eae6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245939"
---
# <a name="set-a-trace-filter-transact-sql"></a>トレース フィルターの設定 (Transact-SQL)
  このトピックでは、ストアド プロシージャを使用して、トレース中のイベントに関して必要な情報のみを取得するフィルターを作成する方法について説明します。  
  
### <a name="to-set-a-trace-filter"></a>トレース フィルターを設定するには  
  
1.  トレースが既に実行中の場合は、 **@status = 0** を指定して **sp_trace_setstatus** を実行し、トレースを停止します。  
  
2.  **sp_trace_setfilter** を実行して、トレース中のイベントに関して取得する情報の種類を構成します。  
  
> [!IMPORTANT]
>  通常のストアド プロシージャとは異なり、すべての [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ストアド プロシージャ (<strong>sp_trace_*xx*</strong>) で、パラメーターのデータ型が厳密に定義されており、データ型の自動変換はサポートしていません。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
## <a name="see-also"></a>参照  
 [トレースへのフィルターの適用](../../relational-databases/sql-trace/filter-a-trace.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler のストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
