---
title: ファイル復元 (完全復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a78b177b1fb429535a4bb9b271d0b1dbc4eedc79
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921943"
---
# <a name="file-restores-full-recovery-model"></a>ファイル復元 (完全復旧モデル)
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
  
     オンライン ページおよびファイルの復元に対するサポートの詳細については、「[SQL Server 2014 の各エディションでサポートされる機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。 オンライン復元の詳細については、「[オンライン復元 &#40;SQL Server&#41;](online-restore-sql-server.md)」を参照してください。  
  
    > [!TIP]  
    >  ファイル復元のためにデータベースをオフラインにする場合は、次の [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) ステートメントを実行して復元シーケンスを開始する前に、データベースをオフラインにしてください。ALTER DATABASE *database_name* SET OFFLINE。  
  
  
  
##  <a name="Overview"></a> 破損したファイルのファイル バックアップからの復元  
  
1.  1 つ以上の破損したファイルを復元するには、 [ログ末尾のバックアップ](tail-log-backups-sql-server.md)を作成してください。  
  
     ログが破損したためにログ末尾のバックアップを作成できない場合は、データベース全体を復元する必要があります。  
  
     トランザクション ログのバックアップ方法の詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)」を参照してください。  
  
    > [!IMPORTANT]  
    >  オフライン ファイル復元では、必ずファイルの復元前にログ末尾のバックアップを行う必要があります。 オンライン ファイル復元では、必ずファイルの復元後にログ バックアップを行う必要があります。 ファイルを他のデータベースと一貫性のある状態に復旧できるようにする必要があるため、このログ バックアップが必要になります。  
  
2.  破損したファイルについては、そのファイルの最新のファイル バックアップから復元します。  
  
3.  差分バックアップがある場合は、復元したファイルごとに最新のファイルの差分バックアップを復元します。  
  
4.  トランザクション バックアップを順番に復元します。復元したファイルの中で最も古いファイルに対応するバックアップの復元から始め、最後に手順 1. で作成したログ末尾のバックアップを復元します。  
  
     データベースを一貫性のある状態にするには、ファイル バックアップより後に作成されたトランザクション ログ バックアップを復元する必要があります。 トランザクション ログ バックアップは、復元するファイルに関連のある変更のみが適用されるので、すばやくロールフォワードできます。 破損していないファイルに関しては、コピーされずにロールフォワードが行われるので、データベース全体の復元より個別のファイルの復元の方が適している場合があります。 ただし、ログ バックアップのチェーンは、全体を読み取る必要があります。  
  
5.  データベースを復旧します。  
  
> [!NOTE]  
>  ファイル バックアップを使用して、データベースを以前の時点の状態に復元することもできます。 この操作を行うには、ファイル バックアップの完全なセットを復元してから、一番最近に復元されたファイル バックアップの後の時点までのトランザクション ログ バックアップを順番に復元する必要があります。 特定の時点への復旧の詳細については、「[SQL Server データベースを特定の時点に復元する方法 &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)」を参照してください。  
  
## <a name="transact-sql-restore-sequence-for-an-offline-file-restore-full-recovery-model"></a>オフラインのファイル復元用の Transact-SQL 復元シーケンス (完全復旧モデル)  
 ファイル復元シナリオは、適切なデータをコピーし、ロールフォワードして、復旧する単一の復元シーケンスで構成されます。  
  
 ここでは、ファイル復元シーケンスに必要な [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) オプションを示しています。 説明の目的に関係しない構文や詳細は、省略しています。  
  
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
  
-   [例: 読み取り/書き込みファイルのオンライン復元 &#40;完全復旧モデル&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;完全復旧モデル&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
-   [例: プライマリ ファイル グループと他のファイル グループを 1 つオフラインで復元する &#40;完全復旧モデル&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **ファイルおよびファイル グループを復元するには**  
  
-   [新しい場所へのファイルの復元 &#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A> (SMO)  
  

  
## <a name="see-also"></a>関連項目  
 [バックアップと復元: 相互運用性と共存 &#40;SQL Server&#41;](backup-and-restore-interoperability-and-coexistence-sql-server.md)   
 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [ファイルの完全バックアップ &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [復元と復旧の概要 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [データベースの全体復元 &#40;単純復旧モデル&#41;](complete-database-restores-simple-recovery-model.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
