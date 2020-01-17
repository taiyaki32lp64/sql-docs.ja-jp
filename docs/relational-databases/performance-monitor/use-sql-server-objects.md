---
title: SQL Server オブジェクトの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- server performance [SQL Server], objects for monitoring
- database monitoring [SQL Server], objects for monitoring
- charts [SQL Server]
- System Monitor [SQL Server], counters
- counters [SQL Server], listed
- objects [SQL Server], performance monitoring
- objects [SQL Server], Windows System Monitor
- performance counters [SQL Server], about performance counters
- System Monitor [SQL Server], objects
- performance counters [SQL Server]
- counters [SQL Server], about performance counters
- tuning databases [SQL Server], objects for monitoring
- database performance [SQL Server], objects for monitoring
- SQL Server, objects
- monitoring performance [SQL Server], objects for monitoring
- Windows System Monitor [SQL Server], objects
- Windows System Monitor [SQL Server], counters
- counters [SQL Server]
- performance counters [SQL Server], listed
ms.assetid: bcd731b1-3c4e-4086-b58a-af7a3af904ad
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 15aa957b25323337f3b76b4f54f89a7121567a24
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982186"
---
# <a name="use-sql-server-objects"></a>SQL Server オブジェクトの使用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、システム モニターで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを実行しているコンピューターの利用状況を監視できるオブジェクトとカウンターが用意されています。 オブジェクトとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ロックや Windows プロセスなど任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースです。 各オブジェクトには、監視するオブジェクトのさまざまな特性を示す 1 つ以上のカウンターが含まれます。 たとえば、 **SQL Server Locks** オブジェクトには、 **Number of Deadlocks/sec** や **Lock Timeouts/sec**という名前のカウンターが含まれています。  
  
 同じ種類の複数のリソースがコンピューター上に存在する場合、オブジェクトによっては複数のインスタンスがある場合があります。 たとえば、システムに複数のプロセッサが搭載されている場合、オブジェクトの種類 **Processor** には複数のインスタンスがあります。 オブジェクトの種類 **Databases** には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータベースごとに 1 つのインスタンスがあります。 **Memory Manager** オブジェクトなど一部のオブジェクトの種類には、1 しかインスタンスのないものもあります。 あるオブジェクトの種類に複数のインスタンスがある場合には、インスタンスごとに、または多くの場合は一度にすべてのインスタンスに、統計を追跡するためのカウンターを追加できます。 既定のインスタンスのカウンターは、**SQLServer:** _\<オブジェクト名>_ という形式で表示されます。 名前付きインスタンスのカウンターは、**MSSQL$** _\<インスタンス名>_ **:** _\<カウンター名>_ または **SQLAgent$** _\<インスタンス名>_ **:** _\<カウンター名>_ という形式で表示されます。  
  
 グラフでカウンターを追加または削除し、グラフ設定を保存して、システム モニターを起動したときに監視する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトとカウンターを指定できます。  
  
 システム モニターは、任意の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カウンターの統計を表示するように構成することができます。 また、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カウンターにしきい値を設定して、カウンターがしきい値を超えたときに警告を生成することもできます。 警告を構成する方法の詳細については、「 [SQL Server データベース警告の作成](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)」を参照してください。  
  
> [!TIP]  
>  動的管理ビュー [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) のクエリによって、パフォーマンス カウンターの値を返すこともできます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の統計情報は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスがインストールされているときにのみ表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを停止して再起動すると、SQL Server の統計情報の表示も中断され、自動的に再開されます。 システム モニター スナップインでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されていないときでも、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のカウンターが表示されます。 クラスター化されたインスタンスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているノードでのみ、パフォーマンス カウンターが機能します。  
  
 このトピックには、次のセクションが含まれます。  
  
-   [SQL Server エージェント パフォーマンス オブジェクト](#SQLServerAgentPOs)  
  
-   [Service Broker のパフォーマンス オブジェクト](#ServiceBrokerPOs)  
  
-   [SQL Server パフォーマンス オブジェクト](#SQLServerPOs)  
  
-   [SQL Server レプリケーション パフォーマンス オブジェクト](#SQLServerReplicationPOs)  
  
-   [SSIS Pipeline カウンター](#SsisPipelineCounters)  
  
-   [必要な権限](#RequiredPermissions)  
  
##  <a name="SQLServerAgentPOs"></a> SQL Server エージェント パフォーマンス オブジェクト  
 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント用のパフォーマンス オブジェクトの一覧を示します。  
  
|パフォーマンス オブジェクト|[説明]|  
|------------------------|-----------------|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント警告についての情報を提供します。|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブについての情報を提供します。|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップについての情報を提供します。|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントについての一般的な情報を提供します。|  
  
##  <a name="ServiceBrokerPOs"></a> Service Broker のパフォーマンス オブジェクト  
 次の表は、 [!INCLUDE[ssSB](../../includes/sssb-md.md)]用のパフォーマンス オブジェクトの一覧を示します。  
  
|パフォーマンス オブジェクト|[説明]|  
|------------------------|-----------------|  
|[SQLServer:Broker Activation](../../relational-databases/performance-monitor/sql-server-broker-activation-object.md)|[!INCLUDE[ssSB](../../includes/sssb-md.md)]のアクティブなタスクについての情報を提供します。|  
|[SQLServer:Broker Statistics](../../relational-databases/performance-monitor/sql-server-broker-statistics-object.md)|[!INCLUDE[ssSB](../../includes/sssb-md.md)] についての一般的な情報を提供します。|  
|[SQLServer:Broker Transport](../../relational-databases/performance-monitor/sql-server-broker-dbm-transport-object.md)|[!INCLUDE[ssSB](../../includes/sssb-md.md)] のネットワークについての情報を提供します。|  
  
##  <a name="SQLServerPOs"></a> SQL Server パフォーマンス オブジェクト  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトについて説明します。  
  
|パフォーマンス オブジェクト|[説明]|  
|------------------------|-----------------|  
|[SQLServer:Access Methods](../../relational-databases/performance-monitor/sql-server-access-methods-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース オブジェクトの割り当てを検索して計測します。たとえば、インデックスとデータに割り当てられているインデックス検索の数またはページ数を計測します。|  
|[SQLServer:Backup Device](../../relational-databases/performance-monitor/sql-server-backup-device-object.md)|バックアップ デバイスのスループットなど、バックアップ操作と復元操作で使用するバックアップ デバイスについての情報を提供します。|  
|[SQLServer:Batch Resp Statistics](../../relational-databases/performance-monitor/sql-server-batch-resp-statistics-object.md)|SQL バッチ応答時間を追跡するカウンターです。| 
|[SQLServer: Buffer Manager](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]freememory **や** buffer cache hit ratio **など、** で使用するメモリ バッファーについての情報を提供します。|  
|[SQL Server: Buffer Node](../../relational-databases/performance-monitor/sql-server-buffer-node.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によるフリー ページの要求頻度とアクセスの頻度についての情報を提供します。|  
|[SQLServer:Catalog Metadata](../../relational-databases/performance-monitor/sql-server-catalog-metadata-object.md)|SQL Server のカタログ メタデータ マネージャー オブジェクトを定義します。| 
|[SQLServer:CLR](../../relational-databases/performance-monitor/sql-server-clr-object.md)|共通言語ランタイム (CLR: Common Language Runtime) に関する情報を提供します。|  
|[SQLServer:Columnstore](../../relational-databases/performance-monitor/sql-server-columnstore-object.md)|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。<br /><br /> 列ストアインデックスの行グループとセグメントに関する情報を提供します。|  
|[SQLServer:Cursor Manager by Type](../../relational-databases/performance-monitor/sql-server-cursor-manager-by-type-object.md)|カーソルについての情報を提供します。|  
|[SQLServer:Cursor Manager Total](../../relational-databases/performance-monitor/sql-server-cursor-manager-total-object.md)|カーソルについての情報を提供します。|  
|[SQLServer:Database Mirroring](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)|データベース ミラーリングについての情報を提供します。|  
|[SQLServer:Databases](../../relational-databases/performance-monitor/sql-server-databases-object.md)|使用できるログ用空きディスク領域やデータベース内のアクティブなトランザクションの数など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースについての情報を提供します。 このオブジェクトには、複数のインスタンスが存在することがあります。|  
|[SQL Server:Deprecated Features](../../relational-databases/performance-monitor/sql-server-deprecated-features-object.md)|非推奨機能が使用された回数をカウントします。|  
|[SQLServer:Exec Statistics](../../relational-databases/performance-monitor/sql-server-execstatistics-object.md)|実行統計についての情報を提供します。|  
|[SQLServer:External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。<br /><br /> 外部スクリプトの実行についての情報を提供します。|  
|[SQLServer:FileTable](../../relational-databases/performance-monitor/sql-server-filetable-object.md)|FileTable と非トランザクション アクセスに関する統計です。|  
|[SQLServer:General Statistics](../../relational-databases/performance-monitor/sql-server-general-statistics-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続しているユーザーの数など、一般的なサーバー全体の利用状況についての情報を提供します。|  
|[SQL Server:HADR Availability Replica](../../relational-databases/performance-monitor/sql-server-availability-replica.md)|現在割り当てられているロック構造の総数など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 可用性レプリカについての情報を提供します。|  
|[SQL Server:HADR Database Replica](../../relational-databases/performance-monitor/sql-server-database-replica.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)] データベース レプリカについての情報を提供します。|  
|[SQL Server:HTTP Storage](../../relational-databases/performance-monitor/sql-server-http-storage-object.md)|「[Microsoft Azure 内の SQL Server データ ファイル](../../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)」を使用するときに Microsoft Azure Storage アカウントを監視するための情報を提供します。|  
|[SQLServer:Latches](../../relational-databases/performance-monitor/sql-server-latches-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用されるデータベース ページなど、内部リソースのラッチについての情報を提供します。|  
|[SQLServer:Locks](../../relational-databases/performance-monitor/sql-server-locks-object.md)|ロック タイムアウトやデッドロックなど、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]による各ロック要求についての情報を提供します。 このオブジェクトには、複数のインスタンスが存在することがあります。|  
|[SQLServer:LogPool FreePool](../../relational-databases/performance-monitor/sql-server-logpool-freepool-object.md)|ログ プール内の空きプールに関する統計を説明します。|
|[SQLServer:Memory Broker Clerks](../../relational-databases/performance-monitor/sql-server-memory-broker-clerks-object.md)|Memory Broker Clerk に関する統計です。|
|[SQLServer:Memory Manager](../../relational-databases/performance-monitor/sql-server-memory-manager-object.md)|現在割り当てられているロック構造の総数など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメモリの利用状況についての情報を提供します。|  
|[SQLServer:Plan Cache](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)|ストアド プロシージャ、トリガー、クエリ プランなど、オブジェクトを保存するために使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] キャッシュについての情報を提供します。|  
|[SQLServer:Query Store](../../relational-databases/performance-monitor/sql-server-query-store-object.md)|クエリ ストアに関する情報を提供します。|  
|[SQLServer:Resource Pool Stats](../../relational-databases/performance-monitor/sql-server-resource-pool-stats-object.md)|リソース ガバナーのリソース プール統計に関する情報を提供します。|  
|[SQLServer:SQL Errors](../../relational-databases/performance-monitor/sql-server-sql-errors-object.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーについての情報を提供します。|  
|[SQLServer:SQL Statistics](../../relational-databases/performance-monitor/sql-server-sql-statistics-object.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] で受信する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのバッチ数など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クエリの側面についての情報を提供します。|  
|[SQLServer:Transactions](../../relational-databases/performance-monitor/sql-server-transactions-object.md)|トランザクションの総数やスナップショット トランザクションの数など、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のアクティブなトランザクションについての情報を提供します。|  
|[SQLServer:User Settable](../../relational-databases/performance-monitor/sql-server-user-settable-object.md)|カスタム監視を実行します。 各カウンターは、監視する値を返すカスタム ストアド プロシージャまたは任意の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントにすることができます。|  
|[SQLServer:Wait Statistics](../../relational-databases/performance-monitor/sql-server-wait-statistics-object.md)|待機についての情報を提供します。|  
|[SQLServer:Workload Group Stats](../../relational-databases/performance-monitor/sql-server-workload-group-stats-object.md)|リソース ガバナーのワークロード グループ統計に関する情報を提供します。|  
  
##  <a name="SQLServerReplicationPOs"></a> SQL Server レプリケーション パフォーマンス オブジェクト  
 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション用のパフォーマンス オブジェクトの一覧を示します。  
  
|パフォーマンス オブジェクト|[説明]|  
|------------------------|-----------------|  
|**SQLServer:Replication Agents**<br /><br /> **SQLServer:Replication Snapshot**<br /><br /> **SQLServer:Replication Logreader**<br /><br /> **SQLServer:Replication Dist.**<br /><br /> **SQLServer:Replication Merge**<br /><br /> 詳細については、「 [Monitoring Replication with System Monitor](../../relational-databases/replication/monitor/monitoring-replication-with-system-monitor.md)」を参照してください。|レプリケーション エージェントの利用状況についての情報を提供します。|  
  
##  <a name="SsisPipelineCounters"></a> SSIS Pipeline カウンター  
 **SSIS Pipeline** カウンターの詳細については、「 [パフォーマンス カウンター](../../integration-services/performance/performance-counters.md)」を参照してください。  
  
##  <a name="RequiredPermissions"></a> 必要な権限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQLAgent:Alerts **以外の**オブジェクトを使用する際の権限は Windows のアクセス許可に依存しています。 **SQLAgent:Alerts** を使用するには、ユーザーは **sysadmin**固定サーバー ロールのメンバーでなければなりません。  
  
## <a name="see-also"></a>参照  
 [パフォーマンス オブジェクトの使用](../../ssms/agent/use-performance-objects.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
