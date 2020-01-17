---
title: '実証: インメモリ OLTP のパフォーマンスの向上 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c9477a318d2cb4f9886d67da8a4f8b5967cc180
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63071787"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>実証: インメモリ OLTP によるパフォーマンスの向上
  この例では、インメモリ OLTP を使用した場合のパフォーマンスの向上を取り上げます。メモリ最適化テーブルと従来のディスク ベースのテーブルとに対してまったく同じ Transact-SQL クエリを実行したときの応答時間の違いを比較します。 応答時間は一般に、ネイティブ コンパイル ストアド プロシージャでメモリ最適化テーブルを照会したときに最短となります。そこで、ネイティブにコンパイルされたストアド プロシージャも (同じクエリに基づいて) 作成、実行して、その点を実証することにします。 このサンプルを通じて証明されるのは、メモリ最適化テーブルのデータにアクセスしたときに得られるパフォーマンス向上の一面 (挿入操作時のデータ アクセス効率) だけです。 このサンプルはシングル スレッドで、インメモリ OLTP のコンカレンシーの利点を利用していません。 コンカレンシーを使用するワークロードでは、さらにパフォーマンスが向上します。  
  
> [!NOTE]  
>  メモリ最適化テーブルを示す別のサンプルについては、「 [SQL Server 2014 のインメモリ OLTP のサンプル](https://msftdbprodsamples.codeplex.com/releases/view/114491)します。  
  
 このサンプルを実行するために、次の作業を行います。  
  
1.  という名前のデータベースを作成する**imoltp**を設定して、インメモリ OLTP を使用してそのファイルの詳細を変更します。  
  
2.  サンプルに必要なデータベース オブジェクトとして、3 つのテーブルと 1 つのネイティブ コンパイル ストアド プロシージャを作成します。  
  
3.  各種のクエリを実行して、クエリごとの応答時間を表示します。  
  
 セットアップに、 **imoltp**例では、データベースは、まず空のフォルダーを作成: **c:\imoltp_data**、し、次のコードを実行します。  
  
```sql  
USE master  
GO  
  
-- Create a new database.  
CREATE DATABASE imoltp  
GO  
  
-- Prepare the database for In-Memory OLTP by  
-- adding a memory-optimized filegroup to the database.  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_file_group  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
-- Add a file (to hold the memory-optimized data) to the new filegroup.  
ALTER DATABASE imoltp ADD FILE (name='imoltp_file', filename='c:\imoltp_data\imoltp_file')  
    TO FILEGROUP imoltp_file_group;  
GO  
  
```  
  
 次に、各種のデータ アクセス手法をデモンストレーションする目的で使用するディスク ベースのテーブルと 2 つのメモリ最適化テーブル、ネイティブ コンパイル ストアド プロシージャを、以下のコードを実行して作成します。  
  
```sql  
USE imoltp  
GO  
  
-- If the tables or stored procedure already exist, drop them to start clean.  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'DiskBasedTable')  
   DROP TABLE [dbo].[DiskBasedTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects WHERE NAME = 'InMemTable')  
   DROP TABLE [dbo].[InMemTable]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'InMemTable2')  
   DROP TABLE [dbo].[InMemTable2]  
GO  
  
IF EXISTS (SELECT NAME FROM sys.objects  WHERE NAME = 'usp_InsertData')  
   DROP PROCEDURE [dbo].[usp_InsertData]  
GO  
  
-- Create a traditional disk-based table.  
CREATE TABLE [dbo].[DiskBasedTable] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
)  
GO  
  
-- Create a memory-optimized table.  
CREATE TABLE [dbo].[InMemTable] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a 2nd memory-optimized table.  
CREATE TABLE [dbo].[InMemTable2] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
GO  
  
-- Create a natively-compiled stored procedure.  
CREATE PROCEDURE [dbo].[usp_InsertData]   
  @rowcount INT,  
  @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[inMemTable2](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
END  
GO  
  
```  
  
 これでセットアップは完了です。クエリを実行する準備が整いました。クエリで応答時間を表示し、データ アクセス手法ごとのパフォーマンスを比較することができます。  
  
 この例の目的上、次のコードを複数回実行する必要があります。 初回実行時の結果は、初期メモリ割り当てによるマイナスの影響を含んでいるため、無視してください。  
  
```sql  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Delete data from all tables to reset the example.  
DELETE FROM [dbo].[DiskBasedTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[inMemTable]   
    WHERE [c1]>0  
GO  
DELETE FROM [dbo].[InMemTable2]   
    WHERE [c1]>0  
GO  
  
-- Declare parameters for the test queries.  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
DECLARE @timems INT;  
DECLARE @starttime datetime2 = sysdatetime();  
  
-- Disk-based table queried with interpreted Transact-SQL.  
BEGIN TRAN  
  WHILE @I <= @rowcount  
  BEGIN  
    INSERT INTO [dbo].[DiskBasedTable](c1,c2) VALUES (@i, @c);  
    SET @i += 1;  
  END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (disk-based table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with interpreted Transact-SQL.  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN  
  WHILE @i <= @rowcount  
    BEGIN  
      INSERT INTO [dbo].[InMemTable](c1,c2) VALUES (@i, @c);  
      SET @i += 1;  
    END  
COMMIT  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with interpreted Transact-SQL).';  
  
-- Memory-optimized table queried with a natively-compiled stored procedure.  
SET @starttime = sysdatetime();  
  
EXEC usp_InsertData @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT CAST(@timems AS VARCHAR(10)) + ' ms (memory-optimized table with natively-compiled stored procedure).';  
  
```  
  
 実際の応答時間を比較すると、メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャを用いた手法の方が、従来型のディスク ベースのテーブルに対して同じワークロードを実行した場合よりも一貫して応答時間が短いことがわかります。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP を実証する adventureworks の拡張機能](../../database-engine/extensions-to-adventureworks-to-demonstrate-in-memory-oltp.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](in-memory-oltp-in-memory-optimization.md)   
 [メモリ最適化テーブル](memory-optimized-tables.md)   
 [ネイティブ コンパイル ストアド プロシージャ](natively-compiled-stored-procedures.md)   
 [メモリ最適化テーブルを使用するための要件](requirements-for-using-memory-optimized-tables.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER DATABASE の File および Filegroup オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)   
 [CREATE PROCEDURE とメモリ最適化テーブル](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
