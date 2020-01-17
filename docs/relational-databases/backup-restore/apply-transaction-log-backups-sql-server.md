---
title: トランザクション ログ バックアップの適用 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], log backups
- transaction log backups [SQL Server], applying backups
- online restores [SQL Server], log backups
- transaction log backups [SQL Server], quantity needed for restore sequence
- backups [SQL Server], log backups
ms.assetid: 9b12be51-5469-46f9-8e86-e938e10aa3a1
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 62d90931cdc1d7748f47edabb31e5f9404b1262d
ms.sourcegitcommit: e7c3c4877798c264a98ae8d51d51cb678baf5ee9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916198"
---
# <a name="apply-transaction-log-backups-sql-server"></a>トランザクション ログ バックアップの適用 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックは完全復旧モデルと一括ログ復旧モデルのみに関連します。  
  
 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの復元の一環として行う、トランザクション ログ バックアップの適用について説明します。  
 
##  <a name="Requirements"></a> トランザクション ログ バックアップを復元するための要件  
 トランザクション ログ バックアップを適用するには、次の要件を満たしている必要があります。  
  
-   **復元シーケンスに必要なログ バックアップの保持:** 復元シーケンスを完了できるだけのログ レコードがバックアップされている必要があります。 復元シーケンスを開始する前に、必要なログ バックアップ (必要な場合は [ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) も含む) が用意されている必要があります。  
  
-   **正しい復元順序:** 先に、データベースの前回の完全バックアップまたは差分バックアップを復元する必要があります。 次に、その完全バックアップまたは差分バックアップの後に作成されたすべてのトランザクション ログを日時順に復元する必要があります。 このログ チェーン内のトランザクション ログ バックアップが失われたかまたは損傷している場合は、失われたトランザクション ログよりも前のトランザクション ログのみを復元できます。  
  
-   **データベースはまだ復旧されていない:** データベースは、最後のトランザクション ログが適用されるまで復旧できません。 いずれかの中間トランザクション ログ バックアップを復元した後 (ログ チェーンが終わる前) にデータベースを復旧する場合、その時点以降にデータベースを復元するには、データベースの完全バックアップから復元シーケンス全体を再度開始する必要があります。  
  
    > [!TIP]
    > ベスト プラクティスとして、すべてのログ バックアップを復元することをお勧めします (`RESTORE LOG *database_name* WITH NORECOVERY`)。 次に、最後のログ バックアップを復元した後、別の操作でデータベースを復旧します (`RESTORE DATABASE *database_name* WITH RECOVERY`)。  
  
##  <a name="RecoveryAndTlogs"></a> 復旧とトランザクション ログ  
 復元操作を完了してデータベースを復旧すると、データベースの整合性を確保するために、復旧プロセスが実行されます。 復旧プロセスの詳細については、「[復元と復旧の概要 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)」を参照してください。
 
 復旧プロセスが完了すると、データベースはオンラインになり、そのデータベースにそれ以上のトランザクション ログ バックアップを適用できなくなります。 たとえば、一連のトランザクション ログ バックアップに、実行時間が長いトランザクションが含まれているとします。 トランザクションの開始は最初のトランザクション ログ バックアップに記録されていますが、トランザクションの終了は 2 番目のトランザクション ログ バックアップに記録されています。 最初のトランザクション ログ バックアップには、コミットやロールバック操作は記録されていません。 最初のトランザクション ログ バックアップが適用されたときに復旧操作を実行すると、実行時間が長いトランザクションは不完全だと見なされ、そのトランザクションに関して最初のトランザクション ログ バックアップに記録されたデータ変更がロールバックされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、この時点より後で 2 番目のトランザクション ログ バックアップを適用することはできません。  
  
> [!NOTE]
> 状況によっては、ログの復元中にファイルを明示的に追加できます。  
  
##  <a name="PITrestore"></a> ログ バックアップを使用し、障害発生時まで復元する  
 次のような一連のイベントが発生したとします。  
  
|Time|イベント|  
|----------|-----------|  
|午前 8 時|データベースの完全バックアップを作成するために、データベースをバックアップします。|  
|正午|トランザクション ログのバックアップ。|  
|午後 4 時|トランザクション ログのバックアップ。|  
|午後 6 時|データベースの完全バックアップを作成するために、データベースをバックアップします。|  
|午後 8 時|トランザクション ログのバックアップ。|  
|午後 9 時 45 分|障害が発生します。|  
  
> この一連のバックアップの例の詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)」を参照してください。  
  
 午後 9時 45分の状態にデータベースを復元するには (障害の時点)、次の代替手順のいずれかを使用します。  

 **代替手順 1: データベースの最新の完全バックアップを使用したデータベースの復元**  
  
1.  障害発生時点にアクティブなトランザクション ログのログ末尾のバックアップを作成します。  
  
2.  午前 8 時に作成した 復元よりも処理に時間がかかります。 代わりに、より近い時刻の午後 6 時の データベースの完全バックアップを復元してから、午後 8 時の ログ バックアップとログ末尾のバックアップを適用します。  
  
 **代替手順 2: データベースの以前の完全バックアップを使用したデータベースの復元**  
  
> この代替手順は、問題が生じて午後 6 時の 復元よりも処理に時間がかかります。 この方法では、午後 6 時のデータベースの完全バックアップからの 復元よりも処理に時間がかかります。  
  
1.  障害発生時点にアクティブなトランザクション ログのログ末尾のバックアップを作成します。  
  
2.  午前 8 時に作成した データベースの完全バックアップを復元し、4 つすべてのトランザクション ログ バックアップを順に復元します。 これにより、午後 9 時 45 分までに完了したすべてのトランザクションがロールフォワードされます。  
  
     この代替手順は、一連のデータベースの完全バックアップにまたがるトランザクション ログ バックアップのチェーンを保持することにより、冗長性を伴うセキュリティが提供されることになります。  
  
> 場合によっては、トランザクション ログを使用して特定の時点までデータベースを復元することもできます。 詳細については、「 [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **トランザクション ログのバックアップを適用するには**  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
 **復旧ポイントまで復元するには**  
  
-   [完全復旧モデルで障害発生時点までデータベースを復元する &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
-   [マークされたトランザクションを含む関連データベースの復旧](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)  
  
-   [ログ シーケンス番号への復旧 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
 **WITH NORECOVERY を使用してバックアップを復元した後、データベースを回復するには**  
  
-   [データを復元しないデータベースの復旧 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)      
  
