---
title: STUnion (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STUnion (geography Data Type)
- STUnion_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STUnion method
ms.assetid: 9bf87691-efd8-4c53-bd2f-eefe0acd19ca
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 34f63ee6609c93dd9435930bfe347a0fa610ce33
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120761"
---
# <a name="stunion-geography-data-type"></a>STUnion (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **geography** インスタンスと別の **geography** インスタンスの和集合を表すオブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STUnion ( other_geography )  
```  
  
## <a name="arguments"></a>引数  
 *other_geography*  
 STUnion() を呼び出したインスタンスとの和集合を形成する、別の **geography** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="exceptions"></a>例外  
 このメソッドは、このインスタンスに対蹠点が含まれている場合、**ArgumentException** をスローします。  
  
## <a name="remarks"></a>Remarks  
 **geography** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、半球より大きい空間インスタンスをサポートしています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サーバー上で返される結果セットが **FullGlobe** インスタンスに拡張されています。  
  
 結果に円弧が含まれるのは、入力インスタンスに円弧が含まれる場合のみです。  
  
 このメソッドは正確ではありません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-computing-the-union-of-two-polygons"></a>A. 2 つの多角形の和集合を計算する  
 `STUnion()` を使用して 2 つの `Polygon` インスタンスの和集合を計算する例を次に示します。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('POLYGON((-122.351 47.656, -122.341 47.656, -122.341 47.661, -122.351 47.661, -122.351 47.656))', 4326);  
SELECT @g.STUnion(@h).ToString();  
```  
  
### <a name="b-producing-a-fullglobe-result"></a>B. FullGlobe の結果を生成する  
 `FullGlobe` で 2 つの `STUnion()` インスタンスを結合するときに、`Polygon` を生成する例を次に示します。  
  
```
 DECLARE @g geography = 'POLYGON ((-122.358 47.653, -122.358 47.658,-122.348 47.658, -122.348 47.649, -122.358 47.653))';  
 DECLARE @h geography = 'POLYGON ((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
### <a name="c-producing-a-triagonal-hole-from-a-union-of-a-curvepolygon-and-a-triagonal-hole"></a>C. CurvePolygon と Polygon の和集合から三角形の穴を生成する。  
 `CurvePolygon` と `Polygon` インスタンスの和集合から三角形の穴を生成する例を次に示します。  
  
```
 DECLARE @g geography = 'POLYGON ((-0.5 0, 0 1, 0.5 0.5, -0.5 0))';  
 DECLARE @h geography = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 0, 0.7 0.7, 0 1), (0 1, 0 0)))';  
 SELECT @g.STUnion(@h).ToString();
 ```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
