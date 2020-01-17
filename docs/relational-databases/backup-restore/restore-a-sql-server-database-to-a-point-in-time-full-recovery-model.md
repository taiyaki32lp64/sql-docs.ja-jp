---
title: SQL Server データベースを特定の時点に復元する方法 (完全復旧モデル) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- STOPAT clause [RESTORE LOG statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
ms.assetid: 3a5daefd-08a8-4565-b54f-28ad01a47d32
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f4a4a91c4703bd4634f471e3d6bc0b9b4baf2305
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908885"
---
# <a name="restore-a-sql-server-database-to-a-point-in-time-full-recovery-model"></a>SQL Server データベースを特定の時点に復元する方法 (完全復旧モデル)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベースを特定の時点まで復元する方法について説明します。 このトピックは、完全復旧モデルまたは一括ログ復旧モデルを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにのみ関連しています。  
  
> [!IMPORTANT]  
>  一括ログ復旧モデルでは、ログ バックアップに一括ログ記録された変更内容が含まれていると、そのバックアップ内の特定の時点への復旧を行うことができません。 データベースは、トランザクション ログ バックアップの終了時点へ復旧する必要があります。  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **SQL Server データベースを特定の時点まで復元する場合に使用するツール:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   特定の復元時点が不明な場合の STANDBY を使用した検索  
  
-   復元シーケンスの早い段階での特定時点の指定  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています (FROM DATABASE_SNAPSHOT オプションを使用する場合、データベースは常に存在します)。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 **特定の時点にデータベースを復元するには**  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]の適切なインスタンスに接続し、サーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。 復元するデータベースに応じて、ユーザー データベースを選択するか、 **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[復元]** をポイントして、 **[データベース]** をクリックします。  
  
4.  **[全般]** ページの **復元元**のセクションを使用して、復元するバックアップ セットの復元元ファイルと場所を指定します。 以下のオプションの 1 つを選択します。  
  
    -   **[データベース]**  
  
         復元するデータベースをドロップダウン リストから選択します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    > [!NOTE]  
    >  別のサーバーで作成されたバックアップの場合、復元先のサーバーには指定されたデータベースのバックアップ履歴情報が存在しません。 この場合、 **[デバイス]** をクリックして、復元するファイルまたはデバイスを手動で指定します。  
  
    -   **[デバイス]**  
  
         参照ボタン ( **[...]** ) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[バックアップ メディアの種類]** ボックスから、デバイスの種類を 1 つ選択します。 **[バックアップ メディア]** ボックスにデバイスを追加するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
         **[ソース: デバイス: データベース]** リスト ボックスで、復元するデータベースの名前を選択します。  
  
         **メモ** この一覧は **[デバイス]** をクリックした場合にのみ使用できます。 選択されたデバイスにバックアップを持つデータベースのみが使用できるようになります。  
  
5.  **復元先のセクション**の **[データベース]** ボックスに、復元するデータベースの名前が自動的に表示されます。 データベースの名前を変更するには、 **[データベース]** ボックスに新しい名前を入力します。  
  
6.  **[タイムライン]** をクリックして、 **[バックアップのタイムライン]** ダイアログ ボックスにアクセスします。  
  
7.  **[復元先]** セクションで、 **[特定の日付と時刻]** をクリックします。  
  
8.  **[日付]** と **[時刻]** ボックスを使用するか、スライダー バーを使用して、復元を止める特定の日付と時刻を指定します。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  **[タイムラインの間隔]** ボックスを使用して、タイムラインに表示される時間を変更します。  
  
9. 特定の時点を指定すると、データベース復旧アドバイザーによって、その特定の時点に復元するために必要なバックアップだけが **[復元するバックアップ セット]** グリッドの **[復元]** 列で選択されます。 これらの選択されたバックアップは、特定の時点への復元用として推奨される復元プランを示しています。 特定の時点への復元操作には選択されているバックアップのみを使用するようにします。  
  
     **[復元するバックアップ セット]** グリッドの列の詳細については、「[データベースの復元 &#40;[全般] ページ&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)」を参照してください。 データベースの復旧アドバイザーの詳細については、「[復元と復旧の概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)」を参照してください。  
  
10. **[オプション]** ページの **[復元オプション]** パネルでは、状況に応じて、次の任意のオプションを選択できます。  
  
    -   **[既存のデータベースを上書きする (WITH REPLACE)]**  
  
    -   **[レプリケーションの設定を保存する (WITH KEEP_REPLICATION)]**  
  
    -   **[復元するデータベースへのアクセスを制限する (WITH RESTRICTED_USER)]**  
  
     これらのオプションの詳細については、「[データベースの復元 &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)」を参照してください。  
  
11. **[復旧状態]** ボックスのオプションを選択します。 このボックスの選択内容により、復元操作後のデータベースの状態が決まります。  
  
    -   **[RESTORE WITH RECOVERY]** : コミットされていないトランザクションをロールバックして、データベースを使用可能な状態にします。これが既定の動作です。 別のトランザクション ログは復元できません。 このオプションは、必要なバックアップをすべて復元する場合に選択します。  
  
    -   **[RESTORE WITH NORECOVERY]** : データベースは操作不可状態のままとなり、コミットされていないトランザクションはロールバックされません。 別のトランザクション ログは復元できます データベースは、復旧されるまで使用できません。  
  
    -   **[RESTORE WITH STANDBY]** : データベースを読み取り専用モードにします。 コミットされていないトランザクションは元に戻されますが、復旧結果を元に戻せるように元に戻す操作をスタンバイ ファイルに保存します。  
  
     オプションの詳細については、「[データベースの復元 &#40;[オプション] ページ&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)」を参照してください。  
  
12. 選択した時点まで復元するために必要であれば、 **[復元の前にログ末尾のバックアップを実行する]** が選択されます。 この設定を変更する必要はありません。ログの末尾をバックアップする必要がない場合でも、そのように選択してかまいません。  
  
13. データベースへのアクティブな接続がある場合、復元操作は失敗する可能性があります。 **とデータベース間のすべてのアクティブな接続を閉じるには、** [既存の接続を閉じる] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] オプションをオンにします。 このチェック ボックスをオンにすると、データベースは復元操作の実行前にシングル ユーザー モードに設定され、復元操作の完了後にマルチユーザー モードに設定されます。  
  
14. 復元操作と復元操作の間に、その都度、確認のメッセージを表示するには、 **[各バックアップを復元する前に確認する]** をオンにします。 通常は、その必要はありません。データベースが大きく、復元操作のステータスを監視する必要がある場合にのみ使用します。  

##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 **Before you begin**  
  
 指定した時点への復元は、常にログ バックアップから行われます。 復元シーケンスのすべての RESTORE ステートメントで、同一の STOPAT 句で目的の時点またはトランザクションを指定する必要があります。 特定の時点への復元の前提条件として、最初にエンド ポイントが目的の復元時点よりも前になっているデータベースの完全バックアップを復元する必要があります。 このデータベースの完全バックアップは、データベースの最新の完全バックアップより古くてもかまいません。ただし、これは、データベースの完全バックアップを復元した後で、目的の時点を含むログ バックアップまで後続のログ バックアップをすべて復元する場合に限ります。  
  
 復元するデータベース バックアップを識別しやすくするには、RESTORE DATABASE ステートメントで WITH STOPAT 句をオプションで指定し、指定した目的の時点に対してデータのバックアップが近すぎる場合はエラーが発生するようにします。 データ バックアップに目的の時点が含まれている場合でも、常にデータ バックアップ全体が復元されます。  
  
 **[!INCLUDE[tsql](../../includes/tsql-md.md)] の基本構文**  
  
 RESTORE LOG *database_name* FROM <backup_device> WITH STOPAT **=** _time_ **,** RECOVERY...  
  
 復旧ポイントは、 **time** で指定する *datetime*の値以前に行われた最後のトランザクション コミットの時点です。  
  
 特定の時点より前に行われた変更のみを復元するには、復元するバックアップごとに WITH STOPAT **=** _time_ を指定します。 これにより、目的の時点を過ぎる危険性を回避できます。  
  
 **特定の時点にデータベースを復元するには**  
  
> [!NOTE]  
>  この手順の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  データベースを復元するサーバー インスタンスに接続します。  
  
2.  NORECOVERY オプションを指定した RESTORE DATABASE ステートメントを実行します。  
  
    > [!NOTE]  
    >  部分復元シーケンスで [FILESTREAM](../../relational-databases/blob/filestream-sql-server.md) ファイル グループを除外した場合、特定の時点への復元はサポートされません。 復元シーケンスを強制的に実行して続行することもできます。 ただし、RESTORE ステートメントから除外された FILESTREAM ファイル グループは復元できません。 特定の時点への復元を強制的に実行するには、STOPAT、STOPATMARK、または STOPBEFOREMARK オプションに CONTINUE_AFTER_ERROR オプションを組み合わせて指定します。これらのオプションは、後続の RESTORE LOG ステートメントでも指定する必要があります。 CONTINUE_AFTER_ERROR を指定した場合、部分復元シーケンスは正常に実行されますが、FILESTREAM ファイル グループは復元できなくなります。  
  
3.  差分バックアップが存在する場合、データベースを復旧せずに最新のデータベースの差分バックアップを復元します (RESTORE DATABASE *database_name* FROM *backup_device* WITH NORECOVERY)。  
  
4.  各トランザクション ログ バックアップを作成順に適用して、ログの復元を停止する時点を指定します (RESTORE DATABASE *database_name* FROM <backup_device> WITH STOPAT **=** _time_ **,** RECOVERY)。  
  
    > [!NOTE]  
    >  RECOVERY オプションと STOPAT オプション。 トランザクション ログ バックアップに、要求した時点の情報が格納されていない場合、たとえば、指定した日時がトランザクション ログに記録されている時点より後の場合などに、警告が生成されます。この場合、データベースは復旧されません。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、データベースを `12:00 AM` `April 15, 2020` の状態に復元し、複数のログ バックアップが関連する復元操作を行います。 バックアップ デバイス `AdventureWorksBackups`において、復元するデータベース全体のバックアップはデバイス上の 3 番目のバックアップ セット (`FILE = 3`)、最初のログ バックアップは 4 番目のバックアップ セット (`FILE = 4`)、2 番目のログ バックアップは 5 番目のバックアップ セット (`FILE = 5`) です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースは、単純復旧モデルを使用しています。 ただし、ログ バックアップを可能にするために、データベースの完全バックアップを行う前に、 `ALTER DATABASE AdventureWorks SET RECOVERY FULL`を使用して、データベースが完全復旧モデルを使用するように設定されています。  
  
```  
RESTORE DATABASE AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks WITH RECOVERY;   
GO  
  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [SSMS を使用してデータベース バックアップを復元する](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [完全復旧モデルで障害発生時点までデータベースを復元する &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [ログ シーケンス番号への復旧 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recover-to-a-log-sequence-number-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ToPointInTime%2A> (SMO)  
  
## <a name="see-also"></a>参照  
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-headeronly-transact-sql.md)  
  
  
