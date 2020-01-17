---
title: 再生をブレークポイント (SQL Server Profiler) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- breakpoints [SQL Server]
- traces [SQL Server], replaying
ms.assetid: 3caf751e-df3b-40c7-b5e8-4490ae178e0c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33860d4e84e828b404236527dbe3c8c8cf6becc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183518"
---
# <a name="replay-to-a-breakpoint-sql-server-profiler"></a>ブレークポイントまでの再生 (SQL Server Profiler)
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して、再生するトレース ファイルまたはトレース テーブルにブレークポイントを設定する方法について説明します。 トレースの再生を開始する前に、トレース ファイルまたはトレース テーブルにブレークポイントを設定しておくと、特定のイベントが発生したときにトレースの再生を一時停止できます。 トレース再生中にブレークポイントを使用するとデバッグが簡単になります。これは、長いトレース スクリプトの再生を短いセグメントに分けて小刻みに分析できるからです。  
  
### <a name="to-replay-to-a-breakpoint"></a>ブレークポイントまで再生するには  
  
1.  再生するトレース ファイルまたはトレース テーブルを開きます。 詳細については、「 [トレース ファイルを開く &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) や [トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)に付属の定義済みチューニング テンプレートを使用します。  
  
     開いたトレース ファイルまたはトレース テーブルに、再生に必要なイベント クラスが含まれていることを確認します。 詳細については、「 [再生を実行するための必要条件](replay-requirements.md)」を参照してください。  
  
2.  トレース ウィンドウで、ブレークポイントとして使用するイベントをクリックします。 ブレークポイントを設定するには、次の 3 つの方法があります。  
  
    -   F9 キーを押します。  
  
    -   **[再生]** メニューの **[ブレークポイントの設定/解除]** をクリックします。  
  
    -   イベントを右クリックし、 **[ブレークポイントの設定/解除]** をクリックします。  
  
     選択したトレース イベントの横に赤い点が表示され、それがトレースのブレークポイントであることを示します。  
  
     複数のブレークポイントを設定するには、この手順を繰り返します。  
  
3.  **[再生]** メニューの **[開始]** をクリックし、トレースを再生するサーバーに接続します。  
  
4.  **[構成の再生]** ダイアログ ボックスで設定を確認し、 **[OK]** をクリックします。  
  
     再生が開始され、ブレークポイントに達すると一時停止します。  
  
5.  F5 キーを押して再生を再開し、次のブレークポイントに進みます。  
  
6.  手順 5. をトレースの最後まで繰り返します。  
  
## <a name="see-also"></a>関連項目  
 [カーソルまでの再生 &#40;SQL Server Profiler&#41;](replay-to-a-cursor-sql-server-profiler.md)   
 [トレースの再生](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
