---
title: LineString | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 57abfdd5679e4ab68f83959f44fce143056c2c7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048657"
---
# <a name="linestring"></a>LineString
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **LineString** は、一連の点と、それらを結ぶ線分を表す 1 次元のオブジェクトです。  
  
## <a name="linestring-instances"></a>LineString インスタンス  
 次の図は、 **LineString** インスタンスの例です。  
  
 ![geometry LineString インスタンスの例](../../relational-databases/spatial/media/linestring.gif "geometry LineString インスタンスの例")  
  
この図は次のことを示しています。  
  
-   図 1 は、単純な閉じていない **LineString** インスタンスです。  
  
-   図 2 は、単純でない、閉じていない **LineString** インスタンスです。  
  
-   図 3 は、閉じている単純な **LineString** インスタンスです。したがって、このインスタンスはリングです。  
  
-   図 4 は、閉じている単純でない **LineString** インスタンスです。したがって、このインスタンスはリングではありません。  
  
### <a name="accepted-instances"></a>許容されるインスタンス  
許容される **LineString** インスタンスはジオメトリ変数に入力できますが、これらが有効な **LineString** インスタンスであるとは限りません。 **LineString** インスタンスが許容されるには、次の条件を満たす必要があります。 インスタンスは、2 つ以上の異なる点から構成されているか、または空である必要があります。 次に示す LineString instances インスタンスは許容されます。  
  
```sql  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
`@g3` の場合、 **LineString** インスタンスは許容されますが、有効ではありません。  
  
次に示す **LineString** インスタンスは許容されません。 `System.FormatException`がスローされます。  
  
```sql  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>有効なインスタンス  
**LineString** インスタンスを有効にするためには、次の条件を満たす必要があります。  
  
1.  **LineString** インスタンスが許容されていること。  
2.  **LineString** インスタンスが空でない場合は、2 つ以上の異なる点が含まれていること。  
3.  **LineString** インスタンスは、それ自体を 2 つ以上の連続する点の区間に重ねることはできない。  
  
次に示す **LineString** インスタンスは有効です。  
  
```sql  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
次に示す **LineString** インスタンスは無効です。  
  
```sql  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
> **LineString** の重複の検出は浮動小数点計算に基づいて行われますが、この計算は正確ではありません。  
  
## <a name="examples"></a>使用例  
### <a name="example-a"></a>例 A。    
次の例は、3 つの点を持つ `geometry``LineString` インスタンスを作成する方法を示しています。このインスタンスの SRID は 0 です。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
### <a name="example-b"></a>例 B。   
`LineString` インスタンスのそれぞれの点には、Z (昇格) 値と M (メジャー) 値を含めることができます。 次の例では、上の例で作成した `LineString` インスタンスに M 値を追加します。 M および Z は NULL 値にすることができます。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
### <a name="example-c"></a>例 C。   
次の例は、同じ 2 つの点を持つ `geometry LineString` インスタンスを作成する方法を示しています。 `IsValid` 呼び出しは、 **LineString** インスタンスが無効であることを示します。 `MakeValid` 呼び出しは、 **LineString** インスタンスを **Point**に変換します。  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);  
IF @g.STIsValid() = 1  
  BEGIN  
     SELECT @g.ToString() + ' is a valid LineString.';    
  END  
ELSE  
  BEGIN  
     SELECT @g.ToString() + ' is not a valid LineString.';  
     SET @g = @g.MakeValid();  
     SELECT @g.ToString() + ' is a valid Point.';    
  END  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>参照  
 [STLength &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
