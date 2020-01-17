---
title: STNumPoints (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STNumPoints (geography Data Type)
- STNumPoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumPoints method
ms.assetid: 25ff7ad1-ba5f-4cfb-816a-59255ac1591d
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 320118e7844dfe40e45be9a893ad7bf45faff8bc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120900"
---
# <a name="stnumpoints-geography-data-type"></a>STNumPoints (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** インスタンス内の各図形に含まれる地点の合計数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STNumPoints ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型:**SqlInt32**  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、**geography** インスタンスの記述に含まれている地点をカウントします。 重複する地点はカウントされます。ただし、セグメント間の接続点は 1 つとしてカウントされます。 対象となるインスタンスがコレクションの場合、このメソッドは、コレクション内の地点の合計数を返します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-retrieving-the-total-number-of-points-in-a-linestring"></a>A. LineString 内の地点の合計数を取得する  
 `LineString` インスタンスを作成し、`STNumPoints()` を使用して、インスタンスの記述で使用されている地点の数を確認する例を次に示します。  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STNumPoints();  
```  
  
### <a name="b-retrieving-the-total-number-of-points-in-a-geometrycollection"></a>B. GeometryCollection 内の地点の合計数を取得する  
 次の例では、`GeometryCollection` 内のすべての要素の地点の合計数を返します。  
  
```  
DECLARE @g geography = 'GEOMETRYCOLLECTION(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)  
    ,CURVEPOLYGON(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)))';  
SELECT @g.STNumPoints();  
```  
  
### <a name="c-returning-the-number-of-points-in-a-compoundcurve"></a>C. CompoundCurve 内の地点の数を返す  
 次の例では、CompoundCurve インスタンスに含まれる地点の数を返します。 STNumPoints() はセグメント間の接続点を 1 つとしてカウントするため、このクエリは 6 ではなく 5 を返します。  
  
```
 DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658),( -122.348 47.658, -121.56 48.12, -122.358 47.653))'  
 SELECT @g.STNumPoints();
 ```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
