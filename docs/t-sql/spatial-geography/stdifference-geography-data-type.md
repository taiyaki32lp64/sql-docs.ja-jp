---
title: STDifference (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDifference_TSQL
- STDifference (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDifference (geography Data Type)
ms.assetid: 1cde5054-b91a-41bb-812a-08c9308738af
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7ddc3324099be031fff61c2268094b85e9fab143
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042342"
---
# <a name="stdifference-geography-data-type"></a>STDifference (geography データ型)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  別の **geography** インスタンスの外部にある任意の **geography** インスタンスの地点のセットを表すオブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
.STDifference ( other_geography )  
```  
  
## <a name="arguments"></a>引数  
 *other_geography*  
 STDifference() を呼び出したインスタンスからどの地点を削除するかを示す、別の **geography** インスタンスです。  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 戻り値の型: **geography**  
  
 CLR の戻り値の型:**SqlGeography**  
  
## <a name="exceptions"></a>例外  
 このメソッドは、このインスタンスに対蹠点が含まれている場合、**ArgumentException** をスローします。  
  
## <a name="remarks"></a>Remarks  
 **geography** インスタンスの SRID (spatial reference ID) が一致しない場合、このメソッドは常に null を返します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サーバー上で返される結果セットが **FullGlobe** インスタンスに拡張されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、半球より大きい空間インスタンスをサポートしています。 結果に円弧が含まれるのは、入力インスタンスに円弧が含まれる場合のみです。 このメソッドは正確ではありません。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-computing-the-difference-between-two-geography-instances"></a>A. 2 つの geography インスタンス間の差異を計算する  
 `STDifference()` を使用して 2 つの **geography** インスタンスの差分を計算する例を次に示します。  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SET @h = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STDifference(@h).ToString();  
```  
  
### <a name="b-using-a-fullglobe-with-stdifference"></a>B. STDifference() と共に FullGlobe を使用する  
 `FullGlobe` インスタンスを使用する例を次に示します。 最初の結果は空の `GeometryCollection` で、2 番目の結果は `Polygon` インスタンスです。 `STDifference()` は、`GeometryCollection` インスタンスがパラメーターのときに空の `FullGlobe` を返します。 呼び出し元の `geography` インスタンスのすべての点が、`FullGlobe` インスタンスに含まれています。  
  
```
 DECLARE @g geography = 'POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
 DECLARE @h geography = 'FULLGLOBE';  
 SELECT @g.STDifference(@h).ToString(),  
 @h.STDifference(@g).ToString();
 ```  
  
## <a name="see-also"></a>参照  
 [Geography インスタンスの OGC メソッド](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
