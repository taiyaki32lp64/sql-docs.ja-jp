---
title: データベースの照合順序の設定または変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 38c29f8d70b3cc72baf81e2ae23082fe270ba573
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874027"
---
# <a name="set-or-change-the-database-collation"></a>データベースの照合順序の設定または変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でデータベースの照合順序を設定および変更する方法を説明します。 照合順序を指定しない場合、サーバーの照合順序が使用されます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **データベースの照合順序を設定または変更する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   Windows Unicode 専用の照合順序は、COLLATE 句で `nchar`、`nvarchar`、および `ntext` の各データ型を列レベルと式レベルのデータに適用する場合にのみ使用できます。 データベースまたはサーバー インスタンスの照合順序を変更するために、COLLATE 句で使用することはできません。  
  
-   指定した照合順序、または参照先のオブジェクトで使用される照合順序で、Windows でサポートされていないコード ページが使用されていると、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] でエラーが表示されます。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   サポートされる照合順序名は、「 [Windows 照合順序名 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql) 」と「 [SQL Server 照合順序名 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)」で確認できます。または、 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql) システム関数を使用できます。  
  
-   データベースの照合順序を変更すると、次の変更が行われます。  
  
    -   システム テーブル内の `char` 型、`varchar` 型、`text` 型、`nchar` 型、`nvarchar` 型、または `ntext` 型の列はすべて、新しい照合順序に変更されます。  
  
    -   ストアド プロージャおよびユーザー定義関数で使用されている `char` 型、`varchar` 型、`text` 型、`nchar` 型、`nvarchar` 型、または `ntext` 型の既存のパラメーターおよびスカラー値の戻り値はすべて、新しい照合順序に変更されます。  
  
    -   `char` 型、`varchar` 型、`text` 型、`nchar` 型、`nvarchar` 型、または `ntext` 型のシステム データ型およびこれらを基にしたユーザー定義データ型はすべて、新しい既定の照合順序に変更されます。  
  
-   ユーザー データベースに作成する新しいオブジェクトの照合順序は、 [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) ステートメントの COLLATE 句を使用して変更できます。 このステートメントを実行しても、既存のユーザー定義テーブルの列の照合順序は変わりません。 [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql)の COLLATE 句で変更することができます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 CREATE DATABASE  
 **master** データベースの CREATE DATABASE 権限か、CREATE ANY DATABASE 権限または ALTER ANY DATABASE 権限が必要です。  
  
 ALTER DATABASE  
 データベースに対する ALTER 権限が必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-set-or-change-the-database-collation"></a>データベースの照合順序を設定または変更するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続して、そのインスタンスを展開します。次に、 **[データベース]** を展開します。  
  
2.  新しいデータベースを作成する場合は、 **[データベース]** を右クリックし、 **[新しいデータベース]** をクリックします。 既定の照合順序を使用しない場合は、 **[オプション]** ページをクリックし、 **[照合順序]** ボックスの一覧から照合順序を選択します。  
  
     データベースが既に存在する場合は、使用するデータベースを右クリックし、 **[プロパティ]** をクリックします。 **[オプション]** ページをクリックし、 **[照合順序]** ボックスの一覧から照合順序を選択します。  
  
3.  終了したら **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-set-the-database-collation"></a>データベースの照合順序を設定するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、 [COLLATE](/sql/t-sql/statements/collations) 句を使用して照合順序名を指定する方法を示しています。 この例は、 `MyOptionsTest` 照合順序を使用する `Latin1_General_100_CS_AS_SC` を作成します。 データベースを作成したら、 `SELECT` ステートメントを実行して設定を検証します。  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>データベースの照合順序を変更するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例は、 [ALTER DATABASE](/sql/t-sql/statements/collations) ステートメントで [COLLATE](/sql/t-sql/statements/alter-database-transact-sql) 句を使用して照合順序名を変更する方法を示しています。 `SELECT` ステートメントを実行して変更を確認します。  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>関連項目  
 [照合順序と Unicode のサポート](collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [SQL Server 照合順序名 &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Windows 照合順序名 &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)   
 [照合順序の優先順位 &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
