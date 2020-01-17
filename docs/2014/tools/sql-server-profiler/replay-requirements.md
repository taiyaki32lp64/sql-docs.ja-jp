---
title: 再生の要件 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], replaying traces
- traces [SQL Server], replaying
- replaying traces
- TSQL_Replay template [SQL Server]
ms.assetid: 0e01dfc7-84b9-47f6-8bf7-b0656df4fa7d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b9da4b68bba6358ff473846fb710f8fa6454e5d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62688596"
---
# <a name="replay-requirements"></a>再生を実行するための必要条件
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] または Distributed Replay Utility を使用してトレース データを再生するには、特定のイベント クラスと列のセットがトレースにキャプチャされている必要があります。 **TSQL_Replay** トレース テンプレートを使用して、後で再生に使用するトレースを構成した場合、これらの設定は既定で有効になります。 このトピックでは、これらの設定と、再生を実行するためのその他の必要条件について説明します。  
  
> [!NOTE]  
>  (アクティブなコンカレント接続が多数ある、またはスループットが高い) 集中型の OLTP アプリケーションを再生する場合は、Distributed Replay Utility を使用することをお勧めします。 Distributed Replay Utility では、複数のコンピューターからのトレース データを再生し、ミッションクリティカルなワークロードをより正確にシミュレートできます。 詳細については、「 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)」を参照してください。  
  
## <a name="event-classes-required-for-replay"></a>再生に必要なイベント クラス  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で再生するには、監視するイベント クラスのほかに、以下の一連のイベント クラスをトレースにキャプチャする必要があります。  
  
-   **CursorClose**(サーバー側のカーソルを再生する場合のみ必要)  
  
-   **CursorExecute** (サーバー側のカーソルを再生する場合のみ必要)  
  
-   **CursorOpen** (サーバー側のカーソルを再生する場合のみ必要)  
  
-   **CursorPrepare** (サーバー側のカーソルを再生する場合のみ必要)  
  
-   **CursorUnprepare** (サーバー側のカーソルを再生する場合のみ必要)  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **ExistingConnection**  
  
-   **RPC Output Parameter**  
  
-   **RPC:Completed**  
  
-   **RPC:Starting**  
  
-   **Exec Prepared SQL** (サーバー側の準備された SQL ステートメントを再生する場合のみ必要)  
  
-   **Prepare SQL** (サーバー側の準備された SQL ステートメントを再生する場合のみ必要)  
  
-   **SQL:BatchCompleted**  
  
-   **SQL:BatchStarting**  
  
## <a name="data-columns-required-for-replay"></a>再生に必要なデータ列  
 トレースを再生するには、キャプチャ対象となるデータ列のほかに、以下のデータ列をトレースにキャプチャする必要があります。  
  
-   **Event Class**  
  
-   **EventSequence**  
  
-   **TextData**  
  
-   **Application Name**  
  
-   **LoginName**  
  
-   **DatabaseName**  
  
-   **データベース ID**  
  
-   **ClientProcessID**  
  
-   **HostName**  
  
-   **ServerName**  
  
-   **Binary Data**  
  
-   **SPID**  
  
-   **Start Time**  
  
-   **EndTime**  
  
-   **IsSystem**  
  
-   **NTDomainName**  
  
-   **NTUserName**  
  
-   **Error**  
  
> [!NOTE]  
>  再生するデータをトレースにキャプチャする場合は、トレース テンプレート **TSQL_Replay** を使用します。  
  
## <a name="other-replay-requirements"></a>再生を実行するためのその他の必要条件  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、必要なイベントおよび列が存在するかどうかを再生時に調べます。 この変更によって再生の精度が上がり、必要なデータがない場合でも、再生のトラブルシューティング時に根拠のない作業をしなくて済みます。 必要なデータがトレースにない場合は、再生によってエラーが返され、ファイルの再生が停止します。  
  
 最初にトレースしたサーバー (ソース) 以外の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているサーバーに対してトレースを再生するには、次の条件を満たす必要があります。  
  
-   トレースに含まれるすべてのログインとユーザーが、ターゲット コンピューター上の、ソースと同じデータベース内にあらかじめ作成されていること。  
  
-   ターゲット コンピューターのすべてのログインとユーザーに、ソース コンピューター上と同じ権限が与えられていること。  
  
-   すべてのログイン パスワードが、再生を実行するユーザーと同じであること。  
  
-   ターゲット コンピューター上のデータベース ID が、ソース コンピューター上のデータベース ID と同じであること。 ただし、これらが同じでない場合、トレース内に **DatabaseName** が存在すれば、それに基づいて一致させることができます。  
  
-   トレースに記録されている各ログインの既定データベースが、ターゲット コンピューター上で、ログインの対象データベースにそれぞれ設定されていること。 たとえば、再生するトレースに、ソース コンピューター上の **Fred_Db**データベースに対する **Fred** というログインについての利用状況が含まれているとします。 この場合、ターゲット コンピューター上では、ログイン **Fred**の既定データベースが、 **Fred_Db** に一致するデータベースに設定されていなければなりません (データベース名が異なる場合も同様)。 ログインの既定データベースを設定するには、 **sp_defaultdb** システム ストアド プロシージャを使用します。  
  
 失われたログインや不正なログインに関連付けられたイベントを再生すると、再生エラーとなります。ただし、再生の処理は継続されます。  
  
 トレースの再生に必要な権限の詳細については、「 [SQL Server Profiler の実行に必要な権限](sql-server-profiler.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [トレース テーブルを再生する &#40;SQL Server Profiler&#41;](replay-a-trace-table-sql-server-profiler.md)   
 [トレース ファイルを再生する &#40;SQL Server Profiler&#41;](replay-a-trace-file-sql-server-profiler.md)   
 [SQL Server イベント クラスの参照](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_defaultdb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-defaultdb-transact-sql)   
 [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md)  
  
  
