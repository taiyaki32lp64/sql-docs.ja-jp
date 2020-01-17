---
title: geometry インスタンスの作成、構築、およびクエリ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- planar spatial data [SQL Server], getting started
- geometry data type [SQL Server], getting started
ms.assetid: c6b5c852-37d2-48d0-a8ad-e43bb80d6514
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: cb99c2ff07f30d268980c5c1c4d43a34904cdec9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014312"
---
# <a name="create-construct-and-query-geometry-instances"></a>geometry インスタンスの作成、構築、およびクエリ
  平面空間データ型の `geometry` は、ユークリッド (平面) 座標系のデータを表します。 この型は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では共通言語ランタイム (CLR) のデータ型として実装されています。  
  
 `geometry` 型は、各データベースで使用できるように事前に定義されています。 型のテーブル列を作成する`geometry`操作と`geometry`他の CLR 型を使用すると同じ方法でデータ。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってサポートされている `geometry` データ型 (平面) は、Open Geospatial Consortium (OGC) Simple Features for SQL Specification version 1.1.0 に準拠しています。  
  
 OGC の仕様の詳細については、以下を参照してください。  
  
-   [OGC の仕様、簡易機能アクセス Part 1 - 共通アーキテクチャ](https://go.microsoft.com/fwlink/?LinkId=93628)  
  
-   [OGC の仕様、簡易機能アクセス Part 2 - SQL オプション](https://go.microsoft.com/fwlink/?LinkId=93629)  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次のスキーマで定義されている既存の GML 3.1 標準のサブセットをサポートしています: [https://schemas.microsoft.com/sqlserver/profiles/gml/SpatialGML.xsd](https://go.microsoft.com/fwlink/?LinkId=230959)。  
  
##  <a name="creating"></a> 新しい geometry インスタンスの作成または構築  
  
###  <a name="existing"></a> 既存のインスタンスからの新しい geometry インスタンスの作成  
 `geometry` データ型には、既存のインスタンスに基づいて新しい `geometry` インスタンスを作成するために使用できる組み込みメソッドが数多く用意されています。  
  
 **geometry の周りにバッファーを作成するには**  
 [STBuffer &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stbuffer-geometry-data-type)  
  
 [BufferWithTolerance &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/bufferwithtolerance-geometry-data-type)  
  
 **簡素化されたバージョンの geometry を作成するには**  
 [Reduce &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/reduce-geometry-data-type)  
  
 **geometry の凸包を作成するには**  
 [STConvexHull &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stconvexhull-geometry-data-type)  
  
 **2 つの geometry の積集合から geometry を作成するには**  
 [STIntersection &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stintersection-geometry-data-type)  
  
 **2 つの geometry の和集合から geometry を作成するには**  
 [STUnion &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stunion-geometry-data-type)  
  
 **一方の geometry の、もう一方の geometry と重なる部分を除いた点から geometry を作成するには**  
 [STDifference &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stdifference-geometry-data-type)  
  
 **2 つの geometry の重なる部分を除いた点から geometry を作成するには**  
 [STSymDifference &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stsymdifference-geometry-data-type)  
  
 **既存の geometry 上にある任意の Point インスタンスを作成するには**  
 [STPointOnSurface &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
  
  
###  <a name="wkt"></a> Well-Known Text 入力からの geometry インスタンスの構築  
 `geometry` データ型には、Open Geospatial Consortium (OGC) WKT 表現からジオメトリを生成する組み込みのメソッドが数多く用意されています。 WKT 標準は geometry データをテキスト形式で交換できるテキスト文字列です。  
  
 **WKT 入力から任意の型の geometry インスタンスを構築するには**  
 [STGeomFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeomfromtext-geometry-data-type)  
  
 [Parse &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/parse-geometry-data-type)  
  
 **WKT 入力から geometry Point インスタンスを構築するには**  
 [STPointFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpointfromtext-geometry-data-type)  
  
 **WKT 入力から geometry MultiPoint インスタンスを構築するには**  
 [STMPointFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stmpointfromtext-geometry-data-type)  
  
 **WKT 入力から geometry LineString インスタンスを構築するには**  
 [STLineFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stlinefromtext-geometry-data-type)  
  
 **WKT 入力から geometry MultiLineString インスタンスを構築するには**  
 [STMLineFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stmlinefromtext-geometry-data-type)  
  
 **WKT 入力から geometry Polygon インスタンスを構築するには**  
 [STPolyFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpolyfromtext-geometry-data-type)  
  
 **WKT 入力から geometry MultiPolygon インスタンスを構築するには**  
 [STMPolyFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stmpolyfromtext-geometry-data-type)  
  
 **WKT 入力から geometry GeometryCollection インスタンスを構築するには**  
 [TGeomCollFromText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromtext-geometry-data-type)  
  
  
  
###  <a name="wkb"></a> Well-Known Binary 入力からの geometry インスタンスの構築  
 WKB は、`geometry` データをアプリケーションと SQL データベース間で交換することができる、Open Geospatial Consortium (OGC) で指定されたバイナリ形式です。 次の関数は、WKB 入力を受け入れてジオメトリを構築します。  
  
 **WKB 入力から任意の型の geometry インスタンスを構築するには**  
 [STGeomFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeomfromwkb-geometry-data-type)  
  
 **WKB 入力から geometry Point インスタンスを構築するには**  
 [STPointFromWKB &#40;geometry データ型e&#41;](/sql/t-sql/spatial-geometry/stpointfromwkb-geometry-data-type)  
  
 **WKB 入力から geometry MultiPoint インスタンスを構築するには**  
 [STMPointFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stmpointfromwkb-geometry-data-type)  
  
 **WKB 入力から geometry LineString インスタンスを構築するには**  
 [STLineFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stlinefromwkb-geometry-data-type)  
  
 **WKB 入力から geometry MultiLineString インスタンスを構築するには**  
 [STMLineFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stmlinefromwkb-geometry-data-type)  
  
 **WKB 入力から geometry Polygon インスタンスを構築するには**  
 [STPolyFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stpolyfromwkb-geometry-data-type)  
  
 **WKB 入力から geometry MultiPolygon インスタンスを構築するには**  
 [STMPolyFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stmpolyfromwkb-geometry-data-type)  
  
 **WKB 入力から geometry GeometryCollection インスタンスを構築するには**  
 [STGeomCollFromWKB &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeomcollfromwkb-geometry-data-type)  
  
  
  
###  <a name="gml"></a> GML Text 入力からの geometry インスタンスの構築  
 `geometry`データ型を生成するメソッドを提供する、 `geometry` GML、幾何オブジェクトの XML 表現からのインスタンス。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、GML のサブセットをサポートします。  
  
 **GML 入力から任意の型の geometry インスタンスを構築するには**  
 [GeomFromGml &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/geomfromgml-geometry-data-type)  
  
  
  
##  <a name="returning"></a> geometry インスタンスからの Well-Known Text および Well-Known Binary の取得  
 次のメソッドを使用して、`geometry` インスタンスの WKT 形式または WKB 形式のいずれかを取得できます。  
  
 **geometry インスタンスの WKT 表現を取得するには**  
 [STAsText &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stastext-geometry-data-type)  
  
 [ToString &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/tostring-geometry-data-type)  
  
 **geometry インスタンスの WKT 表現を Z と M の値も含めて取得するには**  
 [AsTextZM &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/astextzm-geometry-data-type)  
  
 **geometry インスタンスの WKB 表現を取得するには**  
 [STAsBinary &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stasbinary-geometry-data-type)  
  
 **geometry インスタンスの GML 表現を取得するには**  
 [AsGml &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/asgml-geometry-data-type)  
  
  
  
##  <a name="querying"></a> geometry インスタンスのプロパティと動作のクエリ  
 すべて`geometry`インスタンスがあるさまざまなメソッドを使用して取得できるプロパティを[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を提供します。 以下のトピックでは、geometry 型のプロパティおよび動作と、geometry 型のクエリを実行するためのメソッドについて説明します。  
  
###  <a name="valid"></a> 有効性、インスタンスの型、および GeometryCollection 情報  
 `geometry` インスタンスを構築したら、次のメソッドを使用して、そのインスタンスが適切な形式であるかどうかを確認したり、インスタンスの型を取得することができます。また、コレクション インスタンスの場合は、特定の `geometry` インスタンスを取得できます。  
  
 **geometry のインスタンスの型を取得するには**  
 [STGeometryType &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeometrytype-geometry-data-type)  
  
 **geometry が特定のインスタンスの型であるかどうかを調べるには**  
 [InstanceOf &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/instanceof-geometry-data-type)  
  
 **geometry インスタンスがそのインスタンスの型に対応する適切な形式であるかどうかを調べるには**  
 [STIsValid &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type)  
  
 **geometry インスタンスをインスタンスの型に対応する適切な形式の geometry インスタンスに変換するには**  
 [MakeValid &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/makevalid-geometry-data-type)  
  
 **geometry コレクション インスタンス内のジオメトリの数を取得するには**  
 [STNumGeometries &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stnumgeometries-geometry-data-type)  
  
 geometry コレクション インスタンス内の特定の geometry を取得するには  
 [STGeometryN &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stgeometryn-geometry-data-type)STGeometryN (geometry データ型)  
  
  
  
###  <a name="number"></a> 点の数  
 空でないすべて`geometry`インスタンスから成るは*ポイント*します。 これらの点は、ジオメトリが描画される平面の X 座標と Y 座標を表します `geometry` には、インスタンスの点に対するクエリを実行するための組み込みメソッドが数多く用意されています。  
  
 **インスタンスを構成する点の数を取得するには**  
 [STNumPoints &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stnumpoints-geometry-data-type)  
  
 **インスタンスの特定の点を取得するには**  
 [STPointN](/sql/t-sql/spatial-geometry/stpointn-geometry-data-type)  
  
 **インスタンス上にある任意の点を取得するには**  
 [STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)  
  
 **インスタンスの始点を取得するには**  
 [STStartPoint](/sql/t-sql/spatial-geometry/ststartpoint-geometry-data-type)  
  
 **インスタンスの終点を取得するには**  
 [STEndpoint](/sql/t-sql/spatial-geometry/stendpoint-geometry-data-type)  
  
 **Point インスタンスの X 座標を取得するには**  
 [STX &#40;geometry データ型&#41;](/sql/t-sql/spatial-geometry/stx-geometry-data-type)  
  
 **Point インスタンスの Y 座標を取得するには**  
 [STY](/sql/t-sql/spatial-geometry/sty-geometry-data-type)  
  
 **Polygon、CurvePolygon、または MultiPolygon インスタンスの幾何学中心点を取得するには**  
 [STCentroid](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type)  
  
  
  
###  <a name="dimension"></a> [ディメンション]  
 空でない `geometry` インスタンスの次元は、0 次元、1 次元、2 次元のいずれかになります。 0 次元の `geometries` (`Point` や `MultiPoint` など) には長さや面積はありません。 1 次元のオブジェクト (`LineString, CircularString, CompoundCurve`、`MultiLineString` など) には長さがあります。 2 次元のインスタンス (`Polygon`、`CurvePolygon`、`MultiPolygon` など) には面積と長さがあります。 空のインスタンスの次元は -1 としてレポートされます。`GeometryCollection` でレポートされる面積は、その内容の型によって異なります。  
  
 **インスタンスの次元を取得するには**  
 [STDimension](/sql/t-sql/spatial-geometry/stdimension-geometry-data-type)  
  
 **インスタンスの長さを取得するには**  
 [STLength](/sql/t-sql/spatial-geometry/stlength-geometry-data-type)  
  
 **インスタンスの面積を取得するには**  
 [STArea](/sql/t-sql/spatial-geometry/starea-geometry-data-type)  
  
  
  
###  <a name="empty"></a> 空  
 *空*`geometry`インスタンスには、すべてのポイントはありません。 空の長さ`LineString, CircularString`、 `CompoundCurve`、および`MultiLineString`インスタンスは 0 になります。 空の `Polygon`、`CurvePolygon`、および `MultiPolygon` インスタンスの面積は 0 です。  
  
 **インスタンスが空かどうかを調べるには**  
 [STIsEmpty](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type)。  
  
  
  
###  <a name="simple"></a> Simple  
 `geometry`するインスタンスの*単純*、これらの要件のどちらも満たす必要があります。  
  
-   インスタンスの各図形が終点以外で自己交差していてはいけない。  
  
-   インスタンスの 2 つの図形が、両方の図形の境界外部の点で互いに交差していてはいけない。  
  
> [!NOTE]  
>  空のジオメトリは常に単純です。  
  
 **インスタンスが単純かどうかを調べるには**  
 [STIsSimple](/sql/t-sql/spatial-geometry/stissimple-geometry-data-type)。  
  
  
  
###  <a name="boundary"></a> 境界、内部、および外部  
 *内部*の`geometry`インスタンスは、インスタンスが占めていた領域と*外部*はスペース占有されていません。  
  
 *境界* は、OGC によって次のように定義されています。  
  
-   `Point` インスタンスと `MultiPoint` インスタンスには境界はありません。  
  
-   `LineString` と `MultiLineString` の境界は、始点と終点 (偶数回出現するものを除く) によって形成されます。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('MULTILINESTRING((0 1, 0 0, 1 0, 0 1), (1 1, 1 0))');  
SELECT @g.STBoundary().ToString();  
```  
  
 `Polygon` インスタンスや `MultiPolygon` インスタンスの境界は、そのリングの集合です。  
  
```  
DECLARE @g geometry;  
SET @g = geometry::Parse('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0), (1 1, 1 2, 2 2, 2 1, 1 1))');  
SELECT @g.STBoundary().ToString();  
```  
  
 **インスタンスの境界を取得するには**  
 [STBoundary](/sql/t-sql/spatial-geometry/stboundary-geometry-data-type)  
  
  
  
###  <a name="envelope"></a> エンベロープ  
 *エンベロープ*の`geometry`インスタンスとも呼ばれる、*境界ボックス*、最小値軸に沿った四角形が作成され、インスタンスの最大値 (X, Y) を調整します。  
  
 **インスタンスのエンベロープを取得するには**  
 [STEnvelope](/sql/t-sql/spatial-geometry/stenvelope-geometry-data-type)  
  
  
  
###  <a name="closure"></a> 閉鎖性  
 A*閉じた*`geometry`インスタンスは、始点と終点が同じです。 `Polygon` インスタンスは閉じていると見なされます。 `Point` インスタンスは閉じていないと見なされます。  
  
 リングは、単純な閉じている `LineString` インスタンスです。  
  
 **インスタンスが閉じているかどうかを調べるには**  
 [STIsClosed](/sql/t-sql/spatial-geometry/stisclosed-geometry-data-type)  
  
 **インスタンスがリングかどうかを調べるには**  
 [STIsRing](/sql/t-sql/spatial-geometry/stisring-geometry-data-type)  
  
 **Polygon インスタンスの外部リングを取得するには**  
 [STExteriorRing](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type)  
  
 **Polygon の内部リングの数を取得するには**  
 [STNumInteriorRing](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type)  
  
 **Polygon の指定した内部リングを取得するには**  
 [STInteriorRingN](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type)  
  
  
  
###  <a name="srid"></a> SRID (spatial reference ID)  
 SRID (spatial reference ID) は、`geometry` インスタンスがどの座標系で表されているかを示す識別子です。 SRID が異なる 2 つのインスタンスを比較することはできません。  
  
 **インスタンスの SRID を設定または取得するには**  
 [STSrid](/sql/t-sql/spatial-geometry/stsrid-geometry-data-type)  
  
 このプロパティは変更できます。  
  
  
  
##  <a name="rel"></a> geometry インスタンス間の関係の特定  
 `geometry` データ型には、2 つの `geometry` インスタンスの関係を調べるために使用できる組み込みメソッドが数多く用意されています。  
  
 **2 つのインスタンスが同じ点の集合で構成されているかどうかを調べるには**  
 [STEquals](/sql/t-sql/spatial-geometry/stequals-geometry-data-type)  
  
 **2 つのインスタンスが互いに離れているかどうかを調べるには**  
 [STDisjoint](/sql/t-sql/spatial-geometry/stdisjoint-geometry-data-type)  
  
 **2 つのインスタンスが交差するかどうかを調べるには**  
 [STIntersects](/sql/t-sql/spatial-geometry/stintersects-geometry-data-type)  
  
 **2 つのインスタンスが相互に接しているかどうかを調べるには**  
 [STTouches](/sql/t-sql/spatial-geometry/sttouches-geometry-data-type)  
  
 **2 つのインスタンスが重なっているかどうかを調べるには**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **2 つのインスタンスが交わるかどうかを調べるには**  
 [STCrosses](/sql/t-sql/spatial-geometry/stcrosses-geometry-data-type)  
  
 **あるインスタンスが別のインスタンスに含まれているかどうかを調べるには**  
 [STWithin](/sql/t-sql/spatial-geometry/stwithin-geometry-data-type)  
  
 **あるインスタンスが別のインスタンスを含んでいるかどうかを調べるには**  
 [STContains](/sql/t-sql/spatial-geometry/stcontains-geometry-data-type)  
  
 **あるインスタンスが別のインスタンスと重なっているかどうかを調べるには**  
 [STOverlaps](/sql/t-sql/spatial-geometry/stoverlaps-geometry-data-type)  
  
 **2 つのインスタンスが空間的に関連するかどうかを調べるには**  
 [STRelate](/sql/t-sql/spatial-geometry/strelate-geometry-data-type)  
  
 **2 つのジオメトリの点の間の最短距離を調べるには**  
 [STDistance](/sql/t-sql/spatial-geometry/stdistance-geometry-data-type)  
  
  
  
##  <a name="defaultsrid"></a> geometry インスタンスの既定の SRID は 0  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の `geometry` インスタンスの既定の SRID は 0 です。 `geometry` 空間データでは、空間インスタンスに特定の SRID がなくても計算を実行できます。したがって、インスタンスは未定義の平面空間に存在することができます。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]では、`geometry` データ型のメソッドの計算で未定義の平面空間を表すために SRID 0 が使用されます。  
  
##  <a name="examples"></a> 使用例  
 次の 2 つの例は、geometry 型のデータの追加方法とクエリ方法を示しています。  
  
-   最初の例では、ID 列と `geometry` 型の `GeomCol1`列を含むテーブルを作成します。 3 番目の列で、 `geometry` 型の列をその Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現で示し、 `STAsText()` メソッドを使用します。 次に 2 つの行が挿入されます。1 つは、 `LineString` の `geometry`インスタンスを含む行で、もう 1 つは `Polygon` インスタンスを含む行です。  
  
    ```  
    IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
        DROP TABLE dbo.SpatialTable;  
    GO  
  
    CREATE TABLE SpatialTable   
        ( id int IDENTITY (1,1),  
        GeomCol1 geometry,   
        GeomCol2 AS GeomCol1.STAsText() );  
    GO  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('LINESTRING (100 100, 20 180, 180 180)', 0));  
  
    INSERT INTO SpatialTable (GeomCol1)  
    VALUES (geometry::STGeomFromText('POLYGON ((0 0, 150 0, 150 150, 0 150, 0 0))', 0));  
    GO  
    ```  
  
-   2 番目の例では、 `STIntersection()` メソッドを使用して、前の例で挿入した 2 つの `geometry` インスタンスが交差する点を返します。  
  
    ```  
    DECLARE @geom1 geometry;  
    DECLARE @geom2 geometry;  
    DECLARE @result geometry;  
  
    SELECT @geom1 = GeomCol1 FROM SpatialTable WHERE id = 1;  
    SELECT @geom2 = GeomCol1 FROM SpatialTable WHERE id = 2;  
    SELECT @result = @geom1.STIntersection(@geom2);  
    SELECT @result.STAsText();  
    ```  
  
  
  
## <a name="see-also"></a>参照  
 [空間データ &#40;SQL Server&#41;](spatial-data-sql-server.md)  
  
  
