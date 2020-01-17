---
title: ODBC ドライバー パフォーマンスのプロファイリング |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- profiling ODBC driver performance data [SQL Server Native Client]
- performance [ODBC]
- application statistics [ODBC]
- time statistics [ODBC]
- ODBC, performance data
- SQL Server Native Client ODBC driver, profiling performance data
- SQLPERF data structure
- statistical information [ODBC]
ms.assetid: 8f44e194-d556-4119-a759-4c9dec7ecead
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f2c16e66c03eee8c5e1616fdaa0f0d1b154b85e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63143588"
---
# <a name="profiling-odbc-driver-performance"></a>ODBC ドライバーのパフォーマンスのプロファイル
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、次の 2 種類のパフォーマンス データをプロファイルできます。  
  
-   実行時間の長いクエリ。  
  
     ドライバーは、指定した時間内にサーバーから応答が得られないクエリをログ ファイルに書き込むことができます。 アプリケーション プログラマやデータベース管理者は、ログに記録された各 SQL ステートメントを確認し、パフォーマンスを改善する方法を判断できます。  
  
-   ドライバーのパフォーマンス データ。  
  
     ドライバーはパフォーマンス統計情報を記録できます。また、この情報をファイルに書き込んだり、SQLPERF というドライバー固有の構造体を使用して、アプリケーションで利用可能にすることができます。 このパフォーマンス統計情報が書き込まれるファイルはタブで区切られており、Microsoft Excel など、タブ区切りのファイルをサポートするスプレッドシートを使用して容易に分析できます。  
  
 各プロファイルは、次の方法で有効にできます。  
  
-   ログ記録が指定されているデータ ソースに接続する。  
  
-   呼び出す[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)プロファイルを制御するドライバー固有の属性を設定します。  
  
 各アプリケーション プロセスは、個別に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのコピーを取得しますが、プロファイルは、ドライバーのコピーとアプリケーション プロセスの組み合わせに対してグローバルに実行されます。 アプリケーションによってプロファイルが有効になると、ドライバー内でアクティブになっている、そのアプリケーションからの全接続に関する情報が、プロファイルによって記録されます。 特にプロファイルを要求していない接続も、プロファイルの対象に含まれます。  
  
 ドライバーがプロファイル ログ (パフォーマンス データまたは実行時間の長いクエリのログ) を開くと、ドライバーで開かれているすべての環境ハンドルがアプリケーションによって解放され、ODBC ドライバー マネージャーがドライバーをアンロードするまで、このプロファイル ログは閉じられません。 アプリケーションが新しい環境ハンドルを開くと、ドライバーの新しいコピーが読み込まれます。 その後、アプリケーションが同じログ ファイルを指定しているデータ ソースに接続するか、同じファイルにログ記録するようにドライバー固有の属性を設定している場合、ドライバーは古いログを上書きします。  
  
 あるアプリケーションが任意のログ ファイルに対してプロファイルの記録を開始し、別のアプリケーションが同じログ ファイルに対してプロファイルの記録を開始しようとすると、2 番目のアプリケーションはプロファイル データをログに記録できません。 最初のアプリケーションがドライバーをアンロードした後に、2 番目のアプリケーションがプロファイルを開始した場合、最初のアプリケーションのデータを記録しているログ ファイルは、2 番目のアプリケーションによって上書きされます。  
  
 アプリケーションから呼び出す場合、アプリケーションは、プロファイルが有効にするデータ ソースに接続している場合、ドライバーは SQL_ERROR を返します**SQLSetConnectOption**をログ記録を開始します。 呼び出し**SQLGetDiagRec**し、次を返します。  
  
```  
SQLState: 01000, pfNative = 0  
ErrorMsg: [Microsoft][SQL Server Native Client]  
   An error has occurred during the attempt to access  
   the log file, logging disabled.  
```  
  
 ドライバーは、環境ハンドルが閉じられると、パフォーマンス データの収集を停止します。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client アプリケーションが、それぞれ固有の環境ハンドルを持つ複数の接続を保持している場合、関連付けられている環境ハンドルのいずれかが閉じられると、ドライバーはパフォーマンス データの収集を停止します。  
  
 ドライバーのパフォーマンス データは、SQLPERF データ構造体に保存するか、タブ区切り形式ファイルに記録できます。 このデータには、次の種類の統計情報が含まれます。  
  
-   アプリケーション プロファイル  
  
-   接続  
  
-   ネットワーク  
  
-   Time  
  
 次の表では、SQLPERF データ構造体のフィールドについて説明します。この説明は、パフォーマンス ログ ファイルに記録される統計情報にも適用されます。  
  
### <a name="application-profile-statistics"></a>アプリケーション プロファイル統計情報  
  
|SQLPERF のフィールド|説明|  
|-------------------|-----------------|  
|TimerResolution|ミリ秒単位で表されたサーバーのクロック時間の最小単位。 通常は 0 (ゼロ) が報告されます。大きな値が報告される場合のみ考慮する必要があります。 サーバー クロックの最小単位が、タイマベースの一部の統計で予想される間隔よりも大きい場合は、統計値が増加する可能性があります。|  
|SQLidu|SQL_PERF_START 以降に処理された INSERT、DELETE、または UPDATE ステートメントの数。|  
|SQLiduRows|SQL_PERF_START 以降に処理された INSERT、DELETE、または UPDATE ステートメントの数。|  
|SQLSelects|SQL_PERF_START 以降に処理された SELECT ステートメントの数。|  
|SQLSelectRows|SQL_PERF_START 以降に選択された行数。|  
|トランザクション|SQL_PERF_START 以降のユーザー トランザクションの数。ロールバックの数も含まれます。 SQL_AUTOCOMMIT_ON の状態で ODBC アプリケーションが実行されている場合は、各コマンドがトランザクションと見なされます。|  
|SQLPrepares|数[SQLPrepare 関数](https://go.microsoft.com/fwlink/?LinkId=59360)sql_perf_start 後呼び出し。|  
|ExecDirects|数**SQLExecDirect** sql_perf_start 後呼び出し。|  
|SQLExecutes|数**SQLExecute** sql_perf_start 後呼び出し。|  
|CursorOpens|SQL_PERF_START 以降にドライバーがサーバー カーソルを開いた回数。|  
|CursorSize|SQL_PERF_START 以降にカーソルによって開かれた結果セット内の行数。|  
|CursorUsed|SQL_PERF_START 以降に実際にドライバーによってカーソルから取得された行数。|  
|PercentCursorUsed|CursorUsed/CursorSize の計算結果になります。 たとえば、アプリケーションによりドライバーでサーバー カーソルが開かれて "SELECT COUNT(*) FROM Authors" が実行され、この SELECT ステートメントの結果セットには 23 行が含まれるとします。 その後、アプリケーションがこれらの行から 3 行のみをフェッチした場合、CursorUsed/CursorSize は 3/23 なので、PercentCursorUsed は 13.043478 になります。|  
|AvgFetchTime|SQLFetchTime/SQLFetchCount の計算結果になります。|  
|AvgCursorSize|CursorSize/CursorOpens の計算結果になります。|  
|AvgCursorUsed|CursorUsed/CursorOpens の計算結果になります。|  
|SQLFetchTime|サーバー カーソルに対してフェッチの完了に要した累積時間。|  
|SQLFetchCount|SQL_PERF_START 以降にサーバー カーソルに対して実行されたフェッチの数。|  
|CurrentStmtCount|ドライバー内で開かれているすべての接続上で、現在開いているステートメント ハンドルの数。|  
|MaxOpenStmt|SQL_PERF_START 以降に同時に開かれたステートメント ハンドルの最大数。|  
|SumOpenStmt|SQL_PERF_START 以降に開かれたステートメント ハンドルの数。|  
|**接続の統計情報:**||  
|CurrentConnectionCount|アプリケーションがサーバーに対して開いている現在アクティブな接続ハンドルの数。|  
|MaxConnectionsOpened|SQL_PERF_START 以降に開かれたコンカレント接続ハンドルの最大数。|  
|SumConnectionsOpened|SQL_PERF_START 以降に開かれた接続ハンドルの合計数。|  
|SumConnectionTime|SQL_PERF_START 以降に開かれたすべての接続の接続時間の合計。 たとえば、アプリケーションが接続を 10 開いていて、各接続を 5 秒間保持していた場合、SumConnectionTime は 50 秒になります。|  
|AvgTimeOpened|SumConnectionsOpened/ SumConnectionTime の計算結果になります。|  
|**ネットワークの統計情報:**||  
|ServerRndTrips|ドライバーがサーバーにコマンドを送信し、応答を受け取った回数。|  
|BuffersSent|SQL_PERF_START 以降にドライバーから [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信された表形式データ ストリーム (TDS) パケットの数。 大量の処理を伴うコマンドは複数のバッファーを使用する可能性があるので、このようなコマンドがサーバーに送信され、6 個のパケットを使用する場合、ServerRndTrips は 1 ずつ増加しますが、BuffersSent は 6 ずつ増加します。|  
|BuffersRec|アプリケーションがドライバーの使用を開始した後に、ドライバーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から受信した TDS パケットの数。|  
|BytesSent|アプリケーションがドライバーの使用を開始した後に、TDS パケットを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に送信されたデータのバイト数。|  
|BytesRec|アプリケーションがドライバーの使用を開始した後に、ドライバーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から TDS パケットを使用して受信したデータのバイト数。|  
  
### <a name="time-statistics"></a>時間統計情報  
  
|SQLPERF のフィールド|説明|  
|-------------------|-----------------|  
|msExecutionTime|SQL_PERF_START 以降、ドライバーが処理に要した累積時間。サーバーからの応答の待ち時間も含まれます。|  
|msNetworkServerTime|ドライバーがサーバーからの応答待ちに要した累積時間。|  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)   
 [ODBC ドライバーのパフォーマンスに関するトピックをプロファイリング&#40;ODBC&#41;](../../native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)  
  
  
