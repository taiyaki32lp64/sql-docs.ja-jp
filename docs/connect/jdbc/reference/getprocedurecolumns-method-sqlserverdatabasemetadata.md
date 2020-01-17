---
title: getProcedureColumns メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedureColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f0df8fe-3cd6-46e4-ae3c-dc23c35676b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1767519cc2f36bac4a70da84efeb8da9e2a1ec3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980754"
---
# <a name="getprocedurecolumns-method-sqlserverdatabasemetadata"></a>getProcedureColumns メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ストアド プロシージャのパラメーターと結果列の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getProcedureColumns(java.lang.String sCatalog,  
                                              java.lang.String sSchema,  
                                              java.lang.String proc,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCatalog*  
  
 カタログ名を含む**文字列**です。 このパラメーターに null を指定すると、カタログ名を使用する必要はありません。  
  
 *sSchema*  
  
 スキーマ名のパターンを含む**文字列**です。 このパラメーターに null を指定すると、スキーマ名を使用する必要はありません。  
  
 *proc*  
  
 プロシージャ名のパターンを含む**文字列**です。  
  
 *col*  
  
 列名のパターンを含む**文字列**です。 このパラメーターに null を指定すると、各列の行が返されます。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この Sqlserverdatabasemetadata.getprocedurecolumns メソッドは、Sqlserverdatabasemetadata.getprocedurecolumns メソッドによって、java メタデータインターフェイスで指定されます。  
  
 getProcedureColumns メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|指定したストアド プロシージャが存在するデータベースの名前です。|  
|PROCEDURE_SCHEM|**String**|ストアド プロシージャのスキーマです。|  
|PROCEDURE_NAME|**String**|ストアド プロシージャの名前です。|  
|COLUMN_NAME|**String**|列の名前です。|  
|COLUMN_TYPE|**short**|列の型。 次のいずれかの値を指定できます。<br /><br /> procedureColumnUnknown (0)<br /><br /> procedureColumnIn (1)<br /><br /> procedureColumnInOut (2)<br /><br /> procedureColumnOut (4)<br /><br /> procedureColumnReturn (5)<br /><br /> procedureColumnResult (3)|  
|DATA_TYPE|**smallint**|java.sql.Types の SQL データ型です。|  
|TYPE_NAME|**String**|データ型の名前です。|  
|PRECISION|**int**|有効桁数の合計。|  
|LENGTH|**int**|データの長さです (バイト)。|  
|SCALE|**short**|小数点以下の桁数です。|  
|RADIX|**short**|数値型の基数です。|  
|NULLABLE|**short**|列に null 値を含めることができるかどうかを示します。 次のいずれかの値を指定できます。<br /><br /> procedureNoNulls (0)<br /><br /> procedureNullable (1)<br /><br /> procedureNullableUnknown (2)|  
|REMARKS|**String**|プロシージャ列の記述です。<br /><br /> <br /><br /> **注:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、この列の値は返されません。|  
|COLUMN_DEF|**String**|列の既定値です。|  
|SQL_DATA_TYPE|**smallint**|この列は、**datetime** データ型と ISO **interval** データ型以外は、**DATA_TYPE** 列と同じです。|  
|SQL_DATETIME_SUB|**smallint**|**SQL_DATA_TYPE** の値が **SQL_DATETIME** または **SQL_INTERVAL** の場合は、**datetime** ISO **interval** サブコードになります。 **datetime** および **ISO interval** 以外のデータ型の場合、この列は NULL です。|  
|CHAR_OCTET_LENGTH|**int**|列の最大バイト数です。|  
|ORDINAL_POSITION|**int**|テーブル内の列のインデックスです。|  
|IS_NULLABLE|**String**|列で null 値が許容されるかどうかを示します。|  
|SS_TYPE_CATALOG_NAME|**String**|UDT (ユーザー定義型) を含むカタログの名前です。|  
|SS_TYPE_SCHEMA_NAME|**String**|UDT (ユーザー定義型) を含むスキーマの名前です。|  
|SS_UDT_CATALOG_NAME|**String**|完全修飾名の UDT (ユーザー定義型) です。|  
|SS_UDT_SCHEMA_NAME|**String**|XML スキーマ コレクション名が定義されているカタログの名前です。 カタログ名が見つからない場合は、この変数に空文字列が含まれます。|  
|SS_UDT_ASSEMBLY_TYPE_NAME|**String**|XML スキーマ コレクション名が定義されているスキーマの名前です。 スキーマ名が見つからない場合は、空文字列です。|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|**String**|XML スキーマ コレクションの名前です。 名前が見つからない場合は、空文字列です。|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|**String**|UDT (ユーザー定義型) を含むカタログの名前です。|  
|SS_XML_SCHEMACOLLECTION_NAME|**String**|UDT (ユーザー定義型) を含むスキーマの名前です。|  
|SS_DATA_TYPE|**tinyint**|拡張ストアド プロシージャによって使用される [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型です。<br /><br /> <br /><br /> **注:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって返されるデータ型の詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「データ型 (Transact-SQL)」を参照してください。|  
  
> [!NOTE]  
>  getProcedureColumns メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_sproc_columns (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースで、getProcedureColumns メソッドを使用して uspGetBillOfMaterials ストアド プロシージャに関する情報を返す方法を示します。  
  
```  
public static void executeGetProcedureColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedureColumns(null, null, "uspGetBillOfMaterials", null);  
      ResultSetMetaData rsmd = rs.getMetaData();  
  
      // Display the result set data.  
      int cols = rsmd.getColumnCount();  
      while(rs.next()) {  
         for (int i = 1; i <= cols; i++) {  
            System.out.println(rs.getString(i));  
         }  
      }  
      rs.close();  
   }   
  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
