---
title: MultiPolygon | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiPolygon geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 2c5db358-2a16-49d9-aac5-a74e86813932
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: ccb2689b24914a0a953c1b9f7325cd5aa9c75d0d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014120"
---
# <a name="multipolygon"></a>MultiPolygon
  `MultiPolygon` インスタンスは、0 個以上の `Polygon` インスタンスのコレクションです。  
  
## <a name="polygon-instances"></a>Polygon インスタンス  
 次の図は、`MultiPolygon` インスタンスの例です。  
  
 ![geometry MultiPolygon インスタンスの例](../../database-engine/media/multipolygon.gif "geometry MultiPolygon インスタンスの例")  
  
 この図は次のことを示しています。  
  
-   図 1 は、2 つの `Polygon` 要素を持つ `MultiPolygon` インスタンスです。 境界は、2 つの外部リングと 3 つの内部リングによって定義されています。  
  
-   図 2 は、2 つの `MultiPolygon` 要素を持つ `Polygon` インスタンスです。 境界は、2 つの外部リングと 3 つの内部リングによって定義されています。 2 つの `Polygon` 要素は接点で交差しています。  
  
### <a name="accepted-instances"></a>許容されるインスタンス  
 次のいずれかの条件が満たされている場合、`MultiPolygon` インスタンスは許容されます。  
  
-   空の `MultiPolygon` インスタンスである。  
  
-   `MultiPolygon` インスタンスを構成するすべてのインスタンスが、許容される `Polygon` インスタンスである。 詳細については、受け入れられる`Polygon`インスタンスを参照してください[多角形](../spatial/polygon.md)します。  
  
 次の例に示す許容される`MultiPolygon`インスタンス。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
```  
  
 次の例に、 `System.FormatException`をスローする MultiPolygon インスタンスを示します。  
  
```  
DECLARE @g geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3)))';  
```  
  
 MultiPolygon の 2 番目のインスタンスは LineString インスタンスであり、許容される Polygon インスタンスではありません。  
  
### <a name="valid-instances"></a>有効なインスタンス  
 `MultiPolygon` インスタンスは、空の `MultiPolygon` インスタンスであるか、次の条件を満たす場合に有効です。  
  
1.  すべてのインスタンスを構成する、`MultiPolygon`インスタンスが、有効な`Polygon`インスタンス。 有効な`Polygon`インスタンスを参照してください[多角形](../spatial/polygon.md)します。  
  
2.  `Polygon` インスタンスを構成する `MultiPolygon` インスタンスが重なっていない。  
  
 次の例に、2 つの有効な `MultiPolygon` インスタンスと 1 つの無効な `MultiPolygon` インスタンスを示します。  
  
```  
DECLARE @g1 geometry = 'MULTIPOLYGON EMPTY';  
DECLARE @g2 geometry = 'MULTIPOLYGON(((1 1, 1 -1, -1 -1, -1 1, 1 1)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
DECLARE @g3 geometry = 'MULTIPOLYGON(((2 2, 2 -2, -2 -2, -2 2, 2 2)),((1 1, 3 1, 3 3, 1 3, 1 1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
 `@g2` は、2 つの `Polygon` インスタンスが 1 つの接点のみで接しているため有効です。 `@g3` は、2 つの `Polygon` インスタンスの内部が互いに重なっているため無効です。  
  
## <a name="examples"></a>使用例  
 次の例では、 `geometry``MultiPolygon` インスタンスを作成し、2 つ目の構成要素の Well-Known Text (WKT) を返します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON(((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1)), ((9 9, 9 10, 10 9, 9 9)))');  
SELECT @g.STGeometryN(2).STAsText();  
```  
  
 次の例では、空の `MultiPolygon` インスタンスを作成します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTIPOLYGON EMPTY');  
```  
  
## <a name="see-also"></a>参照  
 [Polygon](../spatial/polygon.md)   
 [STArea &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type)   
 [STCentroid &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)   
 [STPointOnSurface &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [空間データ &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
