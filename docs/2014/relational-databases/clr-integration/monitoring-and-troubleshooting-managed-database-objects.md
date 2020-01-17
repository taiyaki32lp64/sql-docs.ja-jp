---
title: マネージ データベース オブジェクトの監視とトラブルシューティング |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], performance
- monitoring [CLR integration]
- performance [CLR integration]
ms.assetid: a7b589ac-104d-4b68-b4aa-9f5fc192b13d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f03266a5460e9e34a404256e5df415f799b29d98
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918926"
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>マネージド データベース オブジェクトの監視とトラブルシューティング
  ここでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で実行されるマネージド データベース オブジェクトとアセンブリの監視およびトラブルシューティングに使用できるツールに関する情報を提供します。  
  
## <a name="profiler-trace-events"></a>プロファイラー トレース イベント  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、データベース エンジンで発生するイベントを監視するための SQL トレースとイベント通知が用意されています。 SQL トレースは、指定したイベントを記録することによって、パフォーマンスのトラブルシューティング、データベースの利用状況の監査、テスト環境のサンプル データの収集、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントとストアド プロシージャのデバッグ、およびパフォーマンス分析ツール用のデータの収集に役立ちます。 詳細については、次を参照してください。 [SQL トレース](../sql-trace/sql-trace.md)と[拡張イベント](../extended-events/extended-events.md)します。  
  
|イベント|説明|  
|-----------|-----------------|  
|[Assembly Load イベント クラス](../../database-engine/assembly-load-event-class.md)|アセンブリの読み込み要求 (成功と失敗) の監視に使用されます。|  
|[SQL:BatchStarting イベント クラスは](../event-classes/sql-batchstarting-event-class.md)、 [SQL:BatchCompleted イベント クラス](../event-classes/sql-batchcompleted-event-class.md)|開始または完了した [!INCLUDE[tsql](../../../includes/tsql-md.md)] バッチに関する情報を提供します。|  
|[SP: Starting イベント クラス](../event-classes/sp-starting-event-class.md)、 [SP: Completed イベント クラス](../event-classes/sp-completed-event-class.md)|[!INCLUDE[tsql](../../../includes/tsql-md.md)] ストアド プロシージャの実行の監視に使用されます。|  
|[SQL:StmtStarting イベント クラス](../event-classes/sql-stmtstarting-event-class.md)、 [SQL:StmtCompleted イベント クラス](../event-classes/sql-stmtcompleted-event-class.md)|CLR および [!INCLUDE[tsql](../../../includes/tsql-md.md)] ルーチンの実行の監視に使用されます。|  
  
## <a name="performance-counters"></a>パフォーマンス カウンター  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、システム モニターで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピューターの利用状況の監視に使用できるオブジェクトとカウンターが用意されています。 オブジェクトとは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ロックや Windows プロセスなど任意の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースです。 各オブジェクトには、監視するオブジェクトのさまざまな特性を示す 1 つ以上のカウンターが含まれます。 詳細については、「 [SQL Server オブジェクトの使用](../performance-monitor/use-sql-server-objects.md)」を参照してください。  
  
|オブジェクト|説明|  
|------------|-----------------|  
|[SQL Server の CLR オブジェクト](../performance-monitor/sql-server-clr-object.md)|CLR での総実行時間です。|  
  
## <a name="windows-system-monitor-perfmonexe-counters"></a>Windows システム モニター (PERFMON.EXE) カウンター  
 Windows システム モニター (PERFMON.EXE) ツールには、CLR 統合アプリケーションの監視に使用できるパフォーマンス カウンターがいくつか用意されています。 .NET CLR パフォーマンス カウンターを "sqlservr" プロセス名でフィルタリングすることにより、実行中の CLR 統合アプリケーションを追跡できます。  
  
|パフォーマンス オブジェクト|説明|  
|------------------------|-----------------|  
|SqlServer:CLR|サーバーの CPU 統計を提供します。|  
|.NET CLR Exceptions|1 秒あたりの例外数を追跡します。|  
|.NET CLR Loading|サーバーに読み込まれている AppDomains とアセンブリに関する情報を提供します。|  
|.NET CLR Memory|CLR のメモリ使用量に関する情報を提供します。 このオブジェクトを使用すると、メモリ使用量が大きすぎる場合に警告を出すことができます。|  
|.NET Data Provider for SQL Server|1 秒あたりの接続数と切断数を追跡します。 このオブジェクトを使用すると、データベースの利用状況を監視できます。|  
  
## <a name="catalog-views"></a>カタログ ビュー  
 カタログ ビューは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベース エンジンによって使用される情報を返します。 カタログ ビューはカタログ メタデータへの最も一般的なインターフェイスであり、この情報を取得、変換、およびカスタマイズした形式で表示するための、最も効率的な方法となります。したがって、カタログ ビューを使用することをお勧めします。 ユーザーが利用できるすべてのカタログ メタデータがカタログ ビューを通じて公開されています。 詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)」を参照してください。  
  
|カタログ ビュー|説明|  
|------------------|-----------------|  
|[sys.assemblies &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assemblies-transact-sql)|データベースに登録されているアセンブリに関する情報を返します。|  
|[sys.assembly_references &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-references-transact-sql)|他のアセンブリを参照するアセンブリを示します。|  
|[sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)|アセンブリで定義されている関数、ストアド プロシージャ、およびトリガーに関する情報を返します。|  
|[sys.assembly_files &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-files-transact-sql)|データベースに登録されているアセンブリ ファイルに関する情報を返します。|  
|[sys.assembly_types &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-types-transact-sql)|アセンブリで定義されているユーザー定義型 (UDT) を示します。|  
|[sys.module_assembly_usages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql)|CLR モジュールを定義しているアセンブリを示します。|  
|[sys.parameter_type_usages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)|ユーザー定義型のパラメーターに関する情報を返します。|  
|[sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)|CLR トリガーを定義しているアセンブリを示します。|  
|[sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)|CLR トリガーなど、サーバー上にあるサーバーレベル DDL トリガーを示します。|  
|[sys.type_assembly_usages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql)|ユーザー定義型を定義しているアセンブリを示します。|  
|[sys.types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)|データベースに登録されているシステム定義型およびユーザー定義型を返します。|  
  
## <a name="dynamic-management-views"></a>動的管理ビュー  
 動的管理ビューと動的管理関数では、サーバーの状態情報が返されます。返された情報は、サーバー インスタンスのヘルス状態の監視、問題の診断、パフォーマンスのチューニングに使用できます。 詳細については、次を参照してください。[動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../views/views.md)します。  
  
|DMV (DMV)|説明|  
|---------|-----------------|  
|[sys.dm_clr_appdomains &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql)|サーバー内の各アプリケーション ドメインに関する情報を提供します。|  
|[sys.dm_clr_loaded_assemblies &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql)|サーバー上に登録されている各マネージド アセンブリを示します。|  
|[sys.dm_clr_properties &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql)|ホストされている CLR に関する情報を返します。|  
|[sys.dm_clr_tasks &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql)|実行中のすべての CLR タスクを示します。|  
|[sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)|クエリ実行を高速化するため [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でキャッシュされたクエリ実行プランに関する情報を返します。|  
|[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)|キャッシュされたクエリ プランの集計パフォーマンス統計を返します。|  
|[sys.dm_exec_requests (&) #40 です。TRANSACT-SQL と #41 です。](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内で実行中の各要求に関する情報を返します。|  
|[sys.dm_os_memory_clerks &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql)|CLR メモリ クラークなど、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンス内でアクティブになっているすべてのメモリ クラークを返します。|  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
