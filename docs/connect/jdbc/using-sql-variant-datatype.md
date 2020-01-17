---
title: 使用して Sql_variant データ型 |Microsoft Docs
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
ms.openlocfilehash: cdede5d41d5ad7fc22cfed3f1efa9f95612032ca
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025843"
---
# <a name="using-sql_variant-data-type"></a>Sql_variant データ型の使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

バージョン6.3.0 の場合、JDBC driver は sql_variant データ型をサポートします。 Sql_variant は、このページで後ほど説明するいくつかの制限付きで、テーブル値パラメーターや BulkCopy などの機能を使用する場合にもサポートされます。 すべてのデータ型を sql_variant データ型に格納することはできません。 Sql_variant でサポートされているデータ型の一覧については、SQL Server の[ドキュメント](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql)を確認してください。

##  <a name="populating-and-retrieving-a-table"></a>テーブルの設定と取得:
次のように sql_variant 列を含むテーブルがあると仮定します。

```sql
CREATE TABLE sampleTable (col1 sql_variant)  
```

ステートメントを使用して値を挿入するサンプルスクリプトを次に示します。

```java
try (Statement stmt = connection.createStatement()){
    stmt.execute("insert into sampleTable values (1)");
}
```

準備されたステートメントを使用した値の挿入:

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into sampleTable values (?)")) {
    preparedStatement.setObject(1, 1);  
    preparedStatement.execute();
}
```      

渡されるデータの基になる型がわかっている場合は、それぞれの setter を使用できます。 たとえば、 `preparedStatement.setInt()`は整数値を挿入するときに使用できます。

```java
try (PreparedStatement preparedStatement = con.prepareStatement("insert into table values (?)")) {
    preparedStatement.setInt (1, 1);
    preparedStatement.execute();
}
```

テーブルから値を読み取るために、それぞれの getter を使用できます。 たとえば、 `getInt()`または`getString()`メソッドは、サーバーからの値がわかっている場合に使用できます。    

```java
try (SQLServerResultSet resultSet = (SQLServerResultSet) stmt.executeQuery("select * from sampleTable ")) {
    resultSet.next();          
    resultSet.getInt(1); //or rs.getString(1); or rs.getObject(1);
}
```

## <a name="using-stored-procedures-with-sql_variant"></a>Sql_variant でストアドプロシージャを使用する:   
次のようなストアドプロシージャがあるとします。     

```java
String sql = "CREATE PROCEDURE " + inputProc + " @p0 sql_variant OUTPUT AS SELECT TOP 1 @p0=col1 FROM sampleTable ";
``` 
    
出力パラメーターを登録する必要があります:

```java
try (CallableStatement callableStatement = con.prepareCall(" {call " + inputProc + " (?) }")) {
    callableStatement.registerOutParameter(1, microsoft.sql.Types.SQL_VARIANT);      
    callableStatement.execute();
}
```

## <a name="limitations-of-sql_variant"></a>Sql_variant の制限事項は次のとおりです。
- Tvp を使用して、sql_variant に格納`datetime`されている`date`値をテーブル`getDateTime()` `getSmallDateTime()` / `smalldatetime` /に設定し、を呼び出す/場合 / `getDate()`ResultSet は動作せず、次の例外をスローします。
    
    `Java.lang.String cannot be cast to java.sql.Timestamp`
   
    回避策: `getString()`代わり`getObject()`にまたはを使用します。 
    
- TVP を使用してテーブルにデータを入力し、sql_variant で null 値を送信することはサポートされていません。例外がスローされます。
    
    `Inserting null value with column type sql_variant in TVP is not supported.`

## <a name="see-also"></a>参照

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
