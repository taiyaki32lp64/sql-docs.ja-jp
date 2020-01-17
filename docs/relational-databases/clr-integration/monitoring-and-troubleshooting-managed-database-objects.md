---
title: マネージデータベースオブジェクトの監視とトラブルシューティング
description: マネージデータベースオブジェクトとアセンブリ (CLR) の監視とトラブルシューティングに使用できるツールについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: e04b5308aeca5881f624122c70ad74c27417a46b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258332"
---
# <a name="monitoring-and-troubleshooting-managed-database-objects"></a>マネージド データベース オブジェクトの監視とトラブルシューティング
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ここでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で実行されるマネージド データベース オブジェクトとアセンブリの監視およびトラブルシューティングに使用できるツールに関する情報を提供します。  
  
## <a name="profiler-trace-events"></a>プロファイラー トレース イベント  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、データベース エンジンで発生するイベントを監視するための SQL トレースとイベント通知が用意されています。 SQL トレースは、指定したイベントを記録することによって、パフォーマンスのトラブルシューティング、データベースの利用状況の監査、テスト環境のサンプル データの収集、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとストアド プロシージャのデバッグ、およびパフォーマンス分析ツール用のデータの収集に役立ちます。 詳細については、「 [SQL トレース](../../relational-databases/sql-trace/sql-trace.md)と[拡張イベント](../../relational-databases/extended-events/extended-events.md)」を参照してください。  
  
|イベント|説明|  
|-----------|-----------------|  
|[Assembly Load イベントクラス](/sql/database-engine/assembly-load-event-class)|アセンブリの読み込み要求 (成功と失敗) の監視に使用されます。|  
|[Sql: BatchStarting イベントクラス](../../relational-databases/event-classes/sql-batchstarting-event-class.md)、 [Sql: Batchstarting イベントクラス](../../relational-databases/event-classes/sql-batchcompleted-event-class.md)|開始または完了した [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチに関する情報を提供します。|  
|[Sp: Starting イベントクラス](../../relational-databases/event-classes/sp-starting-event-class.md)、 [Sp: Completed イベントクラス](../../relational-databases/event-classes/sp-completed-event-class.md)|
  [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャの実行の監視に使用されます。|  
|[Sql: StmtStarting イベントクラス](../../relational-databases/event-classes/sql-stmtstarting-event-class.md)、 [Sql: StmtCompleted イベントクラス](../../relational-databases/event-classes/sql-stmtcompleted-event-class.md)|CLR および [!INCLUDE[tsql](../../includes/tsql-md.md)] ルーチンの実行の監視に使用されます。|  
  
## <a name="performance-counters"></a>パフォーマンス カウンター  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、システム モニターで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピューターの利用状況の監視に使用できるオブジェクトとカウンターが用意されています。 オブジェクトとは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロックや Windows プロセスなど任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースです。 各オブジェクトには、監視するオブジェクトのさまざまな特性を示す 1 つ以上のカウンターが含まれます。 詳細については、「 [SQL Server オブジェクトの使用](../../relational-databases/performance-monitor/use-sql-server-objects.md)」を参照してください。  
  
|オブジェクト|説明|  
|------------|-----------------|  
|[SQL Server、CLR オブジェクト](../../relational-databases/performance-monitor/sql-server-clr-object.md)|CLR での総実行時間です。|  
  
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
 カタログ ビューは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンによって使用される情報を返します。 カタログビューはカタログメタデータに最も一般的なインターフェイスであり、この情報を取得、変換、およびカスタマイズされた形式で表示するための最も効率的な方法を提供するため、カタログビューを使用することをお勧めします。 すべてのユーザーが利用できるカタログメタデータは、カタログビューによって公開されます。 詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」を参照してください。  
  
|カタログ ビュー|説明|  
|------------------|-----------------|  
|[アセンブリ &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)|データベースに登録されているアセンブリに関する情報を返します。|  
|[assembly_references &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assembly-references-transact-sql.md)|他のアセンブリを参照するアセンブリを示します。|  
|[assembly_modules &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|アセンブリで定義されている関数、ストアド プロシージャ、およびトリガーに関する情報を返します。|  
|[assembly_files &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assembly-files-transact-sql.md)|データベースに登録されているアセンブリ ファイルに関する情報を返します。|  
|[assembly_types &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-assembly-types-transact-sql.md)|アセンブリで定義されているユーザー定義型 (UDT) を示します。|  
|[module_assembly_usages &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-module-assembly-usages-transact-sql.md)|CLR モジュールを定義しているアセンブリを示します。|  
|[parameter_type_usages &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)|ユーザー定義型のパラメーターに関する情報を返します。|  
|[server_assembly_modules &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql.md)|CLR トリガーを定義しているアセンブリを示します。|  
|[server_triggers &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-server-triggers-transact-sql.md)|CLR トリガーなど、サーバー上にあるサーバーレベル DDL トリガーを示します。|  
|[type_assembly_usages &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-type-assembly-usages-transact-sql.md)|ユーザー定義型を定義しているアセンブリを示します。|  
|[sys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)|データベースに登録されているシステム定義型およびユーザー定義型を返します。|  
  
## <a name="dynamic-management-views"></a>動的管理ビュー  
 動的管理ビューと動的管理関数では、サーバーの状態情報が返されます。返された情報は、サーバー インスタンスのヘルス状態の監視、問題の診断、パフォーマンスのチューニングに使用できます。 詳細については、「 [transact-sql&#41;&#40;動的管理ビューと関数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)」を参照してください。  
  
|DMV (DMV)|説明|  
|---------|-----------------|  
|[dm_clr_appdomains &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)|サーバー内の各アプリケーション ドメインに関する情報を提供します。|  
|[dm_clr_loaded_assemblies &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)|サーバー上に登録されている各マネージド アセンブリを示します。|  
|[dm_clr_properties &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-properties-transact-sql.md)|ホストされている CLR に関する情報を返します。|  
|[dm_clr_tasks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-tasks-transact-sql.md)|実行中のすべての CLR タスクを示します。|  
|[dm_exec_cached_plans &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)|クエリ実行を高速化するため [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でキャッシュされたクエリ実行プランに関する情報を返します。|  
|[dm_exec_query_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)|キャッシュされたクエリ プランの集計パフォーマンス統計を返します。|  
|[dm_exec_requests &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内で実行中の各要求に関する情報を返します。|  
|[dm_os_memory_clerks &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)|CLR メモリ クラークなど、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内でアクティブになっているすべてのメモリ クラークを返します。|  
  
## <a name="see-also"></a>参照  
 [共通言語ランタイム &#40;CLR&#41; 統合プログラミングの概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
