---
title: STArea (geometry Data Type) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geometry Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea (geometry Data Type)
ms.assetid: a7dd6083-c649-4ac3-885d-1234e0db62f1
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: fcaad3c2fb8337c64612d5ef5532bcbc4ed4b91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100991"
---
# <a name="starea-geometry-data-type"></a>STArea (geometry データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geometry** インスタンスの合計面積を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STArea ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **float**  
  
 CLR の戻り値の型:**SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 **geometry** インスタンスに含まれるすべての図形が 0 次元または 1 次元の図形の場合、`STArea()` は 0 を返します。 **geometry** インスタンスが初期化されていない場合、`STArea()` は **NULL** を返します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-computing-the-area-of-a-polygon-instance"></a>A. Polygon インスタンスの面積を計算する  
 `Polygon``geometry` インスタンスを作成し、ポリゴンの面積を計算する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STArea();  
```  
  
### <a name="b-computing-the-area-of-a-curvepolygon-instance"></a>B. CurvePolygon インスタンスの面積を計算する  
 `CurvePolygon` インスタンスの面積を計算する例を次に示します。  
  
```
 DECLARE @g geometry;  
 SET @g = geometry::Parse('CURVEPOLYGON(CIRCULARSTRING(0 2, 2 0, 4 2, 4 2, 0 2))');  
 SELECT @g.STArea() AS Area;
 ```  
  
## <a name="see-also"></a>参照  
 [Geometry インスタンスの OGC メソッド](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  
