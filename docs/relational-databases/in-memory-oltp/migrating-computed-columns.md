---
title: 計算列の移行 | Microsoft Docs
ms.custom: ''
ms.date: 12/17/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 64a9eade-22c3-4a9d-ab50-956219e08df1
author: MightyPen
ms.author: genemi
monikerRange: =sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 36a0a6f82499a617a37b7cc9b848a33ec29c2ce3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68050131"
---
# <a name="migrating-computed-columns"></a>計算列の移行

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

計算列は、メモリ最適化テーブルではサポートされていません。 ただし、計算列をシミュレートすることはできます。

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降、メモリ最適化テーブルとインデックスで計算列がサポートされています。

ディスク ベース テーブルをメモリ最適化テーブルに移行するときは、計算列を保存する必要性を検討してください。 メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャのさまざまなパフォーマンス特性によって、保存の必要性がなくなる場合があります。  
  
## <a name="non-persisted-computed-columns"></a>保存されない計算列  
 保存されない計算列の効果をシミュレートするには、メモリ最適化テーブルのビューを作成します。 ビューを定義する SELECT ステートメントで、計算列の定義をビューに追加します。 ネイティブ コンパイル ストアド プロシージャ内を除き、計算列からの値を使用するクエリは、このビューから読み取る必要があります。 ネイティブ コンパイル ストアド プロシージャ内では、計算列の定義によって、SELECT、UPDATE、または DELETE ステートメントを更新する必要があります。  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is not persisted.  
CREATE VIEW dbo.v_order_details AS  
   SELECT  
      OrderId,  
      ProductId,  
      SalePrice,  
      Quantity,  
      Quantity * SalePrice AS Total  
   FROM dbo.order_details  
```  
  
## <a name="persisted-computed-columns"></a>保存される計算列  
 保存される計算列の効果をシミュレートするには、テーブルに挿入するためのストアド プロシージャとテーブルを更新するためのストアド プロシージャを作成します。 テーブルに対する挿入または更新を行う場合、これらのストアド プロシージャを呼び出してそれぞれのタスクを実行します。 ストアド プロシージャ内では、元のディスク ベース テーブルでの計算列の定義のように、入力に従って算定フィールドの値を計算します。 次に、ストアド プロシージャ内では必要に応じて、テーブルに対する挿入を更新を実行します。  
  
```sql  
-- Schema for the table dbo.OrderDetails:  
-- OrderId int not null primary key,  
-- ProductId int not null,  
-- SalePrice money not null,  
-- Quantity int not null,  
-- Total money not null  
--  
-- Total is computed as SalePrice * Quantity and is persisted.  
-- we need to create insert and update procedures to calculate Total.  

CREATE PROCEDURE sp_insert_order_details   
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  
-- for bulk inserts, accept a table-valued parameter into the stored procedure  
-- and use an INSERT INTO SELECT statement.  

DECLARE @total money = @SalePrice * @Quantity  
INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
@OrderId int, @ProductId int, @SalePrice money, @Quantity int  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (LANGUAGE = N'english', TRANSACTION ISOLATION LEVEL = SNAPSHOT)  

-- compute the value here.   
-- this stored procedure works with single rows only.  

DECLARE @total money = @SalePrice * @Quantity  
UPDATE dbo.OrderDetails   
SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
WHERE OrderId = @OrderId  
END  
GO  
```  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
