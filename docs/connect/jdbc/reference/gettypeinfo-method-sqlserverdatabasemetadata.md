---
title: getTypeInfo メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTypeInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 23208f01-c1bf-4235-b29c-9051d3df59a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cb9b1b632d5a17b7c8f497e30a4f033932f09b33
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978517"
---
# <a name="gettypeinfo-method-sqlserverdatabasemetadata"></a>getTypeInfo メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在のデータベースによってサポートされる、すべての標準 SQL 型に関する記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getTypeInfo()  
```  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getTypeInfo メソッドは、java.sql.DatabaseMetaData インターフェイスの getTypeInfo メソッドで規定されています。  
  
 getTypeInfo メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|TYPE_NAME|**String**|データ型の名前です。|  
|DATA_TYPE|**short**|java.sql.Types の SQL データ型です。|  
|PRECISION|**int**|有効桁数の合計。|  
|LITERAL_PREFIX|**String**|定数の先頭に記述する文字または文字列です。|  
|LITERAL_SUFFIX|**String**|定数の末尾に記述する文字または文字列です。|  
|CREATE_PARAMS|**String**|データ型の作成パラメーターの記述です。|  
|NULLABLE|**short**|列に null 値を含めることができるかどうかを示します。 次のいずれかの値を指定できます。<br /><br /> typeNoNulls (0)<br /><br /> typeNullable (1)<br /><br /> typeNullableUnknown (2)|  
|CASE_SENSITIVE|**boolean**|データ型の大文字と小文字を区別するかどうかを示します。 大文字と小文字を区別する場合は "**true**"、区別しない場合は "**false**" です。|  
|SEARCHABLE|**short**|列を SQL の WHERE 句で使用できるかどうかを示します。 次のいずれかの値を指定できます。<br /><br /> typePredNone (0)<br /><br /> typePredChar (1)<br /><br /> typePredBasic (2)<br /><br /> typeSeachable (3)|  
|UNSIGNED_ATTRIBUTE|**boolean**|データ型の符号を示します。 符号なしの場合は "**true**"、符号ありの場合は "**false**" です。|  
|FIXED_PREC_SCALE|**boolean**|データ型に money 値を指定できるかどうかを示します。 money 型の場合は "**true**"、それ以外の場合は "**false**" です。|  
|AUTO_INCREMENT|**boolean**|データ型を自動インクリメントできるかどうかを示します。 自動インクリメントできる場合は "**true**"、それ以外の場合は "**false**" です。|  
|LOCAL_TYPE_NAME|**String**|データ型のローカライズされた名前です。|  
|MINIMUM_SCALE|**short**|小数点以下の最大桁数です。|  
|MAXIMUM_SCALE|**short**|小数点以下の最小桁数です。|  
|SQL_DATA_TYPE|**int**|JDBC ドライバーではサポートされていません。|  
|SQL_DATETIME_SUB|**int**|JDBC ドライバーではサポートされていません。|  
|NUM_PREC_RADIX|**int**|列が保持できる最大数を計算する場合のビット数または桁数です。|  
|INTERVAL_PRECISION|**smallint**|期間の先頭の有効桁数の値です。|  
|USERTYPE|**smallint**|**systypes** テーブルから **usertype** の値が返されます。 詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックを参照してください。|  
  
> [!NOTE]  
>  getTypeInfo メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_datatype_info (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getTypeInfo メソッドを使用して、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のデータベースで使用されるデータ型に関する情報を返す方法を示します。  
  
```  
public static void executeGetTypeInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTypeInfo();  
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
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
