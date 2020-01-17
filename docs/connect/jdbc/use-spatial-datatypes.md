---
title: 空間データ型を使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f133fa066ef2c486cf7bb40c5b653c99e077bc46
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026942"
---
# <a name="using-spatial-datatypes"></a>空間データ型の使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

空間データ型 (Geometry および Geography) は、JDBC Driver preview release 6.5.0 の開始をサポートしています。 現在、空間データ型は、ストアドプロシージャ、テーブル値パラメーター (TVP)、BulkCopy、および Always Encrypted ではサポートされていません。 このページでは、JDBC ドライバーを使用した Geometry データ型と Geography データ型のさまざまなユースケースを示します。 空間データ型の概要については、「[空間データ型の概要」](https://docs.microsoft.com/sql/relational-databases/spatial/spatial-data-types-overview)ページをご覧ください。

## <a name="creating-a-geometry--geography-object"></a>Geometry/geography オブジェクトの作成

Geometry / Geography オブジェクトを作成する主な方法は 2 つあります - Well-Known Text (WKT) または、Well-Known Binary (WKB) のいずれかから変換します。

### <a name="creating-from-wkt"></a>作成 (WKT から)

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
Geography geogWKT = Geography.STGeomFromText(geoWKT, 4326);
```

これにより、空間参照システム識別子 (SRID) 0 を持つ LINESTRING Geometry オブジェクトと、SRID 4326 を持つ Geography オブジェクトが作成されます。

### <a name="creating-from-wkb"></a>作成 (WKB から)

```java
byte[] geomWKB = Hex.decodeHex("00000000010403000000000000000000F03F00000000000000000000000000000000000000000000F03F000000000000F0BF000000000000000001000000010000000001000000FFFFFFFF0000000002".toCharArray());
byte[] geogWKB = Hex.decodeHex("E61000000104030000000000000000000000000000000000F03F000000000000F03F00000000000000000000000000000000000000000000F0BF01000000010000000001000000FFFFFFFF0000000002".toCharArray());

Geometry geomWKT = Geometry.deserialize(geomWKB);
Geography geogWKT = Geography.deserialize(geogWKB);
```

これにより、以前 WKT から作成された Geometry オブジェクトと Geography オブジェクトが作成されます。

## <a name="working-with-a-geometry--geography-object"></a>Geometry/Geography オブジェクトの操作

ユーザーは SQL Server に次のようなテーブルを持つと仮定します。

```sql
CREATE TABLE sampleTable (c1 geometry)  
```

Geometry 値を挿入するサンプルスクリプトは次のようになります。

```java
String geoWKT = "LINESTRING(1 0, 0 1, -1 0)";
Geometry geomWKT = Geometry.STGeomFromText(geoWKT, 0);
SQLServerPreparedStatement pstmt = (SQLServerPreparedStatement) connection.prepareStatement("insert into sampleTable values (?)");
pstmt.setGeometry(1, geomWKT);  
pstmt.execute();
```

Geography 列と**setgeography ()** メソッドを使用して、geography に対応する同じことを行うこともできます。

Geometry/Geography 列を読み取るには、次のようにします。

```java
try(SQLServerResultSet rs = (SQLServerResultSet)stmt.executeQuery("select * from geomTable")) {
    while(rs.next()){
        rs.getGeometry(1);
    }
}
```

Geography 列と**Getgeography ()** メソッドを使用して、geography に対応する同じことを行うこともできます。

## <a name="newly-introduced-apis"></a>新しく導入された Api

これらは、この追加で導入された新しいパブリック Api であり、 **SQLServerPreparedStatement**、 **SQLServerResultSet**、 **Geometry**、 **Geography**の各クラスに含まれています。

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

|方法|[説明]|
|:------|:----------|
|void setGeometry(int n, Geometry x)| 指定されたパラメーターを、指定した microsoft .sql. Geometry クラスオブジェクトに設定します。
|void setGeography(int n, Geography x)| 指定されたパラメーターを、特定の microsoft .sql. Geography クラスオブジェクトに設定します。

### <a name="sqlserverresultset"></a>SQLServerResultSet

|方法|[説明]|
|:------|:----------|
|Geometry getGeometry (int colunIndex)| この ResultSet オブジェクトの現在の行の指定された列の値を Java プログラミング言語の com. sqlserver. Geometry オブジェクトとして返します。
|Geometry getGeometry (文字列 columnName)| この ResultSet オブジェクトの現在の行の指定された列の値を Java プログラミング言語の com. sqlserver. Geometry オブジェクトとして返します。
|Geography getGeography(int colunIndex)| この ResultSet オブジェクトの現在の行の指定された列の値を、Java プログラミング言語の com. sqlserver. jdbc. Geography オブジェクトとして返します。
|Geography getGeography (文字列 columnName)| この ResultSet オブジェクトの現在の行の指定された列の値を、Java プログラミング言語の com. sqlserver. jdbc. Geography オブジェクトとして返します。

### <a name="geometry"></a>Geometry

|方法|[説明]|
|:------|:----------|
|Geometry STGeomFromText (String wkt, int SRID)| インスタンスに格納されている Z (標高) 値と M (メジャー) 値で補完された、Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現からの Geometry インスタンス用のコンストラクター。
|Geometry STGeomFromWKB(byte[] wkb)| Open Geospatial Consortium (OGC) の Well-Known Binary (WKB) 表現からの Geometry インスタンス用のコンストラクター。
|ジオメトリ逆シリアル化 (byte [] wkb)| 空間データの内部 SQL Server 形式の Geometry インスタンスのコンストラクター。
|ジオメトリ解析 (文字列 wkt)| Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現からの Geometry インスタンス用のコンストラクター。 空間参照識別子の既定値は0です。
|ジオメトリポイント (double x、double y、int SRID)| X 値と Y 値および空間参照識別子からポイントインスタンスを表す Geometry インスタンスのコンストラクター。
|String STAsText()| Geometry インスタンスにおける Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を返します。 このテキストは、インスタンスに格納されている Z (標高) 値または M (メジャー) 値を含みません。
|byte [] STAsBinary ()| Geometry インスタンスにおける Open Geospatial Consortium (OGC) の Well-Known Binary (WKB) 表現を返します。 この値には、インスタンスに格納されている Z 値または M 値が含まれません。
|byte [] serialize ()| Geometry 型の内部 SQL Server 形式を表すバイトを返します。
|boolean hasM()| オブジェクトに M (メジャー) 値が含まれている場合は、を返します。
|ブール値 hasZ ()| オブジェクトに Z (標高) 値が含まれている場合は、を返します。
|Double getX ()| X 座標値を返します。
|二重 getY ()| Y 座標の値を返します。
|Double getM ()| オブジェクトの M (メジャー) 値を返します。
|Double getZ ()| オブジェクトの Z (標高) 値を返します。
|int getSrid()| 空間参照識別子 (SRID) 値を返します。
|boolean isNull()| Geometry オブジェクトが null の場合はを返します。
|int STNumPoints()| Geometry オブジェクト内の点の数を返します。
|String STGeometryType()| geometry インスタンスで表される Open Geospatial Consortium (OGC) の型名を返します。
|String asTextZM()| Geometry オブジェクトの Well-known Text (WKT) 表現を返します。
|文字列 toString ()| Geometry オブジェクトの文字列表現を返します。

### <a name="geography"></a>Geography

|方法|[説明]|
|:------|:----------|
|Geography STGeomFromText (String wkt, int SRID)| インスタンスに格納されている Z (標高) 値と M (メジャー) 値で補完された、Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現からの Geography インスタンス用のコンストラクター。
|Geography STGeomFromWKB(byte[] wkb)| Open Geospatial Consortium (OGC) の Well-Known Binary (WKB) 表現からの Geography インスタンス用のコンストラクター。
|Geography 逆シリアル化 (byte [] wkb)| 空間データの内部 SQL Server 形式からの Geography インスタンスのコンストラクター。
|Geography parse (文字列 wkt)| Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現からの Geography インスタンス用のコンストラクター。 空間参照識別子の既定値は0です。
|Geography point (double lon、double lat、int SRID)| Point インスタンスを経度、緯度、空間参照識別子 (SRID) で表す Geography インスタンス用のコンストラクター。
|String STAsText()| Geography インスタンスにおける Open Geospatial Consortium (OGC) の Well-Known Text (WKT) 表現を返します。 このテキストは、インスタンスに格納されている Z (標高) 値または M (メジャー) 値を含みません。
|byte [] STAsBinary ())| Geography インスタンスにおける Open Geospatial Consortium (OGC) の Well-Known Binary (WKB) 表現を返します。 この値には、インスタンスに格納されている Z 値または M 値が含まれません。
|byte [] serialize ()| Geography 型の内部 SQL Server 形式を表すバイトを返します。
|boolean hasM()| オブジェクトに M (メジャー) 値が含まれている場合は、を返します。
|ブール値 hasZ ()| オブジェクトに Z (標高) 値が含まれている場合は、を返します。
|Double getLatitude ()| 緯度の値を返します。
|Double getLongitude()| 経度の値を返します。
|Double getM ()| オブジェクトの M (メジャー) 値を返します。
|Double getZ ()| オブジェクトの Z (標高) 値を返します。
|int getSrid()| 空間参照識別子 (SRID) 値を返します。
|boolean isNull()| Geography オブジェクトが null の場合、を返します。
|int STNumPoints()| Geography オブジェクト内の点の数を返します。
|String STGeographyType()| geography インスタンスで表される Open Geospatial Consortium (OGC) の型名を返します。
|String asTextZM()| Geography オブジェクトの Well-known Text (WKT) 表現を返します。
|文字列 toString ()| Geography オブジェクトの文字列表現を返します。

## <a name="limitations-of-spatial-datatypes"></a>空間データ型の制限

1. 空間サブデータ型**CircularString**、 **CompoundCurve**、 **Curvepolygon**、および**fullglobe**は、2012以降の SQL Server 以降でのみサポートされます。

2. Always Encrypted を空間データ型と共に使用することはできません。

3. 現在、ストアドプロシージャ、TVP、および BulkCopy 操作は、空間データ型ではサポートされていません。

## <a name="see-also"></a>参照

[空間データ型のサンプル (JDBC)](../../connect/jdbc/spatial-data-types-sample.md)
