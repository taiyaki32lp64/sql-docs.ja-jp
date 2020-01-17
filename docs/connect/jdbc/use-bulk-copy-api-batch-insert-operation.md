---
title: MSSQL JDBC Driver で一括コピー API を使用してバッチ挿入操作を実行する |Microsoft Docs
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
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027103"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>バッチ挿入操作に一括コピー API を使用する

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 for SQL Server は、Azure Data Warehouse に対する一括コピー API の使用をサポートしています。 この機能を使用すると、バッチ挿入操作の実行時にドライバーが一括コピー操作を実行できるようになります。 ドライバーは、通常のバッチ挿入操作と同じデータを挿入するときに、パフォーマンスを向上させることを目的としています。 ドライバーは、通常のバッチ挿入操作の代わりに、一括コピー API を利用して、ユーザーの SQL クエリを解析します。 バッチ挿入機能の一括コピー API とその制限事項の一覧を有効にするためのさまざまな方法を以下に示します。 このページには、使用状況とパフォーマンスの向上を示す小さなサンプルコードも含まれています。

この機能は、PreparedStatement および callablestatement の`executeBatch()`  &  `executeLargeBatch()` api にのみ適用されます。

## <a name="prerequisites"></a>Prerequisites

一括コピー API を有効にするには、次の2つの前提条件があります。

* サーバーは Azure Data Warehouse である必要があります。
* クエリは挿入クエリである必要があります (クエリにはコメントが含まれている場合がありますが、この機能を有効にするには、クエリの先頭に INSERT キーワードを使用する必要があります)。

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>バッチ挿入用の一括コピー API の有効化

一括コピー API を有効にするには、次の3つの方法があります。

### <a name="1-enabling-with-connection-property"></a>1.接続プロパティを使用した有効化

**Usebulkcopyforbatchinsert = true;** を接続文字列に追加すると、この機能が有効になります。

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2.SQLServerConnection オブジェクトから setUseBulkCopyForBatchInsert () メソッドを使用して有効にする

**SQLServerConnection を**呼び出すと、この機能が有効になります。

SQLServerConnection は、 **usebulkcopyforbatchinsert**接続プロパティの現在の値を取得し**ます。**

**Usebulkcopyforbatchinsert**の値は、初期化時に PreparedStatement ごとに変わりません。 後続の SQLServerConnection の呼び出しは、その値に関して、既に作成された PreparedStatement には影響しません **。**

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3.SQLServerDataSource オブジェクトから setUseBulkCopyForBatchInsert () メソッドを使用して有効にする

上記と同様ですが、SQLServerDataSource を使用して SQLServerConnection オブジェクトを作成します。 どちらの方法も、同じ結果が得られます。

## <a name="known-limitations"></a>既知の制限事項

現在、この機能に適用される制限事項があります。

* パラメーター化されていない値 (など`INSERT INTO TABLE VALUES (?, 2`) を含む Insert クエリはサポートされていません。 この関数でサポートされているパラメーターは、ワイルドカード (?) だけです。
* 挿入選択式 (など`INSERT INTO TABLE SELECT * FROM TABLE2`) を含む insert クエリはサポートされていません。
* 複数の値式 (など`INSERT INTO TABLE VALUES (1, 2) (3, 4)`) を含む Insert クエリはサポートされていません。
* OPTION 句が後に続く Insert クエリ、複数のテーブルと結合されたクエリ、または別のクエリの後に続く挿入クエリはサポートされていません。
* 一括コピー API `MONEY` `SMALLMONEY` `DATE`の制限`GEOGRAPHY`により、、、、、、、、、およびの各データ型は現在、この場合はサポートされていません。 `DATETIME` `DATETIMEOFFSET` `SMALLDATETIME` `TIME` `GEOMETRY`機能.

"SQL server" に関連するエラーがないためにクエリが失敗した場合、ドライバーはエラーメッセージをログに記録し、バッチ挿入の元のロジックにフォールバックします。

## <a name="example"></a>例

次に示すのは、(通常の一括コピー API) シナリオで、1000行の Azure DW に対するバッチ挿入操作のユースケースを示すコード例です。

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

結果:

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>参照

[JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
