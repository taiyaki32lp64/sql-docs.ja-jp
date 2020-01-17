---
title: Showplan XML イベントを個別に保存する
titleSuffix: SQL Server Profiler
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 73a95255bcce173fa0ce2141b4f968d7efab7e57
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165579"
---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>Showplan XML イベントを個別に保存する方法 (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、トレースにキャプチャされた **Showplan XML** イベントを [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で個別の .SQLPlan ファイルに保存する方法について説明します。 **Showplan XML** イベント ファイルは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で開くことができるので、イベントごとの実行プランをグラフィカルに表示できます。  
  
## <a name="save-showplan-xml-events-separately"></a>Showplan XML イベントを個別に保存する  
  
1. **[ファイル]** メニューの **[新しいトレース]** を選択し、SQL Server のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** を選択し、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2. **[トレースのプロパティ]** ダイアログ ボックスの **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3. **[使用するテンプレート]** の一覧から、トレースの基にするトレース テンプレートを選択します。 テンプレートを使用しない場合は **[空白]** を選択します。  
  
4. 次のいずれかの操作を行います。  
  
    -   トレースをファイルにキャプチャするには、 **[ファイルに保存]** チェック ボックスをオンにします。 **[最大ファイル サイズの設定]** ボックスに値を指定します。 
    
        必要に応じて、 **[ファイル ロールオーバーを有効にする]** および **[サーバーがトレース データを処理する]** チェック ボックスをオンにします。  
  
    -   トレースをデータベース テーブルにキャプチャするには、 **[テーブルに保存する]** チェック ボックスをオンにします。 
    
        必要に応じて、 **[最大行数の設定 (1000 行単位)]** チェック ボックスをオンにし、値を指定します。  
  
5. 必要に応じて、 **[トレース停止時刻を有効にする]** チェック ボックスをオンにして、停止日時を指定します。 
  
6. **[イベントの選択]** タブを選択します。  
  
7. **[Events]** データ列で **[Performance]** イベント カテゴリを展開し、 **[Showplan XML]** チェック ボックスをオンにします。 **Performance** イベント カテゴリが表示されない場合は、 **[すべてのイベントを表示する]** チェック ボックスをオンにしてください。  
  
     **[トレースのプロパティ]** ダイアログ ボックスに **[イベント抽出の設定]** タブが追加されます。  
  
8. **[イベント抽出の設定]** タブで、 **[XML プラン表示イベントを個別に保存する]** を選択します。  
  
9. **[名前を付けて保存]** ダイアログ ボックスで、 **Showplan XML** イベントを保存するファイル名を入力します。  
  
10. 1 つの XML ファイルにすべての **Showplan XML** イベントを保存するには、 **[1 つのファイルにすべての XML プラン表示バッチを保存する]** を選択します。 または、**Showplan XML** イベントごとに新しい XML ファイル を作成するには、 **[個別のファイルに各 XML プラン表示バッチを保存する]** を選択します。  
  
11. SQL Server Management Studio で **Showplan XML** イベント ファイルを表示するには、 **[ファイル]** メニューの **[開く]** をポイントして、 **[ファイル]** を選択します。 **Showplan XML** イベント ファイルを保存したディレクトリに参照し、イベント ファイルを選択して開きます。 **Showplan XML** イベント ファイルには .SQLPlan ファイル拡張子が付いています。  

## <a name="see-also"></a>参照  
 [SQL Server Profiler でのプラン表示結果を使用したクエリの分析](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
