---
title: SQL Server Profiler を使用したトレースの表示と分析 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], viewing traces
- SQL Server Profiler, viewing traces
- traces [SQL Server], viewing
- SQL Server Profiler, troubleshooting
- troubleshooting [SQL Server], traces
- events [SQL Server], finding inside trace
- Profiler [SQL Server Profiler], troubleshooting
- traces [SQL Server], events
ms.assetid: 17e821ca-a12e-4192-acc1-96765d9ae266
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd9b95821ee673e259273f880aefe8606fe81d71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211025"
---
# <a name="view-and-analyze-traces-with-sql-server-profiler"></a>SQL Server Profiler を使用したトレースの表示と分析
  トレースにキャプチャされたイベント データを表示するには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用します。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、定義されたトレース プロパティに基づいてデータが表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータを分析するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] や [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーなどの別のプログラムにデータをコピーする方法があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーは、 **Text** データ列がトレースに含まれている場合、SQL バッチおよびリモート プロシージャ コール (RPC) のイベントを含んだトレース ファイルを使用できます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーで使用する適切なイベントと列がキャプチャされるようにするには、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]に付属の定義済みチューニング テンプレートを使用します。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用してトレースを開くとき、そのトレース ファイルが [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] または SQL トレース システムのストアド プロシージャによって作成されている場合は、トレース ファイルに .trc というファイル拡張子が付いている必要はありません。  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、SQL トレース ファイル (.log) と汎用 SQL スクリプト ファイルも読み取ることができます。 ファイル拡張子 .log がない SQL トレース ファイル、たとえば trace.txt を開く場合は、ファイル形式として **SQLTrace_Log** を指定します。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] の日付および時刻の表示形式は、トレース分析を行いやすいように設定できます。  
  
## <a name="troubleshooting-data"></a>データのトラブルシューティング  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用すると、トレースまたはトレース ファイルを **Duration**、 **CPU**、 **Reads**、または **Writes** の各データ列でグループ化することにより、データをトラブルシューティングできます。 トラブルシューティングできるデータの例としては、実行時間のかかるクエリや、論理読み取り操作の数が例外的に多いクエリなどがあります。  
  
 さらに、トレースをテーブルに保存し、 [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用してイベント データをクエリすることにより、追加の情報を検索できます。 たとえば、どの **SQL:BatchCompleted** イベントの待機時間が長すぎるかを調べるには、次のように実行します。  
  
```  
SELECT  TextData, Duration, CPU  
FROM    trace_table_name  
WHERE   EventClass = 12 -- SQL:BatchCompleted events  
AND     CPU < (Duration * 1000)  
```  
  
> [!NOTE]  
>  サーバーはマイクロ秒 (100 万分の 1 (10<sup>-6</sup>) 秒) 単位でのイベント期間、およびイベントにより使用されるミリ秒 (10<sup>-3</sup> 秒) 単位での CPU 時間をレポートします。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のグラフィカル ユーザー インターフェイスに、既定ではミリ秒単位で **Duration** 列が表示されますが、トレースがファイルまたはデータベース テーブルに保存されると、 **Duration** 列の値はマイクロ秒単位で記述されます。  
  
## <a name="displaying-object-names-when-viewing-traces"></a>トレースを確認するときのオブジェクト名の表示  
 オブジェクトの識別子 (**Object ID**) でなく名前を表示するには、 **Object Name** データ列に加えて **Server Name** と **Database ID** の各データ列もキャプチャする必要があります。  
  
 **Object ID** データ列でグループ化する場合は、まず **Server Name** と **Database ID** の各データ列でグループ化してから、 **Object ID** データ列でグループ化してください。 同様に、 **Index ID** データ列でグループ化する場合は、まず **Server Name**、 **Database ID**、および **Object ID** の各データ列でグループ化してから、 **Index ID** データ列でグループ化してください。 サーバーとデータベース (およびインデックス ID の場合はオブジェクト) の間ではオブジェクト ID とインデックス ID は一意でないので、この順序でグループ化する必要があります。  
  
## <a name="finding-specific-events-within-a-trace"></a>トレース内での特定のイベントの検索  
 トレース内のイベントを検索およびグループ化するには、次の手順を実行します。  
  
1.  トレースを作成します。  
  
    -   トレースを定義する場合、キャプチャするその他のデータ列に加え、 **Event Class**、 **ClientProcessID**、 **Start Time** の各データ列もキャプチャします。 詳細については、「[トレースの作成 &#40;SQL Server Profiler&#41;](create-a-trace-sql-server-profiler.md)」を参照してください。  
  
    -   **Event Class** データ列でキャプチャされたデータをグループ化し、トレースをファイルまたはテーブルにキャプチャします。 キャプチャされたデータをグループ化するには、[トレースのプロパティ] ダイアログ ボックスの **[イベントの選択]** タブで **[列の構成]** をクリックします。 詳細については、「[トレースに表示される列の構成 &#40;SQL Server Profiler&#41;](organize-columns-displayed-in-a-trace-sql-server-profiler.md)」を参照してください。  
  
    -   トレースを開始して、適切な時間が経過するか、適切な数のイベントがキャプチャされたら、トレースを停止します。  
  
2.  対象のイベントを検索します。  
  
    -   トレース ファイルまたはテーブルを開き、必要なイベント クラスのノード、たとえば **Deadlock Chain**を展開します。 詳細については、「 [トレース ファイルを開く &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) や [トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)に付属の定義済みチューニング テンプレートを使用します。  
  
    -   目的のイベントが見つかるまで、トレース データ全体を検索します。 **の** [編集] **メニューの** [検索] [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用すると、トレース内の値を検索するときに便利です。 トレースするイベントの **ClientProcessID** データ列に加えて **Start Time** データ列の値を書き留めておきます。  
  
3.  コンテキスト内でイベントを表示します。  
  
    -   トレースのプロパティを表示し、 **ClientProcessID**ClientProcessID **Event Class** の各データ列もキャプチャする必要があります。  
  
    -   表示する各クライアント プロセス ID のノードを展開します。 トレース全体を手動で検索するか、または前の対象イベントの **Start Time** 値が見つかるまで **[検索]** オプションを使用します。 選択した各クライアント プロセス ID に属するその他のイベントと共に、イベントは発生順に表示されます。 たとえば、トレース内にキャプチャされた **Deadlock** データ列に加えて **Deadlock Chain**イベントは、展開されたクライアント プロセス ID 内の **SQL:BatchStarting**events within the expデータ列に加えてed client process ID.  
  
 これと同じ方法で、グループ化されたイベントを見つけることができます。 目的のイベントが見つかったら、 **ClientProcessID**、 **ApplicationName**、その他のイベント クラスでイベントをグループ化すると、関連する動作を発生順に表示できます。  
  
## <a name="see-also"></a>関連項目  
 [保存されているトレースの表示 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-a-saved-trace-transact-sql.md)   
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql)   
 [フィルター情報の表示 &#40;SQL Server Profiler&#41;](view-filter-information-sql-server-profiler.md)   
 [フィルター情報の表示 &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/view-filter-information-transact-sql.md)   
 [トレース ファイルを開く &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md)   
 [トレース テーブルを開く &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md)  
  
  
