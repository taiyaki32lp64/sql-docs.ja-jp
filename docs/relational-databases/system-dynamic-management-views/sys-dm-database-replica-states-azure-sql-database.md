---
title: dm_database_replica_states (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_replica_states_TSQL
- sys.dm_database_replica_states
- dm_database_replica_states
- dm_database_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_database_replica_states dynamic management view
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0b8fab1b53e5a86139728f49169c50cfa014698a
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983064"
---
# <a name="sysdm_database_replica_states-azure-sql-database"></a>sys.dm_database_replica_states (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  ローカルレプリカの状態を公開しているデータベースの行を返します。  
  
> [!IMPORTANT]
> アクションと上位レベルの状態によっては、データベース状態情報が使用できなくなったり、古くなったりする可能性があります。 また、値はローカルに関連しているものに限られます。 
   
|列名|データ型|説明 (プライマリレプリカ上)|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|データベースの識別子。|  
|**group_id**|**uniqueidentifier**|データベースが属する可用性グループの識別子。|  
|**replica_id**|**uniqueidentifier**|可用性グループ内の可用性レプリカの識別子。|  
|**group_database_id**|**uniqueidentifier**|可用性グループ内のデータベースの識別子。 この識別子は、このデータベースが参加しているすべてのレプリカで同じです。|  
|**is_local**|**bit**|可用性データベースがローカルであるかどうか。次のいずれかになります。<br /><br /> 0 = データベースは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対してローカルではありません。<br /><br /> 1 = データベースはサーバー インスタンスに対してローカルです。|  
|**is_primary_replica**|**bit**|レプリカがプライマリの場合は1、データベースが属する可用性グループのセカンダリレプリカである場合は0を返します。 これは、分散型可用性グループまたはアクティブ geo レプリケーション関係のプライマリデータベースまたはセカンダリデータベースを参照しません。<br /><br />**適用対象:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。|  
|**synchronization_state**|**tinyint**|データ移動の状態。次のいずれかの値です。<br /><br /> 0 = 同期されていません。 プライマリ データベースの場合、データベースがそのトランザクション ログを対応するセカンダリ データベースと同期する準備ができていないことを示します。 セカンダリ データベースの場合、データベースが接続の問題によりログの同期を開始していないか、データベースが中断されているか、起動中またはロールの切り替え中にデータベースが遷移状態になっていることを示します。<br /><br /> 1 = 同期中です。 プライマリデータベースの場合は、データベースがセカンダリデータベースからのスキャン要求を受け入れる準備ができていることを示します。 セカンダリ データベースについては、そのデータベースのアクティブなデータ移動が行われていることを示します。<br /><br /> 2 = 同期済み。 プライマリ データベースでは、"SYNCHRONIZING" の代わりに、"SYNCHRONIZED" と表示されます。 同期コミットのセカンダリ データベースでは、データベース レプリカでフェールオーバーの準備ができていることをローカル キャッシュが示している場合、およびデータベース レプリカが同期中である場合、"同期済み" と表示されます。<br /><br /> 3 = 元に戻す。 セカンダリ データベースがプライマリ データベースからページをアクティブに取得している場合の元に戻すプロセスのフェーズを示します。<br />**注意:** セカンダリレプリカ上のデータベースが復元中の状態にある場合、セカンダリレプリカに強制的にフェールオーバーすると、そのデータベースはプライマリデータベースとして起動できない状態のままになります。 データベースをセカンダリデータベースとして再接続する必要があるか、ログバックアップから新しいログレコードを適用する必要があります。<br /><br /> 4 = 初期化中。 セカンダリ データベースが元に戻す LSN からの遅れを取り戻すために必要なトランザクション ログがセカンダリ レプリカに配布され、書き込まれている場合の元に戻すフェーズを示します。<br />**注意:** セカンダリレプリカ上のデータベースが初期化中の状態である場合、セカンダリレプリカに強制的にフェールオーバーすると、そのデータベースはプライマリデータベースとして起動できない状態のままになります。 データベースをセカンダリデータベースとして再接続する必要があるか、ログバックアップから新しいログレコードを適用する必要があります。|  
|**synchronization_state_desc**|**nvarchar(60)**|データ移動の状態の説明。次のいずれかになります。<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> 戻し<br /><br /> 初期化|  
|**is_commit_participant**|**bit**|0 = このデータベースに対してトランザクションのコミットが同期されていません。<br /><br /> 1 = このデータベース レプリカに対してトランザクションのコミットが同期されています。<br /><br /> 非同期コミットの可用性レプリカにあるデータベースの場合、この値は常に 0 になります。<br /><br /> 同期コミット可用性レプリカのデータベースの場合、この値はプライマリデータベースでのみ正確です。|  
|**synchronization_health**|**tinyint**|可用性レプリカの可用性グループに参加しているデータベースの同期状態と可用性レプリカの可用性モード (同期コミットモードまたは非同期コミットモード) の共通部分を反映します。次の値。<br /><br /> 0 = 異常です。 データベースの**synchronization_state**が 0 (同期していません) です。<br /><br /> 1 = 部分的に正常。 同期コミット可用性レプリカのデータベースは、 **synchronization_state**が 1 (同期中) の場合、部分的に正常と見なされます。<br /><br /> 2 = 正常。 同期コミット可用性レプリカのデータベースは、 **synchronization_state**が 2 (SYNCHRONIZED) の場合に正常と見なされ、非同期コミット可用性レプリカのデータベースは、 **synchronization_state**が 1 (同期中) の場合に正常と見なされます。|  
|**synchronization_health_desc**|**nvarchar(60)**|可用性データベースの**synchronization_health**の説明。<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> 戻ら|  
|**database_state**|**tinyint**|0 = オンライン<br /><br /> 1 = 復元<br /><br /> 2 = 回復中<br /><br /> 3 = 復旧保留<br /><br /> 4 = 問題あり<br /><br /> 5 = 緊急<br /><br /> 6 = オフライン<br /><br /> **注:** Sys. databases の**state**列と同じです。|  
|**database_state_desc**|**nvarchar(60)**|可用性レプリカの**database_state**の説明。<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **注:** **State_desc** 、データベースの列と同じです。|  
|**is_suspended**|**bit**|データベースの状態。次のいずれかになります。<br /><br /> 0 = 再開<br /><br /> 1 = 中断|  
|**suspend_reason**|**tinyint**|データベースが中断されている場合、中断状態の理由は次のいずれかになります。<br /><br /> 0 = ユーザーの操作<br /><br /> 1 = パートナーからの中断<br /><br /> 2 = やり直し<br /><br /> 3 = キャプチャ<br /><br /> 4 = 適用<br /><br /> 5 = 再起動<br /><br /> 6 = 元に戻す<br /><br /> 7 = 再検証<br /><br /> 8 = セカンダリ レプリカの同期ポイントの計算エラー|  
|**suspend_reason_desc**|**nvarchar(60)**|データベースの中断状態の理由の説明。次のいずれかになります。<br /><br /> SUSPEND_FROM_USER: ユーザーが手動でデータ移動を中断しました<br /><br /> SUSPEND_FROM_PARTNER = 強制フェールオーバー後にデータベースレプリカが中断される<br /><br /> SUSPEND_FROM_REDO: 再実行フェーズ中にエラー発生しました<br /><br /> SUSPEND_FROM_APPLY = ログをファイルに書き込むときにエラーが発生しました (エラーログを参照してください)<br /><br /> SUSPEND_FROM_CAPTURE: プライマリ レプリカのログをキャプチャ中にエラーが発生しました<br /><br /> SUSPEND_FROM_RESTART: データベースを再起動する前にデータベース レプリカが中断されました (エラー ログを参照してください)<br /><br /> SUSPEND_FROM_UNDO: 元に戻すフェーズ中にエラー発生しました (エラー ログを参照してください)<br /><br /> SUSPEND_FROM_REVALIDATION = 再接続時にログ変更の不一致が検出されました (エラーログを参照してください)<br /><br /> SUSPEND_FROM_XRF_UPDATE: 共通のログ ポイントが見つかりません (エラー ログを参照してください)|  
|**recovery_lsn**|**numeric(25,0)**|プライマリ レプリカの場合、復旧後またはフェールオーバー後、プライマリ データベースが新しいログ レコードを書き込む前のトランザクション ログの末尾。 特定のセカンダリデータベースについて、この値が現在書き込まれている LSN (last_hardened_lsn) よりも小さい場合、recovery_lsn は、このセカンダリデータベースが再同期する必要がある値 (つまり、に戻して再初期化する) です。 この値が現在書き込まれている LSN 以上の場合、再同期は不要であり、発生しません。<br /><br /> **recovery_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログシーケンス番号 (LSN) ではありません。|  
|**truncation_lsn**|**numeric(25,0)**|プライマリレプリカでは、プライマリデータベースについて、対応するすべてのセカンダリデータベースにおける最小ログ切り捨て LSN が反映されます。 ローカル ログの切り捨てが (バックアップ操作などにより) ブロックされている場合、この LSN はローカル切り捨て LSN を超える可能性があります。<br /><br /> 特定のセカンダリ データベースでは、対象となるデータベースの切り捨てポイントが反映されます。<br /><br /> **truncation_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。|  
|**last_sent_lsn**|**numeric(25,0)**|すべてのログブロックがプライマリによって送信されたポイントを示すログブロック識別子。 これは、最後に送信されたログ ブロックの ID ではなく、次に送信されるログ ブロックの ID です。<br /><br /> **last_sent_lsn**には、0で埋め込まれたログブロック ID が反映されます。これは実際のログシーケンス番号ではありません。|  
|**last_sent_time**|**datetime**|最後のログブロックが送信された時刻。|  
|**last_received_lsn**|**numeric(25,0)**|このセカンダリデータベースをホストするセカンダリレプリカによって受信されたすべてのログブロックの最大ポイントを示すログブロック ID。<br /><br /> **last_received_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。|  
|**last_received_time**|**datetime**|最後に受信したメッセージのログ ブロック ID がセカンダリ レプリカで読み取られた時刻。|  
|**last_hardened_lsn**|**numeric(25,0)**|セカンダリデータベースで最後に書き込まれた LSN のログレコードを含むログブロックの先頭。<br /><br /> 非同期コミットプライマリデータベース、または現在のポリシーが "delay" である同期コミットデータベースでは、値は NULL です。 その他の同期コミットプライマリデータベースの場合、 **last_hardened_lsn**は、すべてのセカンダリデータベースで書き込まれた lsn の最小値を示します。<br /><br /> **注: last_hardened_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。|  
|**last_hardened_time**|**datetime**|セカンダリデータベースで、最後に書き込まれた LSN のログブロック識別子の時刻 (**last_hardened_lsn**)。 プライマリ データベースの場合、書き込まれた LSN の最小値に対応する時刻が反映されます。|  
|**last_redone_lsn**|**numeric(25,0)**|セカンダリデータベースで再実行された最後のログレコードの実際のログシーケンス番号。 **last_redone_lsn**は常に**last_hardened_lsn**未満です。|  
|**last_redone_time**|**datetime**|セカンダリ データベースでログ レコードが最後に再実行された時刻。|  
|**log_send_queue_size**|**bigint**|セカンダリ データベースに送信されていない、プライマリ データベースのログ レコードの量 (KB 単位)。|  
|**log_send_rate**|**bigint**|プライマリレプリカインスタンスが最後のアクティブ期間中にデータを送信した平均速度 (kb/秒)。|  
|**redo_queue_size**|**bigint**|まだ再実行されていないセカンダリレプリカのログファイル内のログレコードの量 (KB 単位)。|  
|**redo_rate**|**bigint**|特定のセカンダリデータベースでログレコードが再実行される平均速度 (kb/秒)。|  
|**filestream_send_rate**|**bigint**|FILESTREAM ファイルがセカンダリ レプリカに配布される速度 (KB/秒)。|  
|**end_of_log_lsn**|**numeric(25,0)**|ログ LSN のローカル終了。 プライマリデータベースとセカンダリデータベースのログキャッシュ内の最後のログレコードに対応する実際の LSN。 プライマリ レプリカの場合、セカンダリ行には、セカンダリ レプリカがプライマリ レプリカに送信した最新の進捗状況メッセージからのログ LSN の末尾が反映されます。<br /><br /> **end_of_log_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。|  
|**last_commit_lsn**|**numeric(25,0)**|トランザクション ログの最終コミット レコードに対応する実際のログ シーケンス番号。<br /><br /> プライマリ データベースの場合、これは処理された最終コミット レコードに対応します。 セカンダリ データベースの行には、セカンダリ レプリカがプライマリ レプリカに送信したログ シーケンス番号が反映されます。<br /><br /> セカンダリ レプリカの場合、これは再実行された最終コミット レコードです。|  
|**last_commit_time**|**datetime**|最終コミット レコードに対応する時刻。<br /><br /> セカンダリ データベースの場合、この時刻はプライマリ データベースと同じになります。<br /><br /> プライマリ レプリカの場合、各セカンダリ データベースの行に、そのセカンダリ データベースをホストするセカンダリ レプリカがプライマリ レプリカに報告した時刻が表示されます。 プライマリデータベースの行と特定のセカンダリデータベースの行の間の時刻の差は、再実行プロセスが検出され、進行状況がプライマリレプリカに報告されていることを前提として、目標復旧時点 (RPO) を表します。セカンダリレプリカによって。|  
|**low_water_mark_for_ghosts**|**bigint**|プライマリデータベースのゴーストクリーンアップで使用される下限を示す、データベースの単調に増加する数。 この数が時間の経過と共に増加していない場合は、ゴーストクリーンアップが行われない可能性があることを意味します。 プライマリ レプリカでは、クリーンアップする非実体行を決定するために、すべての可用性レプリカ (プライマリ レプリカを含む) でこのデータベースのこの列の最小値を使用します。|  
|**secondary_lag_seconds**|**bigint**|同期中にセカンダリレプリカがプライマリレプリカの背後にある秒数。<br /><br />**適用対象:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
|**quorum_commit_lsn**|**numeric(25,0)**|単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。|
|**quorum_commit_time**|**datetime**|単に情報を示すためだけに特定されます。 サポートされていません。 将来の互換性は保証されません。|


## <a name="permissions"></a>アクセス許可

データベースに対する VIEW DATABASE STATE 権限が必要です。


## <a name="see-also"></a>参照

- [AlwaysOn 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)
- [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)
