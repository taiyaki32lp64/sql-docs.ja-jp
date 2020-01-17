---
title: スパース列 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7d4237e0-818f-4639-9093-d5ac9683fc71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 328b25b4494ff69368147c9369a0949f3094108f
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027723"
---
# <a name="sparse-columns"></a>スパース列

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

スパース列は、NULL 値用にストレージが最適化されている通常の列です。 スパース列によって、NULL 以外の値を取得するためのオーバーヘッドは増大しますが、NULL 値に必要となる領域は削減されます。 少なくとも 20 ～ 40% の領域を削減できる場合は、スパース列の使用を検討してください。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0 では、[!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] (以降) のサーバーに接続する場合、スパース列がサポートされます。 スパース列および列セットの列を特定するために、[SQLServerDatabaseMetaData.getColumns](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md)、[SQLServerDatabaseMetaData.getFunctionColumns](../../connect/jdbc/reference/getfunctioncolumns-method-sqlserverdatabasemetadata.md)、または [SQLServerDatabaseMetaData.getProcedureColumns](../../connect/jdbc/reference/getprocedurecolumns-method-sqlserverdatabasemetadata.md) を使用できます。

このサンプルのコード ファイルは SparseColumns.java という名前で、次の場所にあります。  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\sparse  
```

列セットは、すべてのスパース列を型指定されていない XML 形式で返す計算列です。 テーブルに多数の列 (1,024 を超える列) があるか、個別のスパース列の操作が煩雑である場合は、列セットの使用を検討してください。 列セットには、最大で 30,000 列を含めることができます。

## <a name="example"></a>例

### <a name="description"></a>[説明]

このサンプルでは、列セットの検出方法を示します。 また、列セットの XML 出力を解析して、スパース列からデータを取得する方法も示します。

コード リストは Java ソース コードです。 アプリケーションをコンパイルする前に、接続文字列を変更します。

### <a name="code"></a>コード

```java
import java.io.StringReader;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.ResultSetMetaData;
import java.sql.SQLException;
import java.sql.Statement;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;

import org.w3c.dom.Document;
import org.w3c.dom.Node;
import org.w3c.dom.NodeList;
import org.xml.sax.InputSource;


public class SparseColumns {

    public static void main(String args[]) {

        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(connectionUrl); Statement stmt = con.createStatement()) {

            createColdCallingTable(stmt);

            // Determine the column set column
            String columnSetColName = null;
            String strCmd = "SELECT name FROM sys.columns WHERE object_id=(SELECT OBJECT_ID('ColdCalling')) AND is_column_set = 1";

            try (ResultSet rs = stmt.executeQuery(strCmd)) {
                if (rs.next()) {
                    columnSetColName = rs.getString(1);
                    System.out.println(columnSetColName + " is the column set column!");
                }
            }

            strCmd = "SELECT * FROM ColdCalling";
            try (ResultSet rs = stmt.executeQuery(strCmd)) {

                // Iterate through the result set
                ResultSetMetaData rsmd = rs.getMetaData();

                DocumentBuilderFactory dbf = DocumentBuilderFactory.newInstance();
                DocumentBuilder db = dbf.newDocumentBuilder();
                InputSource is = new InputSource();
                while (rs.next()) {
                    // Iterate through the columns
                    for (int i = 1; i <= rsmd.getColumnCount(); ++i) {
                        String name = rsmd.getColumnName(i);
                        String value = rs.getString(i);

                        // If this is the column set column
                        if (name.equalsIgnoreCase(columnSetColName)) {
                            System.out.println(name);

                            // Instead of printing the raw XML, parse it
                            if (value != null) {
                                // Add artificial root node "sparse" to ensure XML is well formed
                                String xml = "<sparse>" + value + "</sparse>";

                                is.setCharacterStream(new StringReader(xml));
                                Document doc = db.parse(is);

                                // Extract the NodeList from the artificial root node that was added
                                NodeList list = doc.getChildNodes();
                                Node root = list.item(0); // This is the <sparse> node
                                NodeList sparseColumnList = root.getChildNodes(); // These are the xml column nodes

                                // Iterate through the XML document
                                for (int n = 0; n < sparseColumnList.getLength(); ++n) {
                                    Node sparseColumnNode = sparseColumnList.item(n);
                                    String columnName = sparseColumnNode.getNodeName();
                                    // The column value is not in the sparseColumNode, it is the value of the
                                    // first child of it
                                    Node sparseColumnValueNode = sparseColumnNode.getFirstChild();
                                    String columnValue = sparseColumnValueNode.getNodeValue();

                                    System.out.println("\t" + columnName + "\t: " + columnValue);
                                }
                            }
                        } else { // Just print the name + value of non-sparse columns
                            System.out.println(name + "\t: " + value);
                        }
                    }
                    System.out.println();// New line between rows
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static void createColdCallingTable(Statement stmt) throws SQLException {
        stmt.execute("if exists (select * from sys.objects where name = 'ColdCalling')" + "drop table ColdCalling");

        String sql = "CREATE TABLE ColdCalling  (  ID int IDENTITY(1,1) PRIMARY KEY,  [Date] date,  [Time] time,  PositiveFirstName nvarchar(50) SPARSE,  PositiveLastName nvarchar(50) SPARSE,  SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS  );";
        stmt.execute(sql);

        sql = "INSERT ColdCalling ([Date], [Time])  VALUES ('10-13-09','07:05:24')  ";
        stmt.execute(sql);

        sql = "INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  VALUES ('07-20-09','05:00:24', 'AA', 'B')  ";
        stmt.execute(sql);

        sql = "INSERT ColdCalling ([Date], [Time], PositiveFirstName, PositiveLastName)  VALUES ('07-20-09','05:15:00', 'CC', 'DD')  ";
        stmt.execute(sql);
    }
}

```

## <a name="see-also"></a>参照

[JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
