---
title: GeometryCollection | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- GeomCollection geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 4445c0d9-a66b-4d7c-88e4-a66fa6f7d9fd
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 5aceabe5a263cfa53572be6f818ddc905f9742a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014228"
---
# <a name="geometrycollection"></a>GeometryCollection
  `GeometryCollection` は、0 個以上の `geometry` インスタンスまたは `geography` インスタンスのコレクションです。 `GeometryCollection` は空にできます。  
  
## <a name="geometrycollection-instances"></a>GeometryCollection インスタンス  
  
### <a name="accepted-instances"></a>許容されるインスタンス  
 `GeometryCollection` インスタンスが許容されるためには、空の `GeometryCollection` インスタンスであるか、`GeometryCollection` インスタンスを構成するすべてのインスタンスが許容されるインスタンスである必要があります。 次の例に、許容されるインスタンスを示します。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
 次の例では、`LinesString` インスタンス内の `GeometryCollection` インスタンスが許容されないため、`System.FormatException` がスローされます。  
  
```  
DECLARE @g geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1), POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
```  
  
### <a name="valid-instances"></a>有効なインスタンス  
 `GeometryCollection` インスタンスを構成するすべてのインスタンスが有効である場合、`GeometryCollection` インスタンスは有効です。 次の例に、3 つの有効な `GeometryCollection` インスタンスと 1 つの無効な インスタンスを示します。  
  
```  
DECLARE @g1 geometry = 'GEOMETRYCOLLECTION EMPTY';  
DECLARE @g2 geometry = 'GEOMETRYCOLLECTION(LINESTRING EMPTY,POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g3 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, -1 -5, -5 -5, -5 -1, -1 -1)))';  
DECLARE @g4 geometry = 'GEOMETRYCOLLECTION(LINESTRING(1 1, 3 5),POLYGON((-1 -1, 1 -5, -5 5, -5 -1, -1 -1)))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` は、`Polygon` 内の `GeometryCollection` インスタンスが有効ではないため、有効ではありません。  
  
 受け取られる有効なインスタンスについては、 [Point](point.md)、 [MultiPoint](multipoint.md)、 [LineString](linestring.md)、 [MultiLineString](multilinestring.md)、 [Polygon](polygon.md)、 [MultiPolygon](multipolygon.md)を参照してください。  
  
## <a name="examples"></a>使用例  
 `geometry``GeometryCollection` を、 `Point` インスタンスと `Polygon` インスタンスを含む SRID 1 の Z 値でインスタンス化する例を次に示します。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomCollFromText('GEOMETRYCOLLECTION(POINT(3 3 1), POLYGON((0 0 2, 1 10 3, 1 0 4, 0 0 2)))', 1);  
```  
  
## <a name="see-also"></a>参照  
 [空間データ &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
