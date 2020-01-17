---
title: SQL Server on Linux のパフォーマンス機能の概要
description: この記事では、SQL Server を初めて使用する Linux ユーザー向けに SQL Server のパフォーマンス機能について概要を説明します。 これらの例の多くはすべてのプラットフォームで動作しますが、この記事のコンテキストは Linux です。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 60036d26-4797-4872-9a9e-3552841c61be
ms.openlocfilehash: fe60b00654d93c6362a8671318a4b7b88ae90a5f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "67896163"
---
# <a name="walkthrough-for-the-performance-features-of-sql-server-on-linux"></a>SQL Server on Linux のパフォーマンス機能のチュートリアル

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server を初めて使用する Linux ユーザーの場合は、次のタスクを使い、パフォーマンス機能の一部について順を追って説明します。 これらは Linux 独自または固有のものではありませんが、さらに調べる領域について考えるヒントになります。 各例には、その領域の詳細なドキュメントのリンクが記載されています。

> [!NOTE]
> 次の例では、AdventureWorks サンプル データベースを使用します。 このサンプル データベースを入手してインストールする手順については、[Windows から Linux への SQL Server データベースの復元](sql-server-linux-migrate-restore-database.md)に関する記事を参照してください。

## <a name="create-a-columnstore-index"></a>列ストア インデックスを作成する
列ストア インデックスは、列ストアと呼ばれる列データ形式で大量のデータを格納し、クエリを実行するためのテクノロジです。  

1. 次の Transact-SQL コマンドを実行して、SalesOrderDetail テーブルに列ストア インデックスを追加します。

   ```sql
   CREATE NONCLUSTERED COLUMNSTORE INDEX [IX_SalesOrderDetail_ColumnStore]
      ON Sales.SalesOrderDetail
      (UnitPrice, OrderQty, ProductID)
   GO
   ```

2. 列ストア インデックスを使用してテーブルをスキャンする次のクエリを実行します。

   ```sql
   SELECT ProductID, SUM(UnitPrice) SumUnitPrice, AVG(UnitPrice) AvgUnitPrice,
      SUM(OrderQty) SumOrderQty, AVG(OrderQty) AvgOrderQty
   FROM Sales.SalesOrderDetail
      GROUP BY ProductID
      ORDER BY ProductID
   ```

3. 列ストア インデックスの object_id を調べ、それが SalesOrderDetail テーブルの使用状況の統計情報に存在することを確認して、列ストア インデックスが使用されたことを確認します。

   ```sql
   SELECT * FROM sys.indexes WHERE name = 'IX_SalesOrderDetail_ColumnStore'
   GO

   SELECT * 
   FROM sys.dm_db_index_usage_stats
      WHERE database_id = DB_ID('AdventureWorks')
      AND object_id = OBJECT_ID('AdventureWorks.Sales.SalesOrderDetail');
   ```
   
## <a name="use-in-memory-oltp"></a>インメモリ OLTP を使用する
SQL Server には、アプリケーション システムのパフォーマンスを大幅に改善できるインメモリ OLTP 機能があります。  評価ガイドのこのセクションでは、メモリに格納されたメモリ最適化テーブルと、コンパイルや解釈を必要とせずにそのテーブルにアクセスできるネイティブでコンパイルされたストアド プロシージャを作成する手順について説明します。

### <a name="configure-database-for-in-memory-oltp"></a>インメモリ OLTP のデータベースを構成する
1. インメモリ OLTP を使用するには、データベースを 130 以上の互換性レベルに設定することをお勧めします。  AdventureWorks の現在の互換性レベルを確認するには、次のクエリを使用します。  

   ```sql
   USE AdventureWorks
   GO
   SELECT d.compatibility_level
   FROM sys.databases as d
     WHERE d.name = Db_Name();
   GO
   ```
   
   必要に応じて、レベルを 130 に更新します。

   ```sql
   ALTER DATABASE CURRENT
   SET COMPATIBILITY_LEVEL = 130;
   GO
   ```

2. トランザクションがディスクベースのテーブルとメモリ最適化テーブルの両方に関係する場合、トランザクションのメモリ最適化部分が SNAPSHOT というトランザクション分離レベルで動作することが不可欠です。  クロスコンテナー トランザクションのメモリ最適化テーブルにこのレベルを確実に適用するには、以下を実行します。

   ```sql
   ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
   GO
   ```

3. メモリ最適化テーブルを作成する前に、まずメモリ最適化 FILEGROUP とデータ ファイル用コンテナーを作成する必要があります。

   ```sql
   ALTER DATABASE AdventureWorks ADD FILEGROUP AdventureWorks_mod CONTAINS memory_optimized_data
   GO  
   ALTER DATABASE AdventureWorks ADD FILE (NAME='AdventureWorks_mod', FILENAME='/var/opt/mssql/data/AdventureWorks_mod') TO FILEGROUP AdventureWorks_mod
   GO
   ```

### <a name="create-a-memory-optimized-table"></a>メモリ最適化テーブルを作成する
メモリ最適化テーブルのプライマリ ストアはメイン メモリなので、ディスクベースのテーブルとは異なり、データをディスクからメモリ バッファーに読み込む必要はありません。  メモリ最適化テーブルを作成するには、MEMORY_OPTIMIZED = ON 句を使用します。

1. 次のクエリを実行して、メモリ最適化テーブル dbo.ShoppingCart を作成します。  既定では、データは持続性のためにディスクに永続化されます (DURABILITY はスキーマのみを永続化するように設定することもできることに注意してください)。 

   ```sql
   CREATE TABLE dbo.ShoppingCart ( 
   ShoppingCartId INT IDENTITY(1,1) PRIMARY KEY NONCLUSTERED,
   UserId INT NOT NULL INDEX ix_UserId NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000), 
   CreatedDate DATETIME2 NOT NULL, 
   TotalPrice MONEY
   ) WITH (MEMORY_OPTIMIZED=ON) 
   GO
   ```

2. テーブルにいくつかのレコードを挿入します。

   ```sql
   INSERT dbo.ShoppingCart VALUES (8798, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (23, SYSDATETIME(), 45.4) 
   INSERT dbo.ShoppingCart VALUES (80, SYSDATETIME(), NULL) 
   INSERT dbo.ShoppingCart VALUES (342, SYSDATETIME(), 65.4) 
   ```

### <a name="natively-compiled-stored-procedure"></a>ネイティブ コンパイル ストアド プロシージャ
SQL Server は、メモリ最適化テーブルにアクセスするネイティブ コンパイル ストアド プロシージャをサポートしています。 T-SQL ステートメントはマシン コードにコンパイルされ、ネイティブ DLL として保存されるので、従来の T-SQL よりも高速なデータ アクセスとより効率的なクエリ実行が可能になります。   NATIVE_COMPILATION が設定されているストアド プロシージャはネイティブでコンパイルされます。 

1. 次のスクリプトを実行して、ShoppingCart テーブルに多数のレコードを挿入するネイティブ コンパイル ストアド プロシージャを作成します。


   ```sql
   CREATE PROCEDURE dbo.usp_InsertSampleCarts @InsertCount int 
    WITH NATIVE_COMPILATION, SCHEMABINDING AS 
   BEGIN ATOMIC 
   WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')

   DECLARE @i int = 0

   WHILE @i < @InsertCount 
    BEGIN 
     INSERT INTO dbo.ShoppingCart VALUES (1, SYSDATETIME() , NULL) 
     SET @i += 1 
    END
   END 
   ```
2. 1,000,000 行を挿入します。

   ```sql
   EXEC usp_InsertSampleCarts 1000000 
   ```

3. 行が挿入されたことを確認します。

   ```sql
   SELECT COUNT(*) FROM dbo.ShoppingCart 
   ```

### <a name="learn-more-about-in-memory-oltp"></a>インメモリ OLTP の詳細
インメモリ OLTP の詳細については、次のトピックを参照してください。

- [クイック スタート 1:Transact-SQL のパフォーマンスを向上させるインメモリ OLTP テクノロジ](../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)
- [インメモリ OLTP への移行](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)
- [メモリ最適化を使用した一時テーブルとテーブル変数の高速化](../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md)
- [メモリ使用量の監視とトラブルシューティング](../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)
- [インメモリ OLTP (インメモリ最適化)](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)

## <a name="use-query-store"></a>クエリ ストアを使用する
クエリ ストアでは、クエリ、実行プラン、およびランタイム統計に関する詳細なパフォーマンス情報を収集します。

クエリ ストアは既定ではアクティブではなく、ALTER DATABASE を使用して有効にすることができます。

   ```sql
   ALTER DATABASE AdventureWorks SET QUERY_STORE = ON;
   ```

次のクエリを実行して、クエリ ストア内のクエリとプランに関する情報を返します。 

   ```sql
   SELECT Txt.query_text_id, Txt.query_sql_text, Pl.plan_id, Qry.*
   FROM sys.query_store_plan AS Pl
      JOIN sys.query_store_query AS Qry
         ON Pl.query_id = Qry.query_id
      JOIN sys.query_store_query_text AS Txt
         ON Qry.query_text_id = Txt.query_text_id ;
   ```

## <a name="query-dynamic-management-views"></a>クエリ動的管理ビュー
動的管理ビューでは、サーバーの状態情報が返されます。返された情報は、サーバー インスタンスのヘルス状態の監視、問題の診断、パフォーマンスのチューニングに使用できます。

dm_os_wait stats 動的管理ビューのクエリを実行するには:

   ```sql
   SELECT wait_type, wait_time_ms
   FROM sys.dm_os_wait_stats;
   ```
