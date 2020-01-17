---
title: データベースのデータ領域とログ領域情報の表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], space
- status information [SQL Server], space
- displaying space information
- disk space [SQL Server], displaying
- databases [SQL Server], space used
- viewing space information
- space allocation [SQL Server], displaying
- data space [SQL Server]
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4850be4c112f9c0b987d543873cb55af08372455
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62917345"
---
# <a name="display-data-and-log-space-information-for-a-database"></a>データベースのデータ領域とログ領域情報の表示
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベースのデータ領域およびログ領域情報を表示する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **データを表示し、ログ、データベースの領域情報を使用します。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 **sp_spaceused** の実行権限は、 **public** ロールに与えられています。 **@updateusage** パラメーターを指定できるのは、**db_owner** 固定データベース ロールのメンバーだけです。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-display-data-and-log-space-information-for-a-database"></a>データベースのデータ領域とログ領域情報を表示するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開します。  
  
3.  データベースを右クリックし、 **[レポート]** 、 **[標準レポート]** の順にポイントして、 **[ディスク使用量]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-using-spspaceused"></a>sp_spaceused を使用してデータベースのデータ領域とログ領域情報を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) システム ストアド プロシージャを使用して、 `Vendor` テーブルとそのインデックスに対するディスク領域情報を報告します。  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-querying-sysdatabasefiles"></a>querying sys.database_files をクエリすることによってデータベースのデータ領域とログ領域情報を表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) カタログ ビューに対してクエリを実行し、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内のデータ ファイルとログ ファイルに関する特定の情報を取得します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [sys.database_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sp_spaceused &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)   
 [データベースに対するデータ ファイルまたはログ ファイルの追加](add-data-or-log-files-to-a-database.md)   
 [データまたはログ ファイルのデータベースからの削除](delete-data-or-log-files-from-a-database.md)  
  
  
