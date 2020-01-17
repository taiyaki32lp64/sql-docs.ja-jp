---
title: MultiLineString | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- MultiLineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: 95deeefe-d6c5-4a11-b347-379e4486e7b7
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 9244f32b2ee9921d1caaa63b5d6aae9c324049ff
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014208"
---
# <a name="multilinestring"></a>MultiLineString
  A `MultiLineString` 0 個以上のコレクションである`geometry`または**geographyLineString**インスタンス。  
  
## <a name="multilinestring-instances"></a>MultiLineString インスタンス  
 次の図は、`MultiLineString` インスタンスの例です。  
  
 ![geometry MultiLineString インスタンスの例](../../database-engine/media/multilinestring.gif "geometry MultiLineString インスタンスの例")  
  
 この図は次のことを示しています。  
  
-   図 1 は、単純な`MultiLineString`インスタンスの境界を持つ、2 つの 4 つのエンドポイントは、`LineString`要素。  
  
-   図 2 の `MultiLineString` インスタンスは、`LineString` 要素の終点のみで交差しているため単純です。 このインスタンスの境界は、重なっていない 2 つの終点です。  
  
-   図 3 の `MultiLineString` インスタンスは、一方の `LineString` 要素の内部で交差しているため単純ではありません。 この `MultiLineString` インスタンスの境界は 4 つの終点です。  
  
-   図 4 は、単純でなく、閉じていない `MultiLineString` インスタンスです。  
  
-   図 5 は、単純な閉じていない `MultiLineString` です。 それが閉じていないため、その`LineStrings`要素が閉じられていません。 このインスタンスが単純なのは、内部で交差している `LineStrings` インスタンスがないからです。  
  
-   図 6 は、単純な閉じている `MultiLineString` インスタンスです。 このインスタンスが閉じているのは、そのすべての要素が閉じているからです。 このインスタンスが単純なのは、内部で交差している要素がないからです。  
  
### <a name="accepted-instances"></a>許容されるインスタンス  
 MultiLineString`MultiLineString` インスタンスが許容されるためには、空であるか、許容される `LineString` インスタンスのみで構成されている必要があります。 詳細については、受け入れられる`LineString`インスタンスを参照してください[LineString](../spatial/linestring.md)します。 次の例に、許容される `MultiLineString` インスタンスを示します。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
```  
  
 次の例では、2 番目の `LineString` インスタンスが有効ではないため、`System.FormatException` がスローされます。  
  
```  
DECLARE @g geometry = 'MULTILINESTRING((1 1, 3 5),(-5 3))';  
```  
  
### <a name="valid-instances"></a>有効なインスタンス  
 `MultiLineString`インスタンスを有効に、次の条件を満たす必要があります。  
  
1.  `MultiLineString` インスタンスを構成するすべてのインスタンスが、有効な `LineString` インスタンスである。  
  
2.  `LineString` インスタンスを構成する 2 つの `MultiLineString` インスタンスが内部で互いに重ならない。 `LineString` インスタンスは、有限数の接点のみで、互いにまたは他の `LineString` インスタンスと交差するか接することができます。  
  
 次の例に、3 つの有効な `MultiLineString` インスタンスと 1 つの無効な `MultiLineString` インスタンスを示します。  
  
```  
DECLARE @g1 geometry = 'MULTILINESTRING EMPTY';  
DECLARE @g2 geometry = 'MULTILINESTRING((1 1, 3 5), (-5 3, -8 -2))';  
DECLARE @g3 geometry = 'MULTILINESTRING((1 1, 5 5), (1 3, 3 1))';  
DECLARE @g4 geometry = 'MULTILINESTRING((1 1, 3 3, 5 5),(3 3, 5 5, 7 7))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
```  
  
 `@g4` は、2 番目の `LineString` インスタンスが最初の `LineString` インスタンスと内部で重なっているため、有効ではありません。 有限数の接点で接しています。  
  
## <a name="examples"></a>使用例  
 次の例では、2 つの `geometry``MultiLineString` 要素を含む SRID 0 の単純な `LineString` インスタンスを作成しています。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
```  
  
 このインスタンスを別の SRID で作成するには、 `STGeomFromText()` または `STMLineStringFromText()`を使用します。 次の例のように、 `Parse()` を使用して、その後に SRID を変更することもできます。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 2, 1 1), (1 0, 1 1))');  
SET @g.STSrid = 13;  
```  
  
## <a name="see-also"></a>参照  
 [STLength &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STIsClosed &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [MultiLineString](../spatial/linestring.md)   
 [空間データ &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
