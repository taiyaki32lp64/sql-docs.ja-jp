---
title: SQL Server、Databases オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- Databases object
- SQLServer:Databases
- Availability Groups [SQL Server], performance counters
ms.assetid: a7f9e7d4-fff4-4c72-8b3e-3f18dffc8919
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: a8114722ac95c1404a45d8c85bf1736e541fa0ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093603"
---
# <a name="sql-server-databases-object"></a>SQL Server、Databases オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server の **SQLServer:Databases** オブジェクトには、一括コピー操作、バックアップと復元のスループット、およびトランザクション ログの利用状況を監視するためのカウンターがあります。 トランザクションとトランザクション ログを監視すると、データベースで発生しているユーザーの利用状況と、トランザクション ログの空き容量を調べることができます。 ユーザーの利用状況は、データベースのパフォーマンスを決定し、ログ サイズ、ロック、およびレプリケーションに影響を与えます。 下位レベルのログの利用状況を監視して、ユーザーの利用状況やリソースの利用状況を計測すると、パフォーマンスのボトルネックを突き止めるのに役立ちます。  
  
 **Databases** オブジェクトの複数のインスタンスは、同時に監視できます。各インスタンスは、1 つのデータベースを表します。  
  
 次の表で、SQL Server **Databases** カウンターについて説明します。  
  
|SQL Server Databases カウンター|[説明]|  
|-----------------------------------|-----------------|  
|**Active Transactions**|データベースのアクティブなトランザクション数。|  
|**Avg Dist From EOL/LP Request**|最新の VLF 内の要求における、ログ プール要求ごとの、ログの終端からのバイト単位での平均距離。| 
|**Backup/Restore Throughput/sec**|データベースのバックアップ操作と復元操作の読み取り/書き込みの 1 秒あたりのスループット。 たとえば、より多くのバックアップ デバイスを並行して使用した場合、またはより高速なデバイスを使用した場合に、データベース バックアップ操作のパフォーマンスがどのように変化するかを計測することができます。 データベースのバックアップ操作または復元操作のスループットを計測すると、バックアップ操作と復元操作の進行状況およびパフォーマンスを調べることができます。|  
|**Bulk Copy Rows/sec**|1 秒間に一括コピーされた行数。|  
|**Bulk Copy Throughput/sec**|1 秒間に一括コピーされたデータの量 (KB)。|  
|**Commit table entries**|データベースのコミット テーブルのインメモリ部分のサイズ (行数)。 詳細については、「[sys.dm_tran_commit_table &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-tracking-sys-dm-tran-commit-table.md)」を参照してください。|  
|**Data File(s) Size (KB)**|データベース内のすべてのデータ ファイルの合計サイズ (KB)。自動拡張した分のサイズも含みます。 このカウンターは、 **tempdb**の正しいサイズを判断する場合などに役立ちます。|  
|**DBCC Logical Scan Bytes/sec**|DBCC (データベース コンソール コマンド) の 1 秒あたりの論理読み取りスキャン バイト数。|  
|**Group Commit Time/sec**|1 秒あたりのグループ停止時間 (マイクロ秒)。|
|**Log Bytes Flushed/sec**|フラッシュされたログの総バイト数。|  
|**Log Cache Hit Ratio**|ログ キャッシュによって満たされたログ キャッシュ読み取りの比率。|  
|**Log Cache Hit Ratio Base**|内部使用のみです。| 
|**Log Cache Reads/sec**|ログ マネージャー キャッシュを使用して 1 秒間に実行された読み取り数。|  
|**Log File(s) Size (KB)**|データベース内のすべてのトランザクション ログ ファイルの合計サイズ (KB)。|  
|**Log File(s) Used Size (KB)**|データベース内のすべてのログ ファイルの合計使用サイズ (KB)。|  
|**Log Flush Wait Time**|ログがフラッシュされるまでの合計待ち時間 (ミリ秒)。 AlwaysOn セカンダリ データベースの場合、この値はディスクへのログ レコードの書き込みの待ち時間を示します。|  
|**Log Flush Waits/sec**|ログ フラッシュを待機中だった 1 秒あたりのコミットの数。|  
|**Log Flush Write Time (ms)**|最後の 1 秒間に完了したログ フラッシュの書き込みを実行するのにかかった時間 (ミリ秒)。|  
|**Log Flushes/sec**|1 秒あたりのログ フラッシュの回数。|  
|**Log Growths**|データベースのトランザクション ログが拡張された合計回数。|  
|**Log Pool Cache Misses/sec**|ログ プール内でログ ブロックが使用できなかった要求の数。 *ログ プール* は、トランザクション ログのインメモリ キャッシュです。 このキャッシュは、復旧、トランザクション レプリケーション、ロールバック、および [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]のログの読み取りを最適化するために使用されます。|  
|**Log Pool Disk Reads/sec**|ログ ブロックをフェッチするためにログ プールが実行したディスクの読み取り回数。|  
|**Log Pool Hash Deletes/sec**|ログ プールからの未処理ハッシュ エントリの削除の割合。|
|**Log Pool Hash Inserts/sec**|ログ プールへの未処理ハッシュ エントリの挿入の割合。|
|**Log Pool Invalid Hash Entry/sec**|無効であるために失敗したハッシュ参照の割合。|
|**Log Pool Log Scan Pushes/sec**|ログ スキャンごとのログ ブロックのプッシュ率。ディスクからの場合と、メモリからの場合があります。|
|**Log Pool LogWriter Pushes/sec**|ログ ライター スレッドごとのログ ブロックのプッシュ率。|
|**Log Pool Push Empty FreePool/sec**|空きプールが空のため、ログ ブロックのプッシュ率が下がります。|
|**Log Pool Push Low Memory/sec**|メモリが不足しているため、ログ ブロックのプッシュ率が下がります。|
|**Log Pool Push No Free Buffer/sec**|空きバッファーが利用できないため、ログ ブロックのプッシュ率が下がります。|
|**Log Pool Req.Behind Trunc/sec**|切り捨て LSN で要求されたブロックによるログ プールのキャッシュ ミス回数。|
|**Log Pool Requests Base**|内部使用のみです。| 
|**Log Pool Requests Old VLF/sec**|ログの最新の VLF にないログ プール要求。|  
|**Log Pool Requests/sec**|ログ プールで処理されるログ ブロック要求の数。|  
|**Log Pool Total Active Log Size**|共有キャッシュ バッファー マネージャーに現在格納されているアクティブなログの合計 (バイト単位) です。|
|**Log Pool Total Shared Pool Size**|共有キャッシュ バッファー マネージャーの現在のメモリ使用量の合計 (バイト単位) です。|
|**Log Shrinks**|このデータベースのログ圧縮の総数。|  
|**Log Truncations**|トランザクション ログが切り捨てられた回数 (単純復旧モデルの場合)。|  
|**Percent Log Used**|ログの中で使用中の領域の割合。|  
|**Repl.Pending Xacts**|レプリケーション用にマークされていてまだディストリビューション データベースに配信されていないパブリケーション データベースのトランザクション ログ内のトランザクションの数。|  
|**Repl.Trans.Rate**|1 秒間に、パブリケーション データベースのトランザクション ログから読み取られ、ディストリビューション データベースに配信されたトランザクションの数。|  
|**Shrink Data Movement Bytes/sec**|自動圧縮操作、DBCC SHRINKDATABASE ステートメント、または DBCC SHRINKFILE ステートメントによって 1 秒間に移動されているデータの量。|  
|**Tracked transactions/sec**|データベースのコミット テーブルに記録するコミット済みトランザクションの数。|  
|**Transactions/sec**|1 秒間にデータベースに対して開始されたトランザクションの数。<br /><br /> **Transactions/sec** は、XTP のみのトランザクション (ネイティブ コンパイル ストアド プロシージャによって開始されたトランザクション) はカウントしません。|  
|**Write Transactions/sec**|最後の 1 秒間にデータベースに書き込んでコミットしたトランザクションの数。|  
|**XTP Controller DLC Latency Base**|内部使用のみです。| 
|**XTP Controller DLC Latency/Fetch**|Direct Log Consumer に入ってから XTP コントローラーによって取り出されるまでのログ ブロック間における、1 秒あたりの平均待機時間 (マイクロ秒)。|
|**XTP Controller DLC Peak Latency**|XTP コントローラーによる Direct Log Consumer からのフェッチで記録された最大待機時間 (マイクロ秒)。|
|**XTP Controller Log Processed/sec**|XTP コントローラー スレッドによって処理された、1 秒あたりの合計ログ バイト数。|
|**XTP Memory Used (KB)**|データベースの XTP により使用されるメモリ容量です。| 
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server、Database Replica](../../relational-databases/performance-monitor/sql-server-database-replica.md)  
  
  
