---
title: ファイルの復元 (単純復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server]
- simple recovery model [SQL Server]
- restoring files [SQL Server], Transact-SQL restore sequence
- restoring files [SQL Server]
- Transact-SQL restore sequence
- restoring files [SQL Server], simple recovery model
- file restores [SQL Server], simple recovery model
- file restores [SQL Server], Transact-SQL restore sequence
ms.assetid: b6d07386-7c6f-4cc6-be32-93289adbd3d6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5157fcfeb54e22c404dcba29655771a1c2034e2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921827"
---
# <a name="file-restores-simple-recovery-model"></a>ファイルの復元 (単純復旧モデル)
  このトピックは、1 つ以上の読み取り専用セカンダリ ファイル グループが含まれている単純復旧モデルのデータベースのみに関連しています。  
  
 ファイル復元の目標は、データベース全体を復元することなく 1 つ以上の破損したファイルを復元することです。 単純復旧モデルでは、読み取り専用ファイルだけにファイル バックアップがサポートされます。 プライマリ ファイル グループと読み取り/書き込みセカンダリ ファイル グループは、データベース バックアップまたは部分バックアップを復元することで、常に一緒に復元されます。  
  
 これらのファイル復元のシナリオは次のとおりです。  
  
-   オフライン ファイル復元  
  
     *オフライン ファイル復元*では、破損したファイルまたはファイル グループを復元する間、データベースはオフラインになります。 データベースは、復元シーケンスの最後にオンラインになります。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ではすべてのエディションで、オフラインのファイル復元がサポートされます。  
  
-   オンライン ファイル復元  
  
     *オンライン ファイル復元*では、復元中にデータベースがオンラインであれば、データベースをオンラインにしたままファイル復元を実行できます。 ただし、復元操作時は、ファイルが復元される各ファイル グループがオフラインになります。 オフライン ファイル グループ内のすべてのファイルが復旧されると、そのファイル グループは自動的にオンラインになります。  
  
     オンライン ページおよびファイルの復元に対するサポートの詳細については、「[SQL Server 2014 の各エディションでサポートされる機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。 オンライン復元の詳細については、「[オンライン復元 &#40;SQL Server&#41;](online-restore-sql-server.md)」を参照してください。  
  
    > [!TIP]  
    >  ファイル復元のためにデータベースをオフラインにする場合は、次の [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-set-options) ステートメントを実行して復元シーケンスを開始する前に、データベースをオフラインにしてください。ALTER DATABASE *database_name* SET OFFLINE。  
  

  
##  <a name="Overview"></a> 単純復旧モデルでのファイルとファイル グループの復元の概要  
 ファイル復元のシナリオは、次に示すように、適切なデータをコピーし、ロールフォワードして、復旧する単一の復元シーケンスで構成されます。  
  
1.  破損した各ファイルを最新のファイル バックアップから復元します。  
  
2.  復元されたファイルごとに最新のファイルの差分バックアップを復元し、データベースを復旧します。  
  
### <a name="transact-sql-steps-for-file-restore-sequence-simple-recovery-model"></a>ファイル復元シーケンス用の Transact-SQL 手順 (単純復旧モデル)  
 ここでは、単純ファイル復元シーケンスに必要な [!INCLUDE[tsql](../../../includes/tsql-md.md)][RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) オプションを示しています。 説明の目的に関係しない構文や詳細は、省略しています。  
  
 復元シーケンスには、2 つの [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントだけが含まれています。 1 つ目のステートメントは `A`というセカンダリ ファイルを復元します。このファイルは、WITH NORECOVERY を指定して復元されます。 2 つ目の操作では、 `B` と `C` という他の 2 つのファイルを復元します。これらのファイルは、WITH RECOVERY を使用して異なるバックアップ デバイスから復元します。  
  
1.  RESTORE DATABASE *database* FILE **=** _name_of_file_A_  
  
     FROM *file_backup_of_file_A*  
  
     WITH NORECOVERY **;**  
  
2.  RESTORE DATABASE *database* FILE **=** _name_of_file_B_ **,** _name_of_file_C_  
  
     FROM *file_backup_of_files_B_and_C*  
  
     WITH RECOVERY **;**  
  
### <a name="examples"></a>使用例  
  
-   [例: 読み取り専用ファイルのオンライン復元 &#40;単純復旧モデル&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [例: プライマリ ファイル グループと他のファイル グループを 1 つオフラインで復元する &#40;完全復旧モデル&#41;](example-offline-restore-of-primary-and-one-other-filegroup-full-recovery-model.md)  
  
 
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **ファイルおよびファイル グループを復元するには**  
  
-   [既存のファイルにファイルとファイル グループを復元する &#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
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
  
  
