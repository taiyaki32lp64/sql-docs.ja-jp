---
title: パフォーマンスの向上 - インメモリ OLTP
ms.custom: seo-dt-2019
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c6def45d-d2d4-4d24-8068-fab4cd94d8cc
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68cb4e95046ca2fb071ecf2ba7c713cf57646690
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412731"
---
# <a name="demonstration-performance-improvement-of-in-memory-oltp"></a>実証: インメモリ OLTP によるパフォーマンスの向上
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  このトピック内のコード サンプルは、メモリ最適化テーブルの高速なパフォーマンスを実証します。 パフォーマンス向上は、従来の解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)]から、メモリ最適化テーブル内のデータにアクセスする場合にも明白になります。 このパフォーマンス向上は、ネイティブ コンパイル ストアド プロシージャ (NCSProc) からメモリ最適化テーブル内のデータにアクセスするときにさらに大きくなります。  
 
インメモリ OLTP のパフォーマンスを改善できる可能性を示す包括的なデモについては、 [In-Memory OLTP Performance Demo v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)を参照してください。 
  
 この記事のサンプル コードはシングル スレッドで、インメモリ OLTP のコンカレンシーの利点を利用していません。 コンカレンシーを使用するワークロードでは、さらにパフォーマンスが向上します。 このサンプル コードでは、パフォーマンス向上の一面のみ、具体的には INSERT のデータ アクセスの効率性を示します。  
  
 メモリ最適化テーブルによって達成されるパフォーマンス向上は、NCSProc から、メモリ最適化テーブル内のデータにアクセスするときに完全に実現します。  
  
## <a name="code-example"></a>コード例  
 次のサブセクションでは、各手順について説明します。  
  
### <a name="step-1a-prerequisite-if-using-includessnoversionincludesssnoversion-mdmd"></a>手順 1a:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用時の前提条件  
 この最初のサブセクションの手順は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で実行する場合にのみ適用され、 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]で実行する場合には適用されません。 次の操作を行います。  
  
1.  SQL Server Management Studio (SSMS.exe) を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続します。 または、SSMS.exe に類似した任意のツールも使用できます。  
  
2.  **C:\data\\** という名前のディレクトリを手動で作成します。 サンプルの Transact-SQL コードでは、ディレクトリがあらかじめ存在することが想定されています。  
  
3.  短い T-SQL を実行して、データベースおよびそのメモリ最適化ファイル グループを作成します。  
  
```sql  
go  
CREATE DATABASE imoltp;    --  Transact-SQL  
go  
  
ALTER DATABASE imoltp ADD FILEGROUP [imoltp_mod]  
    CONTAINS MEMORY_OPTIMIZED_DATA;  
  
ALTER DATABASE imoltp ADD FILE  
    (name = [imoltp_dir], filename= 'c:\data\imoltp_dir')  
    TO FILEGROUP imoltp_mod;  
go  
  
USE imoltp;  
go  
```  
  
### <a name="step-1b-prerequisite-if-using-includesssdsfullincludessssdsfull-mdmd"></a>手順 1b:[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 使用時の前提条件  
 このサブセクションは、 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]を使用している場合にのみ適用されます。 次の操作を行います。  
  
1.  コード例に使用する既存のテスト データベースを決定します。  
  
2.  新しいテスト データベースを作成する場合は、 [Azure ポータル](https://portal.azure.com) を使用して、 **imoltp**という名前のデータベースを作成します。  
  
 その場合に Azure ポータルを使用する手順については、「 [Get Started with Azure SQL Database (Azure SQL Database の概要)](https://azure.microsoft.com/documentation/articles/sql-database-get-started)」を参照してください。  
  
### <a name="step-2-create-memory-optimized-tables-and-ncsproc"></a>手順 2:メモリ最適化テーブルと NCSProc を作成する  
 この手順では、メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャ (NCSProc) を作成します。 次の操作を行います。  
  
1.  SSMS.exe を使用して、新しいデータベースに接続します。  
  
2.  データベースで、次の T-SQL を実行します。  
  
```sql  
go  
DROP PROCEDURE IF EXISTS ncsp;  
DROP TABLE IF EXISTS sql;  
DROP TABLE IF EXISTS hash_i;  
DROP TABLE IF EXISTS hash_c;  
go  
  
CREATE TABLE [dbo].[sql] (  
  c1 INT NOT NULL PRIMARY KEY,  
  c2 NCHAR(48) NOT NULL  
);  
go  
  
CREATE TABLE [dbo].[hash_i] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE TABLE [dbo].[hash_c] (  
  c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT=1000000),  
  c2 NCHAR(48) NOT NULL  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY = SCHEMA_AND_DATA);  
go  
  
CREATE PROCEDURE ncsp  
    @rowcount INT,  
    @c NCHAR(48)  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS   
  BEGIN ATOMIC   
  WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @i INT = 1;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[hash_c] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
END;  
go  
```  
  
### <a name="step-3-run-the-code"></a>手順 3:コードを実行する  
 ここで、メモリ最適化テーブルによるパフォーマンスを実証するクエリを実行できます。 次の操作を行います。  
  
1.  SSMS.exe を使用して、データベースで次の T-SQL を実行します。  
  
     この最初の実行で生成される速度などのパフォーマンス データをすべて無視します。 最初の実行では、メモリの初期割り当てなど、1 回限りの操作が実行されることを確認します。  
  
2.  もう一度 SSMS.exe を使用して、データベースで次の T-SQL を再実行します。  
  
```sql  
go  
SET STATISTICS TIME OFF;  
SET NOCOUNT ON;  
  
-- Inserts, one at a time.  
  
DECLARE @starttime DATETIME2 = sysdatetime();  
DECLARE @timems INT;  
DECLARE @i INT = 1;  
DECLARE @rowcount INT = 100000;  
DECLARE @c NCHAR(48) = N'12345678901234567890123456789012345678';  
  
-- Harddrive-based table and interpreted Transact-SQL.  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
  BEGIN;  
    INSERT INTO [dbo].[sql] VALUES (@i, @c);  
    SET @i += 1;  
  END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'A: Disk-based table and interpreted Transact-SQL: '  
    + cast(@timems AS VARCHAR(10)) + ' ms';  
  
-- Interop Hash.  
  
SET @i = 1;  
SET @starttime = sysdatetime();  
  
BEGIN TRAN;  
  WHILE @i <= @rowcount  
    BEGIN;  
      INSERT INTO [dbo].[hash_i] VALUES (@i, @c);  
      SET @i += 1;  
    END;  
COMMIT;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'B: memory-optimized table with hash index and interpreted Transact-SQL: '  
    + cast(@timems as VARCHAR(10)) + ' ms';  
  
-- Compiled Hash.  
  
SET @starttime = sysdatetime();  
  
EXECUTE ncsp @rowcount, @c;  
  
SET @timems = datediff(ms, @starttime, sysdatetime());  
SELECT 'C: memory-optimized table with hash index and native SP:'  
    + cast(@timems as varchar(10)) + ' ms';  
go  
  
DELETE sql;  
DELETE hash_i;  
DELETE hash_c;  
go  
```  
  
 次に、2 回目のテスト実行で生成される出力時間の統計を示します。  
  
```sql  
10453 ms , A: Disk-based table and interpreted Transact-SQL.  
5626 ms , B: memory-optimized table with hash index and interpreted Transact-SQL.  
3937 ms , C: memory-optimized table with hash index and native SP.  
```  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
