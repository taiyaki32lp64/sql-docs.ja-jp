---
title: geometry (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- geometry
dev_langs:
- TSQL
helpviewer_keywords:
- spatial data types [SQL Server]
- geometry data type [SQL Server], Transact-SQL
ms.assetid: 3fefdf7b-f931-404c-821c-82c0375eaf51
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a2b65decea6d737801ef1b0b37e44b0c8ae028af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68101016"
---
# <a name="spatial-types---geometry-transact-sql"></a>空間型 - geometry (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  平面空間データ型の **geometry** は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では共通言語ランタイム (CLR) のデータ型として実装されています。 この型は、ユークリッド (平面) 座標系のデータを表します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**geometry** 空間データ型の一連のメソッドをサポートしています。 このようなメソッドには、Open Geospatial Consortium (OGC) 標準で定義されている **geometry** に関するメソッドやその標準に基づいた [!INCLUDE[msCoName](../../includes/msconame-md.md)] の一連の拡張メソッドがあります。  
 
 geometry メソッドの許容誤差は、1.0e-7 * までです。 エクステントは、**geometry** オブジェクトの地点間の最大近似距離です。
  
## <a name="registering-the-geometry-type"></a>geometry 型の登録  
 **geometry** 型は、各データベースで使用できるように事前に定義されています。 **geometry** 型のテーブル列を作成し、他の CLR 型を使用するときと同じように **geometry** データを操作できます。 保存される計算列と保存されない計算列で使用できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-showing-how-to-add-and-query-geometry-data"></a>A. geometry 型のデータの追加方法とクエリ方法を示す  
 次の 2 つの例は、geometry 型のデータの追加方法とクエリ方法を示しています。 最初の例では、ID 列と `geometry` 型の `GeomCol1`列を含むテーブルを作成します。 3 番目の列で、 `geometry` 型の列をその Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現で示し、 `STAsText()` メソッドを使用します。 次に 2 つの行が挿入されます。1 つは、 `LineString` の `geometry`インスタンスを含む行で、もう 1 つは `Polygon` インスタンスを含む行です。  
  
```sql 
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeomCol1 geometry,   
    GeomCol2 AS GeomCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
INSERT INTO SpatialTable (GeomCol1)  
VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geometry-instances"></a>B. 2 つの geometry インスタンスが交差する地点を返す  
 2 番目の例では、 `STIntersection()` メソッドを使用して、前の例で挿入した 2 つの `geometry` インスタンスが交差する点を返します。  
  
```sql  
DECLARE @geom1 geometry;  
DECLARE @geom2 geometry;  
DECLARE @result geometry;  
  
SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geom1.STIntersection(@geom2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geometry-in-a-computed-column"></a>C. 計算列で geometry 型を使用する  
 次の例では、**geometry** 型を使用して、保存される計算列を持つテーブルを作成します。  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geometry,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>参照  
  [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
