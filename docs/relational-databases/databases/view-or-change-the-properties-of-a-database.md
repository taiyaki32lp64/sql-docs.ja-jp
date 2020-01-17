---
title: データベースのプロパティの表示または変更 | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dc1e6d1021e1e7cf30a683d8c81c625a56b9766c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127055"
---
# <a name="view-or-change-the-properties-of-a-database"></a>データベースのプロパティの表示または変更
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)]のデータベースのプロパティを表示または変更する方法について説明します。 データベースのプロパティを変更すると、変更は直ちに有効になります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **以下を使用してデータベースのプロパティを表示または変更するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   AUTO_CLOSE が ON の場合、データベースからデータを取得できないため、 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューの一部の列、および DATABASEPROPERTYEX 関数は、NULL を返します。 これを解決するには、データベースを開きます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 データベースのプロパティを変更するには、データベースに対する ALTER 権限が必要です。 データベースのプロパティを表示するには、少なくとも public データベース ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>データベースのプロパティを表示または変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、表示するデータベースを右クリックします。次に **[プロパティ]** をクリックします。  
  
3.  **[データベースのプロパティ]** ダイアログ ボックスで、任意のページを選択して、対応する情報を表示します。 たとえば、データおよびログ ファイルの情報を表示するには、 **[ファイル]** ページをクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 Transact-SQL を使用すると、さまざまな方法でデータベースのプロパティを表示および変更できます。 データベースのプロパティを表示するには、 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) 関数と [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューを使用します。 データベースのプロパティを変更するには、自分の環境に合う ALTER DATABASE ステートメントのバージョン ([ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) または [ALTER DATABASE (Azure SQL データベース)](../../t-sql/statements/alter-database-azure-sql-database.md)) を使用できます。 データベース スコープのプロパティを表示するには、 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) カタログ ビューを使用します。データベース スコープのプロパティを変更するには、 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) ステートメントを使用します。  
  
#### <a name="to-view-a-property-of-a-database-by-using-the-databasepropertyex-function"></a>DATABASEPROPERTYEX 関数を使用してデータベースのプロパティを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続し、プロパティを表示するデータベースに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [データベースの AUTO_SHRINK データベース オプションのステータスを、](../../t-sql/functions/databasepropertyex-transact-sql.md) DATABASEPROPERTYEX [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] システム関数を使用して取得します。 戻り値が 1 の場合はオプションがオンに、戻り値が 0 の場合はオフに設定されていることを意味します。  
  
    ```sql  
    SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>sys.databases をクエリすることによってデータベースのプロパティを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続し、プロパティを表示するデータベースに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューをクエリして、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースのいくつかのプロパティを表示します。 この例では、データベースの ID 番号 (`database_id`)、データベースが読み取り専用か読み取り/書き込み可能かの情報 (`is_read_only`)、データベースの照合順序 (`collation_name`)、データベースの互換性レベル (`compatibility_level`) を取得します。  
  
    ```sql  
    SELECT database_id, is_read_only, collation_name, compatibility_level  
    FROM sys.databases WHERE name = 'AdventureWorks2012';  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-scoped-configuration-by-querying-sysdatabasesscopedconfiguration"></a>sys.databases_scoped_configuration を照会してデータベース スコープの構成のプロパティを表示するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続し、プロパティを表示するデータベースに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) カタログ ビューのクエリを実行し、現在のデータベースのいくつかのプロパティを表示します。  
  
    ```sql  
    SELECT configuration_id, name, value, value_for_secondary  
    FROM sys.database_scoped_configurations;  
    ```  
  
     詳細については、「 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  
  
#### <a name="to-change-the-properties-of-a-sql-server-2016-database-using-alter-database"></a>ALTER DATABASE を使用して SQL Server 2016 データベースのプロパティを変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーし、クエリ ウィンドウに貼り付けます。 この例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース上のスナップショット分離の状態を確認し、プロパティの状態を変更した後、変更内容を確認します。  
  
     スナップショット分離の状態を確認するには、まず `SELECT` ステートメントを選択し、 **[実行]** をクリックします。  
  
     スナップショット分離の状態を変更するには、 `ALTER DATABASE` ステートメントを選択し、 **[実行]** をクリックします。  
  
     変更内容を確認するには、2 つ目の `SELECT` ステートメントを選択し、 **[実行]** をクリックします。  
  
     [!code-sql[DatabaseDDL#AlterDatabase9](../../relational-databases/databases/codesnippet/tsql/view-or-change-the-prope_1.sql)]  
  
#### <a name="to-change-the-database-scoped-properties-using-alter-database-scoped-configuration"></a>ALTER DATABASE SCOPED CONFIGURATION を使用してデータベース スコープのプロパティを変更するには  
  
1.  SQL Server インスタンスのデータベースに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーし、クエリ ウィンドウに貼り付けます。 次の例では、セカンダリ データベースの MAXDOP をプライマリ データベースの値に設定しています。  
  
    ```sql  
    ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY   
    ```  
  
## <a name="see-also"></a>参照  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  

  
  
