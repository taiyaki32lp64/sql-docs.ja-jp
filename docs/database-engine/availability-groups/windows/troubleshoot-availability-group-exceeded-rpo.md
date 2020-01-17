---
title: 可用性グループ接続の超過 RPO
description: Always On 可用性グループが回復ポイントの目標 (RPO) を超えた場合の一般的な問題と解決策
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 38de1841-9c99-435a-998d-df81c7ca0f1e
author: rothja
ms.author: jroth
ms.openlocfilehash: 92c78d36559a8cb08a7f3368012a94ce3048c93c
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822184"
---
# <a name="troubleshoot-availability-group-exceeded-rpo"></a>トラブルシューティング:可用性グループ接続の超過 RPO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  非同期コミット セカンダリ レプリカへの可用性グループの強制手動フェールオーバーを実行した後に、データ損失が回復ポイントの目標 (RPO) を超えていることが判明する場合があります。 または、「[Always On 可用性グループのパフォーマンスを監視する](monitor-performance-for-always-on-availability-groups.md)」の方法を使用して非同期コミット セカンダリ レプリカの予想されるデータ損失を計算したときに RTO を超過していることが判明します。  
  
 同期コミット セカンダリ レプリカは、データ損失がないことを保証しますが、非同期コミット セカンダリ レプリカのデータ損失の可能性は、セカンダリ レプリカ上で書き込まれるのを待機しているログの量に依存します。  
  
 次のセクションでは、非同期コミット セカンダリ レプリカのデータ損失の可能性が高くなる一般的な原因について説明します。ここでは、可用性グループに関係ないサーバー インスタンスに体系的なパフォーマンスの問題がないことを前提としています。  
  
1.  [長いネットワーク遅延またはスループットが低いネットワークは、プライマリ レプリカでログの構築の原因になります。](#BKMK_LATENCY)  
  
2.  [ディスク I/O のボトルネックのために、セカンダリ レプリカでログの書き込みが遅くなる](#BKMK_IO_BOTTLENECK)  
  
##  <a name="BKMK_LATENCY"></a> 長いネットワーク遅延またはスループットが低いネットワークは、プライマリ レプリカでログの構築の原因になります。  
 データベースが RPO を超える最も一般的な理由は、セカンダリ レプリカに十分な速さで送信できないことです。  
  
### <a name="explanation"></a>説明  
 プライマリ レプリカは、セカンダリ レプリカに送信される未確認メッセージの許可される最大数を超えたときにログ送信のフロー制御をアクティブにします。 これらのメッセージの一部が確認されるまで、セカンダリ レプリカにそれ以上のログ ブロックを送信できません。 セカンダリ レプリカに書き込まれる場合にのみデータ損失を防ぐことができるので、未送信のログ メッセージを構築すると、データ損失の可能性が高くなります。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 セカンダリ レプリカに多数のメッセージが再送信される場合、長いネットワーク待機時間とネットワーク ノイズを示している可能性があります。 DMV 値 **log_send_rate** とパフォーマンス オブジェクトの Log Bytes Flushed/sec を比較することもできます。ログがディスクにフラッシュされる速度が送信される速度よりも早い場合、データ損失の可能性が無制限に増加します。  
  
 また、2 つのパフォーマンス オブジェクト `SQL Server:Availability Replica > Flow Control Time (ms/sec)` と `SQL Server:Availability Replica > Flow Control/sec` を確認することも役に立ちます。 これら 2 つの値を乗算すると、最後の秒で、フロー制御がクリアされるのを待っていた時間が示されます。 長いフロー制御待機時間、小さい送信レート。  
  
 以下のメトリックは、ネットワーク遅延とスループットの診断に役立ちます。 **ping.exe** や[ネットワーク モニター](https://www.microsoft.com/download/details.aspx?id=4865)などの他の Windows ツールを使用して、待機時間とネットワーク使用率を評価できます。  
  
-   DMV `sys.dm_hadr_database_replica_states, log_send_queue_size`  
  
-   DMV `sys.dm_hadr_database_replica_states, log_send_rate`  
  
-   パフォーマンス カウンター`SQL Server:Database > Log Bytes Flushed/sec`  
  
-   パフォーマンス カウンター`SQL Server:Database Mirroring > Send/Receive Ack Time`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Bytes Sent to Replica/sec`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Bytes Sent to Transport/sec`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Flow Control Time (ms/sec)`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Flow Control/sec`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Resent Messages/sec`  

この問題を解決するには、ネットワーク帯域幅をアップグレードするか、不要なネットワーク トラフィックを削除するか減らしてみてください。  


##  <a name="BKMK_IO_BOTTLENECK"></a> ディスク I/O のボトルネックのために、セカンダリ レプリカでログの書き込みが遅くなる  
 データベース ファイルの配置によっては、レポート ワークロードとの I/O の競合により、ログの書き込みが遅くなる可能性があります。  
  
### <a name="explanation"></a>説明  
 ログ ブロックがログ ファイルに書き込まれるとすぐに、データの損失が回避されます。 そのため、ログ フィルとデータ ファイルを分離することが重要です。 ログ ファイルとデータ ファイルの両方が同じハード ディスクにマッピングされている場合、データ ファイルの読み取りを頻繁に行うレポート ワークロードが、ログ書き込み操作に必要な量と同じ I/O リソースを消費します。 低速の書き込みのためにプライマリ レプリカへの確認が遅くなり、そのためにフロー制御の過度のアクティブ化が発生し、フロー制御の待機時間が長くなる可能性があります。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 ネットワークが高待機時間または低スループットの影響を受けていないことを確認した場合、I/O の競合についてセカンダリ レプリカを調査する必要があります。 「[SQL Server: ディスク I/O を最小限に抑える](https://technet.microsoft.com/magazine/jj643251.aspx)」のクエリは、競合を特定する場合に便利です。 便宜上、その記事の例を下に示します。  
  
 次のスクリプトは、SQL Server インスタンス上で実行されているすべての可用性データベースに関して、各データ ファイルとログ ファイルの読み取りと書き込みの回数を表示することができます。 これは平均 I/O 停止時間 (ミリ秒) で並べ替えられます。 数字は、前回のサーバー インスタンスの開始時刻からの累積であることに注意してください。 そのため、しばらく時間が経過した後に 2 つの測定値の差を取得する必要があります。  
  
```sql  
SELECT DB_NAME(database_id) AS   
   [Database Name] ,   
   file_id ,   
   io_stall_read_ms ,   
   num_of_reads ,   
   CAST(io_stall_read_ms / ( 1.0 + num_of_reads ) AS NUMERIC(10, 1)) AS [avg_read_stall_ms] ,   
   io_stall_write_ms ,   
   num_of_writes ,  
   CAST(io_stall_write_ms / ( 1.0 + num_of_writes ) AS NUMERIC(10, 1)) AS [avg_write_stall_ms] ,   
   io_stall_read_ms + io_stall_write_ms AS [io_stalls] ,   
   num_of_reads + num_of_writes AS [total_io] ,   
   CAST(( io_stall_read_ms + io_stall_write_ms ) / ( 1.0 + num_of_reads  
+ num_of_writes) AS NUMERIC(10,1)) AS [avg_io_stall_ms]  
FROM sys.dm_io_virtual_file_stats(NULL, NULL)  
WHERE DB_NAME(database_id) IN (SELECT DISTINCT database_name FROM sys.dm_hadr_database_replica_cluster_states)  
ORDER BY avg_io_stall_ms DESC;  
```  
  
 次のクエリは、システムで保留中の I/O 要求の特定の時点の (累積ではない) スナップショットを提供します。  
  
```sql  
SELECT DB_NAME(mf.database_id) AS [Database] ,   
   mf.physical_name ,  
   r.io_pending ,   
   r.io_pending_ms_ticks ,   
   r.io_type ,   
   fs.num_of_reads ,   
   fs.num_of_writes  
FROM sys.dm_io_pending_io_requests AS r   
INNER JOIN sys.dm_io_virtual_file_stats(NULL, NULL) AS fs ON r.io_handle = fs.file_handle   
INNER JOIN sys.master_files AS mf ON fs.database_id = mf.database_id  
AND fs.file_id = mf.file_id  
ORDER BY r.io_pending , r.io_pending_ms_ticks DESC;  
```  
  
 読み取り I/O と書き込み I/O が相互にどのような比率になっているかを比較して、I/O の競合を識別することができます。  
  
 ボトルネックを診断する際に役立つその他の一部のパフォーマンス カウンターを次に示します。  
  
-   **物理ディスク: すべてのカウンター**  
  
-   **物理ディスク:Avg.Disk sec/Transfer**  
  
-   **SQL Server:Databases > Log Flush Wait Time**  
  
-   **SQL Server:Databases > Log Flush Waits/sec**  
  
-   **SQL Server:Databases > Log Pool Disk Reads/sec**  
  
 I/O のボトルネックを特定し、ログ ファイルとデータ ファイルが同じハード ディスク上に置かれている場合、最初の手順として、データ ファイルとログ ファイルを別々のディスクに置く必要があります。 このベスト プラクティスにより、レポート ワークロードが、プライマリ レプリカからログ バッファーへのログ転送パスに干渉することがなくなり、セカンダリ ディスク上でトランザクションを書き込む機能に影響しなくなります。  
  
## <a name="next-steps"></a>次のステップ  
 [SQL Server (SQL Server 2012 に適用されます) のパフォーマンスに関する問題のトラブルシューティング](https://msdn.microsoft.com/library/dd672789(v=SQL.100).aspx)  
  
  
