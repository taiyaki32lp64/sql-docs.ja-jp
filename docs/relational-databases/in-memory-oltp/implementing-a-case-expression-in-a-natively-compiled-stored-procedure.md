---
title: ネイティブ コンパイル ストアド プロシージャの CASE 式
ms.custom: seo-dt-2019
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2f82db01-da7e-4a7d-8bc0-48b245e6f768
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5c26cd8424000926030d37302606cece6a570668
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412651"
---
# <a name="implementing-a-case-expression-in-a-natively-compiled-stored-procedure"></a>ネイティブ コンパイル ストアド プロシージャに CASE 式を実装する
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**適用対象:** [!INCLUDE[ssSDSFull_md](../../includes/sssdsfull-md.md)] および [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降の SQL Server

CASE 式は、ネイティブ コンパイル T-SQL モジュールでサポートされています。 次の例では、クエリで CASE 式を使用する方法を示します。 

``` 
-- Query using a CASE expression in a natively compiled stored procedure.
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
   SELECT   
      SalesOrderID,   
      CASE (OnlineOrderFlag)   
      WHEN 1 THEN N'Order placed online by customer'  
      ELSE N'Order placed by sales person'  
      END  
   FROM Sales.SalesOrderHeader_inmem
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
``` 

**適用対象:** [!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/ssSQL15-md.md)] 以降の SQL Server

  CASE 式は、ネイティブ コンパイル T-SQL モジュールでサポートされて*いません*。 次のサンプルは、ネイティブ コンパイル ストアド プロシージャに CASE 式の機能を実装する方法を示しています。  
  
 コード サンプルでは、テーブル変数を使用して、単一の結果セットを作成します。 この方法は、データ行の追加コピーを作成する必要があるため、限られた行数を処理する場合にのみ推奨されます。  
  
 この方法のパフォーマンスをテストする必要があります。  
  
```  
-- original query  
SELECT   
   SalesOrderID,   
   CASE (OnlineOrderFlag)   
   WHEN 1 THEN N'Order placed online by customer'  
   ELSE N'Order placed by sales person'  
   END  
FROM Sales.SalesOrderHeader_inmem  
  
--  workaround for CASE in natively compiled stored procedures  
--  use a table for the single resultset  
CREATE TYPE dbo.SOHOnlineOrderResult AS TABLE  
(  
   SalesOrderID uniqueidentifier not null index ix_SalesOrderID,  
     OrderFlag nvarchar(100) not null  
) with (memory_optimized=on)  
go  
  
-- natively compiled stored procedure that includes the query  
CREATE PROCEDURE dbo.usp_SOHOnlineOrderResult  
   WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
   AS BEGIN ATOMIC WITH  
      (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE=N'us_english')  
  
   -- table variable for creating the single resultset  
   DECLARE @result dbo.SOHOnlineOrderResult  
  
   -- CASE OnlineOrderFlag=1  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed online by customer'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag=1  
  
   -- ELSE  
   INSERT @result   
   SELECT SalesOrderID, N'Order placed by sales person'  
      FROM Sales.SalesOrderHeader_inmem  
      WHERE OnlineOrderFlag!=1  
  
   -- return single resultset  
   SELECT SalesOrderID, OrderFlag FROM @result  
END  
GO  
  
EXEC dbo.usp_SOHOnlineOrderResult  
GO  
```  
  
## <a name="see-also"></a>参照  
 [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)   
 [インメモリ OLTP でサポートされていない Transact-SQL の構造](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)  
  
  
