---
title: 満杯になったトランザクション ログのトラブルシューティング (SQL Server エラー 9002) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2c0dc1566693ad8d8c86d7efe47403248788b076
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144728"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>満杯になったトランザクション ログのトラブルシューティング (SQL Server エラー 9002)
  このトピックでは、トランザクション ログが満杯になった場合の対処法について説明し、今後トランザクション ログが満杯になるのを防ぐ方法を示します。 トランザクション ログが満杯になると、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]から 9002 エラーが発行されます。 データベースがオンラインまたは復旧中の場合、ログが満杯になることがあります。 データベースがオンラインの時にログが満杯になると、データベースはオンラインのままですが、読み取り専用になり、更新できません。 復旧中にログが満杯になった場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によりデータベースが RESOURCE PENDING としてマークされます。 いずれの場合も、ログ領域を使用可能にするためのユーザー操作が必要です。  
  
## <a name="responding-to-a-full-transaction-log"></a>トランザクション ログが満杯になった場合の対処法  
 トランザクション ログが満杯になった状況によっては、適切な対処法が異なる場合があります。 特定の条件でログの切り捨てができなくなっている原因を見つけるには、**sys.database** カタログ ビューの **log_reuse_wait** 列と **log_reuse_wait_desc** 列を使用します。 詳細については、「[sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)」を参照してください。 ログの切り捨てが遅れる要因については、「[トランザクション ログ &#40;SQL Server&#41;](the-transaction-log-sql-server.md)」を参照してください。  
  
> [!IMPORTANT]  
>  場合は、データベースの復旧、問題を解決したら、9002 エラーが発生したときに、ALTER DATABASE を使用して、データベースを回復*database_name*をオンラインに設定します。  
  
 満杯になったトランザクション ログのその他の対処法には、以下があります。  
  
-   ログをバックアップします。  
  
-   ディスク領域を解放して、ログが自動的に拡張できるようにします。  
  
-   十分な空き領域があるディスク ドライブにログ ファイルを移動します。  
  
-   ログ ファイルのサイズを増やします。  
  
-   別のディスクにログ ファイルを追加します。  
  
-   実行時間の長いトランザクションを完了または強制終了します。  
  
 これらの対処法については、次のセクションで説明します。 状況に最も適した対処法を選択してください。  
  
### <a name="backing-up-the-log"></a>ログのバックアップ  
 完全復旧モデルまたは一括ログ復旧モデルでは、トランザクション ログを長期間バックアップしていないと、バックアップによりログの切り捨てが妨げられる場合があります。 これまでにログのバックアップをまったく行っていない場合は、2 つのログ バックアップを作成して、[!INCLUDE[ssDE](../../includes/ssde-md.md)]が最後にバックアップされた時点までログを切り捨てられるようにする必要があります。 ログを切り捨てると新しいログ レコード用の領域が解放されます。 ログが再び満杯にならないようにするには、ログを頻繁にバックアップするようにしてください。  
  
 **トランザクション ログのバックアップを作成するには**  
  
> [!IMPORTANT]  
>  データベースが破損している場合、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md)」を参照してください。  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>ディスク領域の解放  
 他のファイルを削除または移動することによって、データベースのトランザクション ログ ファイルが保存されているディスク ドライブのディスク領域を解放できる場合があります。 ディスク領域を解放すると、ログ ファイルは自動的に拡張します。  
  
### <a name="moving-the-log-file-to-a-different-disk"></a>別のディスクへのログ ファイルの移動  
 現在ログ ファイルが保存されているドライブでディスク領域を十分に解放できない場合は、十分な空き領域がある別のドライブにファイルを移動することを検討してください。  
  
> [!IMPORTANT]  
>  ログ ファイルは、圧縮されたファイル システムには配置しないでください。  
  
 **ログ ファイルを移動するには**  
  
-   [データベース ファイルの移動](../databases/move-database-files.md)  
  
### <a name="increasing-the-size-of-a-log-file"></a>ログ ファイルのサイズの拡張  
 ログ ディスク上に使用可能な領域がある場合、ログ ファイルのサイズを増やすことができます。 各ログ ファイルの最大サイズは、2 テラバイト (TB) です。  
  
 **ファイル サイズを大きくには**  
  
 自動拡張が無効に設定されており、データベースがオンラインで、ディスク上に十分な空き領域がある場合、次のいずれかを実行します。  
  
-   ファイル サイズを手動で増やし、単一の拡張増分値を作成します。  
  
-   ALTER DATABASE ステートメントを使用して自動拡張を有効にし、FILEGROWTH オプションに 0 以外の拡張増分値を設定します。  
  
> [!NOTE]  
>  いずれの場合も、現在のサイズ制限に達している場合は、MAXSIZE 値を増やします。  
  
### <a name="adding-a-log-file-on-a-different-disk"></a>別のディスクへのログ ファイルの追加  
 ALTER DATABASE <database_name> ADD LOG FILE ステートメントを使用して、十分な領域がある別のディスク上のデータベースに新しいログ ファイルを追加します。  
  
 **ログ ファイルを追加するには**  
  
-   [データベースに対するデータ ファイルまたはログ ファイルの追加](../databases/add-data-or-log-files-to-a-database.md)  
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [トランザクション ログ ファイルのサイズの管理](manage-the-size-of-the-transaction-log-file.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql)  
  
  
