---
title: ストアド プロシージャを使用した手動トレースの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 247548de6f3a89afac2143347d987a6f6d638c55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714820"
---
# <a name="create-manual-traces-using-stored-procedures"></a>ストアド プロシージャを使用した手動トレースの作成
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のインスタンスでトレースを作成するための [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]システム ストアド プロシージャが用意されています。 これらのシステム ストアド プロシージャを使用して、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]からではなく、ユーザー独自のアプリケーションからトレースを手動で作成することもできます。 これにより、企業のニーズに合わせたカスタム アプリケーションを作成できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次の表に、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスをトレースするためのシステム ストアド プロシージャを示します。  
  
|ストアド プロシージャ|実行するタスク|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql)|トレースに含まれるイベントに関する情報を返します。|  
|[sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)|指定したトレースまたはすべての既存のトレースに関する情報を返します。|  
|[sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)|トレース定義を作成します。 新しいトレースは停止状態になります。|  
|[sp_trace_generateevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql)|ユーザー定義イベントを作成します。|  
|[sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)|イベント クラスまたはデータ列をトレースに追加するか、トレースから削除します。|  
|[sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)|トレースを開始、停止、または終了します。|  
|[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql)|トレースに適用されたフィルターに関する情報を返します。|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)|新しいフィルターまたは変更されたフィルターをトレースに適用します。|  
  
 **ストアド プロシージャを使用してユーザー独自のトレースを定義するには**  
  
1.  **sp_trace_setevent**を使用して、キャプチャするイベントを指定します。  
  
2.  イベント フィルターを指定します。 詳細については、「[トレース フィルターの設定 &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)」を参照してください。  
  
3.  **sp_trace_create** を使用して、キャプチャされたイベント データの出力先を指定します。  
  
 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](../sql-trace/create-a-trace-transact-sql.md)」を参照してください。  
  
 **トレース定義の既定値を設定するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
 **トレース表示の既定値を設定するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **トレースを作成するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../sql-trace/create-a-trace-transact-sql.md)  
  
 **トレース テンプレートからイベントを追加または削除するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
