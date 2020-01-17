---
title: UseFmtOnly | を使用した ParameterMetaData の取得Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 6877a6421622ab52a92b89502c68f47c4c315d93
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025503"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>UseFmtOnly を使用した ParameterMetaData の取得
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Microsoft JDBC Driver for SQL Server には、サーバー **useFmtOnly**からパラメーターメタデータをクエリするための別の方法が含まれています。 この機能は、ドライバーのバージョン7.4 で初めて導入されたものであり、の既知の`sp_describe_undeclared_parameters`問題に対する回避策として必要です。
  
  ドライバーは、主にストアドプロシージャ`sp_describe_undeclared_parameters`を使用してパラメーターメタデータを照会します。これは、ほとんどの状況でパラメーターメタデータを取得する場合に推奨される方法であるためです。 ただし、現在、ストアドプロシージャの実行は次のユースケースでは失敗します。
  
-   Always Encrypted の列に対して
  
-   一時テーブルとテーブル変数に対して
  
-   ビューに対して 
  
  これらのユースケースに関して提案されているソリューションは、ユーザーの SQL クエリでパラメーターとテーブルターゲット`SELECT`を解析`FMTONLY`し、有効になっているクエリを実行することです。 次のスニペットを使用すると、機能を視覚化できます。
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>機能のオン/オフの切り替え 
 機能**useFmtOnly**は既定ではオフになっています。 ユーザーは、を指定`useFmtOnly=true`することで、接続文字列を使用してこの機能を有効にすることができます。 例: `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`」を参照してください。
 
 または、を通じて`SQLServerDataSource`機能を使用することもできます。
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 この機能は、ステートメントレベルでも使用できます。 ユーザーは、を使用して`PreparedStatement.setUseFmtOnly(boolean)`機能のオン/オフを切り替えることができます。
> [!NOTE]  
>  ドライバーは、"接続レベル" プロパティに対してステートメントレベルプロパティの優先順位を設定します。

## <a name="using-the-feature"></a>機能の使用
  有効にすると、ドライバーは、パラメーターの`sp_describe_undeclared_parameters`メタデータを照会するときではなく、新しい機能の使用を内部で開始します。 エンドユーザーがこれ以上操作を行う必要はありません。
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  この機能は、 `SELECT/INSERT/UPDATE/DELETE`クエリのみをサポートしています。 クエリは、サポートされている4つのキーワード、またはサポートされているいずれかのクエリの後にある[共通テーブル式](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017)のいずれかで開始する必要があります。 共通テーブル式内のパラメーターはサポートされていません。

## <a name="known-issues"></a>既知の問題
  現在、機能には、SQL の解析ロジックの欠陥が原因である問題がいくつかあります。 これらの問題は、今後の機能の更新で解決される場合があります。また、以下の説明は、回避策の提案と共に記載されています。
  
A. ' Forward 宣言 ' エイリアスを使用しています
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. テーブルに共有列名がある場合、列名があいまいです
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. パラメーターを使用してサブクエリから選択する
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. SET 句でのサブクエリ
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>参照  
 [接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
