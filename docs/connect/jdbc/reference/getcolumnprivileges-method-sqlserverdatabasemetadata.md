---
title: getColumnPrivileges メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getColumnPrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ab6a671-9573-4b95-8c23-364306c60d25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ae80a8c33f68ad2f3d2c85b1343a5cc0f2b423c5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67952874"
---
# <a name="getcolumnprivileges-method-sqlserverdatabasemetadata"></a>getColumnPrivileges メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  テーブルの列に対するアクセス権の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getColumnPrivileges(java.lang.String catalog,  
                                              java.lang.String schema,  
                                              java.lang.String table,  
                                              java.lang.String col)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 カタログ名を含む**文字列**です。  
  
 *schema*  
  
 スキーマ名を含む**文字列**です。  
  
 *テーブル*  
  
 テーブル名を含む**文字列**です。  
  
 *col*  
  
 列名のパターンを含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getColumnPrivileges メソッドは、java.sql.DatabaseMetaData インターフェイスの getColumnPrivileges メソッドで規定されています。  
  
 getColumnPrivileges メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|カタログ名。|  
|TABLE_SCHEM|**String**|テーブル スキーマ名です。|  
|TABLE_NAME|**String**|テーブル名。|  
|COLUMN_NAME|**String**|列名。|  
|GRANTOR|**String**|アクセス許可を与えるオブジェクトです。|  
|GRANTEE|**String**|アクセスを受け入れるオブジェクトです。|  
|PRIVILEGE|**String**|許可されたアクセスの種類です。|  
|IS_GRANTABLE|**String**|権限を与えられたユーザーが他のユーザーへのアクセスを許可できるかどうかを示します。|  
  
> [!NOTE]  
>  getColumnPrivileges メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_column_privileges (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getColumnPrivileges メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースにある Person.Contact テーブルの FirstName 列に対するアクセス権を返す方法を示します。  
  
```  
public static void executeGetColumnPrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getColumnPrivileges("AdventureWorks", "Person", "Contact", "FirstName");  
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
  
  
