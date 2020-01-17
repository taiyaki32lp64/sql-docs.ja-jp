---
title: 基本データ型を使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: abbd2aa3c277ad36f419de849b02433f17d27403
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026509"
---
# <a name="using-basic-data-types"></a>基本データ型の使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、JDBC の基本データ型を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を Java プログラミング言語によって認識できる形式に変換します。この逆の変換も行います。 JDBC ドライバー は **SQLXML** データ型を含む JDBC 4.0 api および **NCHAR**、 **NVARCHAR**、 **LONGNVARCHAR**、そして **NCLOB** のような National (Unicode) データ型のサポートを提供します。  
  
## <a name="data-type-mappings"></a>データ型マッピング

次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC、および Java プログラミング言語の基本データ型間で行われる既定のマッピングを示しています。  
  
| SQL Server 型   | JDBC 型 (java.sql.Types)                        | Java 言語型          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| binary             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | String                       |
| date               | DATE                                               | java.sql.Date                |
| DATETIME           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset (2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| Decimal            | DECIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| image              | LONGVARBINARY                                      | byte[]                       |
| INT                | INTEGER                                            | INT                          |
| money              | DECIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | String                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String                       |
| NUMERIC            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | String                       |
| REAL               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| SMALLMONEY         | DECIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | String                       |
| time               | TIME (1)                                           | java.sql.Time (1)            |
| TIMESTAMP          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | String                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | String                       |
| varchar(max)       | VARCHAR                                            | String                       |
| xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | String<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Object                       |
| geometry           | VARBINARY                                          | byte[]                       |
| geography          | VARBINARY                                          | byte[]                       |
  
(1) 時刻の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を持つ java.sql.Time を使用する場合は、**sendTimeAsDatetime** 接続プロパティを false に設定します。  
  
(2) **datetimeoffset** の値には、 [datetimeoffset クラス](../../connect/jdbc/reference/datetimeoffset-class.md)を使用してプログラムでアクセスできます。  
  
以下のセクションでは、JDBC ドライバーと基本データ型の使用方法の例を示します。 Java アプリケーションの基本データ型の使用方法の詳細例については、「[基本データ型のサンプル](../../connect/jdbc/basic-data-types-sample.md)」をご覧ください。  
  
## <a name="retrieving-data-as-a-string"></a>文字列としてのデータの取得

文字列として参照するために JDBC 基本データ型にマップされるデータ ソースからデータを取得する必要がある場合、または厳密に型指定されたデータを必要としない場合は、次のように [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) メソッドを使用できます。  
  
[!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>データ型によるデータの取得

データ ソースからデータを取得する必要があり、取得するデータの型がわかっている場合は、SQLServerResultSet クラスのいずれかの get\<Type> メソッドを使用します。これらは、"*getter メソッド*" とも呼ばれます。 get\<Type> メソッドでは、次のように列名または列インデックスを使用できます。  
  
[!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> Scale メソッドを使用した getUnicodeStream および getBigDecimal は非推奨とされており、JDBC ドライバーではサポートされていません。

## <a name="updating-data-by-data-type"></a>データ型によるデータの更新

データソースのフィールドの値を更新する必要がある場合は、SQLServerResultSet クラスのいずれか\<の更新の種類 > メソッドを使用します。 次の例では、[updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md) メソッドを [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) メソッドと組み合わせて使用し、データ ソース内のデータを更新します。  
  
[!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> JDBC ドライバーは、127 文字を超える列名の SQL Server の列を更新できません。 列名が 127 文字を超える列を更新しようとすると、例外がスローされます。  
  
## <a name="updating-data-by-parameterized-query"></a>パラメーター化クエリによるデータの更新

パラメーター化クエリを使用してデータ ソースのデータを更新する必要がある場合は、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスのいずれかの set\<Type> メソッドを使用して、パラメーターのデータ型を設定できます。これらは、"*setter メソッド*" とも呼ばれます。 次の例では、[prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md) メソッドを使用して、パラメーター化クエリをプリコンパイルし、[setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md) メソッドを使用してパラメーターの文字列値を設定してから、[executeUpdate](../../connect/jdbc/reference/executeupdate-method.md) メソッドを呼び出します。  
  
[!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
パラメーター化されたクエリの詳細については、「パラメーターを使用し[た SQL ステートメントの使用](../../connect/jdbc/using-an-sql-statement-with-parameters.md)」を参照してください。  

## <a name="passing-parameters-to-a-stored-procedure"></a>ストアド プロシージャにパラメーターを渡す

入力されたパラメーターをストアド プロシージャに渡す必要がある場合は、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスのいずれかの set\<Type> メソッドを使用して、インデックスまたは名前でパラメーターを設定できます。 次の例では、[prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) メソッドを使用してストアド プロシージャへの呼び出しを設定し、[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) メソッドを使用して呼び出し用のパラメーターを設定してから、[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) メソッドを呼び出します。  
  
[!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> この例では、結果セットはストアド プロシージャの実行結果で返されます。

ストアドプロシージャおよび入力パラメーターと共に JDBC ドライバーを使用する方法の詳細については、「[入力パラメーターを](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)使用したストアドプロシージャの使用」を参照してください。  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>ストアド プロシージャからのパラメーターの取得

ストアド プロシージャからパラメーターを取得する必要がある場合は、まず SQLServerCallableStatement クラスの [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) メソッドを使用して名前またはインデックスで out パラメーターを登録し、ストアド プロシージャへの呼び出しを実行してから、返された out パラメーターを適切な変数に割り当てる必要があります。 次の例では、prepareCall メソッドを使用してストアド プロシージャへの呼び出しを設定し、registerOutParameter メソッドを使用して out パラメーターを設定します。次に、[setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md) メソッドを使用して呼び出し用のパラメーターを設定してから、executeQuery メソッドを呼び出します。 ストアド プロシージャの out パラメーターによって返される値は、[getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md) メソッドを使用して取得します。  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> out パラメーターが返されるだけでなく、ストアド プロシージャの実行結果により作成された結果セットが返されることもあります。  
  
JDBC driver とストアドプロシージャおよび出力パラメーターを使用する方法の詳細については、「 [output パラメーターを](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)使用したストアドプロシージャの使用」を参照してください。  

## <a name="see-also"></a>参照

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
