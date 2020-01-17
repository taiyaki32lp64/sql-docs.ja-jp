---
title: STUnion (geometry データ型) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUnion (geometry Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion (geometry Data Type)
ms.assetid: 5b168118-137d-402f-9173-fee3f365a89c
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 868b344a18494e4b92cd3ee5944cb80ad15ab845
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066220"
---
# <a name="stunion-geometry-data-type"></a>STUnion (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

ある **geometry** インスタンスと別の **geometry** インスタンスの和集合を表すオブジェクトを返します。
  
## <a name="syntax"></a>構文  
  
```  
  
.STUnion ( other_geometry )  
```  
  
## <a name="arguments"></a>引数  
 *other_geometry*  
 `STUnion()` を呼び出したインスタンスとの和集合を形成する、別の **geometry** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **geometry**  
  
 CLR の戻り値の型:**SqlGeometry**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。 結果に円弧が含まれるのは、入力インスタンスに円弧が含まれる場合のみです。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-computing-the-union-of-two-polygon-instances"></a>A. 2 つの Polygon インスタンスの和集合を計算する  
 `STUnion()` を使用して 2 つの `Polygon` インスタンスの和集合を計算する例を次に示します。  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 0 2, 2 2, 2 0, 0 0))', 0);  
SET @h = geometry::STGeomFromText('POLYGON((1 1, 3 1, 3 3, 1 3, 1 1))', 0);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-computing-the-union-of-a-polygon-instance-with-a-curvepolygon-instance"></a>B. Polygon インスタンスと CurvePolygon インスタンスの和集合を計算する  
 次の例は、円弧が含まれた `GeometryCollection` インスタンスを返します。  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(CIRCULARSTRING(0 -4, 4 0, 0 4, -4 0, 0 -4))';  
 DECLARE @h geometry = 'POLYGON((5 -1, 5 -3, 7 -3, 7 -1, 5 -1))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
 `STUnion()` を呼び出したインスタンスは円弧セグメントを含んでいるため、`STUnion()` は円弧セグメントを含む結果を返します。  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

