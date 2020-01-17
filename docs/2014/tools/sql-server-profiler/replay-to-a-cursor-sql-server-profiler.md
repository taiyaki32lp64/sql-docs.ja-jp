---
title: カーソル (SQL Server Profiler) を再生する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f7c4c4b9d2e2e07c53f850fe545d803fa411dbbc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267487"
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>カーソルまでの再生 (SQL Server Profiler)
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、カーソルに到達したときに一時停止するトレース ファイルまたはトレース テーブルの再生方法について説明します。 カーソル到達時点でトレースを一時停止することでデバッグがサポートされることになります。これは、長いトレース スクリプトの再生を、順番に分析できる短いセグメントに分割できるためです。  
  
### <a name="to-replay-to-the-cursor"></a>カーソルまで再生するには  
  
1.  再生するトレース ファイルまたはトレース テーブルを開きます。 詳細については、「 [トレース ファイルを開く &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) や [トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)に付属の定義済みチューニング テンプレートを使用します。  
  
     開いたトレース ファイルまたはトレース テーブルに、再生に必要なイベント クラスが含まれていることを確認します。 詳細については、「 [再生を実行するための必要条件](replay-requirements.md)」を参照してください。  
  
2.  トレース ウィンドウで、イベントを 1 つクリックします。  
  
3.  **[再生]** メニューの **[カーソルまで実行]** をクリックし、トレースを再生するサーバーに接続します。  
  
4.  **[構成の再生]** ダイアログ ボックスで設定を確認し、 **[OK]** をクリックします。  
  
     再生が開始され、最初のカーソルに到達した時点で一時停止されます。  
  
5.  F5 キーを押してトレースを再開します。  
  
6.  手順 5. をトレースの最後まで繰り返します。  
  
## <a name="see-also"></a>参照  
 [ブレークポイントまでの再生 &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)   
 [トレースの再生](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
