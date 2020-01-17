---
title: メモリ最適化テーブル変数 |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: bd102e95-53e2-4da6-9b8b-0e4f02d286d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 485f481819a9712f822f969c04d8e7050ad43bae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774419"
---
# <a name="memory-optimized-table-variables"></a>メモリ最適化テーブル変数
  メモリ最適化テーブル (効率的なデータ アクセスのため) とネイティブ コンパイル ストアド プロシージャ (効率的なクエリ処理とビジネス ロジックの実行のため) に加えて、[!INCLUDE[hek_2](../includes/hek-2-md.md)] では、3 つ目のオブジェクトの種類としてメモリ最適化テーブル型が導入されます。 メモリ最適化テーブル型を使用して作成されたテーブル変数は、メモリ最適化テーブル変数です。  
  
 メモリ最適化テーブル変数には、ディスク ベース テーブル変数と比べて次の利点があります。  
  
-   変数はメモリにしか格納されません。 メモリ最適化テーブル型では、メモリ最適化テーブルで使用されるものと同じメモリ最適化アルゴリズムとデータ構造が使用されるため、データ アクセスがさらに効率的になります。特に、変数をネイティブ コンパイル ストアド プロシージャで使用するときに効率的です。  
  
-   メモリ最適化テーブル変数を使用する場合、tempdb は使用しません。 テーブル変数は tempdb に保存されず、tempdb 内のリソースを使用しません。  
  
 メモリ最適化テーブル変数の一般的な使用シナリオは次のとおりです。  
  
-   中間結果を保存し、ネイティブ コンパイル ストアド プロシージャの複数のクエリに基づいて単一の結果セットを作成します。  
  
-   ネイティブ コンパイル ストアド プロシージャおよびインタープリターで処理されるストアド プロシージャに、テーブル値パラメーターを渡します。  
  
-   ディスク ベース テーブル変数を置き換え、場合によっては、ストアド プロシージャに対してローカルな #temp テーブルを置き換えます。 これは、システムに多くの tempdb の競合がある場合に特に便利です。  
  
-   テーブル変数を使用して、ネイティブ コンパイル ストアド プロシージャのカーソルをシミュレートすることができ、その結果、ネイティブ コンパイル ストアド プロシージャの対象領域の制限を回避できるようになります。  
  
 メモリ最適化テーブルと同様に、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によってメモリ最適化テーブル型ごとに DLL が生成されます (コンパイルは、ときではなく、メモリ最適化テーブル変数を作成するために使用し、メモリ最適化テーブル型が作成されたときに呼び出されます)。この DLL には、インデックスにアクセスし、テーブル変数からデータを取得するための関数が含まれます。 メモリ最適化テーブル変数がテーブル型に基づいて宣言されると、テーブルとテーブル型に対応するインデックス構造のインスタンスがユーザー セッションで作成されます。 その後、テーブル変数をディスク ベース テーブル変数と同じ方法で使用できます。 テーブル変数の行を挿入、更新、および削除でき、 [!INCLUDE[tsql](../includes/tsql-md.md)] クエリで変数を使用できます。 また、ネイティブ コンパイル ストアド プロシージャと、インタープリターによって処理されるストアド プロシージャに、テーブル値パラメーター (TVP) として変数を渡すことができます。  
  
 次の例では、AdventureWorks に基づくインメモリ OLTP のサンプルからメモリ最適化テーブル型 ([SQL Server 2014 のインメモリ OLTP のサンプル](https://msftdbprodsamples.codeplex.com/releases/view/114491))。  
  
```sql
CREATE TYPE Sales.SalesOrderDetailType_inmem
   AS TABLE
(
   OrderQty         smallint   NOT NULL,
   ProductID        int        NOT NULL,

   SpecialOfferID   int        NOT NULL
      INDEX  IX_SpecialOfferID  NONCLUSTERED,

   LocalID          int        NOT NULL,

   INDEX IX_ProductID HASH (ProductID)
      WITH ( BUCKET_COUNT = 8 )
)
WITH ( MEMORY_OPTIMIZED = ON );
```  
  
 このサンプルは、メモリ最適化テーブル型の構文がディスク ベース テーブル型に類似していることを示しています。ただし、次の例外を除きます。  
  
-   `MEMORY_OPTIMIZED=ON` は、テーブル型がメモリ最適化であることを示します。  
  
-   型には少なくとも 1 つのインデックスが必要です。 メモリ最適化テーブルの場合と同様に、ハッシュ インデックスと非クラスター化インデックスを使用できます。  
  
     ハッシュ インデックスの場合、バケット数は予想される一意のキーの数からその 2 倍の数ぐらいまでの範囲にしてください。 詳細については、「 [Determining the Correct Bucket Count for Hash Indexes](../relational-databases/indexes/indexes.md)」を参照してください。  
  
-   メモリ最適化テーブルのデータ型および制約の制限は、メモリ最適化テーブル型にも適用されます。 たとえば、[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] では既定の制約はサポートされますが、CHECK 制約はサポートされません。  
  
 メモリ最適化テーブルと同様に、メモリ最適化テーブル変数には次のことが当てはまります。  
  
-   並列プランはサポートされません。  
  
-   メモリに収まる必要があるため、ディスク リソースを使用しません。  
  
 ディスク ベース テーブル変数は tempdb 内に存在します。 メモリ最適化テーブル変数は、ユーザー データベース内に存在します (ただし、ストレージを消費せず、復旧もされません)。  
  
 インライン構文を使用して、メモリ最適化テーブル変数を作成することはできません。 ディスク ベース テーブル変数とは異なり、最初に型を作成する必要があります。  
  
## <a name="table-valued-parameters"></a>テーブル値パラメーター  
 次のサンプル スクリプトでは、メモリ最適化テーブル型 `Sales.SalesOrderDetailType_inmem` としてテーブル変数を宣言し、変数に 3 つの行を挿入し、変数を TVP として `Sales.usp_InsertSalesOrder_inmem` に渡します。  
  
```sql  
DECLARE @od Sales.SalesOrderDetailType_inmem,  
  @SalesOrderID uniqueidentifier,  
  @DueDate datetime2 = SYSDATETIME()  
  
INSERT @od (LocalID, ProductID, OrderQty, SpecialOfferID) VALUES  
  (1, 888, 2, 1),  
  (2, 450, 13, 1),  
  (3, 841, 1, 1)  
  
EXEC Sales.usp_InsertSalesOrder_inmem  
  @SalesOrderID = @SalesOrderID,  
  @DueDate = @DueDate,  
 @OnlineOrderFlag = 1,  
  @SalesOrderDetails = @od  
```  
  
 メモリ最適化テーブル型は、ストアド プロシージャのテーブル値パラメーター (TVP) の型として使用でき、ディスク ベース テーブル型および TVP とまったく同じようにクライアントから参照できます。 したがって、メモリ最適化 TVP が含まれるストアド プロシージャ、およびネイティブ コンパイル ストアド プロシージャの呼び出しは、ディスク ベース TVP が含まれる、インタープリターによって解釈されるストアド プロシージャの呼び出しとまったく同じように動作します。  
  
## <a name="temp-table-replacement"></a>#temp テーブルの置換  
 次のサンプルは、ストアド プロシージャに対してローカルな #temp のテーブルの代わりとしてのメモリ最適化テーブル型およびテーブル変数を示しています。  
  
```sql  
-- Using SQL procedure and temp table  
CREATE TABLE #tempTable (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
  
CREATE PROCEDURE sqlProc  
AS  
BEGIN  
  TRUNCATE TABLE #tempTable  
  
  INSERT #tempTable VALUES (1)  
  INSERT #tempTable VALUES (2)  
  INSERT #tempTable VALUES (3)  
  SELECT * FROM #tempTable  
END  
GO  
  
-- Using natively compiled stored procedure and table variable  
CREATE TYPE TT AS TABLE (c INT NOT NULL PRIMARY KEY NONCLUSTERED)  
GO  
  
CREATE PROCEDURE NCSPProc  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  DECLARE @tableVariable TT  
  INSERT @tableVariable VALUES (1)  
  INSERT @tableVariable VALUES (2)  
  INSERT @tableVariable VALUES (3)  
  SELECT c FROM @tableVariable  
END  
GO  
```  
  
## <a name="creating-a-single-result-set"></a>単一結果セットの作成  
 次のサンプルでは、中間結果を保存し、ネイティブ コンパイル ストアド プロシージャの複数のクエリに基づいて単一の結果セットを作成する方法を示します。 ここでは、UNION 演算子を使用した `SELECT c1 FROM dbo.t1 UNION SELECT c1 FROM dbo.t2` を計算しています。  
  
```sql  
CREATE DATABASE hk  
GO  
ALTER DATABASE hk ADD FILEGROUP hk_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE hk ADD FILE( NAME = 'hk_mod' , FILENAME = 'c:\data\hk_mod') TO FILEGROUP hk_mod;  
  
USE hk  
GO  
  
CREATE TYPE tab1 AS TABLE (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON)  
  
CREATE TABLE dbo.t1 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
CREATE TABLE dbo.t2 (c1 INT NOT NULL, INDEX idx NONCLUSTERED(c1)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
  
INSERT INTO dbo.t1 VALUES (1), (2)  
INSERT INTO dbo.t2 VALUES (3), (4)  
GO  
  
CREATE PROCEDURE dbo.p1  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
  AS  
  BEGIN ATOMIC WITH ( TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english' )  
  
    DECLARE @t dbo.tab1  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t1;  
  
    INSERT @t (c1)  
    SELECT c1 FROM dbo.t2;  
  
    SELECT c1 FROM @t;  
  END  
GO  
  
EXEC dbo.p1  
GO  
```  
  
## <a name="memory-consumption-for-table-variables"></a>テーブル変数によるメモリ消費  
 テーブル変数によるメモリ消費は、非クラスター化インデックスを除き、メモリ最適化テーブルに似ています。 非クラスター化インデックスを使用してメモリ最適化テーブル変数に多数の行を挿入する場合に、インデックス キーが大きいと、これらのテーブル変数では過剰な量のメモリが使用されます。 大きなテーブル変数を対象とする非クラスター化インデックスは、非クラスター化インデックス テーブルが同じ数の行を挿入する場合に比べて多くのメモリ (インデックス ページ内のより多くメモリ) を必要とします。  
  
 テーブル変数のメモリは、データベースのリソース ガバナー リソース プールから取得されます。  
  
 メモリ最適化テーブルとは異なり、テーブル変数によって消費された (削除された行を含む) メモリは、テーブル変数がスコープ外になると解放されます。  
  
 メモリは、データベースの単一 PGPOOL メモリ コンシューマーの一部として説明されます。  
  
## <a name="see-also"></a>関連項目  
 [Transact-SQL によるインメモリ OLTP のサポート](../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
  
