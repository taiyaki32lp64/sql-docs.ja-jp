---
title: ネイティブコンパイルストアドプロシージャでの OR 演算子の実装 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2528e74-2b1c-48cb-861b-c4e57b51ac35
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 02b55465cc4aed912e6e955883ca8fdbfa4be870
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228209"
---
# <a name="implementing-the-or-operator-in-natively-compiled-stored-procedures"></a>ネイティブ コンパイル ストアド プロシージャでの OR 演算子の実装
  ネイティブ コンパイル ストアド プロシージャ内のクエリ述語では、OR 演算子はサポートされません。 ネイティブ コンパイル ストアド プロシージャ内のクエリ述語では NOT 演算子もサポートされていないため、同等の論理演算子を単独で使用しても、OR 演算子の効果をシミュレートすることはできません。 ただし、OR 演算子の効果は、メモリ最適化テーブル変数を使用してシミュレートすることができます。  
  
## <a name="or-operator-in-where-clause"></a>WHERE 句での OR 演算子  
 WHERE 句に OR 演算子が含まれている場合は、次の方法で動作をシミュレートすることができます。  
  
1.  適切なスキーマを使用して、メモリ最適化テーブル変数を作成します。 これには、定義済みのメモリ最適化テーブル型が必要になります。  
  
2.  OR 演算子によって結合されている述語に従って WHERE 句を 2 つに分割します (最上位レベルの OR 演算子からこの手順を行います)。 WHERE 句に複数の OR 演算子が含まれている場合は、この手順を複数回行う必要があります。 最後の OR 演算子まで、この手順を繰り返します。 たとえば、次のような述語があるとします。  
  
    ```  
    pred1 OR (pred2 AND (pred3 OR pred4)) OR (pred5 AND pred6)  
    ```  
  
     この手順を行うと、次のような述語に分割されます。  
  
    ```  
    pred1  
    pred5 AND pred6  
    pred2 AND pred3  
    pred2 AND pred4  
    ```  
  
3.  手順 2. で分割された 2 つの部分で構成される各ペアを述語としてを使用しクエリを実行します。 手順 1. で作成したメモリ最適化テーブル変数に各クエリの結果を挿入します。  
  
4.  必要に応じて、メモリ最適化テーブル変数から重複する結果を削除します。  
  
5.  メモリ最適化テーブル変数の内容をクエリの結果として使用します。  
  
 次の例では、[!INCLUDE[hek_2](../includes/hek-2-md.md)] 用に更新された AdventureWorks2012 データベースのテーブルを使用します。 このサンプルのファイルをダウンロードするには、 [AdventureWorks Databases-2012、2008R2、および 2008](https://msftdbprodsamples.codeplex.com/releases/view/93587)に移動します。 AdventureWorks2012 に[!INCLUDE[hek_2](../includes/hek-2-md.md)]コードサンプルを適用するには、 [SQL Server 2014 のインメモリ OLTP サンプル](https://msftdbprodsamples.codeplex.com/releases/view/114491)にアクセスします。  
  
 データベースに、次のストアド プロシージャを追加します。 ここでは、ネイティブ コンパイルを使用するように、このストアド プロシージャを変換します。  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_ondisk  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
AS BEGIN  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  WHERE  s.SalesOrderId = @SalesOrderId  
      OR s.SalesOrderDetailId = @SalesOrderDetailId  
      OR s.CarrierTrackingNumber = @CarrierTrackingNumber  
      OR s.ProductID = @ProductId  
      OR (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
END  
GO  
```  
  
 変換後のテーブルとストアド プロシージャのスキーマは、次のようになります。  
  
```  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesOrderDetailType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesOrderDetailTempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  recordcount int not null  
  INDEX ix_fuzzySearchSalesOrderDetailTempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesOrderDetail_inmem  
  @SalesOrderId int = 0, @SalesOrderDetailId int = 0,   
  @CarrierTrackingNumber nvarchar(25) = N'', @ProductId int = 0,   
  @minUnitPrice money = 0, @maxUnitPrice money = 0  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.fuzzySearchSalesOrderDetailType  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderId = @SalesOrderId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.SalesOrderDetailId = @SalesOrderDetailId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.CarrierTrackingNumber COLLATE Latin1_General_BIN2 = @CarrierTrackingNumber COLLATE Latin1_General_BIN2   
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE s.ProductID = @ProductId  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, ModifiedDate)  
  SELECT SalesOrderId, SalesOrderDetailId, ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  WHERE (s.UnitPrice > @minUnitPrice AND s.UnitPrice < @maxUnitPrice)  
  
  -- After the above statements, there will be duplicates inside @retValue  
  -- Delete the duplicates from @retValue  
  DECLARE @duplicates Sales.fuzzySearchSalesOrderDetailTempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, recordcount)   
  SELECT SalesOrderId, SalesOrderDetailId, COUNT(*) AS recordCount  
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId  
  
  -- Now we have one row per pair  
  -- clear and rebuild the result set  
  DELETE FROM @retValue  
  
  INSERT INTO @retValue  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates d ON s.SalesOrderId = d.SalesOrderId AND s.SalesOrderDetailId = d.SalesOrderDetailId  
  
  -- After this every pair of (SalesOrderId, SalesOrderDetailId) in @retValue should be unique.  
  SELECT SalesorderId, SalesOrderDetailId, ModifiedDate FROM @retValue  
END  
GO  
```  
  
## <a name="or-operator-in-join-condition"></a>結合 (JOIN) 条件での OR 演算子  
 SELECT ステートメントの JOIN 条件に OR 演算子が含まれている場合は、次の方法で動作をシミュレートすることができます。 JOIN 条件に複数の OR 演算子が含まれている場合、または OR 演算子を使用した JOIN 条件が複数ある場合は、この手順を複数回行う必要があります。  
  
 OUTER JOIN 条件がある場合は、ここで示す回避策と OUTER JOIN 条件用の回避策を組み合わせることができます。  
  
1.  適切なスキーマを使用して、メモリ最適化テーブル変数を作成します。 これには、定義済みのメモリ最適化テーブル型が必要になります。  
  
2.  OR 演算子によって結合されている述語に従って、JOIN 条件内の述語を 2 つに分割します。 複数の JOIN 条件がある場合は、各 JOIN 条件に対してこの手順を行い、結果のフラグメントの組み合わせを作成することが必要になる場合があります。 たとえば、3 つの JOIN 条件があり、各 JOIN 条件には 1 つの OR 演算子が含まれている場合は、8 個 (2x2x2) の述語を作成できます。  
  
3.  手順 2. で作成された各述語に対して、手順 1. で作成したメモリ最適化テーブル変数に結果を挿入するクエリを作成します。  
  
4.  必要に応じて、メモリ最適化テーブル変数から重複する結果を削除します。  
  
5.  メモリ最適化テーブル変数の内容をクエリの結果として使用します。  
  
 次の例では、[!INCLUDE[hek_2](../includes/hek-2-md.md)] 用に更新された AdventureWorks2012 データベースのテーブルを使用します。 このサンプルのファイルをダウンロードするには、 [AdventureWorks Databases-2012、2008R2、および 2008](https://msftdbprodsamples.codeplex.com/releases/view/93587)に移動します。 AdventureWorks2012 に[!INCLUDE[hek_2](../includes/hek-2-md.md)]コードサンプルを適用するには、 [SQL Server 2014 のインメモリ OLTP サンプル](https://msftdbprodsamples.codeplex.com/releases/view/114491)にアクセスします。  
  
 データベースに、次のストアド プロシージャを追加します。 ここでは、ネイティブ コンパイルを使用するように、このストアド プロシージャを変換します。 この例では、INNER JOIN 条件を使用します。  
  
```  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_ondisk  
  @SpecialOfferId int  
AS BEGIN  
  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_ondisk s  
  JOIN Sales.SpecialOffer_onDisk offer   
    ON s.SpecialOfferID = offer.SpecialOfferID   
    OR s.ProductID IN (SELECT ProductId FROM Sales.SpecialOfferProduct sop WHERE sop.SpecialOfferID = @SpecialOfferId)  
END  
```  
  
 変換後のテーブルとストアド プロシージャのスキーマは、次のようになります。  
  
```  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_Type AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  ModifiedDate datetime2(7) not null  
  INDEX ix_fuzzySearchSalesSpecialOffers_Type NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE TYPE Sales.fuzzySearchSalesSpecialOffers_TempType AS TABLE  
(  
  SalesOrderId int not null,  
  SalesOrderDetailId int not null,  
  SpecialOfferId int not null,  
  recordcount int null  
  INDEX ix_fuzzySearchSalesSpecialOffers_TempType NONCLUSTERED (SalesOrderId, SalesOrderDetailId)  
) WITH (MEMORY_OPTIMIZED = ON)  
GO  
  
CREATE PROCEDURE Sales.usp_fuzzySearchSalesSpecialOffers_inmem  
  @SpecialOfferId int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'ENGLISH')  
  
  DECLARE @retValue Sales.FuzzySearchSalesSpecialOffers_Type  
  
  -- Find all special offers matching the conditions  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOffer_inmem offer   
    ON s.SpecialOfferID = offer.SpecialOfferID  
  
  INSERT INTO @retValue (SalesOrderId, SalesOrderDetailId, SpecialOfferid, ModifiedDate)  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN Sales.SpecialOfferProduct_inmem sop   
    ON sop.SpecialOfferId = @SpecialOfferId AND s.ProductID = sop.ProductId  
  
  -- Now we need to remove the duplicates from @matchingSpecialOffers  
  DECLARE @duplicates Sales.fuzzySearchSalesSpecialOffers_TempType  
  
  INSERT INTO @duplicates (SalesOrderId, SalesOrderDetailId, SpecialOfferid, recordcount)  
  SELECT SalesOrderId, SalesOrderDetailId, SpecialOfferId, COUNT(*)   
  FROM @retValue  
  GROUP BY SalesOrderId, SalesOrderDetailId, SpecialOfferId  
  
  -- now there should be no duplicates within @duplicate  
  -- use @duplicate for join.  
  SELECT s.SalesOrderId, s.SalesOrderDetailId, s.SpecialOfferID, s.ModifiedDate  
  FROM Sales.SalesOrderDetail_inmem s  
  JOIN @duplicates offer   
    ON    s.SalesOrderId = offer.SalesOrderId   
      AND s.SalesOrderDetailId = offer.SalesOrderDetailID   
      AND s.SpecialOfferId = offer.SpecialOfferId  
END  
GO  
```  
  
## <a name="side-effects"></a>副作用  
 WHERE 句や JOIN 条件に複数の OR 演算子が含まれている場合は、動作をシミュレートするために実行する必要があるクエリの数は、指数関数的に増加する可能性があります。 その結果、メモリ最適化テーブル変数の使用が原因で、クエリのパフォーマンスが低下し、メモリの使用量が増加する可能性があります。  
  
## <a name="see-also"></a>参照  
 [ネイティブコンパイルストアドプロシージャの移行に関する問題](../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)  
  
