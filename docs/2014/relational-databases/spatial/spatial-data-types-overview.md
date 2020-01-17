---
title: 空間データ型の概要 | Microsoft Docs
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 9ae74640557f7906ed237341d147926eb3296614
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014046"
---
# <a name="spatial-data-types-overview"></a>空間データ型の概要
  空間データには 2 つの型があります。 `geometry` データ型は平面 (ユークリッド (平面地球)) データをサポートしています。 `geometry` データ型 (平面) は、Open Geospatial Consortium (OGC) Simple Features for SQL Specification version 1.1.0 および SQL MM (ISO 標準) の両方に準拠しています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではそのほかに、`geography` データ型もサポートされています。このデータ型は、GPS の緯度経度座標などの楕円体 (球体地球) データを格納します。  
  
> [!IMPORTANT]  
>  空間データ型の機能強化を含め、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]に導入された空間機能の詳細な説明とサンプルについては、ホワイト ペーパー「 [SQL Server コードネーム "Denali" の新しい空間機能](https://go.microsoft.com/fwlink/?LinkId=226407)」をダウンロードして参照してください。  
  
##  <a name="objects"></a> 空間データ オブジェクト  
 `geometry` データ型と `geography` データ型は、16 の空間データ オブジェクト (インスタンス型) をサポートしています。 ただし、 *インスタンス化可能*なインスタンス型、つまりデータベース内でインスタンスを作成して使用することができる (インスタンス化できる) インスタンス型は、そのうちの 11 種類のみです。 これらのインスタンスとして識別される、親データ型から派生するプロパティによって`Points`、 **LineStrings, CircularStrings**、 `CompoundCurves`、 `Polygons`、`CurvePolygons`または複数のとして`geometry`または`geography`インスタンス、`GeometryCollection`します。 `Geography` 型には、`FullGlobe` という追加のインスタンス型があります。  
  
 次の図は、`geometry` の階層を表しています。`geometry` データ型と `geography` データ型はこの階層に基づいています。 インスタンス化可能な型`geometry`と`geography`青で示されています。  
  
 ![Geometry 型の階層](../../database-engine/media/geom-hierarchy.gif "geometry 型の階層")  
  
 図が示すとおり、10 個のインスタンス化可能な種類の`geometry`と`geography`データ型は`Point`、 `MultiPoint`、 `LineString`、 `CircularString`、 `MultiLineString`、 `CompoundCurve`、 `Polygon`、 `CurvePolygon`、 `MultiPolygon`、および`GeometryCollection`します。 geography データ型には、もう 1 つ `FullGlobe` というインスタンス化可能な型があります。 `geometry`と`geography`型を認識できる特定のインスタンスを適切な形式のインスタンスである限り、インスタンスが明示的に定義されていない場合でもです。 定義する場合など、 `Point` 、STPointFromText() メソッドを使用して明示的にインスタンス`geometry`と`geography`として認識されます、`Point`メソッドの入力が正しく構成されている限り、します。 `STGeomFromText()` メソッドを使用して同じインスタンスを定義した場合は、`geometry` データ型と `geography` データ型の両方で `Point` として認識されます。  
  
 geometry 型および geography 型のサブタイプには、単純型とコレクション型があります。  `STNumCurves()` などのメソッドは、単純型でのみ機能します。  
  
 単純型は、次のとおりです。  
  
-   [Point](../spatial/point.md)  
  
-   [LineString](../spatial/linestring.md)  
  
-   [CircularString](../spatial/circularstring.md)  
  
-   [CompoundCurve](../spatial/compoundcurve.md)  
  
-   [多角形](../spatial/polygon.md)  
  
-   [CurvePolygon](../spatial/curvepolygon.md)  
  
 コレクション型は、次のとおりです。  
  
-   [MultiPoint](../spatial/multipoint.md)  
  
-   [MultiLineString](../spatial/multilinestring.md)  
  
-   [MultiPolygon](../spatial/multipolygon.md)  
  
-   [geography](../spatial/geometrycollection.md)  
  
  
##  <a name="differences"></a> geometry データ型と geography データ型の違い  
 2 つの空間データ型の動作はよく似ていますが、データの格納および操作の方法にいくつかの重要な違いがあります。  
  
### <a name="how-connecting-edges-are-defined"></a>接続エッジの定義方法  
 `LineString` 型と `Polygon` 型の定義データは頂点のみです。  geometry 型の 2 つの頂点間の接続エッジは直線です。  一方、geography 型の 2 つの頂点間の接続エッジは、2 つの頂点を結ぶ短い方の大楕円弧です。  大楕円は、楕円体とその中心を通る平面との交線であり、大楕円弧は、大楕円の円弧セグメントです。  
  
### <a name="how-circular-arc-segments-are-defined"></a>円弧セグメントの定義方法  
 geometry 型の円弧セグメントは、XY デカルト座標平面上に定義されます (Z 値は無視されます)。 geography 型の円弧セグメントは、参照球の曲線セグメントによって定義されます。 参照球の平行線は、両方の円弧の点に一定の緯度角がある、2 つの補助的な円弧によって定義できます。  
  
### <a name="measurements-in-spatial-data-types"></a>空間データ型の測定  
 平面 (平面地球) 座標系では、距離や面積の測定値は座標と同じ測定単位で表されます。 `geometry` データ型を使用した場合、(2, 2) と (5, 6) の間の距離は、使用されている単位に関係なく 5 単位になります。  
  
 楕円体 (球体地球) 座標系では、座標は緯度と経度で表されます。 ただし、長さと面積は、`geography` インスタンスの SRID (Spatial Reference Identifier) によっても異なりますが、通常はメートルと平方メートルで測定されます。 メートルは、`geography` データ型の最も一般的な測定単位です。  
  
### <a name="orientation-of-spatial-data"></a>空間データの方向  
 平面座標系では、ポリゴンのリングの方向は重要ではありません。 たとえば、((0, 0), (10, 0), (0, 20), (0, 0)) によって表されるポリゴンは、((0, 0), (0, 20), (10, 0), (0, 0)) によって表されるポリゴンと同じです。 OGC Simple Features for SQL Specification では、リングの順序は定められていません。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でもリングの順序は強制されません。  
  
 楕円体座標系では、ポリゴンは方向がないと意味がなくなります (あいまいになります)。 たとえば、赤道の周りのリングが北半球を表すのか南半球を表すのかがわからなくなります。 `geography` データ型を使用して空間インスタンスを格納する場合は、リングの方向を指定し、インスタンスの位置を正確に示す必要があります。 楕円体座標系の多角形の内部は、左辺ルールによって定義されます。  
  
 互換性レベルが 100 以下で[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、`geography`データ型には、次の制限。  
  
-   各 `geography` インスタンスが 1 つの半球に収まる必要があります。 半球よりも大きい空間オブジェクトを格納することはできません。  
  
-   Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現または Well-Known Binary (WKB) 表現の `geography` インスタンスでは、半球より大きいオブジェクトが生成される場合に `ArgumentException` がスローされます。  
  
-   `geography`データ型のメソッドを 2 つの入力を必要とする`geography`STIntersection()、STUnion()、STDifference()、STSymDifference() などのインスタンスは、メソッドの結果は 1 つの半球に収まらない場合は null を返します。 STBuffer() でも、出力が 1 つの半球に収まらない場合に null が返されます。  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] の `FullGlobe` は、球全体を覆う特殊な多角形です。 `FullGlobe` には領域がありますが、境界や頂点はありません。  
  
### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>geography データ型では外部リングと内部リングは重要ではない  
 OGC Simple Features for SQL Specification には、外部リングと内部リングがについて説明しますが、この区別はほとんど意味をにとって、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `geography` ; データ型のすべての多角形のリングできます扱われるため、外部リングします。  
  
 OGC の仕様の詳細については、以下を参照してください。  
  
-   [OGC の仕様、簡易機能アクセス Part 1 - 共通アーキテクチャ](https://go.microsoft.com/fwlink/?LinkId=93627)  
  
-   [OGC の仕様、簡易機能アクセス Part 2 - SQL オプション](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
  
##  <a name="circular"></a> 円弧セグメント  
 円弧セグメントでは、`CircularString`、`CompoundCurve`、および `CurvePolygon` の 3 つのインスタンス化可能な型を使用できます。  円弧セグメントは、2 次元平面内の 3 つの点によって定義されます。3 番目のポイントを最初のポイントと同じにすることはできません。  
  
 図 A と図 B は、一般的な円弧のセグメントを示します。 3 つの点が 1 つの円周上にあることに注意してください。  
  
 図 C および図 D は、直線セグメントを円弧セグメントとして定義できる方法を示しています。  2 つの点のみによって定義できる通常の直線セグメントとは異なり、円弧セグメントを定義するには 3 つの点が必要であることに注意してください。  
  
 円弧型を操作するメソッドは、直線セグメントを使用して大まかな円弧を作成します。大まかな円を作成するために使用される直線セグメントの数は、円弧の長さと曲率によって異なります。Z 値はそれぞれの円弧型で格納できますが、メソッドは計算に Z 値を使用しません。  
  
> [!NOTE]  
>  Z 値が円弧セグメントに指定されている場合、円弧セグメントが入力として許容されるようにするには、円弧セグメント内のすべての点で Z 値が同じである必要があります。 たとえば、 `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` は許容されますが、 `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` は許容されません。  
  
### <a name="linestring-and-circularstring-comparison"></a>LineString と CircularString の比較  
 次の図は、同一の二等辺三角形を示しています (三角形 A は直線セグメントを使用して三角形を定義し、三角形 B は円弧セグメントを使用して三角形を定義しています)。  
  
 ![](../../database-engine/media/7e382f76-59da-4b62-80dc-caf93e637c14.png "7e382f76-59da-4b62-80dc-caf93e637c14")  
  
 この例は、`LineString` インスタンスと `CircularString` インスタンスの両方を使用して上の二等辺三角形を格納する方法を示しています。  
  
```sql  
DECLARE @g1 geometry;  
DECLARE @g2 geometry;  
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);  
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);  
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1  
  BEGIN  
      SELECT @g1.ToString(), @g2.ToString()  
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]  
  END  
```  
  
 `CircularString` インスタンスでは、三角形を定義するために 7 つの点が必要ですが、`LineString` インスタンスでは、三角形を定義するために必要な点は 4 つだけです。 その理由は、`CircularString` インスタンスは直線セグメントではなく円弧セグメントを格納するためです。 したがって、`CircularString` インスタンスに格納される三角形の辺は ABC、CDE、および EFA であるのに対し、`LineString` インスタンスに格納される三角形の辺は AC、CE、および EA です。  
  
 次のようなコード スニペットがあるとします。  
  
```sql  
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);  
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);  
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];  
```  
  
 このスニペットの結果は、次のようになります。  
  
```  
LS LengthCS Length  
5.65685...6.28318...  
```  
  
 次の図は、各型の格納方法を示します (赤い線は`LineString``@g1`を示し、青い線の表示`CircularString``@g2`)。  
  
 ![](../../database-engine/media/e52157b5-5160-4a4b-8560-50cdcf905b76.png "e52157b5-5160-4a4b-8560-50cdcf905b76")  
  
 上の図が示すように、`CircularString` インスタンスでは `LineString` インスタンスよりも少ない点を使用して、さらに高い精度で曲面境界を格納します。 `CircularString` インスタンスは、たとえば特定の点から半径 20 マイルの検索を行う際など、円形境界を格納する場合に便利です。 `LineString` インスタンスは、四角い都市区画のような直線的な境界を格納する場合に適しています。  
  
### <a name="linestring-and-compoundcurve-comparison"></a>LineString と CompoundCurve の比較  
 次のコード例は、`LineString` インスタンスと `CompoundCurve` インスタンスを使用して同じ図を格納する方法を示します。  
  
```sql  
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');  
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');  
```  
  
 または  
  
 上の例では、`LineString` インスタンスまたは `CompoundCurve` インスタンスで図を格納できます。  次の例では、`CompoundCurve` を使用して円のスライスを格納します。  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  
  
 `CompoundCurve` インスタンスは円弧セグメント (2 2, 1 3, 0 2) を直接格納できますが、`LineString` インスタンスでは曲線をいくつかの小さな直線セグメントに変換する必要があります。  
  
### <a name="circularstring-and-compoundcurve-comparison"></a>CircularString と CompoundCurve の比較  
 次のコード例は、`CircularString` インスタンスに円のスライスを格納する方法を示します。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');  
SELECT @g.ToString(), @g.STLength();  
```  
  
 `CircularString` インスタンスを使用して円のスライスを格納するには、各直線セグメントで 3 つの点を使用する必要があります。  中間点が不明な場合は、中間点を計算するか、次のスニペットで示すように直線セグメントの端点を二重にする必要があります。  
  
```sql  
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');  
```  
  
 `CompoundCurve` インスタンスは `LineString` コンポーネントおよび `CircularString` コンポーネントを許可して、認識される必要がある点が、円のスライスの直線セグメントの 2 点だけになるようにします。  このコード例は、`CompoundCurve` を使用して同じ図を格納する方法を示します。  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');  
SELECT @g.ToString(), @g.STLength();  
```  
  
### <a name="polygon-and-curvepolygon-comparison"></a>Polygon と CurvePolygon の比較  
 `CurvePolygon` インスタンスは、外部リングと内部リングを定義するときに `CircularString` インスタンスと `CompoundCurve` インスタンスを使用できます。  `Polygon` インスタンスは、`CircularString` および `CompoundCurve` の円弧型を使用することはできません。  
  
  
## <a name="see-also"></a>参照  
 [空間データ &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [geometry データ型メソッド リファレンス](/sql/t-sql/spatial-geometry/spatial-types-geometry-transact-sql)   
 [geography データ型メソッド リファレンス](/sql/t-sql/spatial-geography/spatial-types-geography)   
 [STNumCurves &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stnumcurves-geometry-data-type)   
 [STNumCurves &#40;geography データ型&#41;](/sql/t-sql/spatial-geography/stnumcurves-geography-data-type)   
 [STGeomFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)   
 [STGeomFromText #40;geography データ型&#41;](/sql/t-sql/spatial-geography/stgeomfromtext-geography-data-type)  
  
  
