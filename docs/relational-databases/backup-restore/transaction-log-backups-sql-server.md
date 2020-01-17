---
title: トランザクション ログのバックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server]
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 491016d02dfdb890914633333e19a3138c01779d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041354"
---
# <a name="transaction-log-backups-sql-server"></a>トランザクション ログのバックアップ (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのみに関連しています。 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのトランザクション ログのバックアップについて説明します。  
  
 少なくとも 1 つの完全バックアップを作成しておかなければ、ログ バックアップを作成できません。 完全バックアップを作成しておくと、いつでもトランザクション ログをバックアップできます。ただし、そのログのバックアップが既に進行中である場合、バックアップを開始できません。 
 
作業損失の可能性を最小限に抑え、トランザクション ログを切り捨てられるように、ログ バックアップを頻繁に行うことをお勧めします。 
 
一般的に、データベース管理者は完全バックアップを定期的に (たとえば週 1 回) 作成しますが、必要に応じて短い間隔で (たとえば 1 日 1 回) 差分データベース バックアップを作成します。 データベース バックアップとは別に、トランザクション ログのバックアップを頻繁に作成します。 最適なバックアップ間隔は、バックアップの種類に応じて、データの重要度、データベースのサイズ、サーバーの作業負荷などの要因によって異なります。 効率的な手法の導入については、このトピックの「[推奨事項](#Recommendations)」を参照してください。 
   
##  <a name="LogBackupSequence"></a> 一連のログ バックアップの動作  
 トランザクション ログのバックアップの *ログ チェーン* のシーケンスは、データのバックアップとは関連がありません。 たとえば、次の一連のイベントが発生したとします。  
  
|Time|イベント|  
|----------|-----------|  
|午前 8 時|データベースのバックアップ。|  
|正午|トランザクション ログのバックアップ。|  
|午後 4 時|トランザクション ログのバックアップ。|  
|午後 6 時|データベースのバックアップ。|  
|午後 8 時|トランザクション ログのバックアップ。|  
  
 午後 8 時に作成されたトランザクション ログ バックアップには、午後 4 時以降のトランザクション ログ レコードが含まれていて、この間午後 6 時にデータベースの完全バックアップが作成されています。トランザクション ログ バックアップのシーケンスは、午前 8 時に最初にデータベースの完全バックアップが作成されてから、午後 8 時のトランザクション ログ バックアップまで継続しています。 これらのログ バックアップを適用する方法の詳細については、「 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)」の例を参照してください。  
  
##  <a name="Recommendations"></a> 推奨事項  
  
-   トランザクション ログが破損すると、前回の有効なバックアップ以降に行われた作業が失われます。 そのため、ログ ファイルはフォールト トレランス ストレージに置くことを強くお勧めします。  
  
-   データベースが破損した場合、またはデータベースを復元する場合は、 [ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) を作成して、データベースを現在の状態に復元できるようにすることをお勧めします。  
  
-   既定では、バックアップ操作が成功するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほどエラー ログが大きくなることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。  

-   ログ バックアップは、ビジネス要件に対応するために十分な頻度で作成してください。特に、ログ ストレージに障害が起こった場合に生じる作業損失に対する許容範囲を考慮してください。 
   -   ログ バックアップを行う適切な頻度は、作業損失に対する許容範囲と、ログ バックアップを保存、管理、復元できる量とのバランスによります。 復旧計画を導入するときは必要な [RTO](https://wikipedia.org/wiki/Recovery_time_objective) と [RPO](https://wikipedia.org/wiki/Recovery_point_objective) について、特にログ バックアップの頻度について検討してください。
   -   15 分から 30 分間隔でログ バックアップを行えば十分でしょう。 業務上、作業損失の可能性を最小限に抑えることが求められる場合は、ログ バックアップの頻度を増やすことを検討します。 ログ バックアップの頻度を増やせば、ログ切り捨ての頻度も高くなり、ログ ファイルが小さくなる利点もあります。  
  
> [!IMPORTANT]
> 復元する必要があるログ バックアップの数を制限するには、定期的なデータのバックアップが不可欠です。 たとえば、データベースの完全バックアップを毎週実行し、差分バックアップを毎日実行するようにスケジュールできます。  
> 繰り返しになりますが、復旧計画を導入するときは必要な [RTO](https://wikipedia.org/wiki/Recovery_time_objective) と [RPO](https://wikipedia.org/wiki/Recovery_point_objective) について、特に、データベースの完全バックアップと差分バックアップの頻度について検討してください。
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **トランザクション ログのバックアップを作成するには**  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 バックアップ ジョブのスケジュールを設定するには、「 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)」を参照してください。  
  

## <a name="see-also"></a>参照  
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [SQL Server トランザクション ログのアーキテクチャと管理ガイドのトランザクション ログ バックアップ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Backups)     
 [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
