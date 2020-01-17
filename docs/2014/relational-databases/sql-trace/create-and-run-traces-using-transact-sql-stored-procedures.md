---
title: Transact-SQL ストアド プロシージャを使用したトレースの作成と実行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7922638ed06f52740a3c34f6e66ff72dbb5bbd98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714809"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Transact-SQL ストアド プロシージャを使用したトレースの作成と実行
  トレースの作成や実行を Microsoft [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して行うか、システム ストアド プロシージャを使用して行うかによって、SQL トレースでのトレースの処理が異なります。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]の代替手段として、 [!INCLUDE[tsql](../../includes/tsql-md.md)] システム ストアド プロシージャを使用してトレースを作成および実行できます。 システム ストアド プロシージャを使用したトレースの処理は、次のようになります。  
  
1.  **sp_trace_create**を使用して、トレースを作成します。  
  
2.  **sp_trace_setevent**によりイベントを追加します。  
  
3.  必要に応じて、 **sp_trace_setfilter**によりフィルターを設定します。  
  
4.  **sp_trace_setstatus**によりトレースを開始します。  
  
5.  **sp_trace_setstatus**によりトレースを停止します。  
  
6.  **sp_trace_setstatus**によりトレースを閉じます。  
  
    > [!NOTE]  
    >  [!INCLUDE[tsql](../../includes/tsql-md.md)] システム ストアド プロシージャを使用すると、サーバー側のトレースが作成されます。これにより、ディスク上に空き領域があり、かつ書き込みエラーが発生しない限り、イベントが失われないことが保証されます。 ディスクがいっぱいになるか、ディスク障害が発生した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの実行は続行されますが、トレースは停止されます。 **c2 audit mode** が設定されていて、書き込みエラーが発生すると、トレースが停止され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスがシャットダウンされます。 **c2 audit mode** 設定の詳細については、「 [c2 audit mode サーバー構成オプション](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[SQL トレースの最適化](sql-trace.md)|システム パフォーマンスへのトレースの影響を軽減する方法について説明します。|  
|[トレースへのフィルターの適用](filter-a-trace.md)|トレースでのフィルターの使用について説明します。|  
|[トレース ファイルとテーブル サイズの制限](limit-trace-file-and-table-sizes.md)|トレース データが書き込まれるファイルやテーブルのサイズを制限する方法について説明します。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] でのみ、トレース情報をテーブルに書き込むことができます。|  
|[トレースのスケジュール設定](schedule-traces.md)|トレースの開始時刻や終了時刻を設定する方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql)  
  
  
