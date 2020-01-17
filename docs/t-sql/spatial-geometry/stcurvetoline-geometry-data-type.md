---
title: STCurveToLine (geometry データベース型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- STCurveToLine method (geometry)
ms.assetid: abc80b32-4152-4e10-b816-798b901e0ac5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5bc1bdb1ece65113422af1e9a8ebe09de0db1fa1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930308"
---
# <a name="stcurvetoline-geometry-data-type"></a>STCurveToLine (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

円弧を含む **geometry** インスタンスの多角形近似を返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STCurveToLine ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 空の **geometry** インスタンス変数に空の **GeometryCollection** インスタンスを返し、初期化されていない **geometry** 変数に **NULL** を返します。  
  
 メソッドによって返される多角形近似は、メソッドの呼び出しに使用した **geometry** インスタンスによって変わります。  
  
-   **CircularString** または **CompoundCurve** インスタンスに対して **LineString** インスタンスを返します。  
  
-   **CurvePolygon** インスタンスに対して **Polygon** インスタンスを返します。  
  
-   そのインスタンスが **CircularString**、**CompoundCurve**、**CurvePolygon** インスタンスではない場合、**geometry** インスタンスのコピーを返します。 たとえば、**Point** インスタンスである **geometry** インスタンスに対しては、`STCurveToLine` メソッドは **Point** インスタンスを返します。  
  
 SQL/MM 仕様とは異なり、`STCurveToLine` メソッドでは、多角形近似の計算に z 座標の値が使用されません。 このメソッドでは、呼び出し元 **geography** インスタンスに存在する z 座標値は無視されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-an-uninitialized-geometry-variable-and-empty-instance"></a>A. 初期化されていないジオメトリ変数と空のインスタンスを使用する  
 次の例では、最初の **SELECT** ステートメントで初期化されていない **geometry** インスタンスを使用して `STCurveToLine` メソッドを呼び出し、2 つ目の **SELECT** ステートメントで空の **geometry** インスタンスを使用します。 したがって、最初のステートメントには **NULL** が返され、2 つ目のステートメントには **GeometryCollection** コレクションが返されます。  
  
```
 DECLARE @g geometry; 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType(); 
 SET @g = geometry::Parse('LINESTRING EMPTY'); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="b-using-a-linestring-instance"></a>B. LineString インスタンスを使用する  
 次の例の **SELECT** ステートメントでは、**LineString** インスタンスを使用して STCurveToLine メソッドを呼び出します。 したがって、**LineString** インスタンスが返されます。  
  
```
 DECLARE @g geometry; 
 SET @g = geometry::Parse('LINESTRING(1 3, 5 5, 4 3, 1 3)'); 
 SET @g = @g.STCurveToLine(); 
 SELECT @g.STGeometryType();
 ```  
  
### <a name="c-using-a-circularstring-instance"></a>C. CircularString インスタンスを使用する  
 次の例の最初の **SELECT** ステートメントでは、**CircularString** インスタンスを使用して STCurveToLine メソッドを呼び出します。 したがって、**LineString** インスタンスが返されます。 この **SELECT** ステートメントでは、ほとんど同じ 2 つのインスタンスの長さの比較も行います。  さらに、2 つ目の **SELECT** ステートメントは、各インスタンスのポイントの数を返します。  **CircularString** インスタンスについては 5 個だけポイントが返され、**LineString** インスタンスについては 65 個のポイントが返されます。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0)'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type], @g1.STLength() AS [G1 Perimeter], @g2.STLength() AS [G2 Perimeter], @g2.ToString() AS [G2 Def]; 
 SELECT @g1.STNumPoints(), @g2.STNumPoints();
 ```  
  
### <a name="d-using-a-curvepolygon-instance"></a>D. CurvePolygon インスタンスを使用する  
 次の例の **SELECT** ステートメントでは、**CurvePolygon** インスタンスを使用して STCurveToLine メソッドを呼び出します。 したがって、このメソッドでは **Polygon** インスタンスが返されます。  
  
```
 DECLARE @g1 geometry, @g2 geometry; 
 SET @g1 = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(10 0, 0 10, -10 0, 0 -10, 10 0))'); 
 SET @g2 = @g1.STCurveToLine(); 
 SELECT @g1.STGeometryType() AS [G1 Type], @g2.STGeometryType() AS [G2 Type];
 ```  
  
## <a name="see-also"></a>参照  
 [空間データ型の概要](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [STLength &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STNumPoints &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STGeometryType &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)  
  
  

