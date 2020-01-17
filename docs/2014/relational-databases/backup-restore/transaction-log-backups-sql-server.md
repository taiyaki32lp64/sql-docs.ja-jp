---
title: トランザクション ログのバックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up [SQL Server], transaction logs
- transaction log backups [SQL Server], creating
- log backups [SQL Server[
- transaction log backups [SQL Server], sequencing
ms.assetid: f4a44a35-0f44-4a42-91d5-d73ac658a3b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6dc94409e607c91944a2263ac5dfb3e8a3f4ce54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62920688"
---
# <a name="transaction-log-backups-sql-server"></a>トランザクション ログのバックアップ (SQL Server)
  このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのみに関連しています。 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのトランザクション ログのバックアップについて説明します。  
  
 少なくとも 1 つの完全バックアップを作成しておかなければ、ログ バックアップを作成できません。 完全バックアップを作成しておくと、いつでもトランザクション ログをバックアップできます。ただし、そのログのバックアップが既に進行中である場合、バックアップを開始できません。 作業損失の可能性を最小限に抑え、トランザクション ログを切り捨てられるように、ログ バックアップを頻繁に行うことをお勧めします。 一般的に、データベース管理者は完全バックアップを定期的に (たとえば週 1 回) 作成しますが、必要に応じて短い間隔で (たとえば 1 日 1 回) 差分データベース バックアップを作成します。 データベース バックアップとは別に、トランザクション ログのバックアップを頻繁に (たとえば 10 分おきに) 作成します。 最適なバックアップ間隔は、バックアップの種類に応じて、データの重要度、データベースのサイズ、サーバーの作業負荷などの要因によって異なります。  
  
 **このトピックの内容**  
  
-   [ログ バックアップのシーケンスのしくみ](#LogBackupSequence)  
  
-   [推奨事項](#Recommendations)  
  
-   [関連タスク](#RelatedTasks)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="LogBackupSequence"></a> ログ バックアップのシーケンスのしくみ  
 トランザクション ログのバックアップの *ログ チェーン* のシーケンスは、データのバックアップとは関連がありません。 たとえば、次の一連のイベントが発生したとします。  
  
|Time|イベント|  
|----------|-----------|  
|午前 8 時|データベースのバックアップ。|  
|正午|トランザクション ログのバックアップ。|  
|午後 4 時|トランザクション ログのバックアップ。|  
|午後 6 時|データベースのバックアップ。|  
|午後 8 時|トランザクション ログのバックアップ。|  
  
 午後 8 時に作成されたトランザクション ログ バックアップには、 午後 4 時から午後 8 時までのトランザクション ログ レコードが含まれています。 その間、午後 6 時に、データベースの完全バックアップが作成されています。 トランザクション ログ バックアップのシーケンスは、午前 8 時に最初にデータベースの完全バックアップが作成されて以降、 午後 8 時に作成された最後のトランザクション ログ バックアップまで継続しています。 これらのログ バックアップを適用する方法の詳細については、「 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)」の例を参照してください。  
  
##  <a name="Recommendations"></a> 推奨事項  
  
-   トランザクション ログが破損すると、前回の有効なバックアップ以降に行われた作業が失われます。 そのため、ログ ファイルはフォールト トレランス ストレージに置くことを強くお勧めします。  
  
-   データベースが破損した場合、またはデータベースを復元する場合は、 [ログ末尾のバックアップ](tail-log-backups-sql-server.md) を作成して、データベースを現在の状態に復元できるようにすることをお勧めします。  
  
-   既定では、バックアップ操作が成功するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほどエラー ログが大きくなることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **トランザクション ログのバックアップを作成するには**  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 バックアップ ジョブのスケジュールを設定するには、「 [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md)」を参照してください。  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
 [なし] :  
  
## <a name="see-also"></a>関連項目  
 [トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [SQL Server データベースのバックアップと復元](back-up-and-restore-of-sql-server-databases.md)   
 [ログ末尾のバックアップ &#40;SQL Server&#41;](tail-log-backups-sql-server.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)  
  
  
