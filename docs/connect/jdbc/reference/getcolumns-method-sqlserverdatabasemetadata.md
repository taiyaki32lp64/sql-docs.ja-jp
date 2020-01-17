---
title: getColumns メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f173fa5d-e114-4a37-a5c4-2baad9ff3af1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d34f5748a5a85d67754ea9a001ba1819935e53a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952837"
---
# <a name="getcolumns-method-sqlserverdatabasemetadata"></a>getColumns メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたカタログで使用できるテーブル列の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getColumns(java.lang.String catalog,  
                                     java.lang.String schema,  
                                     java.lang.String table,  
                                     java.lang.String col)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 カタログ名を含む**文字列**です。  
  
 *schema*  
  
 スキーマ名のパターンを含む**文字列**です。  
  
 *テーブル*  
  
 テーブル名のパターンを含む**文字列**です。  
  
 *col*  
  
 列名のパターンを含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getColumns メソッドは、java.sql.DatabaseMetaData インターフェイスの getColumns メソッドで規定されています。  
  
 getColumns メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|カタログ名。|  
|TABLE_SCHEM|**String**|テーブル スキーマ名です。|  
|TABLE_NAME|**String**|テーブル名。|  
|COLUMN_NAME|**String**|列名。|  
|DATA_TYPE|**smallint**|java.sql.Types の SQL データ型です。|  
|TYPE_NAME|**String**|データ型の名前です。|  
|COLUMN_SIZE|**int**|列の完全桁数です。|  
|BUFFER_LENGTH|**smallint**|データの転送サイズです。|  
|DECIMAL_DIGITS|**smallint**|列の小数点以下の桁数です。|  
|NUM_PREC_RADIX|**smallint**|列の基数です。|  
|NULLABLE|**smallint**|列が null を許容するかどうかを示します。 次のいずれかの値を指定できます。<br /><br /> columnNoNulls (0)<br /><br /> columnNullable (1)|  
|REMARKS|**String**|列に関連付けられているコメントです。<br /><br /> **注:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、この列に対して常に null が返されます。|  
|COLUMN_DEF|**String**|列の既定値です。|  
|SQL_DATA_TYPE|**smallint**|記述子の TYPE フィールドでの SQL データ型の値です。 datetime データ型と SQL-92 interval データ型以外は、DATA_TYPE 列と同じです。 この列は常に値が返されます。|  
|SQL_DATETIME_SUB|**smallint**|datetime および SQL-92 interval データ型のサブタイプ コードです。 他のデータ型の場合、この列は NULL を返します。|  
|CHAR_OCTET_LENGTH|**int**|列の最大バイト数です。|  
|ORDINAL_POSITION|**int**|テーブル内の列のインデックスです。|  
|IS_NULLABLE|**String**|列で null 値が許容されるかどうかを示します。|  
|SS_IS_SPARSE|**smallint**|列がスパース列の場合は 1、それ以外の場合は 0 になります。<sup>1</sup>|  
|SS_IS_COLUMN_SET|**smallint**|列がスパース column_set 列の場合は 1、それ以外の場合は 0 になります。 <sup>1</sup>|  
|SS_IS_COMPUTED|**smallint**|TABLE_TYPE の列が計算列であるかどうかを示します。 <sup>1</sup>|  
|IS_AUTOINCREMENT|**String**|列が自動インクリメントされる場合は "YES" です。 列が自動インクリメントされない場合は "NO" です。 列が自動インクリメントされるかどうかをドライバーが判断できない場合は "" (空の文字列) です。 <sup>1</sup>|  
|SS_UDT_CATALOG_NAME|**String**|UDT (ユーザー定義型) を含むカタログの名前です。 <sup>1</sup>|  
|SS_UDT_SCHEMA_NAME|**String**|UDT (ユーザー定義型) を含むスキーマの名前です。 <sup>1</sup>|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|完全修飾名の UDT (ユーザー定義型) です。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML スキーマ コレクション名が定義されているカタログの名前です。 カタログ名が見つからない場合は、この変数に空文字列が含まれます。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|XML スキーマ コレクション名が定義されているスキーマの名前です。 スキーマ名が見つからない場合は、空文字列です。 <sup>1</sup>|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|XML スキーマ コレクションの名前です。 名前が見つからない場合は、空文字列です。 <sup>1</sup>|  
|SS_DATA_TYPE|**tinyint**|拡張ストアド プロシージャによって使用される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型です。<br /><br /> **注** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって返されるデータ型の詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「データ型 (Transact-SQL)」を参照してください。|  
  
 (1) [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] に接続している場合、この列はありません。  
  
> [!NOTE]  
>  getColumns メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_columns (Transact-SQL)」を参照してください。  
  
 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 では、次の動作が以前のバージョンの JDBC Driver から変更されています。  
  
 DATA_TYPE 列には、次の変更点があります。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型|JDBC Driver 2.0 (または、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] に接続されている場合) での戻り値の型と関連付けられている数値定数|[!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] 以降に接続されている場合の JDBC Driver 3.0 での戻り値の型と関連付けられている数値定数|  
|-------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|  
|8 KB を超えるユーザー定義型|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geography|LONGVARBINARY (-4)|VARBINARY (-3)|  
|geometry|LONGVARBINARY (-4)|VARBINARY (-3)|  
|varbinary(max)|LONGVARBINARY (-4)|VARBINARY (-3)|  
|nvarchar(max)|LONGVARCHAR (-1) または LONGNVARCHAR (JDBC 4) (-16)|VARCHAR (12) または NVARCHAR (JDBC 4) (-9)|  
|varchar(max)|LONGVARCHAR (-1)|VARCHAR (12)|  
|time|VARCHAR (12) または NVARCHAR (JDBC 4) (-9)|TIME (-154)|  
|date|VARCHAR (12) または NVARCHAR (JDBC 4) (-9)|DATE (91)|  
|datetime2|VARCHAR (12) または NVARCHAR (JDBC 4) (-9)|TIMESTAMP (93)|  
|datetimeoffset|VARCHAR (12) または NVARCHAR (JDBC 4) (-9)|microsoft.sql.Types.DATETIMEOFFSET (-155)|  
  
 COLUMN_SIZE 列には、次の変更点があります。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型|JDBC Driver 2.0 での戻り値の型|JDBC Driver 3.0 での戻り値の型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|nvarchar(max)|1073741823|2147483647 (データベースのメタデータ)|  
|xml|1073741823|2147483647 (データベースのメタデータ)|  
|8 KB 以下のユーザー定義型|8 KB (結果セットとパラメーターのメタデータ)|ストアド プロシージャによって返される実際のサイズです。|  
|time||この型の文字列表記の長さ (文字数) です (秒部分に許容される最大有効桁数を想定)。|  
|date||time と同じです。|  
|datetime2||time と同じです。|  
|datetimeoffset||time と同じです。|  
  
 BUFFER_LENGTH 列には、次の変更点があります。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型|JDBC Driver 2.0 での戻り値の型|JDBC Driver 3.0 での戻り値の型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|8 KB を超えるユーザー定義型||2147483647|  
  
 TYPE_NAME 列には、次の変更点があります。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型|JDBC Driver 2.0 での戻り値の型|JDBC Driver 3.0 での戻り値の型|  
|-------------------------------------------------------------------|------------------------------------|------------------------------------|  
|varchar(max)|text|varchar|  
|varbinary(max)|image|varbinary|  
  
 DECIMAL_DIGITS 列には、次の変更点があります。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の型|JDBC Driver 2.0|JDBC Driver 3.0|  
|--------------------------------------------------------------|---------------------|---------------------|  
|time|null|7 (または、指定した場合はそれより少なくなります)|  
|date|null|null|  
|datetime2|null|7 (または、指定した場合はそれより少なくなります)|  
|datetimeoffset|null|7 (または、指定した場合はそれより少なくなります)|  
  
 SQL_DATA_TYPE 列には、次の変更点があります。  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型|JDBC Driver 2.0 での [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 のデータ値|JDBC Driver 3.0 での [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2008 のデータ値|  
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|  
|varchar(max)|-10|-9|  
|nvarchar(max)|-1|-9|  
|xml|-10|-152|  
|8 KB 以下のユーザー定義型|-3|-151|  
|8 KB を超えるユーザー定義型|JDBC Driver 2.0 では使用できません。|-151|  
|geography|-4|-151|  
|geometry|-4|-151|  
|hierarchyid|-4|-151|  
|time|-9|92|  
|date|-9|91|  
|datetime2|-9|93|  
|datetimeoffset|-9|-155|  
  
## <a name="example"></a>例  
 次の例では、getColumns メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースにある Person.Contact テーブルの情報を返す方法を示します。  
  
```  
import java.sql.*;  
public class c1 {  
   public static void main(String[] args) {  
      String connectionUrl = "jdbc:sqlserver://localhost:1433;databaseName=AdventureWorks;integratedsecurity=true";  
  
      Connection con = null;  
      Statement stmt = null;  
      ResultSet rs = null;  
  
      try {  
         Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");  
         con = DriverManager.getConnection(connectionUrl);  
         DatabaseMetaData dbmd = con.getMetaData();  
         rs = dbmd.getColumns("AdventureWorks", "Person", "Contact", "FirstName");  
  
         ResultSet r = dbmd.getColumns(null, null, "Contact", null);  
         ResultSetMetaData rm = r.getMetaData();   
         int noofcols = rm.getColumnCount();  
  
         if (r.next())  
            for (int i = 0 ; i < noofcols ; i++ )  
            System.out.println(rm.getColumnName( i + 1 ) + ": \t\t" + r.getString( i + 1 ));  
      }  
  
      catch (Exception e) {}  
      finally {}  
   }  
}  
```  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
