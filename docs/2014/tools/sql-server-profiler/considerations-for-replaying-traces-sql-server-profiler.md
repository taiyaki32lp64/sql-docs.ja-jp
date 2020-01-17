---
title: トレースの再生に関する注意点 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 73fa339f-b71a-4be4-97ca-d4ae84c8b90b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2dd2fe9f5e4e2a5b41c9951b1a38dd819a15aa35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316041"
---
# <a name="considerations-for-replaying-traces-sql-server-profiler"></a>トレースの再生に関する注意点 (SQL Server Profiler)
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、次の種類のトレースを再生できません。  
  
-   トランザクション レプリケーションや他のトランザクションのログ利用状況を含むトレース。 このようなイベントはスキップされます。 他の種類のレプリケーションではトランザクション ログが記録されないので、そのようなレプリケーションは影響を受けません。  
  
-   グローバル一意識別子 (GUID) を必要とする操作を含むトレース。 このようなイベントはスキップされます。  
  
-   **bcp**ユーティリティ、BULK INSERT、READTEXT、WRITETEXT、UPDATETEXT ステートメントを必要とする **text**列、 **ntext** 列、および **image** 列での操作やフルテキスト操作を含むトレース。 このようなイベントはスキップされます。  
  
-   セッションをバインドする **sp_getbindtoken** および **sp_bindsession** システム ストアド プロシージャを含むトレース。 このようなイベントはスキップされます。  
  
> [!NOTE]  
>  あらかじめ構成された再生テンプレート (**TSQL_Replay**) を使用せず、必要なすべてのデータをキャプチャしていないトレースは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では再生されません。 詳細については、「 [再生を実行するための必要条件](replay-requirements.md)」を参照してください。  
  
 トレースの再生に必要な権限の詳細については、「 [SQL Server Profiler の実行に必要な権限](sql-server-profiler.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [bcp Utility](../bcp-utility.md)   
 [SQL Server イベント クラスの参照](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)   
 [sp_bindsession &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [READTEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/readtext-transact-sql)   
 [WRITETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/writetext-transact-sql)   
 [UPDATETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/updatetext-transact-sql)  
  
  
