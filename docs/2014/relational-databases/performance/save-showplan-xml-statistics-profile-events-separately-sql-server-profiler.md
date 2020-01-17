---
title: Showplan XML Statistics Profile イベントを個別に保存 (SQL Server Profiler) | Microsoft Docs
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
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 79f3f41d4224baacd485c7d2151db0f3f2059f86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150628"
---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>Showplan XML Statistics Profile イベントを個別に保存 (SQL Server Profiler)
  このトピックでは、トレースでキャプチャされる **Showplan XML Statistics Profile** イベントを、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して個別の SQLPlan ファイルに保存する方法について説明します。 **Showplan XML Statistics Profile** イベント ファイルは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で開くことができ、イベントごとの実行プランをグラフィカルに表示できます。  
  
### <a name="to-save-showplan-xml-statistics-events-separately"></a>Showplan XML Statistics Profile イベントを個別に保存するには  
  
1.  **[ファイル]** メニューの **[新しいトレース]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
     **[トレースのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  **[接続の確立直後にトレースを開始する]** チェック ボックスがオンになっている場合、 **[トレースのプロパティ]** ダイアログ ボックスは表示されず、すぐにトレースが開始されます。 この設定を無効にするには、 **[ツール]** メニューの **[オプション]** をクリックし、 **[接続の確立直後にトレースを開始する]** チェック ボックスをオフにします。  
  
2.  **[トレースのプロパティ]** ダイアログ ボックスの **[トレース名]** ボックスに、トレースの名前を入力します。  
  
3.  **[使用するテンプレート]** ボックスの一覧で、トレースのベースとなるトレース テンプレートを選択します。テンプレートを使用しない場合は、 **[空白]** を選択します。  
  
4.  次のいずれかの操作を行います。  
  
    -   トレースをファイルに記録する場合は、 **[ファイルに保存]** をクリックします。 **[最大ファイル サイズの設定 (MB)]** ボックスに値を指定します。  
  
         必要に応じて、 **[ファイル ロールオーバーを有効にする]** チェック ボックスと **[サーバーがトレース データを処理する]** チェック ボックスをオンにします。  
  
    -   トレースをデータベース テーブルに記録する場合は、 **[テーブルに保存]** をクリックします。  
  
         必要に応じて、 **[最大行数の設定 (1000 行単位)]** チェック ボックスをオンにし、値を指定します。  
  
5.  必要に応じて、 **[トレース停止時刻を有効にする]** チェック ボックスをオンにして、停止日時を指定します。  
  
6.  **[イベントの選択]** タブをクリックします。  
  
7.  **Events**データ列で、 **Performance**イベント カテゴリを展開し、 **[Showplan XML Statistics Profile]** チェック ボックスをオンにします。 **Performance** イベント カテゴリが表示されない場合は、 **[すべてのイベントを表示する]** チェック ボックスをオンにしてください。  
  
     **[トレースのプロパティ]** ダイアログ ボックスに **[イベント抽出の設定]** タブが追加されます。  
  
8.  **[イベント抽出の設定]** タブで、 **[XML プラン表示イベントを個別に保存する]** チェック ボックスをオンにします。  
  
9. **[名前を付けて保存]** ダイアログ ボックスで、 **Showplan XML Statistics Profile** イベントを格納するファイル名を入力します。  
  
10. **[1 つのファイルにすべての XML プラン表示バッチを保存する]** をクリックし、1 つの XML ファイルにすべての **Showplan XML Statistics Profile** イベントを保存します。または、 **[個別のファイルに各 XML プラン表示バッチを保存する]** をクリックし、 **Showplan XML Statistics Profile** イベントごとに新しい XML ファイルを作成します。  
  
11. SQL Server Management Studio で **Showplan XML Statistics Profile** イベント ファイルを表示するには、 **[ファイル]** メニューで **[開く]** をポイントし、 **[ファイル]** をクリックします。 **Showplan XML Statistics Profile** イベント ファイルを保存したディレクトリに移動し、ファイルを選択して開きます。 **Showplan XML Statistics Profile** イベント ファイルの拡張子は .SQLPlan です。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Profiler での Showplan 結果を使用したクエリの分析](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
