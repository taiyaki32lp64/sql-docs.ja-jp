---
title: 保存されているトレースの表示 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c468376a67b955c467177161e3ea4bd932bb25a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907026"
---
# <a name="view-a-saved-trace-transact-sql"></a>保存されているトレースの表示 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、組み込み関数を使用して、保存されているトレースを表示する方法について説明します。  
  
### <a name="to-view-a-specific-trace"></a>特定のトレースを表示するには  
  
1.  情報が必要なトレースの ID を指定して **fn_trace_getinfo** を実行します。 この関数は、トレース、トレースのプロパティ、およびそのプロパティに関する情報を一覧にしたテーブルを返します。  

     この関数を呼び出すには、次のステートメントを実行します。  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>既存のトレースをすべて表示するには  
  
1.  **または** を指定して `0` fn_trace_getinfo `default`を実行します。 この関数は、すべてのトレース、そのプロパティ、およびプロパティに関する情報を一覧にしたテーブルを返します。  
  
     この関数を呼び出すには、次のようにします。  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 組み込み関数 **fn_trace_getinfo**を実行するには、ユーザーに次の権限が必要です。  
  
 サーバーの ALTER TRACE  
  
## <a name="see-also"></a>参照  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [SQL Server Profiler を使用したトレースの表示と分析](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
