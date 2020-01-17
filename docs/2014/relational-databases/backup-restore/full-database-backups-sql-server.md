---
title: データベースの完全バックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- backups [SQL Server], database
- backing up databases [SQL Server], full backups
- estimating database backup size
- backing up [SQL Server], size of backup
- database backups [SQL Server], full backups
- size [SQL Server], backups
- database backups [SQL Server], about backing up databases
ms.assetid: 4d933d19-8d21-4aa1-8153-d230cb3a3f99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 713e2e507fd98f6d3d87fe60e075e587725ddaf2
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890342"
---
# <a name="full-database-backups-sql-server"></a>データベースの完全バックアップ (SQL Server)
  データベースの完全バックアップでは、データベース全体をバックアップします。 このバックアップにはトランザクション ログの一部が含まれるため、データベースの完全バックアップを復元した後に、データベース全体を復旧することができます。 データベースの完全バックアップは、バックアップが完了した時点でのデータベースを表します。  
  
> [!TIP]  
>  データベース サイズが大きくなると、データベースの完全バックアップにかかる時間は長くなり、必要な記憶領域も増加します。 このため、大きなデータベースの場合は、データベースの完全バックアップを一連の *差分データベース バックアップ*で補完することができます。 詳細については、「 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  データベースをバックアップすると、TRUSTWORTHY は OFF に設定されます。 TRUSTWORTHY を ON に設定する方法については「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)」を参照してください。  
  
 **このトピックの内容**  
  
-   [単純復旧モデルでのデータベース バックアップ](#DbBuRMs)  
  
-   [完全復旧モデルでのデータベース バックアップ](#DbBuRMf)  
  
-   [データベースの完全バックアップを使用したデータベースの復元](#RestoreDbBu)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="DbBuRMs"></a> 単純復旧モデルでのデータベース バックアップ  
 単純復旧モデルでは、データベースをバックアップした後に障害が発生すると、その間の作業内容が失われる可能性があります。 作業損失の可能性は、次のバックアップまで、データを更新するたびに増加します。次の完全バックアップで作業損失の可能性はゼロに戻り、そこから再び増加していきます。 作業損失の可能性は、バックアップ間の時間が増加します。 次の図に、データベースの完全バックアップのみを使用するバックアップ方法における作業損失の可能性を示します。  
  
 ![データベース バックアップ間でのデータ損失の危険性](../../database-engine/media/bnr-rmsimple-1-fulldb-backups.gif "データベース バックアップ間でのデータ損失の危険性")  
  
### <a name="example--includetsqlincludestsql-mdmd"></a>例 ([!INCLUDE[tsql](../../../includes/tsql-md.md)])  
 次の例では、WITH FORMAT を使用してデータベースの完全バックアップを作成することにより、既存のバックアップを上書きして新しいメディア セットを作成します。  
  
```  
-- Back up the AdventureWorks2012 database to new media set.  
BACKUP DATABASE AdventureWorks2012  
    TO DISK = 'Z:\SQLServerBackups\AdventureWorksSimpleRM.bak'   
    WITH FORMAT;  
GO  
```  
  
##  <a name="DbBuRMf"></a> 完全復旧モデルでのデータベース バックアップ  
 完全復旧と一括ログ復旧を使用するデータベースには、データベース バックアップが必要です。ただし、それだけでは十分とは言えません。 トランザクション ログのバックアップも必要です。 次の図に、完全復旧モデルで可能な限り単純化したバックアップ方法を示します。  
  
 ![一連の完全データベース バックアップとログ バックアップ](../../database-engine/media/bnr-rmfull-1-fulldb-log-backups.gif "一連の完全データベース バックアップとログ バックアップ")  
  
 ログのバックアップを作成する方法については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)」を参照してください。  
  
### <a name="example--includetsqlincludestsql-mdmd"></a>例 ([!INCLUDE[tsql](../../../includes/tsql-md.md)])  
 次の例では、WITH FORMAT を使用してデータベースの完全バックアップを作成することにより、既存のバックアップを上書きして新しいメディア セットを作成します。 その後、トランザクション ログをバックアップします。 実際の状況では、一連の定期的なログ バックアップを実行する必要があります。 この例では、完全復旧モデルが使用されるように [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースを設定します。  
  
```  
USE master;  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
-- Back up the AdventureWorks2012 database to new media set (backup set 1).  
BACKUP DATABASE AdventureWorks2012  
  TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012FullRM.bak'   
  WITH FORMAT;  
GO  
--Create a routine log backup (backup set 2).  
BACKUP LOG AdventureWorks2012 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012FullRM.bak';  
GO  
```  
  
##  <a name="RestoreDbBu"></a> データベースの完全バックアップを使用したデータベースの復元  
 データベースを復元することによって、データベースの完全バックアップからワン ステップで任意の場所にデータベース全体を再作成できます。 データベースの完全バックアップには、バックアップ完了時までデータベースを復旧するのに十分なトランザクション ログが含まれています。 復元されたデータベースは、データベース バックアップが完了した時点の元のデータベースの状態から、コミットされていないトランザクションを差し引いた状態と一致します。 完全復旧モデルでは、さらに、後続のすべてのトランザクション ログ バックアップを復元する必要があります。 データベースが復旧されると、コミットされていないトランザクションはロールバックされます。  
  
 詳細については、「[データベースの全体復元 &#40;単純復旧モデル&#41;](complete-database-restores-simple-recovery-model.md)」または「[データベースの全体復元 &#40;完全復旧モデル&#41;](complete-database-restores-full-recovery-model.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベースの完全バックアップを作成するには**  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
 **バックアップ ジョブのスケジュールを設定するには**  
  
 [メンテナンス プラン ウィザードの使用](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データベースのバックアップと復元](back-up-and-restore-of-sql-server-databases.md)   
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [Analysis Services データベースのバックアップと復元](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)  
  
  
