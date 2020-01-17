---
title: セカンダリ可用性グループ レプリカで変更が表示されない
ms.description: Troubleshoot to determine why changes occurring on a primary replica are not reflected on the secondary replica for an Always On availability group.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: c602fd39-db93-4717-8f3a-5a98b940f9cc
author: rothja
ms.author: jroth
ms.openlocfilehash: 55dc6787960fbb4979bbe0d21f27f0fa43437662
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243009"
---
# <a name="determine-why-changes-from-primary-replica-are-not-reflected-on-secondary-replica-for-an-always-on-availability-group"></a>可用性グループでセカンダリ レプリカにプライマリ レプリカの変更が反映されない理由を判断する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  クライアント アプリケーションは、プライマリ レプリカの更新を正常に完了しますが、セカンダリ レプリカのクエリを実行すると、変更が反映されていないことが示されます。 この場合、可用性の同期状態は正常であると仮定します。 ほとんどの場合、この動作は、数分後に解決します。  
  
 変更が数分後にセカンダリ レプリカでまだ反映されていない場合、同期ワークフローにボトルネックがある可能性があります。 ボトルネックの場所は、セカンダリ レプリカが同期コミットまたは非同期コミットのどちらに設定されているかどうかによって異なります。  
  
 **[同期コミット]**  
  
 プライマリ レプリカでの正常な更新がセカンダリ レプリカに既に同期されているか、またはログ レコードがセカンダリ レプリカでセキュリティ強化のためにフラッシュされています。 そのため、ボトルネックは、セカンダリ レプリカでログがフラッシュされた後に発生する再実行プロセスにあります。  
  
 ただし、再実行の確認後、セカンダリ レプリカ上のすべての読み取りワークロードは、スナップショット分離になります。  
  
  -   プライマリ レプリカでの実行時間の長いトランザクション  
  
  -   セカンダリ レプリケーションでの再実行  


**[非同期コミット]**  
 
 非同期コミットでは、トランザクションがローカル ディスクにフラッシュされるとすぐに確認をコミットするため、ボトルネックは、その後のどこかの場所で発生する可能性があります。  
 
  -   プライマリ レプリカでの実行時間の長いトランザクション  
  
  -   ネットワークの遅延またはスループット  
  
  -   セカンダリ レプリカでログの強化  
  
  -   セカンダリ レプリカで再実行  


以下のセクションでは、プライマリ レプリカで変更が読み取り専用クエリでセカンダリ レプリカに反映されていない一般的な原因について説明します。  


##  <a name="BKMK_OLDTRANS"></a> 実行時間の長いアクティブなトランザクション  
 プライマリ レプリカでの実行時間の長いトランザクションは、更新がセカンダリ レプリカで読み取られることを妨げます。  
  
### <a name="explanation"></a>説明  
 セカンダリ レプリカ上のすべての読み取りワークロードは、スナップショット分離クエリです。 スナップショット分離では、読み取り専用のクライアントは、再実行ログ内の最も古いアクティブなトランザクションの開始時点でセカンダリ レプリカの可用性データベースを参照します。 トランザクションが数時間コミットされていない場合、未完了のトランザクションが、新しい更新を表示できないようにすべての読み取り専用クエリをブロックします。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 プライマリ レプリカで、 [DBCC OPENTRAN &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-opentran-transact-sql.md) を使用して、最も古いアクティブなトランザクションを表示し、それらをロールバックできるかどうかを確認します。 最も古いアクティブなトランザクションがロールバックされ、セカンダリ レプリカに同期された後、セカンダリ レプリカ上の読み取りワークロードは、次に古いアクティブなトランザクションの先頭までの可用性データベース内の更新を確認できます。  
  
##  <a name="BKMK_LATENCY"></a> 長いネットワーク遅延またはスループットが低いネットワークは、プライマリ レプリカでログの構築の原因になります。  
 長いネットワーク遅延または低いスループットは、セカンダリ レプリカに十分な速さでログが送信されることを妨げます。  
  
### <a name="explanation"></a>説明  
 プライマリ レプリカは、セカンダリ レプリカに送信される未確認メッセージの許可される最大数を超えたときにログ送信のフロー制御をアクティブにします。 これらのメッセージの一部が確認されるまで、セカンダリ レプリカにそれ以上のログ ブロックを送信できません。 このような状況は、データ損失の可能性に重要な影響があり、場合によって、回復ポイントの目標 (RPO) を損なうことがあります。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 高い DMV 値 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) は、プライマリ レプリカでログが保持されていることを示す可能性があります。 この値を [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) で除算すると、セカンダリ レプリカでデータがキャッチされるまでの時間の大まかな推定値を得ることができます。  
  
 また、2 つのパフォーマンス オブジェクト [SQL Server: 可用性レプリカ > フロー制御時間 (ミリ秒/秒)](~/relational-databases/performance-monitor/sql-server-availability-replica.md) と [SQL Server: 可用性レプリカ > フロー制御/秒](~/relational-databases/performance-monitor/sql-server-availability-replica.md)を確認することも役に立ちます。これら 2 つの値を乗算すると、最後の秒で、フロー制御がクリアされるのを待っていた時間が示されます。 長いフロー制御待機時間、小さい送信レート。  
  
 以下に、ネットワーク遅延とスループットの診断に役立つメトリックの一覧を示します。 **ping.exe** などの他の Windows ツールを使用して、ネットワーク使用率を評価できます。  
  
-   DMV [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   DMV [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)  
  
-   パフォーマンス カウンター`SQL Server:Database > Log Bytes Flushed/sec`  
  
-   パフォーマンス カウンター`SQL Server:Database Mirroring > Send/Receive Ack Time`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Bytes Sent to Replica/sec`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Bytes Sent to Transport/sec`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Flow Control Time (ms/sec)`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Flow Control/sec`  
  
-   パフォーマンス カウンター`SQL Server:Availability Replica > Resent Messages/sec`  
  
 この問題を解決するには、ネットワーク帯域幅をアップグレードするか、不要なネットワーク トラフィックを削除するか減らしてみてください。  
  
##  <a name="BKMK_REDOBLOCK"></a> 別のレポート ワークロードが再実行スレッドの実行をブロックする  
 セカンダリ レプリカの再実行スレッドが、実行時間の長い読み取り専用クエリによるデータ定義言語 (DDL) の変更をブロックしています。 再実行スレッドが読み取りワークロードで利用できるように追加の更新を提供するには、その前に再実行スレッドがブロック解除される必要があります。  
  
### <a name="explanation"></a>説明  
 セカンダリ レプリカで、読み取り専用のクエリが、スキーマ安定度 (`Sch-S`) ロックを取得します。 これらの `Sch-S` ロックは、DDL の変更を実行するためのスキーマ変更 (`Sch-M`) ロックを再実行スレッドが取得できないようにブロックします。 ブロックされた再実行スレッドは、ブロック解除されるまで、ログ レコードを適用できません。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 再実行スレッドがブロックされると、`sqlserver.lock_redo_blocked` と呼ばれる拡張イベントが生成されます。 さらに、DMV sys.dm_exec_request をクエリして、どのセッションが再実行スレッドをブロックしているかを調べ、是正措置を行うことができます。 次のクエリでは、再実行スレッドをブロックしているレポートのワークロードのセッション ID を返します。  
  
```sql  
select session_id, command, blocking_session_id, wait_time, wait_type, wait_resource   
from sys.dm_exec_requests where command = 'DB STARTUP'  
```  
  
 レポート ワークロードを完了させて、その時点で再実行スレッドをブロック解除させるか、ブロックしているセッション ID で [KILL &#40;Transact-SQL&#41; ](~/t-sql/language-elements/kill-transact-sql.md) を実行して直ちに再実行スレッドをブロック解除することができます。  
  
##  <a name="BKMK_REDOBEHIND"></a> リソースの競合のために再実行スレッドが遅れる  
 セカンダリ レプリカでの大量のレポート ワークロードのために、セカンダリ レプリカのパフォーマンスが低下し、再実行スレッドが遅れています。  
  
### <a name="explanation"></a>説明  
 セカンダリ レプリカでログ レコードを適用しているときに、再実行スレッドがログ ディスクからログ レコードを読み取り、各ログ レコードについて、ログ レコードを適用するために、データ ページにアクセスします。 ページがバッファー プールにまだ存在しない場合、ページ アクセスは I/O バウンド (物理ディスクへのアクセス) になる可能性があります。 I/O バウンドのレポート ワークロードがある場合、レポート ワークロードは、再実行スレッドと I/O リソースを競合し、再実行スレッドの速度が低下することがあります。 このような状況は、更新されたデータを読み取るその他のレポート ワークロードに影響するだけでなく、RTO にも影響します。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 次の DMV クエリを使用して、`last_redone_lsn` と `last_received_lsn` の間の違いを測定することで、再実行スレッドがどの程度遅れているかを確認できます。  
  
```sql  
select recovery_lsn, truncation_lsn, last_hardened_lsn, last_received_lsn,   
   last_redone_lsn, last_redone_time  
from sys.dm_hadr_database_replica_states  
  
```  
  
 再実行スレッドが実際に遅れている場合、セカンダリ レプリカのパフォーマンスの低下の根本原因を調査する必要があります。 レポート ワークロードとの I/O の競合がある場合、[リソース ガバナー](~/relational-databases/resource-governor/resource-governor.md)を使用して、レポート ワークロードによって使用される CPU サイクルを制御し、取得される I/O サイクルを間接的にある程度制御することができます。 たとえば、レポート ワークロードが CPU の 10% を消費していても、ワークロードが I/O バウンドになっている場合は、リソース ガバナーを使用して、CPU リソースの使用率を 5% に制限し、読み取りワークロードを制限して、I/O への影響を最小限に抑えることができます。  
  
## <a name="next-steps"></a>次のステップ  
 [SQL Server 2008 のパフォーマンスに関する問題のトラブルシューティング](https://msdn.microsoft.com/library/dd672789(v=sql.100).aspx) 
  
  
