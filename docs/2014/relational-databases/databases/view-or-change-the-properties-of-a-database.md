---
title: データベースのプロパティの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10ad92286011f6f81fbaff5ab4908007e16bdd45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62870952"
---
# <a name="view-or-change-the-properties-of-a-database"></a>データベースのプロパティの表示または変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベースのプロパティを表示または変更する方法について説明します。 データベースのプロパティを変更すると、変更は直ちに有効になります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用してデータベースのプロパティを表示または変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   AUTO_CLOSE が ON の場合、データベースからデータを取得できないため、 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) カタログ ビューの一部の列、および DATABASEPROPERTYEX 関数は、NULL を返します。 これを解決するには、USE ステートメントを実行してデータベースを開きます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>データベースのプロパティを表示または変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、表示するデータベースを右クリックします。次に **[プロパティ]** をクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、任意のページを選択して、対応する情報を表示します。 たとえば、データおよびログ ファイルの情報を表示するには、 **[ファイル]** ページをクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-view-a-property-of-a-database-by-using-databasepropertyex"></a>DATABASEPROPERTYEX を使用してデータベースのプロパティを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [データベースの AUTO_SHRINK データベース オプションのステータスを、](/sql/t-sql/functions/databasepropertyex-transact-sql) DATABASEPROPERTYEX [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] システム関数を使用して取得します。 戻り値が 1 の場合はオプションがオンに、戻り値が 0 の場合はオフに設定されていることを意味します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
GO  
  
```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>sys.databases をクエリすることによってデータベースのプロパティを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) カタログ ビューをクエリして、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのいくつかのプロパティを表示します。 この例では、データベースの ID 番号 (`database_id`)、データベースが読み取り専用か読み取り/書き込み可能かの情報 (`is_read_only`)、データベースの照合順序 (`collation_name`)、データベースの互換性レベル (`compatibility_level`) を取得します。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT database_id, is_read_only, collation_name, compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-properties-of-a-database"></a>データベースのプロパティを変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーし、クエリ ウィンドウに貼り付けます。 この例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース上のスナップショット分離の状態を確認し、プロパティの状態を変更した後、変更内容を確認します。  
  
     スナップショット分離の状態を確認するには、まず `SELECT` ステートメントを選択し、 **[実行]** をクリックします。  
  
     スナップショット分離の状態を変更するには、 `ALTER DATABASE` ステートメントを選択し、 **[実行]** をクリックします。  
  
     変更内容を確認するには、2 つ目の `SELECT` ステートメントを選択し、 **[実行]** をクリックします。  
  
 [!code-sql[DatabaseDDL#AlterDatabase9](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase9)]  
  
## <a name="see-also"></a>関連項目  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [ALTER DATABASE SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [ALTER DATABASE データベース ミラーリング &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
  
