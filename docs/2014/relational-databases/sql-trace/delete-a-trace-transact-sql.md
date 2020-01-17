---
title: トレースの削除 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], deleting
- removing traces
- deleting traces
ms.assetid: a5502814-b281-42dd-b885-5c9368025ae6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 57d80824ab0dde301a0b96239636cf0f79ca032c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714740"
---
# <a name="delete-a-trace-transact-sql"></a>トレースの削除 (Transact-SQL)
  このトピックでは、ストアド プロシージャを使用してトレースを削除する方法について説明します。  
  
 トレース ストアド プロシージャを使用した例については、「[トレースの作成 &#40;Transact-SQL&#41;](create-a-trace-transact-sql.md)」を参照してください。  
  
### <a name="to-delete-a-trace"></a>トレースを削除するには  
  
1.  **@status = 0** を指定して **sp_trace_setstatus** を実行し、トレースを停止します。  
  
2.  **@status = 2** を指定して **sp_trace_setstatus** を実行し、トレースを閉じてトレースの情報をサーバーから削除します。  
  
> [!NOTE]  
>  トレースを閉じるには、最初にそのトレースを停止する必要があります。  
  
## <a name="see-also"></a>参照  
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)   
 [SQL Server Profiler のストアド プロシージャ &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql)  
  
  
