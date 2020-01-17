---
title: Deadlock Graph の保存 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], saving deadlock graphs
- graphs [SQL Server]
- saving deadlock graphs
ms.assetid: bf1fc906-abd6-4a89-842e-da0d66b2defe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 33757ad1f8085ce141b8e206f2c3fd99c7dcba90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150702"
---
# <a name="save-deadlock-graphs-sql-server-profiler"></a>Deadlock Graph の保存 (SQL Server Profiler)
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して Deadlock Graph を保存する方法について説明します。 Deadlock Graph は XML ファイルとして保存されます。  
  
### <a name="to-save-deadlock-graph-events-separately"></a>Deadlock Graph のイベントを個別に保存するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、SQL Server のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  [トレースのプロパティ] ダイアログ ボックスの **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[使用するテンプレート]** ボックスの一覧で、トレースの基本として使用するトレース テンプレートを選択します。テンプレートを使用しない場合は、 **[空白]** を選択します。  
  
4.  次のいずれかの操作を行います。  
  
    -   トレースをファイルにキャプチャするには、 **[ファイルに保存]** チェック ボックスをオンにします。 **[最大ファイル サイズの設定]** ボックスに値を指定します。  
  
         必要に応じて、 **[ファイル ロールオーバーを有効にする]** チェック ボックスと **[サーバーがトレース データを処理する]** チェック ボックスをオンにします。  
  
    -   トレースをデータベース テーブルにキャプチャするには、 **[テーブルに保存する]** チェック ボックスをオンにします。  
  
         必要に応じて、 **[最大行数の設定 (1000 行単位)]** チェック ボックスをオンにし、値を指定します。  
  
5.  必要に応じて、 **[トレース停止時刻を有効にする]** チェック ボックスをオンにして、停止日時を指定します。  
  
6.  **[イベントの選択]** タブをクリックします。  
  
7.  **[Events]** データ列で、 **[Locks]** イベント カテゴリを展開し、 **[Deadlock graph]** チェック ボックスをオンにします。 Locks イベント カテゴリが表示されない場合は、 **[すべてのイベントを表示する]** チェック ボックスをオンにして表示します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスに **[イベント抽出の設定]** タブが追加されます。  
  
8.  **[イベント抽出の設定]** タブで、 **[デッドロック XML イベントを個別に保存する]** チェック ボックスをオンにします。  
  
9. **[名前を付けて保存]** ダイアログ ボックスで、Deadlock Graph のイベントを格納するファイル名を入力します。  
  
10. 1 つの XML ファイルに Deadlock Graph のすべてのイベントを保存するには、 **[1 つのファイルにすべてのデッドロック XML バッチを保存する]** をクリックします。また、Deadlock Graph ごとに新しい XML ファイルを作成するには、 **[個別のファイルに各デッドロック XML バッチを保存する]** をクリックします。  
  
 デッドロック ファイルを保存した後は、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でファイルを開くことができます。 詳細については、「[デッドロック ファイルを開く、表示、および印刷する方法 &#40;SQL Server Management Studio&#41;](open-view-and-print-a-deadlock-file-sql-server-management-studio.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler を使用したデッドロックの分析](../../tools/sql-server-profiler/analyze-deadlocks-with-sql-server-profiler.md)  
  
  
