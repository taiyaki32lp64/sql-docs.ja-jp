---
title: 高度なデータ型を使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b39461d3-48d6-4048-8300-1a886c00756d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a50bc3e4fae8fe45004374d3dd019a0f65fe544f
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027009"
---
# <a name="using-advanced-data-types"></a>高度なデータ型の使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、JDBC の高度なデータ型を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を Java プログラミング言語によって認識できる形式に変換します。  
  
## <a name="remarks"></a>Remarks

次の表は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、JDBC、および Java プログラミング言語の高度なデータ型間で行われる既定のマッピングを示しています。  
  
|SQL Server 型|JDBC 型 (java.sql.Types)|Java 言語型|  
|----------------------|-----------------------------------|-------------------------|  
|varbinary(max)<br /><br /> image|LONGVARBINARY|byte[] \(既定)、Blob、InputStream、String|  
|text<br /><br /> varchar(max)|LONGVARCHAR|String (既定)、Clob、InputStream|  
|ntext<br /><br /> nvarchar(max)|LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0)|String (既定)、Clob、NClob|  
|xml|LONGVARCHAR<br /><br /> SQLXML|String (既定)、InputStream、Clob、byte[]、Blob、SQLXML|  
|Udt<sup>1</sup>|VARBINARY|String (既定)、byte[]、InputStream|  
|sqlvariant|SQLVARIANT|Object|  
|geometry<br /><br /> geography|VARBINARY|byte[]|  


<sup>1</sup> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では、バイナリ データとしての CLR UDT の送受信をサポートしていますが、CLR メタデータの操作はサポートしていません。  
  
以下のセクションでは、JDBC ドライバーと高度なデータ型の使用方法の例を示します。  
  
## <a name="blob-and-clob-and-nclob-data-types"></a>BLOB、CLOB、および NCLOB データ型

JDBC ドライバーは、java.sql.Blob、java.sql.Clob、および java.sql.NClob インターフェイスのすべてのメソッドを実装しています。  
  
> [!NOTE]  
> CLOB 値は、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (以降) の大きな値のデータ型で使用できます。 具体的には、CLOB 型は**varchar (max)** データ型と**nvarchar (max)** データ型で使用でき、BLOB 型は**varbinary (max)** および**image**データ型と共に使用できます。また、NCLOB types は**ntext**および**nvarchar (max) と共に使用できます。)** .  

## <a name="large-value-data-types"></a>大きな値のデータ型

以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、大きな値のデータ型には特殊な処理が必要でした。 大きな値をとるデータ型とは、最大行サイズが 8 KB を超えるデータ型のことです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、2^31 バイトまでの大きさの値を格納できる、**varchar** データ型、**nvarchar** データ型、**varbinary** データ型用の max 指定子が導入されました。 テーブル列や [!INCLUDE[tsql](../../includes/tsql-md.md)] 変数に、**varchar(max)** データ型、**nvarchar(max)** データ型、または **varbinary(max)** データ型を指定できます。  

大きな値の型を操作する主要なシナリオには、データベースからの取得とデータベースへの追加があります。 以下のセクションでは、これらのタスクを実行するためのさまざまな方法について説明します。  

### <a name="retrieving-large-value-types-from-a-database"></a>データベースからの大きな値の型の取得

**varchar(max)** データ型など、バイナリ以外の大きな値のデータ型をデータベースから取得する場合、方法の 1 つはデータを文字ストリームとして読み取ることです。 以下の例では、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) メソッドを使用してデータベースからデータを取得し、これを結果セットとして返します。 次に、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの [getCharacterStream](../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) メソッドを使用し、大きな値のデータを結果セットから読み取ります。  

```java
ResultSet rs = stmt.executeQuery("SELECT TOP 1 * FROM Test1");  
rs.next();  
Reader reader = rs.getCharacterStream(2);  
```

> [!NOTE]
> この方法は、 **text**、 **ntext**、および**nvarchar (max)** データ型にも使用できます。  

**varbinary(max)** データ型など、バイナリの大きな値のデータ型をデータベースから取得する場合は、いくつかの方法があります。 最も効率的に行うには、次のようにバイナリ ストリームとしてデータを読み取ります。  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
InputStream is = rs.getBinaryStream(2);  
```

また、[getBytes](../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md) メソッドを使用し、次のように byte 配列としてデータを読み取ることもできます。  

```java
ResultSet rs = stmt.executeQuery("SELECT photo FROM mypics");  
rs.next();  
byte [] b = rs.getBytes(2);  
```

> [!NOTE]  
> BLOB としてデータを読み取ることもできます。 ただし、前述の 2 つの方法より効率が下がります。  

### <a name="adding-large-value-types-to-a-database"></a>データベースへの大きな値の型の追加

JDBC ドライバーを使用した大きいデータのアップロードは、メモリ内に収まる場合は、適切に行うことができます。メモリ内に収まらない場合は、ストリームを使用するのが主要なオプションです。 ただし、最も効率的に大きいデータをアップロードするためには、ストリーム インターフェイスを使用します。  

次に示すように、文字列やバイトを使用する方法もあります。  

```java
PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (c1_id, c2_vcmax) VALUES (?, ?)");  
pstmt.setInt(1, 1);  
pstmt.setString(2, htmlStr);  
pstmt.executeUpdate();  
```

> [!NOTE]  
> この方法は、 **text**、 **ntext**、および**nvarchar (max)** 列に格納されている値にも使用できます。  

サーバーにイメージ ライブラリがあり、バイナリ イメージ ファイル全体を **varbinary(max)** 列にアップロードする必要がある場合、JDBC ドライバーで最も効率的にこれを行うには、次に示すようにストリームを直接使用します。  

```java
try (PreparedStatement pstmt = con.prepareStatement("INSERT INTO test1 (Col1, Col2) VALUES(?,?)")) { 
  File inputFile = new File("CLOBFile20mb.jpg");  
  try (FileInputStream inStream = new FileInputStream(inputFile)) {
    int id = 1;  
    pstmt.setInt(1,id);  
    pstmt.setBinaryStream(2, inStream);  
    pstmt.executeUpdate();
  }
}
```

> [!NOTE]  
> CLOB または BLOB メソッドの使用は、大きいデータをアップロードする際に効率的ではありません。  

### <a name="modifying-large-value-types-in-a-database"></a>データベースの大きな値の型の変更

多くの場合、データベース上の大きい値を更新または変更する際は、`UPDATE`、`WRITE`、`SUBSTRING` などの [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを使用して、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスおよび [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラス経由でパラメーターを渡して行うことをお勧めします。  

アーカイブされた HTML ファイルなどの大きいテキスト ファイル内で、ある単語を置き換える必要がある場合は、次のように Clob オブジェクトを使用することができます。  

```java
String SQL = "SELECT * FROM test1;";  
try (Statement stmt = con.createStatement(ResultSet.TYPE_SCROLL_SENSITIVE, ResultSet.CONCUR_UPDATABLE)
     ResultSet rs = stmt.executeQuery(SQL)) {
  rs.next();

  Clob clob = rs.getClob(2);  
  long pos = clob.position("dog", 1);  
  clob.setString(pos, "cat");  
  rs.updateClob(2, clob);  
  rs.updateRow();  
}
```

また、すべての作業をサーバー上で行い、準備された UPDATE ステートメントにパラメーターを渡すこともできます。  

大きな値の型の詳細については、SQL Server オンライン ブックの「大きな値をとるデータ型の使用」を参照してください。  

## <a name="xml-data-type"></a>XML データ型

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、XML ドキュメントとフラグメントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納できる **xml** データ型を提供します。 **xml** データ型は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での組み込みデータ型の 1 つであり、**int** や **varchar** などの他の組み込みデータ型といくつかの点で似ています。 他の組み込み型と同様に、**xml** データ型は、テーブルの作成時に列型として使用したり、変数の型やパラメーターの型、関数の戻り値の型として使用したり、[!INCLUDE[tsql](../../includes/tsql-md.md)] CAST や CONVERT 関数内で使用したりすることができます。  
  
JDBC ドライバーでは、**xml** データ型は、文字列、byte 配列、ストリーム、CLOB、BLOB、または SQLXML オブジェクトとしてマップできます。 文字列が既定値です。 JDBC Driver Version 2.0 以降では、SQLXML インターフェイスを導入した JDBC 4.0 API がサポートされます。 SQLXML インターフェイスには、XML データを操作するための各種のメソッドが定義されています。 **SQLXML**データ型は、 **xml**データ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]型にマップされます。 **SQLXML** Java データ型を使用して、リレーショナル データベースから XML データを読み取ったり、リレーショナル データベースに XML データを書き込んだりする方法については、「[XML データのサポート](../../connect/jdbc/supporting-xml-data.md)」を参照してください。  
  
JDBC ドライバーにおける **xml** データ型の実装では、以下の操作がサポートされます。  
  
- 最も一般的なプログラミング シナリオに対し、標準 Java UTF-16 文字列として XML にアクセスできます。  
  
- UTF-8 および他の 8 ビットでエンコードされた XML を入力できます。  
  
- 他の XML プロセッサやディスク ファイルとのやり取りのために UTF-16 でエンコードされている場合、先頭に BOM の付いた byte 配列として XML にアクセスできます。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、UTF-16 でエンコードされた XML に対しては先頭の BOM が必要です。 XML パラメーターの値がバイト配列として指定されている場合は、アプリケーションでこれを提供する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、常に BOM または埋め込みエンコード宣言のない UTF-16 文字列として XML 値を出力します。 XML 値が byte[]、BinaryStream、または Blob として取得される場合、UTF-16 BOM が値の前に付いています。  
  
**xml** データ型の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「xml データ型」を参照してください。  
  
## <a name="user-defined-data-type"></a>ユーザー定義データ型  

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] にユーザー定義型 (UDT) が導入されたことにより、オブジェクトやカスタム データ構造を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに格納できるため、SQL 型システムを拡張することができます。 UDT は複数のデータ型を持つことができ、動作を定義できます。この点は、1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム データ型から構成される従来の別名データ型と異なります。 UDT は、検証可能なコードを生成する、Microsoft .NET 共通言語ランタイム (CLR) によってサポートされている任意の言語を使用して定義されます。 その言語には、Microsoft Visual C# および Visual Basic .NET が含まれます。 データは .NET Framework ベースのクラスまたは構造体のフィールドとプロパティとして公開され、動作はクラスまたは構造体のメソッドによって定義されます。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、UDT をテーブルの列定義、[!INCLUDE[tsql](../../includes/tsql-md.md)] バッチの変数、または [!INCLUDE[tsql](../../includes/tsql-md.md)] の関数やストアド プロシージャの引数として使用できます。  
  
ユーザー定義データ型の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「ユーザー定義型のインスタンスの使用と変更」を参照してください。  
  
## <a name="sql_variant-data-type"></a>Sql_variant データ型

Sql_variant データ型の詳細については、「 [sql_variant データ型の使用](../../connect/jdbc/using-sql-variant-datatype.md)」を参照してください。  

## <a name="spatial-data-types"></a>空間データ型

空間データ型の詳細については、「空間データ型の[使用](../../connect/jdbc/use-spatial-datatypes.md)」を参照してください。  

## <a name="see-also"></a>参照

[JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
