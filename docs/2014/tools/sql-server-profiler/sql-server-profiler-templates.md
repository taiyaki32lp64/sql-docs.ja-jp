---
title: SQL Server Profiler テンプレート |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- default SQL Server Profiler templates
- templates [SQL Server], SQL Server Profiler
- Profiler [SQL Server Profiler], templates
- trace templates [SQL Server]
- predefined templates [SQL Server Profiler]
- SQL Server Profiler, templates
ms.assetid: b674e491-dc58-47a1-acdd-7028e9a201fc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5cac924e926d03dffb9116e5ce7194bb784d45fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68186146"
---
# <a name="sql-server-profiler-templates"></a>SQL Server Profiler のテンプレート
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して、トレースに含めるイベント クラスとデータ列を定義するテンプレートを作成できます。 テンプレートを定義して保存したら、選択したイベント クラスごとにデータを記録するトレースを実行できます。 テンプレートは多くのトレースで使用できますが、テンプレート自体は実行できません。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、事前に定義済みのトレース テンプレートが用意されています。これにより、特定のトレースでよく使用するイベント クラスを簡単に構成できるようになります。 たとえば、Standard テンプレートは、ログイン、ログアウト、完了したバッチ、および接続に関する情報を記録するための汎用トレースの作成に役立ちます。 このテンプレートは、変更しないでトレースの実行に使用するか、異なるイベントの構成を持つ新たなテンプレートの基礎として使用できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、定義済みテンプレートからだけでなく、既定ではイベント クラスは含まれていない空のテンプレートからもトレース テンプレートを作成できます。 空のトレース テンプレートは、計画したトレースがどの定義済みテンプレートの構成とも似ていないときに使用します。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、さまざまな種類のサーバーをトレースできます。 たとえば、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をトレースできます。  ただし、含めることができるイベント クラスは、サーバーの種類によって異なります。 したがって、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、さまざまなサーバー向けのさまざまなテンプレートが用意されており、選択したサーバーの種類に対応する特定のテンプレートを使用できます。  
  
## <a name="predefined-templates"></a>定義済みテンプレート  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] には、Standard (既定) テンプレート以外にも、特定の種類のイベントを監視するための定義済みテンプレートがいくつか用意されています。 次の表に、定義済みテンプレート、その目的、および情報をキャプチャする対象となるイベント クラスを示します。  
  
|テンプレート名|テンプレートの目的|イベント クラス|  
|-------------------|----------------------|-------------------|  
|SP_Counts|ストアド プロシージャの実行動作の推移をキャプチャします。|**SP:Starting**|  
|Standard|汎用トレースを作成する基になるテンプレート。 実行されるすべてのストアド プロシージャと [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチをキャプチャします。 データベース サーバーの全般的な利用状況を監視するために使用します。|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Completed**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL|クライアントから [!INCLUDE[tsql](../../includes/tsql-md.md)] に送信されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントと、それらが実行された時刻をキャプチャします。 クライアント アプリケーションをデバッグするために使用します。|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Duration|クライアントから [!INCLUDE[tsql](../../includes/tsql-md.md)] に送信されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントとそれらの実行時間 (ミリ秒単位) をキャプチャし、期間でグループ化します。 低速のクエリを特定するために使用します。|**RPC:Completed**<br /><br /> **SQL:BatchCompleted**|  
|TSQL_Grouped|[!INCLUDE[tsql](../../includes/tsql-md.md)] に送信されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントと、それらが実行された時刻をキャプチャします。 ステートメントを送信したユーザーまたはクライアントで情報をグループ化します。 特定のクライアントまたはユーザーからのクエリを調べるために使用します。|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SQL:BatchStarting**|  
|TSQL_Locks|クライアントから [!INCLUDE[tsql](../../includes/tsql-md.md)] に送信されたすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ステートメントを例外ロック イベントと共にキャプチャします。 デッドロック、ロック タイムアウト、およびロックのエスカレーションの各イベントをトラブルシューティングするために使用します。|**Blocked Process Report**<br /><br /> **SP:StmtCompleted**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:StmtCompleted**<br /><br /> **SQL:StmtStarting**<br /><br /> **Deadlock Graph**<br /><br /> **Lock:Cancel**<br /><br /> **Lock:Deadlock**<br /><br /> **Lock:Deadlock Chain**<br /><br /> **Lock:Escalation**<br /><br /> **Lock:Timeout (timeout>0)**|  
|TSQL_Replay|トレースの再生に必要な [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントに関する詳細情報をキャプチャします。 ベンチマーク テストなどの反復チューニングを実行するために使用します。|**CursorClose**<br /><br /> **CursorExecute**<br /><br /> **CursorOpen**<br /><br /> **CursorPrepare**<br /><br /> **CursorUnprepare**<br /><br /> **Audit Login**<br /><br /> **Audit Logout**<br /><br /> **Existing Connection**<br /><br /> **RPC Output Parameter**<br /><br /> **RPC:Completed**<br /><br /> **RPC:Starting**<br /><br /> **Exec Prepared SQL**<br /><br /> **Prepare SQL**<br /><br /> **SQL:BatchCompleted**<br /><br /> **SQL:BatchStarting**|  
|TSQL_SPs|実行中のすべてのストアド プロシージャに関する詳細情報をキャプチャします。 ストアド プロシージャを構成するステップを分析するために使用します。 プロシージャが再コンパイルされる可能性がある場合は、 **SP:Recompile** イベントを追加します。|**Audit Login**<br /><br /> **Audit Logout**<br /><br /> **ExistingConnection**<br /><br /> **RPC:Starting**<br /><br /> **SP:Completed**<br /><br /> **SP:Starting**<br /><br /> **SP:StmtStarting**<br /><br /> **SQL:BatchStarting**|  
|Tuning|ストアド プロシージャと [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチの実行に関する情報をキャプチャします。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーでデータベースをチューニングするためのワークロードとして使用できるトレース出力を生成するために使用します。|**RPC:Completed**<br /><br /> **SP:StmtCompleted**<br /><br /> **SQL:BatchCompleted**|  
  
 イベント クラスの詳細については、「 [SQL Server イベント クラスの参照](../../relational-databases/event-classes/sql-server-event-class-reference.md)」を参照してください。  
  
## <a name="default-template"></a>既定のテンプレート  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、すべての新しいトレースに適用される既定のテンプレートとして **Standard** テンプレートが自動的に指定されます。 ただし、他の定義済みテンプレートまたはユーザー定義テンプレートを既定のテンプレートにすることもできます。 既定のテンプレートを変更するには、 **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[全般]** タブを使用してテンプレートを作成または編集するときに、 **[選択したサーバーの種類に対する既定のテンプレートとして使用する]** チェック ボックスをオンにします。  
  
 **[トレース テンプレートのプロパティ]** ダイアログ ボックスに移動するには、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] で、 **[ファイル]** メニューの **[テンプレート]** を選択して、 **[新しいテンプレート]** または **[テンプレートの編集]** をクリックします。  
  
> [!NOTE]  
>  既定のテンプレートは、サーバーの特定の種類固有のテンプレートです。 あるサーバーの種類の既定のテンプレートを変更しても、他のサーバーの種類の既定のテンプレートには影響しません。 特定のサーバーの既定のテンプレートを設定する方法の詳細については、「[トレース定義の既定値の設定 &#40;SQL Server Profiler&#41;](set-trace-definition-defaults-sql-server-profiler.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [トレース テンプレートの作成 &#40;SQL Server Profiler&#41;](create-a-trace-template-sql-server-profiler.md)   
 [トレース テンプレートの変更 &#40;SQL Server Profiler&#41;](../../database-engine/modify-a-trace-template-sql-server-profiler.md)   
 [トレース テンプレートのエクスポート &#40;SQL Server Profiler&#41;](export-a-trace-template-sql-server-profiler.md)   
 [トレース テンプレートのインポート &#40;SQL Server Profiler&#41;](import-a-trace-template-sql-server-profiler.md)  
  
  
