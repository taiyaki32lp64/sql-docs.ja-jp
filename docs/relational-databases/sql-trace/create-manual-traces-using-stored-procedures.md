---
title: ストアド プロシージャを使用した手動トレースの作成
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d24b9300b5ce5d727d7e9b53c42cea4571ad066f
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095975"
---
# <a name="create-manual-traces-using-stored-procedures"></a>ストアド プロシージャを使用した手動トレースの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[tsql](../../includes/tsql-md.md)] のインスタンスでトレースを作成するための [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]システム ストアド プロシージャが用意されています。 これらのシステム ストアド プロシージャを使用して、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]からではなく、ユーザー独自のアプリケーションからトレースを手動で作成することもできます。 これにより、企業のニーズに合わせたカスタム アプリケーションを作成できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 次の表に、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスをトレースするためのシステム ストアド プロシージャを示します。  
  
|ストアド プロシージャ|実行するタスク|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)|トレースに含まれるイベントに関する情報を返します。|  
|[sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)|指定したトレースまたはすべての既存のトレースに関する情報を返します。|  
|[sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)|トレース定義を作成します。 新しいトレースは停止状態になります。|  
|[sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)|ユーザー定義イベントを作成します。|  
|[sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)|イベント クラスまたはデータ列をトレースに追加するか、トレースから削除します。|  
|[sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|トレースを開始、停止、または終了します。|  
|[sys.fn_trace_getfilterinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)|トレースに適用されたフィルターに関する情報を返します。|  
|[sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|新しいフィルターまたは変更されたフィルターをトレースに適用します。|  
  
 **ストアド プロシージャを使用してユーザー独自のトレースを定義するには**  
  
1.  **sp_trace_setevent**を使用して、キャプチャするイベントを指定します。  
  
2.  イベント フィルターを指定します。 詳細については、「[トレース フィルターの設定 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)」を参照してください。  
  
3.  **sp_trace_create** を使用して、キャプチャされたイベント データの出力先を指定します。  

 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)」を参照してください。  
  
 **トレース定義の既定値を設定するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
 **トレース表示の既定値を設定するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **トレースを作成するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
 **トレース テンプレートからイベントを追加または削除するには**  
  
 [SQL Server Profiler](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
