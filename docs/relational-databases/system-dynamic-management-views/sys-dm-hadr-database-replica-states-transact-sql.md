---
title: dm_hadr_database_replica_states (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_hadr_database_states_TSQL
- sys.dm_hadr_database_states
- dm_hadr_database_states
- dm_hadr_database_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_hadr_database_replica_states dynamic management view
ms.assetid: 1a17b0c9-2535-4f3d-8013-cd0a6d08f773
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83b3c369add51a853078dd64a8861d633ac330ec
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982276"
---
# <a name="sysdm_hadr_database_replica_states-transact-sql"></a>sys.dm_hadr_database_replica_states (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカルインスタンスが可用性レプリカをホストしている Always On 可用性グループに参加しているデータベースごとに1行のデータを返します。 この動的管理ビューは、プライマリ レプリカとセカンダリ レプリカの両方の状態情報を公開します。 セカンダリ レプリカの場合、このビューはサーバー インスタンス上のセカンダリ データベースごとに 1 行のデータを返します。 プライマリ レプリカの場合、このビューはプライマリ データベースごとに 1 行のデータと、対応するセカンダリ データベースについての追加の行のデータを返します。  
  
> [!IMPORTANT]
> アクションおよび上位レベルの状態によっては、データベースの状態情報が使用できないか、最新でない場合があります。 また、値はローカルに関連しているものに限られます。 たとえば、プライマリレプリカでは、 **[last_hardened_lsn]** 列の値には、セカンダリレプリカが現在使用している可能性のある実際に書き込まれた lsn 値ではなく、現在プライマリレプリカで使用できる特定のセカンダリデータベースに関する情報が反映されます。  
   
|列名|データ型|説明 (プライマリ レプリカの場合)|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|SQL Server のインスタンス内で一意な、データベースの識別子。 これは、[データベース](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)カタログビューに表示される値と同じです。|  
|**group_id**|**uniqueidentifier**|データベースが属する可用性グループの識別子。|  
|**replica_id**|**uniqueidentifier**|可用性グループ内の可用性レプリカの識別子。|  
|**group_database_id**|**uniqueidentifier**|可用性グループ内のデータベースの識別子。 この識別子は、このデータベースが参加しているすべてのレプリカで同じです。|  
|**is_local**|**bit**|可用性データベースがローカルであるかどうか。次のいずれかになります。<br /><br /> 0 = データベースは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対してローカルではありません。<br /><br /> 1 = データベースはサーバー インスタンスに対してローカルです。|  
|**is_primary_replica**|**bit**|セカンダリ レプリカである場合、レプリカがプライマリ サーバー、または 0 の場合は、1 を返します。<br /><br />**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。|  
|**synchronization_state**|**tinyint**|データ移動の状態。次のいずれかの値です。<br /><br /> 0 = 同期されていません。 プライマリ データベースの場合、データベースがそのトランザクション ログを対応するセカンダリ データベースと同期する準備ができていないことを示します。 セカンダリ データベースの場合、データベースが接続の問題によりログの同期を開始していないか、データベースが中断されているか、起動中またはロールの切り替え中にデータベースが遷移状態になっていることを示します。<br /><br /> 1 = 同期中です。 プライマリデータベースの場合は、データベースがセカンダリデータベースからのスキャン要求を受け入れる準備ができていることを示します。 セカンダリ データベースについては、そのデータベースのアクティブなデータ移動が行われていることを示します。<br /><br /> 2 = 同期済み。 プライマリ データベースでは、"SYNCHRONIZING" の代わりに、"SYNCHRONIZED" と表示されます。 同期コミットのセカンダリ データベースでは、データベース レプリカでフェールオーバーの準備ができていることをローカル キャッシュが示している場合、およびデータベース レプリカが同期中である場合、"同期済み" と表示されます。<br /><br /> 3 = 元に戻す。 セカンダリ データベースがプライマリ データベースからページをアクティブに取得している場合の元に戻すプロセスのフェーズを示します。<br />**注意:** セカンダリレプリカ上のデータベースが復元中の状態にある場合、セカンダリレプリカに強制的にフェールオーバーすると、そのデータベースはプライマリデータベースとして起動できない状態のままになります。 データベースにセカンダリ データベースとして再接続するか、ログ バックアップから新しいログ レコードを適用する必要があります。<br /><br /> 4 = 初期化中。 セカンダリ データベースが元に戻す LSN からの遅れを取り戻すために必要なトランザクション ログがセカンダリ レプリカに配布され、書き込まれている場合の元に戻すフェーズを示します。<br />**注意:** セカンダリレプリカ上のデータベースが初期化中の状態である場合、セカンダリレプリカに強制的にフェールオーバーすると、そのデータベースはプライマリデータベースとして起動できない状態のままになります。 データベースにセカンダリ データベースとして再接続するか、ログ バックアップから新しいログ レコードを適用する必要があります。|  
|**synchronization_state_desc**|**nvarchar(60)**|データ移動の状態の説明。次のいずれかになります。<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> REVERTING<br /><br /> INITIALIZING|  
|**is_commit_participant**|**bit**|0 = このデータベース レプリカに対してトランザクションのコミットが同期されていません。<br /><br /> 1 = このデータベース レプリカに対してトランザクションのコミットが同期されています。<br /><br /> 非同期コミットの可用性レプリカにあるデータベースの場合、この値は常に 0 になります。<br /><br /> 同期コミットの可用性レプリカにあるデータベースの場合、この値はプライマリ データベースでのみ正確です。|  
|**synchronization_health**|**tinyint**|可用性レプリカの可用性グループに参加しているデータベースの同期状態と可用性レプリカの可用性モード (同期コミットモードまたは非同期コミットモード) の共通部分を反映します。次の値。<br /><br /> 0 = 異常です。 データベースの**synchronization_state**が 0 (同期していません) です。<br /><br /> 1 = 部分的に正常。 同期コミット可用性レプリカのデータベースは、 **synchronization_state**が 1 (同期中) の場合、部分的に正常と見なされます。<br /><br /> 2 = 正常。 同期コミット可用性レプリカのデータベースは、 **synchronization_state**が 2 (SYNCHRONIZED) の場合に正常と見なされ、非同期コミット可用性レプリカのデータベースは、 **synchronization_state**が 1 (同期中) の場合に正常と見なされます。|  
|**synchronization_health_desc**|**nvarchar(60)**|可用性データベースの**synchronization_health**の説明。<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**database_state**|**tinyint**|0 = オンライン<br /><br /> 1 = 復元<br /><br /> 2 = 回復します。<br /><br /> 3 = 復旧保留<br /><br /> 4 = 問題あり<br /><br /> 5 = 緊急<br /><br /> 6 = オフライン<br /><br /> **注:** Sys. databases の**state**列と同じです。|  
|**database_state_desc**|**nvarchar(60)**|可用性レプリカの**database_state**の説明。<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **注:** **State_desc** 、データベースの列と同じです。|  
|**is_suspended**|**bit**|データベースの状態。次のいずれかになります。<br /><br /> 0 = 再開<br /><br /> 1 = 中断|  
|**suspend_reason**|**tinyint**|データベースが中断されている場合の中断状態の理由。次のいずれかになります。<br /><br /> 0 = ユーザーのアクション<br /><br /> 1 = パートナーにより中断<br /><br /> 2 = やり直し<br /><br /> 3 = キャプチャ<br /><br /> 4 = 適用<br /><br /> 5 = 再起動<br /><br /> 6 = 取り消し<br /><br /> 7 = 再検証<br /><br /> 8 = セカンダリ レプリカの同期ポイントの計算エラー|  
|**suspend_reason_desc**|**nvarchar(60)**|データベースの中断状態の理由の説明。次のいずれかになります。<br /><br /> SUSPEND_FROM_USER: ユーザーが手動でデータ移動を中断しました<br /><br /> SUSPEND_FROM_PARTNER: 強制フェールオーバー後にデータベース レプリカが中断されます<br /><br /> SUSPEND_FROM_REDO: 再実行フェーズ中にエラー発生しました<br /><br /> SUSPEND_FROM_APPLY: ログをファイルに書き込むときにエラーが発生しました (エラー ログを参照してください)<br /><br /> SUSPEND_FROM_CAPTURE: プライマリ レプリカのログをキャプチャ中にエラーが発生しました<br /><br /> SUSPEND_FROM_RESTART: データベースを再起動する前にデータベース レプリカが中断されました (エラー ログを参照してください)<br /><br /> SUSPEND_FROM_UNDO: 元に戻すフェーズ中にエラー発生しました (エラー ログを参照してください)<br /><br /> SUSPEND_FROM_REVALIDATION: ログの変更の不一致が再接続時に検出されました (エラー ログを参照してください)<br /><br /> SUSPEND_FROM_XRF_UPDATE: 共通のログ ポイントが見つかりません (エラー ログを参照してください)|  
|**recovery_lsn**|**numeric(25,0)**|プライマリ レプリカの場合、復旧後またはフェールオーバー後、プライマリ データベースが新しいログ レコードを書き込む前のトランザクション ログの末尾。 特定のセカンダリ データベースでは、この値が書き込まれた現在の LSN (last_hardened_lsn) 未満の場合、recovery_lsn は、このセカンダリ データベースの再同期先 (つまり、復元先および再初期化先) の値です。 この値が書き込まれた現在の LSN 以上の場合、再同期化は不要であり、実行されません。<br /><br /> **recovery_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号 (LSN) ではありません。 この値の派生方法の詳細については、このトピックの「 [LSN 列の値](#LSNcolumns)について」を参照してください。|  
|**truncation_lsn**|**numeric(25,0)**|プライマリ レプリカの場合、プライマリ データベースで、対応するすべてのセカンダリ データベースを対象とする最小のログ切り捨て LSN が反映されます。 ローカル ログの切り捨てが (バックアップ操作などにより) ブロックされている場合、この LSN はローカル切り捨て LSN を超える可能性があります。<br /><br /> 特定のセカンダリ データベースでは、対象となるデータベースの切り捨てポイントが反映されます。<br /><br /> **truncation_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。|  
|**last_sent_lsn**|**numeric(25,0)**|プライマリによって送信されたすべてのログ ブロックの最後のポイントを示すログ ブロック ID。 これは、最後に送信されたログ ブロックの ID ではなく、次に送信されるログ ブロックの ID です。<br /><br /> **last_sent_lsn**には、0で埋め込まれたログブロック ID が反映されます。これは実際のログシーケンス番号ではありません。|  
|**last_sent_time**|**datetime**|ログ ブロックが最後に送信された時刻。|  
|**last_received_lsn**|**numeric(25,0)**|このセカンダリ データベースをホストするセカンダリ レプリカによって受信されたすべてのログ ブロックの最後のポイントを示すログ ブロック ID。<br /><br /> **last_received_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。|  
|**last_received_time**|**datetime**|最後に受信したメッセージのログ ブロック ID がセカンダリ レプリカで読み取られた時刻。|  
|**last_hardened_lsn**|**numeric(25,0)**|セカンダリ データベースで最後に書き込まれた LSN のログ レコードを含むログ ブロックの先頭。<br /><br /> 現在のポリシーが "遅延" の非同期コミット プライマリ データベースまたは同期コミット データベースでは、値は NULL です。 その他の同期コミットプライマリデータベースの場合、 **last_hardened_lsn**は、すべてのセカンダリデータベースで書き込まれた lsn の最小値を示します。<br /><br /> **注: last_hardened_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。 詳細については、このトピックの「 [LSN 列の値につい](#LSNcolumns)て」を参照してください。|  
|**last_hardened_time**|**datetime**|セカンダリデータベースで、最後に書き込まれた LSN のログブロック識別子の時刻 (**last_hardened_lsn**)。 プライマリ データベースの場合、書き込まれた LSN の最小値に対応する時刻が反映されます。|  
|**last_redone_lsn**|**numeric(25,0)**|セカンダリ データベースで再実行された最後のログ レコードの実際のログ シーケンス番号。 **last_redone_lsn**は常に**last_hardened_lsn**未満です。|  
|**last_redone_time**|**datetime**|セカンダリ データベースでログ レコードが最後に再実行された時刻。|  
|**log_send_queue_size**|**bigint**|セカンダリ データベースに送信されていない、プライマリ データベースのログ レコードの量 (KB 単位)。|  
|**log_send_rate**|**bigint**|プライマリレプリカインスタンスが最後のアクティブ期間中にデータを送信した平均速度 (kb/秒)。|  
|**redo_queue_size**|**bigint**|まだ再実行されていないセカンダリ レプリカのログ ファイル内のログ レコードの量 (KB 単位)。|  
|**redo_rate**|**bigint**|特定のセカンダリデータベースでログレコードが再実行される平均速度 (kb/秒)。|  
|**filestream_send_rate**|**bigint**|FILESTREAM ファイルがセカンダリ レプリカに配布される速度 (KB/秒)。|  
|**end_of_log_lsn**|**numeric(25,0)**|ローカルのログ LSN の末尾。 プライマリ データベースおよびセカンダリ データベースのログ キャッシュ内の最後のログ レコードに対応する実際の LSN。 プライマリ レプリカの場合、セカンダリ行には、セカンダリ レプリカがプライマリ レプリカに送信した最新の進捗状況メッセージからのログ LSN の末尾が反映されます。<br /><br /> **end_of_log_lsn**には、0で埋め込まれたログブロック ID が反映されます。 これは実際のログ シーケンス番号ではありません。 詳細については、このトピックの「 [LSN 列の値につい](#LSNcolumns)て」を参照してください。|  
|**last_commit_lsn**|**numeric(25,0)**|トランザクション ログの最終コミット レコードに対応する実際のログ シーケンス番号。<br /><br /> プライマリ データベースの場合、これは処理された最終コミット レコードに対応します。 セカンダリ データベースの行には、セカンダリ レプリカがプライマリ レプリカに送信したログ シーケンス番号が反映されます。<br /><br /> セカンダリ レプリカの場合、これは再実行された最終コミット レコードです。|  
|**last_commit_time**|**datetime**|最終コミット レコードに対応する時刻。<br /><br /> セカンダリ データベースの場合、この時刻はプライマリ データベースと同じになります。<br /><br /> プライマリ レプリカの場合、各セカンダリ データベースの行に、そのセカンダリ データベースをホストするセカンダリ レプリカがプライマリ レプリカに報告した時刻が表示されます。 プライマリデータベースの行と特定のセカンダリデータベースの行の間の時刻の差は、再実行プロセスが検出され、進行状況がプライマリレプリカに報告されていることを前提として、目標復旧時点 (RPO) を表します。セカンダリレプリカによって。|  
|**low_water_mark_for_ghosts**|**bigint**|プライマリ データベースでの非実体クリーンアップで使用される低レベルのウォーター マークを示すデータベースの単調に増加する数値。 この数値が時間の経過と共に増加しない場合は、非実体クリーンアップが行われない可能性があることを意味します。 プライマリ レプリカでは、クリーンアップする非実体行を決定するために、すべての可用性レプリカ (プライマリ レプリカを含む) でこのデータベースのこの列の最小値を使用します。|  
|**secondary_lag_seconds**|**bigint**|同期中にセカンダリレプリカがプライマリレプリカの背後にある秒数。<br /><br />**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。|  
  
##  <a name="LSNcolumns"></a>LSN 列の値について  
 **End_of_log_lsn**、 **last_hardened_lsn**、 **last_received_lsn**、 **last_sent_lsn**、 **recovery_lsn**、および**truncation_lsn**の各列の値は、実際のログシーケンス番号 (lsn) ではありません。 これらの各値には、0 が埋め込まれたログ ブロック ID が反映されます。  
  
 **end_of_log_lsn**、 **last_hardened_lsn**、 **recovery_lsn**は、flush lsn です。 たとえば、 **last_hardened_lsn**は、既にディスク上にあるブロックを超えた次のブロックの開始を示します。  そのため、 **last_hardened_lsn**の値 < LSN はディスク上にあります。  この値以上の LSN はフラッシュされません。  
  
 **Dm_hadr_database_replica_states**によって返される lsn 値のうち、 **last_redone_lsn**だけが実際の lsn になります。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [Always On 可用性グループ &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [可用性グループの監視 &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
  
