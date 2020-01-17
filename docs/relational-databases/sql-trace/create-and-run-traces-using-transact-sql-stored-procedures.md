---
title: Transact-SQL ストアド プロシージャを使用したトレースの作成と実行
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 80347417-338d-4bea-8885-91fae5181cfe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3d1c5a85072bec1fc304156268680c201ad2245e
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095642"
---
# <a name="create-and-run-traces-using-transact-sql-stored-procedures"></a>Transact-SQL ストアド プロシージャを使用したトレースの作成と実行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
|トピック|[説明]|  
|-----------|-----------------|  
|[SQL トレースの最適化](../../relational-databases/sql-trace/optimize-sql-trace.md)|システム パフォーマンスへのトレースの影響を軽減する方法について説明します。|  
|[トレースへのフィルターの適用](../../relational-databases/sql-trace/filter-a-trace.md)|トレースでのフィルターの使用について説明します。|  
|[トレース ファイルとテーブル サイズの制限](../../relational-databases/sql-trace/limit-trace-file-and-table-sizes.md)|トレース データが書き込まれるファイルやテーブルのサイズを制限する方法について説明します。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] でのみ、トレース情報をテーブルに書き込むことができます。|  
|[トレースのスケジュール設定](../../relational-databases/sql-trace/schedule-traces.md)|トレースの開始時刻や終了時刻を設定する方法について説明します。|  
  
## <a name="see-also"></a>参照  
 [sp_trace_create &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
