---
title: Showplan XML イベントを個別に保存する方法 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: 33320a7a-36e8-401c-876d-5b82c49abd85
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c92c08349a473aa4a83205cc539eec3577619109
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150430"
---
# <a name="save-showplan-xml-events-separately-sql-server-profiler"></a>Showplan XML イベントを個別に保存する方法 (SQL Server Profiler)
  このトピックでは、トレースにキャプチャされた **Showplan XML** イベントを [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で個別の .SQLPlan ファイルに保存する方法について説明します。 **で** Showplan XML [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]イベント ファイルを開くことができ、これによって各イベントのグラフィカル実行プランを表示できます。  
  
### <a name="to-save-showplan-xml-events-separately"></a>Showplan XML イベントを個別に保存するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、SQL Server のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレースのプロパティ]** ダイアログ ボックスの **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[使用するテンプレート]** ボックスの一覧で、トレースの基本として使用するトレース テンプレートを選択します。テンプレートを使用しない場合は、 **[空白]** を選択します。  
  
4.  次のいずれかの操作を行います。  
  
    -   トレースをファイルにキャプチャするには、 **[ファイルに保存]** チェック ボックスをオンにします。 **[最大ファイル サイズの設定]** ボックスに値を指定します。 必要に応じて、 **[ファイル ロールオーバーを有効にする]** および **[サーバーがトレース データを処理する]** チェック ボックスをオンにします。  
  
    -   トレースをデータベース テーブルにキャプチャするには、 **[テーブルに保存する]** チェック ボックスをオンにします。 必要に応じて、 **[最大行数の設定 (1000 行単位)]** チェック ボックスをオンにし、値を指定します。  
  
5.  必要に応じて、 **[トレース停止時刻を有効にする]** チェック ボックスをオンにして、停止日時を指定します。  
  
6.  **[イベントの選択]** タブをクリックします。  
  
7.  **[Events]** データ列で **[Performance]** イベント カテゴリを展開し、 **[Showplan XML]** チェック ボックスをオンにします。 **[Performance]** イベント カテゴリが表示されない場合は、 **[すべてのイベントを表示する]** チェック ボックスをオンにしてください。  
  
     **[トレースのプロパティ]** ダイアログ ボックスに **[イベント抽出の設定]** タブが追加されます。  
  
8.  **[イベント抽出の設定]** タブで、 **[XML プラン表示イベントを個別に保存する]** チェック ボックスをオンにします。  
  
9. **[名前を付けて保存]** ダイアログ ボックスで、 **Showplan XML** イベントを保存するファイル名を入力します。  
  
10. **[1 つのファイルにすべての XML プラン表示バッチを保存する]** をクリックして、すべての **Showplan XML** イベントを 1 つの XML ファイルに保存します。または、 **[個別のファイルに各 XML プラン表示バッチを保存する]** をクリックして、 **Showplan XML** イベントごとに新しい XML ファイルを作成します。  
  
11. SQL Server Management Studio で **Showplan XML** イベント ファイルを表示するには、 **[ファイル]** メニューの **[開く]** をポイントして、 **[ファイル]** をクリックします。 **Showplan XML** イベント ファイルを保存したディレクトリに移動し、イベント ファイルを選択して開きます。 **Showplan XML** イベント ファイルには .SQLPlan ファイル拡張子が付いています。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Profiler での Showplan 結果を使用したクエリの分析](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
