---
title: LineString | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- LineString geometry subtype [SQL Server]
- geometry subtypes [SQL Server]
ms.assetid: e50d0b86-8b31-4285-be71-ad05c7712cbd
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 6bc07f8770e6cd7d1fb1e4b4e6e40ca8b1c5256f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014201"
---
# <a name="linestring"></a>LineString
  `LineString` は、一連の点と、それらを結ぶ線分を表す 1 次元のオブジェクトです。  
  
## <a name="linestring-instances"></a>LineString インスタンス  
 次の図は、`LineString` インスタンスの例です。  
  
 ![geometry LineString インスタンスの例](../../database-engine/media/linestring.gif "geometry LineString インスタンスの例")  
  
 この図は次のことを示しています。  
  
-   図 1 は、単純な閉じていない `LineString` インスタンスです。  
  
-   図 2 は、単純でない、閉じていない `LineString` インスタンスです。  
  
-   図 3 は、閉じている単純な `LineString` インスタンスです。したがって、このインスタンスはリングです。  
  
-   図 4 は、閉じている単純でない `LineString` インスタンスです。したがって、このインスタンスはリングではありません。  
  
### <a name="accepted-instances"></a>許容されるインスタンス  
 許容される `LineString` インスタンスはジオメトリ変数に入力できますが、これらが有効な `LineString` インスタンスであるとは限りません。 `LineString` インスタンスが許容されるには、次の条件を満たす必要があります。 インスタンスは、2 つ以上の異なる点から構成されているか、または空である必要があります。 次に示す LineString instances インスタンスは許容されます。  
  
```  
DECLARE @g1 geometry = 'LINESTRING EMPTY';  
DECLARE @g2 geometry = 'LINESTRING(1 1,2 3,4 8, -6 3)';  
DECLARE @g3 geometry = 'LINESTRING(1 1, 1 1)';  
```  
  
 `@g3` の場合、`LineString` インスタンスは許容されますが、有効ではありません。  
  
 次に示す `LineString` インスタンスは許容されません。 `System.FormatException`がスローされます。  
  
```  
DECLARE @g geometry = 'LINESTRING(1 1)';  
```  
  
### <a name="valid-instances"></a>有効なインスタンス  
 `LineString` インスタンスを有効にするためには、次の条件を満たす必要があります。  
  
1.  `LineString` インスタンスが許容されていること。  
  
2.  `LineString` インスタンスが空でない場合は、2 つ以上の異なる点が含まれていること。  
  
3.  `LineString` インスタンスは、それ自体を 2 つ以上の連続する点の区間に重ねることはできない。  
  
 次に示す `LineString` インスタンスは有効です。  
  
```  
DECLARE @g1 geometry= 'LINESTRING EMPTY';  
DECLARE @g2 geometry= 'LINESTRING(1 1, 3 3)';  
DECLARE @g3 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0)';  
DECLARE @g4 geometry= 'LINESTRING(1 1, 3 3, 2 4, 2 0, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid();  
  
```  
  
 次に示す `LineString` インスタンスは無効です。  
  
```  
DECLARE @g1 geometry = 'LINESTRING(1 4, 3 4, 2 4, 2 0)';  
DECLARE @g2 geometry = 'LINESTRING(1 1, 1 1)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
> [!WARNING]  
>  `LineString` の重複の検出は浮動小数点計算に基づいて行われますが、この計算は正確ではありません。  
  
## <a name="examples"></a>使用例  
 次の例は、3 つの点を持つ `geometry``LineString` インスタンスを作成する方法を示しています。このインスタンスの SRID は 0 です。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1, 2 4, 3 9)', 0);  
```  
  
 `LineString` インスタンスのそれぞれの点には、Z (昇格) 値と M (メジャー) 値を含めることができます。 次の例では、上の例で作成した `LineString` インスタンスに M 値を追加します。 M および Z は NULL 値にすることができます。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(1 1 NULL 0, 2 4 NULL 12.3, 3 9 NULL 24.5)', 0);  
```  
  
 次の例は、同じ 2 つの点を持つ `geometry LineString` インスタンスを作成する方法を示しています。 `IsValid` 呼び出しは、`LineString` インスタンスが無効であることを示します。`MakeValid` 呼び出しは、`LineString` インスタンスを `Point` に変換します。  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::STGeomFromText('LINESTRING(1 3, 1 3)',0);  
IF @g.STIsValid() = 1  
  BEGIN  
     SELECT @g.ToString() + ' is a valid LineString.';    
  END  
ELSE  
  BEGIN  
     SELECT @g.ToString() + ' is not a valid LineString.';  
     SET @g = @g.MakeValid();  
     SELECT @g.ToString() + ' is a valid Point.';    
  END  
  
```  
  
 上のコード スニペットは、次の結果を返します。  
  
```  
LINESTRING(1 3, 1 3) is not a valid LineString  
POINT(1 3) is a valid Point.  
```  
  
## <a name="see-also"></a>関連項目  
 [STLength &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)   
 [STStartPoint &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)   
 [STEndpoint &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)   
 [STPointN &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)   
 [STNumPoints &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)   
 [STIsRing &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)   
 [STIsClosed &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)   
 [STPointOnSurface &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)   
 [空間データ &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)  
  
  
