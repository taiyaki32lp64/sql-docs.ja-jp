---
title: suspect_pages テーブルの管理 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- 824 (Database Engine error)
- restoring pages [SQL Server]
- pages [SQL Server], suspect
- pages [SQL Server], restoring
- suspect_pages system table
- suspect pages [SQL Server]
- restoring [SQL Server], pages
ms.assetid: f394d4bc-1518-4e61-97fc-bf184d972e2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0f6c6afc1822e2f56189aace2836a15486d1b73b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921958"
---
# <a name="manage-the-suspectpages-table-sql-server"></a>suspect_pages テーブルの管理 (SQL Server)
  このトピックでは、 **または** を使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] suspect_pages [!INCLUDE[tsql](../../includes/tsql-md.md)]テーブルを管理する方法について説明します。 **suspect_pages** テーブルは、問題があると考えられるページに関する情報を保持するためのテーブルであり、復元が必要かどうかを判断する際に使用します。 [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) テーブルは、 [msdb データベース](../databases/msdb-database.md)にあります。  
  
 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] がデータ ページの読み取りを試みたときに次のエラーのいずれかを検出すると、ページは "問題あり" と見なされます。  
  
-   [823 エラー](../errors-events/mssqlserver-823-database-engine-error.md) : ディスク エラー (特定のハードウェア エラー) など、オペレーティング システムで実行された巡回冗長検査 (CRC) によって発生したエラーです。  
  
-   [824 エラー](../errors-events/mssqlserver-824-database-engine-error.md): 正しくないページ (すべての論理エラー) などです。  
  
 問題があると考えられるすべてのページのページ ID が **suspect_pages** テーブルに記録されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、次のような通常の処理中に検出された問題のあるページを記録します。  
  
-   クエリがページを読み取る必要があるとき  
  
-   DBCC CHECKDB 操作の実行中  
  
-   バックアップ操作の実行中  
  
 **suspect_pages** テーブルは、復元操作、DBCC 修復操作、データベースの削除操作などの実行中にも必要に応じて更新されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **suspect_pages テーブルを管理する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   **suspect_pages テーブルに記録されるエラー**  
  
     **suspect_pages** テーブルには、824 エラーにより失敗したページごとに 1 行ずつ、上限を 1,000 行として格納されます。 次の表に、 **suspect_pages** テーブルの **event_type** 列にログ記録されるエラーを示します。  
  
    |エラーの説明|**event_type** 値|  
    |-----------------------|---------------------------|  
    |オペレーティング システムの CRC エラーによって発生した 823 エラー、または、不適切なチェックサムまたは破損ページ (不適切なページ ID) 以外の 824 エラー|1|  
    |不適切なチェックサム|2|  
    |正しくないページ|3|  
    |復元済み (ページは不適切と見なされた後で復元されました)|4|  
    |修復済み (DBCC、AlwaysOn、またはミラーリングで修復されたページ)|5|  
    |DBCC による割り当て解除|7|  
  
     **suspect_pages** テーブルには、一時的なエラーも記録されます。 一時的なエラーの原因としては、I/O エラー (たとえば、ケーブルが取りはずされた場合) や、反復的なチェックサム テストで一時的にエラーになったページなどがあります。  
  
-   **データベース エンジンによる suspect_pages テーブルの更新方法**  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、 **suspect_pages** テーブルに対して次のアクションを行います。  
  
    -   テーブルに空き容量がある場合は、エラーの発生を示す 824 エラーをすべて記録し、エラー カウンターの値を増やします。 修復、復元、または割り当て解除による修正の後に、ページにエラーがある場合は、 **number_of_errors** カウントの値を増やし、 **last_update** 列を更新します。  
  
    -   リストされているページが復元や修復操作によって修正された場合は、そのページが修復 ( **event_type** = 5) または復元 (**event_type** = 4) されたことを示すために**suspect_pages** の行を更新します。  
  
    -   DBCC チェックを実行すると、エラーのないページは修復済み (**event_type** = 5) または割り当て解除済み (**event_type** = 7) としてマークされます。  
  
-   **suspect_pages テーブルに対する自動更新**  
  
     次のいずれかの理由によりデータ ファイルのページの読み取りに失敗すると、データベース ミラーリング パートナーまたは AlwaysOn 可用性レプリカは **suspect_pages** テーブルを更新します。  
  
    -   オペレーティング システムの CRC エラーによって発生した 823 エラー  
  
    -   824 エラー (破損ページなどの論理破損)  
  
     次に示す操作を行うと、 **suspect_pages** テーブルの行も自動的に更新されます。  
  
    -   DBCC CHECKDB REPAIR_ALLOW_DATA_LOSS を実行すると、割り当て解除または修復を行った各ページを示すために、 **suspect_pages** テーブルが更新されます。  
  
    -   完全復元、ファイル復元、またはページ復元を行うと、復元されたページのエントリが復元済みとしてマークされます。  
  
     次に示す操作を行うと、 **suspect_pages** テーブルの行が自動的に削除されます。  
  
    -   ALTER DATABASE REMOVE FILE。  
  
    -   DROP DATABASE  
  
-   **データベース管理者が担う管理の役割**  
  
     suspect_pages テーブルの管理は、主に古い行を削除することで、データベース管理者が行います。 **suspect_pages** テーブルのサイズには制限があり、このテーブルに空き領域がなくなると新しいエラーはログに記録されません。 このテーブルがいっぱいになるのを防ぐには、データベース管理者またはシステム管理者が、手動でこのテーブルから行を削除することによって古いエントリを削除する必要があります。 そのため、復元済みまたは修復済みの **event_type** を含む行や、古い **last_update** 値を含む行を、定期的に削除またはアーカイブすることをお勧めします。  
  
     suspect_pages テーブルの処理を監視するには、 [Database Suspect Data Page イベント クラス](../event-classes/database-suspect-data-page-event-class.md)を使用します。 一時的なエラーが原因で、 **suspect_pages** テーブルに行が追加されることがあります。 このテーブルに多数の行が追加されている場合、I/O サブシステムに問題がある可能性があります。 テーブルに追加されている行数が急激に増加している場合は、I/O サブシステムの考えられる問題を調査することをお勧めします。  
  
     データベース管理者は、レコードの挿入や更新も行うことができます。 たとえば、問題のあるページが実際には一貫性の取れている状態であることが確かであっても、しばらくレコードを残しておきたい場合に、行を更新できると便利です。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **msdb** に対するアクセスを持つユーザー は、 **suspect_pages** テーブルのデータを読み取ることができます。 suspect_pages テーブルに対する UPDATE 権限を持つすべてのユーザーは、そのレコードを更新できます。 **msdb** の **db_owner** 固定データベース ロールのメンバーまたは **sysadmin** 固定サーバー ロールのメンバーは、レコードの挿入、更新、および削除を行うことができます。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-manage-the-suspectpages-table"></a>suspect_pages テーブルを管理するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]のインスタンスに接続して、そのインスタンスを展開します。次に、 **[データベース]** を展開します。  
  
2.  **[システム データベース]** 、 **[msdb]** 、 **[テーブル]** 、 **[システム テーブル]** の順に展開します。  
  
3.  **[dbo.suspect_pages]** を展開し、 **[上位 200 行の編集]** を右クリックします。  
  
4.  クエリ ウィンドウで、目的の行を編集、更新、または削除します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-manage-the-suspectpages-table"></a>suspect_pages テーブルを管理するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 次の例は、 `suspect_pages` テーブルからいくつかの行を削除します。  
  
```  
-- Delete restored, repaired, or deallocated pages.  
DELETE FROM msdb..suspect_pages  
   WHERE (event_type = 4 OR event_type = 5 OR event_type = 7);  
GO  
  
```  
  
 次の例は、 `suspect_pages` テーブル内の不適切なページを返します。  
  
```  
-- Select nonspecific 824, bad checksum, and torn page errors.  
SELECT * FROM msdb..suspect_pages  
   WHERE (event_type = 1 OR event_type = 2 OR event_type = 3);  
GO  
  
```  
  
## <a name="see-also"></a>関連項目  
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [DBCC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)   
 [ページ復元 &#40;SQL Server&#41;](restore-pages-sql-server.md)   
 [suspect_pages &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-tables/suspect-pages-transact-sql)   
 [MSSQLSERVER_823](../errors-events/mssqlserver-823-database-engine-error.md)   
 [MSSQLSERVER_824](../errors-events/mssqlserver-824-database-engine-error.md)  
  
  
