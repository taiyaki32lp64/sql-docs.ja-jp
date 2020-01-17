---
title: geography インスタンスの作成、構築、およびクエリ | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geography data type [SQL Server]
- geodetic data type [SQL Server]
- geography data type [SQL Server], about geography data type
ms.assetid: b585851e-d15b-411f-adeb-aeabeb777c0b
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b942e32e78a0a66e2d650ad36202bdf0effebc05
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68048753"
---
# <a name="create-construct-and-query-geography-instances"></a>geography インスタンスの作成、構築、およびクエリ
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  地理空間データ型の **geography**は、球体地球座標系のデータを表します。 この型は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では .NET 共通言語ランタイム (CLR) のデータ型として実装されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **geography** データ型は、GPS の緯度経度座標などの楕円体 (球体地球) データを格納します。  
  
 **geography** 型は、各データベースで使用できるように事前に定義されています。 **geography** 型のテーブル列を作成し、システムが提供する他のデータ型を使用するときと同じように **geography** データを操作できます。  
  
##  <a name="creating"></a> 新しい geography インスタンスの作成または構築  
  
###  <a name="existing"></a> 既存のインスタンスからの新しい geography インスタンスの作成  
 **geography** データ型には、既存のインスタンスに基づいて新しい **geography** インスタンスを作成するために使用できる組み込みメソッドが数多く用意されています。  
  
 **geography の周りにバッファーを作成するには**  
 [STBuffer &#40;geography データ型&#41;](../../t-sql/spatial-geography/stbuffer-geography-data-type.md)  
  
 **geography の周りにバッファーを作成して許容誤差を指定するには**  
 [BufferWithTolerance &#40;geography データ型&#41;](../../t-sql/spatial-geography/bufferwithtolerance-geography-data-type.md)  
  
 **2 つの geography インスタンスの積集合から geography を作成するには**  
 [STIntersection &#40;geography データ型&#41;](../../t-sql/spatial-geography/stintersection-geography-data-type.md)  
  
 **2 つの geography インスタンスの和集合から geography を作成するには**  
 [STUnion &#40;geography データ型&#41;](../../t-sql/spatial-geography/stunion-geography-data-type.md)  
  
 **一方の geography の、もう一方の geography と重なる部分を除いた点から geography を作成するには**  
 [STDifference &#40;geography データ型&#41;](../../t-sql/spatial-geography/stdifference-geography-data-type.md)  
  
###  <a name="wkt"></a> Well-Known Text 入力からの geography インスタンスの構築  
 **geography** データ型には、Open Geospatial Consortium (OGC) WKT 表現から geography を生成する組み込みのメソッドが数多く用意されています。 WKT 標準は geography データをテキスト形式で交換できるテキスト文字列です。  
  
 **WKT 入力から任意の型の geography インスタンスを構築するには**  
 [STGeomFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
 [Parse &#40;geography データ型&#41;](../../t-sql/spatial-geography/parse-geography-data-type.md)  
  
 **WKT 入力から geography Point インスタンスを構築するには**  
 [STPointFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stpointfromtext-geography-data-type.md)  
  
 **WKT 入力から geography MultiPoint インスタンスを構築するには**  
 [STMPointFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stmpointfromtext-geography-data-type.md)  
  
 **WKT 入力から geography LineString インスタンスを構築するには**  
 STLineFromText (geography データ型)  
  
 **WKT 入力から geography MultiLineString インスタンスを構築するには**  
 [STMLineFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stmlinefromtext-geography-data-type.md)  
  
 **WKT 入力から geography Polygon インスタンスを構築するには**  
 [STPolyFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stpolyfromtext-geography-data-type.md)  
  
 **WKT 入力から geography MultiPolygon インスタンスを構築するには**  
 [STMPolyFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stmpolyfromtext-geography-data-type.md)  
  
 **WKT 入力から geography GeometryCollection インスタンスを構築するには**  
 [STGeomCollFromText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeomcollfromtext-geography-data-type.md)  
  
###  <a name="wkb"></a> Well-Known Binary 入力からの geography インスタンスの構築  
 WKB は、 **Geography** データをクライアント アプリケーションと SQL データベース間で交換することができる、OGC で指定されたバイナリ形式です。 次の関数は、WKB 入力を受け入れて geography インスタンスを構築します。  
  
 **WKB 入力から任意の型の geography インスタンスを構築するには**  
 [STGeomFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeomfromwkb-geography-data-type.md)  
  
 **WKB 入力から geography Point インスタンスを構築するには**  
 [STPointFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stpointfromwkb-geography-data-type.md)  
  
 **WKB 入力から geography MultiPoint インスタンスを構築するには**  
 [STMPointFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stmpointfromwkb-geography-data-type.md)  
  
 **WKB 入力から geography LineString インスタンスを構築するには**  
 [STLineFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stlinefromwkb-geography-data-type.md)  
  
 **WKB 入力から geography MultiLineString インスタンスを構築するには**  
 [STMLineFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stmlinefromwkb-geography-data-type.md)  
  
 **WKB 入力から geography Polygon インスタンスを構築するには**  
 [STPolyFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stpolyfromwkb-geography-data-type.md)  
  
 **WKB 入力から geography MultiPolygon インスタンスを構築するには**  
 [STMPolyFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stmpolyfromwkb-geography-data-type.md)  
  
 **WKB 入力から geography GeometryCollection インスタンスを構築するには**  
 [STGeomCollFromWKB &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeomcollfromwkb-geography-data-type.md)STGeomCollFromWKB (geography データ型)  
  
###  <a name="gml"></a> GML Text 入力からの geography インスタンスの構築  
 **geography** データ型には、GML ( **geography** インスタンスの XML 表現) から **geography** インスタンスを生成するメソッドが用意されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、GML のサブセットをサポートします。  
  
 Geography Markup Language の詳細については、OGC の仕様の[「OGC Specification」の「Geography Markup Language」](https://go.microsoft.com/fwlink/?LinkId=93629)を参照してください。  
  
 **GML 入力から任意の型の geography インスタンスを構築するには**  
 [GeomFromGML &#40;geography データ型&#41;](../../t-sql/spatial-geography/geomfromgml-geography-data-type.md)  
  
##  <a name="returning"></a> geography インスタンスからの Well-Known Text および Well-Known Binary の取得  
 次のメソッドを使用して、 **geography** インスタンスの WKT 形式または WKB 形式のいずれかを取得できます。  
  
 **geography インスタンスの WKT 表現を取得するには**  
 [STAsText &#40;geography データ型&#41;](../../t-sql/spatial-geography/stastext-geography-data-type.md)  
  
 [ToString &#40;geography データ型&#41;](../../t-sql/spatial-geography/tostring-geography-data-type.md)  
  
 **geography インスタンスの WKT 表現を Z と M の値も含めて取得するには**  
 [AsTextZM &#40;geography データ型&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
 **geography インスタンスの WKB 表現を取得するには**  
 [STAsBinary &#40;geography データ型&#41;](../../t-sql/spatial-geography/stasbinary-geography-data-type.md)  
  
 **geography インスタンスの GML 表現を取得するには**  
 [AsGml &#40;geography データ型&#41;](../../t-sql/spatial-geography/asgml-geography-data-type.md)  
  
##  <a name="query"></a> geography インスタンスのプロパティと動作のクエリ  
 すべての **geography** インスタンスには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のメソッドを使用して取得できるいくつかのプロパティがあります。 以下のトピックでは、geography 型のプロパティおよび動作と、geography 型に対するクエリを実行するためのメソッドについて説明します。  
  
###  <a name="valid"></a> 有効性、インスタンスの型、および GeometryCollection 情報  
 **geography** インスタンスを構築した後、次のメソッドを使用して、インスタンスの型を取得することができます。また、 **GeometryCollection** インスタンスの場合は、特定の **geography** インスタンスを返します。  
  
 **geography インスタンスの型を取得するには**  
 [STGeometryType &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)  
  
 **geography が特定のインスタンスの型であるかどうかを調べるには**  
 [InstanceOf &#40;geography データ型&#41;](../../t-sql/spatial-geography/instanceof-geography-data-type.md)  
  
 **geography インスタンスがそのインスタンスの型に対応する適切な形式であるかどうかを調べるには**  
 [STNumGeometries &#40;geography データ型&#41;](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md)  
  
 **GeometryCollection インスタンス内の特定の geography を取得するには**  
 [STGeometryN &#40;geography データ型&#41;](../../t-sql/spatial-geography/stgeometryn-geography-data-type.md)STGeometryN (geography データ型)  
  
###  <a name="number"></a> 点の数  
 空でないすべての **geography** インスタンスは *点*で構成されています。 これらの点は、 **geography** インスタンスが描画される地球の緯度経度座標を表します。 **geography** データ型には、インスタンスの点に対するクエリを実行するための組み込みメソッドが数多く用意されています。  
  
 **インスタンスを構成する点の数を取得するには**  
 [STNumPoints &#40;geography データ型&#41;](../../t-sql/spatial-geography/stnumpoints-geography-data-type.md)  
  
 **インスタンスの特定の点を取得するには**  
 [STPointN &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)  
  
 **インスタンスの始点を取得するには**  
 [STStartPoint &#40;geography データ型&#41;](../../t-sql/spatial-geography/ststartpoint-geography-data-type.md)  
  
 **インスタンスの終点を取得するには**  
 [STEndpoint &#40;geography データ型&#41;](../../t-sql/spatial-geography/stendpoint-geography-data-type.md)  
  
###  <a name="dimension"></a> [ディメンション]  
 空でない **geography** インスタンスの次元は、0 次元、1 次元、2 次元のいずれかになります。 0 次元の **geography** インスタンス ( **Point** や **MultiPoint**など) には長さや面積はありません。 1 次元のオブジェクト ( **LineString、CircularString**、 **CompoundCurve**、および **MultiLineString**など) には長さがあります。 2 次元のインスタンス ( **Polygon、CurvePolygon**、および **MultiPolygon**など) には面積と長さがあります。 空のインスタンスは -1 次元としてレポートされます。 **GeometryCollection** ではその内容の最も大きな次元がレポートされます。  
  
 **インスタンスの次元を取得するには**  
 [STDimension &#40;geography データ型&#41;](../../t-sql/spatial-geography/stdimension-geography-data-type.md)  
  
 **インスタンスの長さを取得するには**  
 [STLength &#40;geography データ型&#41;](../../t-sql/spatial-geography/stlength-geography-data-type.md)  
  
 **インスタンスの面積を取得するには**  
 [STArea &#40;geography データ型&#41;](../../t-sql/spatial-geography/starea-geography-data-type.md)  
  
###  <a name="empty"></a> 空  
 _空_の **geography** インスタンスには点はありません。 空の **LineString、CircularString**、**CompoundCurve**、および **MultiLineString** インスタンスの長さは 0 です。 空の **Polygon、CurvePolygon** 、および **MultiPolygon** インスタンスの面積は 0 です。  
  
 **インスタンスが空かどうかを調べるには**  
 [STIsEmpty &#40;geography データ型&#41;](../../t-sql/spatial-geography/stisempty-geography-data-type.md)  
  
###  <a name="closure"></a> 閉鎖性  
 _閉じている_ **geography** インスタンスは、始点と終点が同じである図形です。 **Polygon** インスタンスは閉じていると見なされます。 **Point** インスタンスは閉じていないと見なされます。  
  
 リングは、単純な閉じている **LineString** インスタンスです。  
  
 **インスタンスが閉じているかどうかを調べるには**  
 [STIsClosed &#40;geography データ型&#41;](../../t-sql/spatial-geography/stisclosed-geography-data-type.md)  
  
 **Polygon インスタンスのリングの数を取得するには**  
 [NumRings &#40;geography データ型&#41;](../../t-sql/spatial-geography/numrings-geography-data-type.md)  
  
 **geography インスタンスの指定したリングを取得するには**  
 [RingN &#40;geography データ型&#41;](../../t-sql/spatial-geography/ringn-geography-data-type.md)  
  
###  <a name="srid"></a> SRID (spatial reference ID)  
 SRID (spatial reference ID) は、 **geography** インスタンスがどの楕円体座標系で表されているかを示す識別子です。 SRID が異なる 2 つの **geography** インスタンスを比較することはできません。  
  
 **インスタンスの SRID を設定または取得するには**  
 [STSrid &#40;geography データ型&#41;](../../t-sql/spatial-geography/stsrid-geography-data-type.md)  
  
 このプロパティは変更できます。  
  
##  <a name="rel"></a> geography インスタンスの関係の特定  
 **geography** データ型には、2 つの **geography** インスタンスの関係を調べるために使用できる組み込みメソッドが数多く用意されています。  
  
 **2 つのインスタンスが同じ点の集合で構成されているかどうかを調べるには**  
 [STEquals &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stequals-geometry-data-type.md)  
  
 **2 つのインスタンスが互いに離れているかどうかを調べるには**  
 [STDisjoint &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stdisjoint-geometry-data-type.md)  
  
 **2 つのインスタンスが交差するかどうかを調べるには**  
 [STIntersects &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stintersects-geometry-data-type.md)  
  
 **2 つのインスタンスが交差する点を調べるには**  
 [STIntersection &#40;geography データ型&#41;](../../t-sql/spatial-geography/stintersection-geography-data-type.md)  
  
 **2 つの geography インスタンスの点の間の最短距離を調べるには**  
 [STDistance &#40;geometry データ型&#41;](../../t-sql/spatial-geometry/stdistance-geometry-data-type.md)  
  
 **2 つの geography インスタンスの点の相違を調べるには**  
 [STDifference &#40;geography データ型&#41;](../../t-sql/spatial-geography/stdifference-geography-data-type.md)  
  
 **2 つの geography インスタンスを比較して一方のインスタンスの対称差 (重複しない点) を取得するには**  
 [STSymDifference &#40;geography データ型&#41;](../../t-sql/spatial-geography/stsymdifference-geography-data-type.md)  
  
##  <a name="supportedsrid"></a> geography インスタンスでは必ずサポート対象の SRID を使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] EPSG 標準に基づく SRID をサポートします。 地理空間データを使用して計算を実行したりメソッドを使用したりする際には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でサポートされている SRID を **geography** インスタンスで使用する必要があります。 その SRID が、 **sys.spatial_reference_systems** カタログ ビューに表示される SRID のいずれかに一致する必要があります。 既に説明したように、 **geography** データ型を使用して空間データの計算を実行する場合、計算結果は、データの作成に使用された楕円体によって異なります。これは、各楕円体に特定の SRID (spatial reference identifier) が割り当てられているからです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 既定の SRID 4326 を使用します。SRID 4326 は、 **geography** インスタンスのメソッドを使用する際に WGS 84 空間参照系にマップされます。 WGS 84 (SRID 4326) 以外の空間参照系のデータを使用する場合は、その地理空間データの SRID を確認する必要があります。  
  
##  <a name="examples"></a> 使用例  
次の例は、geography 型のデータの追加方法とクエリ方法を示しています。  
  
### <a name="example-a"></a>例 A. 
この例では、ID 列と `geography` 型の `GeogCol1` 列を含むテーブルを作成します。 3 番目の列で、 `geography` 型の列をその Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現で示し、 `STAsText()` メソッドを使用します。 次に 2 つの行が挿入されます。1 つは、 `LineString` の `geography`インスタンスを含む行で、もう 1 つは `Polygon` インスタンスを含む行です。  
  
```sql  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
  ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText()
   );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="example-b"></a>例 B。
この例では、`STIntersection()` メソッドを使用して、前の例で挿入した 2 つの `geography` インスタンスが交差する点を返します。  
  
```sql  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
## <a name="see-also"></a>参照  
 [空間データ &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
