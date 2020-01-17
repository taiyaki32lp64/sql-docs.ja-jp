---
title: トラブルシューティング:可用性グループ接続の超過 RTO (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: e83e4ef8-92f0-406f-bd0b-dc48dc210517
author: rothja
ms.author: jroth
ms.openlocfilehash: 9b62bcc1eebe8371bc45ae7f565d9aa712f1b1d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013752"
---
# <a name="troubleshoot-availability-group-exceeded-rto"></a>トラブルシューティング:可用性グループ接続の超過 RTO
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  可用性グループのデータ損失のない自動フェールオーバーまたは計画された手動フェールオーバーの後に、フェールオーバー時間が回復時刻の目標 (RTO) を超えていることに気づく場合があります。 または、「[Always On 可用性グループのパフォーマンスを監視する](monitor-performance-for-always-on-availability-groups.md)」の方法を使用して同期コミット セカンダリ レプリカのフェールオーバー時間を推定したとき (自動フェールオーバー パートナーなど)、RTO を超過していることが判明します。  
  
 自動フェールオーバーが完了していない場合、「[Troubleshooting automatic failover problems in SQL Server 2012 Always On environments](https://support.microsoft.com/kb/2833707)」(SQL Server 2012 AlwaysOn の環境での自動フェールオーバーに関する問題のトラブルシューティング) を参照してください。  
  
 次のセクションでは、フェールオーバー時間が RTO を超える一般的な原因について説明します。  
  
1.  [レポート ワークロードが再実行スレッドの実行をブロックする](#BKMK_REDOBLOCK)  
  
2.  [リソースの競合のために再実行スレッドが遅れる](#BKMK_CONTENTION)  
  
##  <a name="BKMK_REDOBLOCK"></a> レポート ワークロードが再実行スレッドの実行をブロックする  
 セカンダリ レプリカの再実行スレッドが、実行時間の長い読み取り専用クエリによるデータ定義言語 (DDL) の変更をブロックしています。  
  
### <a name="explanation"></a>説明  
 セカンダリ レプリカで、読み取り専用のクエリが、スキーマ安定度 (`Sch-S`) ロックを取得します。 これらの `Sch-S` ロックは、DDL の変更を実行するためのスキーマ変更 (`Sch-M`) ロックを再実行スレッドが取得できないようにブロックします。 ブロックされた再実行スレッドは、ブロック解除されるまで、ログ レコードを適用できません。 ブロックが解除されると、ログの末尾に追いつき、後続の元に戻すプロセスとフェールオーバー プロセスを続行することができます。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 再実行スレッドがブロックされると、`sqlserver.lock_redo_blocked` と呼ばれる拡張イベントが生成されます。 さらに、DMV sys.dm_exec_request をクエリして、どのセッションが再実行スレッドをブロックしているかを調べ、是正措置を行うことができます。 次のクエリでは、再実行スレッドをブロックしている読み取り専用クエリのセッション ID を返します。  
  
```sql  
select session_id, command, blocking_session_id, wait_time, wait_type, wait_resource   
from sys.dm_exec_requests where command = 'DB STARTUP'  
```  
  
 レポート ワークロードを完了させて、その時点で再実行スレッドをブロック解除させるか、ブロックしているセッション ID で [KILL &#40;Transact-SQL&#41; ](~/t-sql/language-elements/kill-transact-sql.md) を実行して直ちに再実行スレッドをブロック解除することができます。  
  
##  <a name="BKMK_CONTENTION"></a> リソースの競合のために再実行スレッドが遅れる  
 セカンダリ レプリカでの大量のレポート ワークロードのために、セカンダリ レプリカのパフォーマンスが低下し、再実行スレッドが遅れています。  
  
### <a name="explanation"></a>説明  
 セカンダリ レプリカでログ レコードを適用しているときに、再実行スレッドがログ ディスクからログ レコードを読み取り、各ログ レコードについて、ログ レコードを適用するために、データ ページにアクセスします。 ページがバッファー プールにまだ存在しない場合、ページ アクセスは I/O バウンド (物理ディスクへのアクセス) になる可能性があります。 I/O バウンドのレポート ワークロードがある場合、レポート ワークロードは、再実行スレッドと I/O リソースを競合し、再実行スレッドの速度が低下することがあります。  
  
### <a name="diagnosis-and-resolution"></a>診断と解決  
 次の DMV クエリを使用して、`last_redone_lsn` と `last_received_lsn` の間の違いを測定することで、再実行スレッドがどの程度遅れているかを確認できます。  
  
```sql  
select recovery_lsn, truncation_lsn, last_hardened_lsn, last_received_lsn,   
   last_redone_lsn, last_redone_time  
from sys.dm_hadr_database_replica_states  
  
```  
  
 再実行スレッドが実際に遅れている場合、セカンダリ レプリカのパフォーマンスの低下の根本原因を調査する必要があります。 レポート ワークロードとの I/O の競合がある場合、[リソース ガバナー](~/relational-databases/resource-governor/resource-governor.md)を使用して、レポート ワークロードによって使用される CPU サイクルを制御し、取得される I/O サイクルを間接的にある程度制御することができます。 たとえば、レポート ワークロードが CPU の 10% を消費していても、ワークロードが I/O バウンドになっている場合は、リソース ガバナーを使用して、CPU リソースの使用率を 5% に制限し、読み取りワークロードを制限して、I/O への影響を最小限に抑えることができます。  
  
## <a name="next-steps"></a>次の手順  
 [SQL Server (SQL Server 2012 に適用されます) のパフォーマンスに関する問題のトラブルシューティング](https://msdn.microsoft.com/library/dd672789(v=SQL.100).aspx)  
  
  
