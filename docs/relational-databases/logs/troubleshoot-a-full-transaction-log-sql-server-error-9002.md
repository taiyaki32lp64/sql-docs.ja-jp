---
title: 満杯になったトランザクション ログのトラブルシューティング (エラー 9002)
ms.custom: seo-lt-2019
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: ad8b68338987256f1c7fa01f1f0d56242cef6a7f
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056075"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>満杯になったトランザクション ログのトラブルシューティング (SQL Server エラー 9002)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、トランザクション ログが満杯になった場合の対処法について説明し、今後トランザクション ログが満杯になるのを防ぐ方法を示します。 
  
  トランザクション ログが満杯になると、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] から **9002 エラー**が発行されます。 データベースがオンラインまたは復旧中の場合、ログが満杯になることがあります。 データベースがオンラインの時にログが満杯になると、データベースはオンラインのままですが、読み取り専用になり、更新できません。 復旧中にログが満杯になった場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] によりデータベースが RESOURCE PENDING としてマークされます。 いずれの場合も、ログ領域を使用可能にするためのユーザー操作が必要です。  
  
## <a name="responding-to-a-full-transaction-log"></a>トランザクション ログが満杯になった場合の対処法  
 トランザクション ログが満杯になった状況によっては、適切な対処法が異なる場合があります。 
 
 特定の条件でログの切り捨てができなくなっている原因を見つけるには、**sys.database** カタログ ビューの **log_reuse_wait** 列と **log_reuse_wait_desc** 列を使用します。 詳細については、「[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)」を参照してください。 ログの切り捨てが遅れる要因については、「[トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。  
  
> **重要!!**  
>  データベースの復旧中に 9002 エラーが発生した場合、問題を解決した後で [ALTER DATABASE *database_name* SET ONLINE](../../t-sql/statements/alter-database-transact-sql-set-options.md) ステートメントを使用してデータベースを復旧します。  
  
 満杯になったトランザクション ログのその他の対処法には、以下があります。  
  
-   ログをバックアップします。  
  
-   ディスク領域を解放して、ログが自動的に拡張できるようにします。  
  
-   十分な空き領域があるディスク ドライブにログ ファイルを移動します。  
  
-   ログ ファイルのサイズを増やします。  
  
-   別のディスクにログ ファイルを追加します。  
  
-   実行時間の長いトランザクションを完了または強制終了します。  
  
 これらの対処法については、次のセクションで説明します。 状況に最も適した対処法を選択してください。  
  
## <a name="back-up-the-log"></a>ログをバックアップする  
 完全復旧モデルまたは一括ログ復旧モデルでは、トランザクション ログを長期間バックアップしていないと、バックアップによりログの切り捨てが妨げられる場合があります。 これまでにログのバックアップをまったく行っていない場合は、 **2 つのログ バックアップを作成** して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が最後にバックアップされた時点までログを切り捨てられるようにする必要があります。 ログを切り捨てると新しいログ レコード用の領域が解放されます。 ログが再び満杯にならないようにするには、ログを頻繁にバックアップするようにしてください。  
  
 **トランザクション ログのバックアップを作成するには**  
  
> **重要**  
>  データベースが破損している場合、「[ログ末尾のバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)」を参照してください。  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>ディスク領域の解放  
 他のファイルを削除または移動することによって、データベースのトランザクション ログ ファイルが保存されているディスク ドライブのディスク領域を解放できる場合があります。 ディスク領域を解放すると、ログ ファイルは自動的に拡張します。  
  
### <a name="move-the-log-file-to-a-different-disk"></a>別のディスクへのログ ファイルの移動  
 現在ログ ファイルが保存されているドライブでディスク領域を十分に解放できない場合は、十分な空き領域がある別のドライブにファイルを移動することを検討してください。  
  
> **重要!!** ログ ファイルは、圧縮されたファイル システムには配置しないでください。  
  
 **ログ ファイルの移動**  
  
-   [データベース ファイルの移動](../../relational-databases/databases/move-database-files.md)  
  
### <a name="increase-log-file-size"></a>ログ ファイル サイズを増やす  
 ログ ディスク上に使用可能な領域がある場合、ログ ファイルのサイズを増やすことができます。 各ログ ファイルの最大サイズは、2 テラバイト (TB) です。  
  
 **ファイル サイズを増やす**  
  
 自動拡張が無効に設定されており、データベースがオンラインで、ディスク上に十分な空き領域がある場合、次のいずれかを実行します。  
  
-   ファイル サイズを手動で増やし、単一の拡張増分値を作成します。  
  
-   ALTER DATABASE ステートメントを使用して自動拡張を有効にし、FILEGROWTH オプションに 0 以外の拡張増分値を設定します。  
  
> **注:** いずれの場合も、現在のサイズ制限に達している場合は、MAXSIZE 値を増やします。  
  
### <a name="add-a-log-file-on-a-different-disk"></a>別のディスクへのログ ファイルの追加  
 ALTER DATABASE <database_name> ADD LOG FILE ステートメントを使用して、十分な領域がある別のディスク上のデータベースに新しいログ ファイルを追加します。  
  
 **ログ ファイルの追加**  
  
-   [データベースに対するデータ ファイルまたはログ ファイルの追加](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)  
## <a name="complete-or-kill-a-long-running-transaction"></a>実行時間の長いトランザクションの完了または強制終了
### <a name="discovering-long-running-transactions"></a>実行時間の長いトランザクションの検出
実行時間の非常に長いトランザクションがあると、トランザクション ログがいっぱいになる可能性があります。 実行時間の長いトランザクションを検索するには、以下のいずれかの方法を使用します。
 - **[sys.dm_tran_database_transactions](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)。**
この動的管理ビューは、データベース レベルでのトランザクションに関する情報を返します。 実行時間の長いトランザクションで特に関係のある列としては、最初のログ レコードの時間 [(database_transaction_begin_time)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)、トランザクションの現在の状態 [(database_transaction_state)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)、トランザクション ログ内の開始レコードの [ログ シーケンス番号 (LSN)](../backup-restore/recover-to-a-log-sequence-number-sql-server.md) [(database_transaction_begin_lsn)](../system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)があります。

 - **[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)。**
このステートメントを使用すると、トランザクション所有者のユーザー ID を特定できます。これにより、トランザクションの実行元を特定して、より規則正しくトランザクションを終了する (トランザクションをロールバックするのではなくコミットする) ことができます。

### <a name="kill-a-transaction"></a>トランザクションの強制終了
状況によっては、単にプロセスを終了する必要があります。このような場合、 [KILL](../../t-sql/language-elements/kill-transact-sql.md) ステートメントを使用することがあります。 ただし、強制終了したくない重要なプロセスが実行中の場合は特に、このステートメントの使用には十分注意してください。 詳細については、「 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)」を参照してください。

## <a name="see-also"></a>参照  
[サポート技術情報の記事 - SQL Server を実行しているコンピューターでトランザクション ログのサイズが予期せず増大する、または、ログがいっぱいになる](https://support.microsoft.com/kb/317375) [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)  
  
  
