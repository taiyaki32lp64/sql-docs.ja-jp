---
title: データベースをデータベース スナップショットに戻す | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
author: stevestein
ms.author: sstein
ms.openlocfilehash: c636db77ffdf8249cf03814abca031b0897fb4c9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909506"
---
# <a name="revert-a-database-to-a-database-snapshot"></a>データベースをデータベース スナップショットに戻す
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  オンライン データベースのデータが破損した場合、特定のケースでは、データベースをバックアップから復元する代わりに、データベースをデータが破損した日付より前のデータベース スナップショットに復帰させる方が適切であることがあります。 たとえば、テーブルの削除など、最近の重大なユーザー エラーを元に戻すには、データベースの復帰が役立つ場合があります。 ただし、スナップショットの作成後に行った変更はすべて失われます。  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用して、データベースをデータベース スナップショットに戻す方法:** [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 元に戻す操作は、次の状況ではサポートされません。  
  
-   データベースのスナップショットが複数あります。 元に戻す場合、データベースのスナップショットは 1 つだけになります。そのスナップショットにデータベースを戻します。  
  
-   読み取り専用のファイル グループまたは圧縮されたファイル グループがデータベースにある。  
  
-   ファイルは現在オフラインだが、スナップショットの作成時はオンラインだった。  
  
 データベースを復帰する前に、次の制限について検討してください。  
  
-   復帰は、メディアの復旧を目的としたものではありません。 データベース スナップショットはデータベース ファイルの不完全なコピーであるため、データベースまたはデータベース スナップショットが壊れた場合、スナップショットから復帰することはほぼ不可能です。 復帰が可能であっても、データベースまたはデータベース スナップショットが壊れている場合は、問題が解決しない可能性が高くなります。 このため、データベースの保護には、定期的なバックアップと復元プランのテストが必要です。 詳細については、「 [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)」をご覧ください。  
  
    > [!NOTE]  
    >  データベース スナップショットの作成時点の状態にソース データベースを復元できるようにする必要がある場合は、完全復旧モデルを使用し、そのためのバックアップ ポリシーを実装してください。  
  
-   元のソース データベースは、復帰されたデータベースで上書きされるため、スナップショットの作成後にデータベースに行った更新内容はすべて失われます。  
  
-   また、復帰操作によって古いログ ファイルが上書きされ、ログが再構築されます。 そのため、復帰したデータベースをユーザー エラーの時点までロール フォワードすることはできません。 したがって、データベースを復帰させる前に、ログをバックアップすることをお勧めします。  
  
    > [!NOTE]  
    >  元のログを復元してデータベースをロール フォワードすることはできませんが、元のログ ファイルの情報は失われたデータを再構築する際に役に立つ場合があります。  
  
-   復帰によってログ バックアップ チェーンが中断されます。 したがって、復帰したデータベースのログ バックアップを行う前に、最初にデータベース全体のバックアップまたはファイルのバックアップを行う必要があります。 データベースの完全バックアップをお勧めします。  
  
-   復帰操作中、スナップショットとソース データベースは両方とも使用できなくなります。 ソース データベースとスナップショットには両方とも "復元中" のマークが付けられます。 復帰操作中にエラーが発生した場合は、データベースを再起動すると、復帰操作の終了が試行されます。  
  
-   復帰したデータベースのメタデータは、スナップショット時のメタデータと同じです。  
  
-   復帰を行うと、すべてのフルテキスト カタログが削除されます。  
  
###  <a name="Prerequisites"></a> 前提条件  
 ソース データベースとデータベースの スナップショットが次の前提条件を満たすことを確認してください。  
  
-   データベースが破損していないことを確認する。  
  
    > [!NOTE]  
    >  データベースが破損している場合は、バックアップから復元する必要があります。 詳細については、「[データベースの全体復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)」または「[データベースの全体復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)」を参照してください。  
  
-   エラーの前に作成された最近のスナップショットを特定する。 詳細については、「 [データベース スナップショットの表示 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)」を参照してください。  
  
-   データベース上に現在存在するその他のスナップショットをすべて削除する。 詳細については、「 [データベース スナップショットの削除 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ソース データベースで RESTORE DATABASE 権限を持つユーザーは、データベース スナップショットが作成されたときの状態に復帰させることができます。  
  
##  <a name="TsqlProcedure"></a> データベースをデータベース スナップショットに戻す方法 (Transact-SQL の使用)  
 **データベースをデータベース スナップショットに戻すには**  
  
> [!NOTE]  
>  この手順の例については、このセクションの後半の「 [例 (Transact-SQL)](#TsqlExample)」を参照してください。  
  
1.  データベースを戻す対象になるデータベース スナップショットを特定します。 データベース内のスナップショットは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で参照できます (詳細については、「 [データベース スナップショットの表示 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)」を参照してください)。 また、 **sys.databases &amp;#40;Transact-SQL&amp;#41;** カタログ ビューの [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 列から、ビューのソース データベースを特定することもできます。  
  
2.  他のデータベース スナップショットを削除します。  
  
     スナップショットの削除の詳細については、「 [データベース スナップショットの削除 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)」を参照してください。 データベースで完全復旧モデルを使用している場合は、データベースを戻す前にログをバックアップする必要があります。 詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)」または「[データベースが破損したときのトランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)」を参照してください。  
  
3.  データベースを戻す操作を実行します。  
  
     データベースを戻す操作には、ソース データベースに対して RESTORE DATABASE 権限が必要です。 データベースを戻すには、次の Transact-SQL ステートメントを使用します。  
  
     RESTORE DATABASE *database_name* FROM DATABASE_SNAPSHOT **=** _database_snapshot_name_  
  
     *database_name* はソース データベースで、 *database_snapshot_name* はデータベースを戻す対象になるスナップショットの名前です。 このステートメントでは、バックアップ デバイスではなく、スナップショット名を指定する必要があることに注意してください。  
  
     詳細については、「 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。  
  
    > [!NOTE]  
    >  データベースを戻す操作中、スナップショットとソース データベースはどちらも使用できません。 ソース データベースとスナップショットは、どちらも "復元中" に設定されます。 データベースを戻す操作中にエラーが発生した場合は、データベースを再び起動したときに、データベースを戻す操作の完了を試行します。  
  
4.  データベース スナップショットの作成後にデータベース所有者を変更した場合、戻したデータベースのデータベース所有者を更新できます。  
  
    > [!NOTE]  
    >  戻したデータベースでは、データベース スナップショットの権限と構成 (データベース所有者や復旧モデルなど) が保持されます。  
  
5.  データベースを起動します。  
  
6.  必要に応じて (特に、完全 (または一括ログ) 復旧モデルを使用している場合)、戻したデータベースをバックアップします。 データベースをバックアップするには、「[データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)」を参照してください。  

###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 ここでは、データベースをデータベース スナップショットに戻す、次の例を示します。  
  
-   A. [AdventureWorks データベースのスナップショットを戻す](#Reverting_AW)  
  
-   B. [Sales データベースのスナップショットを戻す](#Reverting_Sales)  
  
####  <a name="Reverting_AW"></a> A. AdventureWorks データベースのスナップショットを戻す  
 この例では、現在、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに 1 つだけスナップショットが存在することを想定しています。 データベースを戻す対象になるスナップショットを作成する例については、「 [データベース スナップショットの作成 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)」を参照してください。  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="Reverting_Sales"></a> B. Sales データベースのスナップショットを戻す  
 この例では、現在、 **Sales** データベースに 2 つのスナップショット ( **sales_snapshot0600** および **sales_snapshot1200**) が存在することを想定しています。 古いスナップショットを削除し、新しいスナップショットにデータベースを戻します。  
  
 この例で使用するサンプル データベースおよびスナップショットを作成するためのコードについては、次の各トピックを参照してください。  
  
-   **Sales** データベースと **sales_snapshot0600** スナップショットについては、「[CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)」の「ファイル グループのあるデータベースを作成する」および「データベース スナップショットを作成する」を参照してください。  
  
-   **sales_snapshot1200** スナップショットについては、「[データベース スナップショットの作成 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)」の「Sales データベースのスナップショットを作成する」を参照してください。  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベース スナップショットの作成 &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [データベース スナップショットの表示 &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [データベース スナップショットの削除 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [データベース スナップショット &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [データベース ミラーリングとデータベース スナップショット &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
  
