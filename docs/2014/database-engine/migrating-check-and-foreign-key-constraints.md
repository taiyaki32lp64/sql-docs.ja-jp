---
title: 移行のチェックと外部キー制約 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e0a1a1e4-0062-4872-93c3-cd91b7a43c23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2494ab96cc3b4964c26a1ce17593e9b5aece2e7e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774933"
---
# <a name="migrating-check-and-foreign-key-constraints"></a>CHECK 制約と外部キー制約の移行
  チェックと外部キー制約でサポートされていない[!INCLUDE[hek_2](../includes/hek-2-md.md)]で[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]します。 これらのコンストラクトは、通常は、スキーマ内の論理データの整合性を適用する使用し、アプリケーションの機能の正確性を維持するために重要なことができます。  
  
 チェックなどのテーブルに対する論理的な整合性を確認し、外部キー制約は、トランザクションで追加の処理が必要し、一般的にパフォーマンスを受けやすいアプリケーションを避ける必要があります。 ただし、そのようなチェックがアプリケーションに重要な場合は、存在、2 つの回避策。  
  
## <a name="checking-constraints-after-an-insert-update-or-delete-operation"></a>挿入、更新、または削除操作の後に制約のチェック  
 これは回避策は、オプティミスティック変更の大半が制約に違反していないことを前提に基づきます。 この回避策でデータが変更された最初の制約を評価する前にします。 制約に違反すると場合、検出された場合しますが、変更はロールバックされません。  
  
 この回避策では、データの変更は、制約チェックによってブロックされていないため、パフォーマンスに対する影響を最小限の利点があります。 ただし、1 つまたは複数の制約に違反する変更が発生した場合にその変更をロールバック プロセスには時間がかかる場合があります。  
  
## <a name="enforcing-constraints-before-an-insert-update-or-delete-operation"></a>挿入、更新、または削除操作の前に制約を適用します。  
 この回避策の動作をエミュレートする[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]制約。 データの変更が発生し、チェックが失敗した場合に、トランザクションを終了する前に、制約がチェックされます。 このメソッドは、データの変更のパフォーマンスが低下がによりテーブル内のデータが常に、制約を満たしているようになります。  
  
 論理データの整合性が正確さに重要で、変更、制約に違反する可能性が高い場合は、この回避策を使用します。 ただし、整合性を保証するためにはこれらの規則を含むストアド プロシージャをすべてのデータ変更が発生する必要があります。 アドホック クエリおよびその他のストアド プロシージャによって変更が、これらの制約は適用されませんおよびしたがって可能性がありますに違反してに警告なしでします。  
  
## <a name="sample-code"></a>サンプル コード  
 次のサンプルは、AdventureWorks2012 データベースに基づいています。 具体的には、これらのサンプルは、[Sales] に基づいています。[SalesOrderDetail] テーブル、関連付けられているチェック、および一意のインデックスだけでなく外部キー制約。  
  
 ここで指定したストアド プロシージャでは、埋め込み操作のみです。 ストアド プロシージャを更新および削除操作のような構造を持つ必要があります。  
  
## <a name="table-definition-for-the-workarounds"></a>回避策のテーブルの定義  
 前に、メモリ最適化テーブルへの変換は、[Sales] の定義。[SalesOrderDetail] は次のとおりです。  
  
```sql  
USE [AdventureWorks2012]  
GO  
  
CREATE TABLE [Sales].[SalesOrderDetail]([SalesOrderID] [int] NOT NULL,  
   [SalesOrderDetailID] [int] IDENTITY(1,1) NOT NULL,  
   [CarrierTrackingNumber] [nvarchar](25) NULL,  
   [OrderQty] [smallint] NOT NULL,  
   [ProductID] [int] NOT NULL,  
   [SpecialOfferID] [int] NOT NULL,  
   [UnitPrice] [money] NOT NULL,  
   [UnitPriceDiscount] [money] NOT NULL CONSTRAINT [DF_SalesOrderDetail_UnitPriceDiscount]  DEFAULT ((0.0)),  
   [LineTotal]  AS (isnull(([UnitPrice]*((1.0)-[UnitPriceDiscount]))*[OrderQty],(0.0))),  
   [rowguid] [uniqueidentifier] ROWGUIDCOL  NOT NULL CONSTRAINT [DF_SalesOrderDetail_rowguid]  DEFAULT (newid()),  
   [ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SalesOrderDetail_ModifiedDate]  DEFAULT (getdate()),  
 CONSTRAINT [PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID] PRIMARY KEY CLUSTERED   
(  
   [SalesOrderID] ASC,  
   [SalesOrderDetailID] ASC  
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]  
  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail]  WITH CHECK ADD  CONSTRAINT [FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID] FOREIGN KEY([SalesOrderID])  
REFERENCES [Sales].[SalesOrderHeader] ([SalesOrderID])  
ON DELETE CASCADE  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail] CHECK CONSTRAINT [FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID]  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail]  WITH CHECK ADD  CONSTRAINT [FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID] FOREIGN KEY([SpecialOfferID], [ProductID])  
REFERENCES [Sales].[SpecialOfferProduct] ([SpecialOfferID], [ProductID])  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail] CHECK CONSTRAINT [FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID]  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail]  WITH CHECK ADD  CONSTRAINT [CK_SalesOrderDetail_OrderQty] CHECK  (([OrderQty]>(0)))  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail] CHECK CONSTRAINT [CK_SalesOrderDetail_OrderQty]  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail]  WITH CHECK ADD  CONSTRAINT [CK_SalesOrderDetail_UnitPrice] CHECK  (([UnitPrice]>=(0.00)))  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail] CHECK CONSTRAINT [CK_SalesOrderDetail_UnitPrice]  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail]  WITH CHECK ADD  CONSTRAINT [CK_SalesOrderDetail_UnitPriceDiscount] CHECK  (([UnitPriceDiscount]>=(0.00)))  
GO  
  
ALTER TABLE [Sales].[SalesOrderDetail] CHECK CONSTRAINT [CK_SalesOrderDetail_UnitPriceDiscount]  
GO  
```  
  
 後は、メモリ最適化テーブルへの変換は、[Sales] の定義。[SalesOrderDetail] は次のとおりです。  
  
 その rowguid はなくなりました ROWGUIDCOL ではサポートされていない[!INCLUDE[hek_2](../includes/hek-2-md.md)]します。 列が削除されました。 さらに、LineTotal は計算列と、この記事で取り上げませんためも削除されています。  
  
```sql  
USE [AdventureWorks2012]  
GO  
  
CREATE TABLE [Sales].[SalesOrderDetail]([SalesOrderID] [int] NOT NULL,  
   [SalesOrderDetailID] [int] IDENTITY(1,1) NOT NULL,  
   [CarrierTrackingNumber] [nvarchar](25) NULL,  
   [OrderQty] [smallint] NOT NULL,  
   [ProductID] [int] NOT NULL,  
   [SpecialOfferID] [int] NOT NULL,  
   [UnitPrice] [money] NOT NULL,  
   [UnitPriceDiscount] [money] NOT NULL CONSTRAINT [DF_SalesOrderDetail_UnitPriceDiscount]  DEFAULT ((0.0)),  
   [ModifiedDate] [datetime] NOT NULL CONSTRAINT [DF_SalesOrderDetail_ModifiedDate]  DEFAULT (getdate()),  
   CONSTRAINT [PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID] PRIMARY KEY NONCLUSTERED   
   (  
      [SalesOrderID] ASC,  
      [SalesOrderDetailID] ASC  
   ),  
   INDEX [AK_SalesOrderDetail_rowguid] NONCLUSTERED HASH ([rowguid]) WITH (BUCKET_COUNT = 1048576),  
   INDEX [IX_SalesOrderDetail_ProductId] NONCLUSTERED ([ProductId] ASC)) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
  
GO  
```  
  
## <a name="checking-constraints-after-an-insert-update-or-delete-operation"></a>挿入、更新、または削除操作の後に制約のチェック  
  
```sql  
USE AdventureWorks2012  
GO  
  
CREATE PROCEDURE Sales.usp_insert_SalesOrderDetails   
   @SalesOrderId int, @CarrierTrackingNumber nvarchar(25) = null, @OrderQty smallint, @ProductId int, @SpecialOfferID int,   
   @UnitPrice money, @UnitPriceDiscount money = 0.00, @ModifiedDate datetime = null  
AS  
BEGIN  
BEGIN TRANSACTION   
   -- handle defaults for the insert.  
   -- This is to make the insert logic less complex. Default constraints on the table should be in sync with this logic.  
   -- Conversely, you can write an INSERT statement for each case where one or more values for the three columns with default constraints are not specified.  
   IF @ModifiedDate = null SET @ModifiedDate = GETDATE()  
  
   -- Insert the row.  
   INSERT INTO Sales.SalesOrderDetail   
      (SalesOrderID, CarrierTrackingNumber, OrderQty, ProductID, SpecialOfferID, UnitPrice, UnitPriceDiscount, ModifiedDate)  
   VALUES   
      (@SalesOrderId, @CarrierTrackingNumber, @OrderQty, @ProductID, @SpecialOfferID, @UnitPrice, @UnitPriceDiscount, , @ModifiedDate)   
  
   -- Now handle constraints  
   DECLARE @violations TABLE   
   (   
      ConstraintName sysname,  
      ViolatedValue1 sql_variant,  
      ViolatedValue2 sql_variant  
   )  
  
   -- FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID  
   IF NOT EXISTS (SELECT soh.SalesOrderId AS [Exists] FROM Sales.SalesOrderHeader soh WHERE soh.SalesOrderID = @SalesOrderId)   
      INSERT INTO @violations (ConstraintName, ViolatedValue1, ViolatedValue2)   
      VALUES (N'FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID', @SalesOrderId, NULL)  
   -- FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID  
   IF NOT EXISTS (SELECT sop.SpecialOfferID, sop.ProductID FROM [Sales].[SpecialOfferProduct] sop WHERE sop.SpecialOfferID = @SpecialOfferID AND sop.ProductID = @ProductId)  
      INSERT INTO @violations (ConstraintName, ViolatedValue1, ViolatedValue2)   
      VALUES (N'FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID', @SpecialOfferId, @ProductId)  
   -- CK_SalesOrderDetail_OrderQty  
   IF NOT @OrderQty > 0   
      INSERT INTO @violations (ConstraintName, ViolatedValue1, ViolatedValue2)   
      VALUES (N'CK_SalesOrderDetail_OrderQty', @OrderQty, NULL)  
   -- CK_SalesOrderDetail_UnitPrice  
   IF NOT @UnitPrice >= 0.00  
      INSERT INTO @violations (ConstraintName, ViolatedValue1, ViolatedValue2)   
      VALUES (N'CK_SalesOrderDetail_UnitPrice', @UnitPrice, NULL)  
   -- CK_SalesOrderDetail_UnitPriceDiscout  
   IF NOT @UnitPriceDiscount >= 0.00  
      INSERT INTO @violations (ConstraintName, ViolatedValue1, ViolatedValue2)   
      VALUES (N'CK_SalesOrderDetail_UnitPriceDiscount', @UnitPriceDiscount, NULL)  
  
   -- Return a rowset containing violated constraints. On an item that doesn't violate anything, should return an empty rowset.  
   SELECT ConstraintName, ViolatedValue1, ViolatedValue2 FROM @violations  
   COMMIT TRANSACTION  
END  
```  
  
## <a name="enforcing-constraints-before-an-insert-update-or-delete-operation"></a>強制の制約を挿入する前に更新または削除操作  
  
```sql  
USE AdventureWorks2012  
GO  
  
CREATE PROCEDURE Sales.usp_insert_SalesOrderDetails   
   @SalesOrderId int, @CarrierTrackingNumber nvarchar(25) = null, @OrderQty smallint, @ProductId int, @SpecialOfferID int,   
   @UnitPrice money, @UnitPriceDiscount money = 0.00, @ModifiedDate datetime = null  
AS  
BEGIN  
BEGIN TRY  
   BEGIN TRANSACTION  
   -- Verify the constraints first.  
   -- FK_SalesOrderDetail_SalesOrderHeader_SalesOrderID  
   IF NOT EXISTS (SELECT soh.SalesOrderId FROM Sales.SalesOrderHeader soh WHERE soh.SalesOrderID = @SalesOrderId)   
      THROW 50547, N'This SalesOrderId does not exist in SalesOrderHeader', 1  
   -- FK_SalesOrderDetail_SpecialOfferProduct_SpecialOfferIDProductID  
   IF NOT EXISTS (SELECT sop.SpecialOfferID, sop.ProductID FROM [Sales].[SpecialOfferProduct] sop WHERE sop.SpecialOfferID = @SpecialOfferID AND sop.ProductID = @ProductId)  
      THROW 50547, N'This combination of SpecialOfferID and ProductID does not exist in SpecialOfferProduct', 1   
   -- CK_SalesOrderDetail_OrderQty  
   IF NOT @OrderQty > 0   
      THROW 50547, N'OrderQty must be greater than zero.', 1  
   -- CK_SalesOrderDetail_UnitPrice  
   IF NOT @UnitPrice >= 0.00  
      THROW 50547, N'UnitPrice cannot be negative.', 1  
   -- CK_SalesOrderDetail_UnitPriceDiscout  
   IF NOT @UnitPriceDiscount >= 0.00  
      THROW 50547, N'UnitPriceDiscount cannot be negative', 1  
  
   -- All verifications have now passed. Proceed to insert.  
  
   -- handle defaults for the insert.  
   -- This is to make the insert logic less complex. Default constraints on the table should be in sync with this logic.  
   -- Conversely, you can write an INSERT statement for each case where one or more values for the three columns with default constraints are not specified.  
  
   IF @ModifiedDate = null SET @ModifiedDate = GETDATE()  
  
   -- Calculate computed columnn and store it.  
   DECLARE @LineTotal numeric(38, 6)  
   SET @LineTotal = (isnull((@UnitPrice * ((1.0) - @UnitPriceDiscount)) * @OrderQty, (0.0)))  
  
   -- Insert the row.  
   INSERT INTO Sales.SalesOrderDetail   
      (SalesOrderID, CarrierTrackingNumber, OrderQty, ProductID, SpecialOfferID, UnitPrice, UnitPriceDiscount, ModifiedDate)  
   VALUES   
      (@SalesOrderId, @CarrierTrackingNumber, @OrderQty, @ProductID, @SpecialOfferID, @UnitPrice, @UnitPriceDiscount, @ModifiedDate)  
   COMMIT TRANSACTION  
END TRY  
BEGIN CATCH  
   IF @@TRANCOUNT > 0  
      ROLLBACK TRANSACTION  
      THROW;  
END CATCH  
END  
```  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
