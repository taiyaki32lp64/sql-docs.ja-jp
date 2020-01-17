---
title: STSymDifference (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSymDifference_TSQL
- STSymDifference (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STSymDifference (geometry Data Type)
ms.assetid: 1d4cf35a-ca89-4aa4-ae30-e61a0ff18b53
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: ea26c364621910d6dd5148a5753bd6709d3e0f07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066285"
---
# <a name="stsymdifference-geometry-data-type"></a>STSymDifference (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  任意の **geometry** インスタンスと別の **geometry** インスタンスのいずれかに存在する地点すべてを表すオブジェクトを返します。つまり、両方のインスタンスに存在する地点は除外されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STSymDifference ( other_geometry )  
```  
  
## <a name="arguments"></a>引数  
 *other_geometry*  
 `STSymDistance()` を呼び出したインスタンスの対象となる、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。 結果に円弧が含まれるのは、入力インスタンスに円弧が含まれる場合のみです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-computing-the-symmetric-difference-of-two-polygon-instances"></a>A. 2 つの Polygon インスタンスの対称差を計算する  
 次の例では、`STSymDifference()` を使用して 2 つの `Polygon` インスタンスの対称差を計算します。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STSymDifference(@h).ToString();  
```  
  
### <a name="b-computing-the-symmetric-difference-between-a-curvepolygon-and-a-polygon-instance"></a>B. CurvePolygon インスタンスと Polygon インスタンスの対称差を計算する  
 次の例は、`GeometryCollection` と `CurvePolygon` の間の対称差を表す `Polygon` を返します。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 5 -1, 5 3, 1 3, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="c-using-stsymdifference-on-curvepolygon-instance-with-an-inscribed-polygon-instance"></a>C. Polygon インスタンスが内接する CurvePolygon インスタンスで STSymDifference() を使用する  
 次の例は、比較対象の 2 つのインスタンスの対称差を表す、内部 `Polygon` リングを含む `CurvePolygon` インスタンスを返します。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON (CIRCULARSTRING (0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON ((1 -1, 2 -1, 2 1, 1 1, 1 -1))';  
 SELECT @h.STSymDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
