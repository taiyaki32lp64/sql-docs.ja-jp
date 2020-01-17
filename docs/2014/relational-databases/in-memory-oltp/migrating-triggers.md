---
title: トリガーの移行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7df393f26523991abafded74ded242390cb0e3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63071470"
---
# <a name="migrating-triggers"></a>トリガーの移行
  このトピックでは、DDL トリガーと DML トリガー、およびメモリ最適化テーブルについて説明します。  
  
 LOGON トリガーとは、LOGON イベントで起動するように定義されたトリガーです。 LOGON トリガーは、メモリ最適化テーブルに影響しません。  
  
## <a name="ddl-triggers"></a>DDL トリガー  
 DDL トリガーとは、自らを定義しているデータベースまたはサーバーに対して CREATE、ALTER、DROP、GRANT、DENY、REVOKE、または UPDATE STATISTICS の各ステートメントを実行したときに起動するように定義されているトリガーです。  
  
 データベースまたはサーバーで、CREATE_TABLE イベントまたはこのイベントを含むイベント グループに対応する 1 つ以上の DDL トリガーが定義されている場合は、メモリ最適化テーブルを作成できません。 データベースまたはサーバーで、DROP_TABLE イベントまたはこのイベントを含むイベント グループに対応する 1 つ以上の DDL トリガーが定義されている場合は、メモリ最適化テーブルを削除できません。  
  
 CREATE_PROCEDURE、DROP_PROCEDURE、またはこれらのイベントを含むイベント グループに対応する 1 つ以上の DDL トリガーが存在している場合は、ネイティブ コンパイル ストアド プロシージャを作成できません。  
  
## <a name="dml-triggers"></a>DML トリガー  
 メモリ最適化テーブルで DML トリガーを定義することはできません。 ただし、ストアド プロシージャを明示的に使用してデータの挿入、更新、または削除を実行する場合は、インメモリ OLTP により、DML トリガーと同様の効果を達成できます。 システムにアドホック クエリが含まれている場合は、DML トリガーの結果をシミュレートする代わりに、これらのストアド プロシージャを使用してクエリを変換します。  
  
 トリガー イベント (FOR/AFTER または INSTEAD OF) によっては、テーブルに対して INSERT、UPDATE、DELETE を実行する適切なストアド プロシージャをトリガーする内容を含めることもできます。 たとえば、AFTER INSERT トリガーを移行する場合は、適切な INSERT ステートメントの後にトリガーの内容を含めることによって、挿入操作を実行するストアド プロシージャを変更することができます。  
  
 インタープリターによって処理されるストアド プロシージャ、またはネイティブ コンパイル ストアド プロシージャを使用できます。 インタープリターによって処理されるストアド プロシージャを使用する [!INCLUDE[tsql](../../includes/tsql-md.md)] 構造のほとんどは、メモリ最適化されたテーブルに対して実行できます。 ただし、ネイティブ コンパイル ストアド プロシージャでは、[!INCLUDE[tsql](../../includes/tsql-md.md)] 構造のサブセットのみをサポートしています。 について[!INCLUDE[tsql](../../includes/tsql-md.md)]メモリ最適化テーブルでサポートを参照してください[したテーブルを使用して解釈された TRANSACT-SQL](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)します。 について[!INCLUDE[tsql](../../includes/tsql-md.md)]ネイティブ コンパイル ストアド プロシージャでサポートを参照してください[TRANSACT-SQL は、インメモリ OLTP でサポートされていない構造](transact-sql-constructs-not-supported-by-in-memory-oltp.md)します。  
  
 次に、メモリ最適化テーブルに対する DML トリガーの動作をシミュレートする簡単な例を示します。  
  
 このデータベースには、CREATE TABLE、CREATE TRIGGER、および CREATE PROCEDURE の各ステートメントを使用してスクリプト化した次のオブジェクトが含まれています。  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null primary key,  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
)  
GO  
  
CREATE TRIGGER tr_order_details_insteadof_insert  
ON OrderDetails  
INSTEAD OF INSERT AS  
BEGIN  
   DECLARE @pid int, @qty_buy int, @qty_remain int  
   SELECT @pid = ProductId, @qty_buy = Quantity FROM inserted  
   SELECT @qty_remain = Quantity FROM Inventory WHERE ProductId = @pid  
   IF (@qty_remain <= @qty_buy)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      SELECT OrderId, ProductId, SalePrice, Quantity, Total FROM inserted  
      UPDATE Inventory SET Quantity = Quantity - @qty_buy WHERE ProductId = @pid  
   END  
END  
GO  
  
CREATE TRIGGER tr_order_details_after_update  
ON OrderDetails  
AFTER UPDATE AS  
BEGIN  
   INSERT INTO UpdateNotifications (OrderId, UpdateTime) SELECT OrderId, GETDATE() FROM inserted     
END  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
AS BEGIN  
   INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
   VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
AS BEGIN  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
END  
GO  
```  
  
 次の各オブジェクトは、移行前の状態と機能的に等価です。  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 1048576),  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE Inventory  
(  
   ProductId int not null PRIMARY KEY NONCLUSTERED,  
   Quantity int not null  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE UpdateNotifications  
(  
   OrderId int not null,  
   UpdateTime datetime2 not null  
   CONSTRAINT pk_updateNotifications PRIMARY KEY NONCLUSTERED (OrderId, UpdateTime)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   DECLARE @qty_remain int  
   SELECT @qty_remain = Quantity FROM dbo.Inventory WHERE ProductId = @ProductId  
   IF (@qty_remain <= @Quantity)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
      UPDATE dbo.Inventory SET Quantity = Quantity - @Quantity WHERE ProductId = @ProductId  
   END  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
   INSERT INTO dbo.UpdateNotifications (OrderId, UpdateTime) VALUES (@OrderId, GETDATE())  
END  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [インメモリ OLTP への移行](migrating-to-in-memory-oltp.md)  
  
  
