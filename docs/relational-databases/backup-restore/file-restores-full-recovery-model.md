---
title: ファイル復元 (完全復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- full recovery model [SQL Server], performing restores
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- file restores [SQL Server], full recovery model
- restoring files [SQL Server], full recovery model
- Transact-SQL restore sequence
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: d2236a2a-4cf1-4c3f-b542-f73f6096e15c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c4ca01f461d3013482ceca066a6ce141adf0aaae
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908930"
---
# <a name="file-restores-full-recovery-model"></a>ファイル復元 (完全復旧モデル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックは、複数のファイルまたはファイル グループが含まれている、完全復旧モデルまたは一括読み込み復旧モデルを使用するデータベースだけに関連しています。  
  
 ファイル復元の目標は、データベース全体を復元することなく 1 つ以上の破損したファイルを復元することです。 ファイル復元シナリオは、適切なデータをコピーし、ロールフォワードして、復旧する単一の復元シーケンスで構成されます。  
  
 復元中のファイル グループが読み取り/書き込み可能である場合、最後に実行されたデータ バックアップまたは差分バックアップを復元した後、チェーンが途切れていないログ バックアップを適用する必要があります。 これにより、ログ ファイル内の現在アクティブなログ レコードの状態がファイル グループに反映されます。 復旧ポイントは通常ログの末尾付近にありますが、必ずというわけではありません。  
  
 復元中のファイル グループが読み取り専用の場合、通常はログ バックアップを適用する必要がないため、スキップされます。 ファイルが読み取り専用になった後でバックアップが行われた場合、それが復元する最後のバックアップになります。 ロールフォワードは、目的の時点で停止します。  
  
 これらのファイル復元のシナリオは次のとおりです。  
  
-   オフライン ファイル復元  
  
     *オフライン ファイル復元*では、破損したファイルまたはファイル グループを復元する間、データベースはオフラインになります。 データベースは、復元シーケンスの最後にオンラインになります。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ではすべてのエディションで、オフラインのファイル復元がサポートされます。  
  
-   オンライン ファイル復元  
  
     *オンライン ファイル復元*では、復元中にデータベースがオンラインであれば、データベースをオンラインにしたままファイル復元を実行できます。 ただし、復元操作時は、ファイルが復元される各ファイル グループがオフラインになります。 オフライン ファイル グループ内のすべてのファイルが復旧されると、そのファイル グループは自動的にオンラインになります。  
  
     オンライン ページおよびファイルの復元に対するサポートの詳細については、「[Editions and Supported Features for SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」 (SQL Server 2016 の各エディションとサポートされる機能) を参照してください。 オンライン復元の詳細については、「[Online Restore (SQL Server)](../../relational-databases/backup-restore/online-restore-sql-server.md)」 (オンライン復元 (SQL Server)) を参照してください。
  
    > [!TIP]  
    >  ファイル復元のためにデータベースをオフラインにする場合は、次の [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md) ステートメントを実行して復元シーケンスを開始する前に、データベースをオフラインにしてください。ALTER DATABASE *database_name* SET OFFLINE。  
  
  
##  <a name="Overview"></a> 破損したファイルのファイル バックアップからの復元  
  
1.  1 つ以上の破損したファイルを復元するには、 [ログ末尾のバックアップ](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)を作成してください。  
  
     ログが破損したためにログ末尾のバックアップを作成できない場合は、データベース全体を復元する必要があります。  
  
     トランザクション ログのバックアップ方法の詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  オフライン ファイル復元では、必ずファイルの復元前にログ末尾のバックアップを行う必要があります。 オンライン ファイル復元では、必ずファイルの復元後にログ バックアップを行う必要があります。 ファイルを他のデータベースと一貫性のある状態に復旧できるようにする必要があるため、このログ バックアップが必要になります。  
  
2.  破損したファイルについては、そのファイルの最新のファイル バックアップから復元します。  
  
3.  差分バックアップがある場合は、復元したファイルごとに最新のファイルの差分バックアップを復元します。  
  
4.  トランザクション バックアップを順番に復元します。復元したファイルの中で最も古いファイルに対応するバックアップの復元から始め、最後に手順 1. で作成したログ末尾のバックアップを復元します。  
  
     データベースを一貫性のある状態にするには、ファイル バックアップより後に作成されたトランザクション ログ バックアップを復元する必要があります。 トランザクション ログ バックアップは、復元するファイルに関連のある変更のみが適用されるので、すばやくロールフォワードできます。 破損していないファイルに関しては、コピーされずにロールフォワードが行われるので、データベース全体の復元より個別のファイルの復元の方が適している場合があります。 ただし、ログ バックアップのチェーンは、全体を読み取る必要があります。  
  
5.  データベースを復旧します。  

> [!NOTE]  
>  ファイル バックアップを使用して、データベースを以前の時点の状態に復元することもできます。 この操作を行うには、ファイル バックアップの完全なセットを復元してから、一番最近に復元されたファイル バックアップの後の時点までのトランザクション ログ バックアップを順番に復元する必要があります。 特定の時点への復旧の詳細については、「[SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>オフラインのファイル復元用の Transact-SQL 復元シーケンス (完全復旧モデル)  
 ファイル復元シナリオは、適切なデータをコピーし、ロールフォワードして、復旧する単一の復元シーケンスで構成されます。  
  
 ここでは、ファイル復元シーケンスに必要な [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) オプションを示しています。 説明の目的に関係しない構文や詳細は、省略しています。  
  
 このサンプル復元シーケンスでは、WITH NORECOVERY を使用した 2 つのセカンダリ ファイル ( `A` と `B`) のオフライン復元を示します。 次に、NORECOVERY を使用して 2 つのログ バックアップを適用してから、WITH RECOVERY を使用してログ末尾のバックアップを復元します。  
  
> [!NOTE]  
>  このサンプル復元シーケンスでは、まず、ファイルをオフラインにしてからログ末尾のバックアップを作成します。  
  
```  
--Take the file offline.  
ALTER DATABASE database_name MODIFY FILE SET OFFLINE;  
-- Back up the currently active transaction log.  
BACKUP LOG database_name  
   TO <tail_log_backup>  
   WITH NORECOVERY;  
GO   
-- Restore the files.  
RESTORE DATABASE database_name FILE=name   
   FROM <file_backup_of_file_A>   
   WITH NORECOVERY;  
RESTORE DATABASE database_name FILE=<name> ......  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
-- Restore the log backups.  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG database_name FROM <tail_log_backup>   
   WITH RECOVERY;  
```  
  
## <a name="examples"></a>使用例  
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [例: プライマリ ファイル グループと他のファイル グループを 1 つオフラインで復元する &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **ファイルおよびファイル グループを復元するには**  
  
-   [新しい場所へのファイルの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  
  
## <a name="see-also"></a>参照  
 [バックアップと復元: 相互運用性と共存 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [ファイルの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
