---
title: 遅延トランザクション (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- I/O [SQL Server], database recovery
- restoring pages [SQL Server]
- deferred transactions
- modifying transaction deferred state
ms.assetid: 6fc0f9b6-d3ea-4971-9f27-d0195d1ff718
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3cd81ad5125b6822dd59205bad32cb39194712d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075985"
---
# <a name="deferred-transactions-sql-server"></a>遅延トランザクション (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise では、ロールバック (元に戻す) に必要なデータがデータベースの起動時にオフラインになっている場合、損傷したトランザクションが遅延することがあります。 *遅延トランザクション* は、ロールフォワード フェーズの完了時にコミットされておらず、ロールバックを妨げるエラーが発生しているトランザクションです。 トランザクションはロールバックできないので、遅延します。  
  
> [!NOTE]  
>  損傷したトランザクションが遅延するのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise の場合のみです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の他のエディションでは、損傷したトランザクションが原因で起動に失敗します。  
  
 通常、遅延トランザクションが発生する原因は、データベースがロールフォワードされている間に、I/O エラーによってトランザクションに必要なページを読み取れなくなったことにあります。 ただし、ファイル レベルのエラーによって遅延トランザクションが発生する場合もあります。 また、トランザクションのロールバックが必要な時点で部分復元シーケンスが停止し、トランザクションがオフラインになっているデータを必要とする場合にも、遅延トランザクションが発生する可能性があります。  
  
 ユーザー トランザクションのロールバック中に I/O エラーが発生すると、データベース全体がオフラインになります。 データベースがオンラインに戻ると、データベースに保持されていたすべてのロックが再実行フェーズで再度取得され、コミットされていないすべてのトランザクションのロールバックが試みられます。 トランザクションにより変更されるすべてのデータには、トランザクションをロールバックできるまで適切なロックが設定されます。 ロールバックできないトランザクションでロックが解除されるのは、破損が修復されデータベースが再起動されたとき、またはオンライン復元後に、データベースをオンラインにした状態で遅延トランザクションが解決されたときです。 そのときまで、遅延トランザクションは、ロックを保持することで、データベース全体に対する特定の操作を防ぐことができます。 たとえば、遅延トランザクションに CREATE TABLE 命令が含まれる場合、遅延トランザクションが解決するまでユーザーはテーブルを作成できません。  
  
 また、段階的な部分復元によってデータベースが復旧された時点で、まだ復元されていないオフラインのファイル グループに 1 つ以上のアクティブなトランザクションが影響していることが原因で、遅延トランザクションが発生する場合もあります。 これらのトランザクションはロールバックできないため、遅延トランザクションになります。  
  
 次の表に、データベースで復旧を引き起こす操作および I/O に問題が発生した場合の結果を示します。  
  
|操作|解決方法 (I/O の問題が発生する場合または必要なデータがオフラインの場合)|  
|------------|-----------------------------------------------------------------------|  
|サーバーの起動|遅延トランザクション|  
|[復元]|遅延トランザクション|  
|[アタッチ]|アタッチの失敗|  
|Autorestart|遅延トランザクション|  
|データベースまたはデータベース スナップショットの作成|作成の失敗|  
|データベース ミラーリングの再実行|遅延トランザクション|  
|ファイル グループのオフライン化|遅延トランザクション|  
  
## <a name="moving-a-transaction-out-of-the-deferred-state"></a>トランザクションの DEFERRED 状態の解決  
  
> [!IMPORTANT]  
>  遅延トランザクションにより、トランザクション ログはアクティブなままになります。 遅延トランザクションを保持する仮想ログ ファイルは、これらのトランザクションが遅延状態ではなくなるまで、切り捨てることができません。 ログの切り捨ての詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。  
  
 トランザクションの遅延を解決するには、I/O エラーのない状態でデータベースを起動する必要があります。 遅延トランザクションが存在する場合は、I/O エラーの原因を解決する必要があります。 利用可能な解決策を、通常で行われる順序で記載すると、次のようになります。  
  
-   データベースを再起動します。 問題が一時的なものである場合、遅延トランザクションが発生することなくデータベースが起動します。  
  
-   ファイル グループがオフラインになっていたためにトランザクションが遅延した場合、ファイル グループをオンラインに戻します。  
  
     オフラインのファイル グループをオンラインに戻すには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    RESTORE DATABASE database_name FILEGROUP=<filegroup_name>  
    ```  
  
-   データベースを復元します。 オフライン復元後は、すべての遅延トランザクションが解決されます。  
  
     完全復旧モデルまたは一括ログ復旧モデルでは、少数の破損したページによって遅延トランザクションが発生した場合、オンライン ページ復元によってエラーが解決することがあります (サポートされている場合)。  
  
-   遅延トランザクションの原因となっているオフライン状態のファイル グループが不要になった場合は、これらのファイル グループが機能しないようにします。 ファイル グループがオフラインであったことが原因で遅延されたトランザクションは、ファイル グループを機能していない状態にすると、遅延状態ではなくなります。  
  
    > [!IMPORTANT]  
    >  機能していないファイル グループを復旧することはできません。  
  
     詳細については、「 [機能していないファイル グループの削除 &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)」を参照してください。  
  
-   不適切なページが原因でトランザクションが遅延し、適切なデータベースのバックアップが存在しない場合、データベースを修復するには、次のプロセスを使用します。  
  
    -   最初に、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行して、データベースを緊急モードにします。  
  
        ```  
        ALTER DATABASE <database_name> SET EMERGENCY  
        ```  
  
         緊急モードの詳細については、「 [データベースの状態](../../relational-databases/databases/database-states.md)」を参照してください。  
  
    -   次に、下記の DBCC ステートメントのいずれかで DBCC REPAIR_ALLOW_DATA_LOSS オプションを使用してデータベースを修復します: [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)、[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)、または [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。  
  
         DBCC では、不適切なページが検出されると、そのページの割り当てが解除され、関連するすべてのエラーが修復されます。 この方法を使用すると、物理的に一貫性のある状態でデータベースをオンラインに戻すことができます。 ただし、追加されたデータが失われる場合もあるため、この方法は最後の手段として使用してください。  
  
## <a name="see-also"></a>参照  
 [復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [機能していないファイル グループの削除 &#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [ファイルの復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
