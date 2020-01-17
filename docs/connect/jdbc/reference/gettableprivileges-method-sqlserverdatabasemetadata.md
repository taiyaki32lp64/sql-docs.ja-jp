---
title: getTablePrivileges メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getTablePrivileges
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0610d667-a16d-4201-a14b-0a40048911e1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d0fe3b01fd02bf48fb5f38707530e3b3344133e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979221"
---
# <a name="gettableprivileges-method-sqlserverdatabasemetadata"></a>getTablePrivileges メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたカタログ、スキーマ、またはテーブル名のパターンで使用可能な、各テーブルのアクセス権の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getTablePrivileges(java.lang.String catalog,  
                                             java.lang.String schema,  
                                             java.lang.String table)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 カタログ名を含む**文字列**です。 このパラメーターに null を指定すると、カタログ名を使用する必要はありません。  
  
 *schema*  
  
 スキーマ名のパターンを含む**文字列**です。 このパラメーターに null を指定すると、スキーマ名を使用する必要はありません。  
  
 *テーブル*  
  
 テーブル名のパターンを含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getTablePrivileges メソッドは、java.sql.DatabaseMetaData インターフェイスの getTablePrivileges メソッドで規定されています。  
  
 getTablePrivileges メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|カタログ名。|  
|TABLE_SCHEM|**String**|テーブル スキーマ名です。|  
|TABLE_NAME|**String**|テーブル名。|  
|GRANTOR|**String**|アクセス許可を与えるオブジェクトです。|  
|GRANTEE|**String**|アクセスを受け入れるオブジェクトです。|  
|PRIVILEGE|**String**|許可されたアクセスの種類です。|  
|IS_GRANTABLE|**String**|権限を与えられたユーザーが他のユーザーへのアクセスを許可できるかどうかを示します。|  
  
> [!NOTE]  
>  getTablePrivileges メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_table_privileges (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getTablePrivileges メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースにおける Person.Contact テーブルのアクセス権を返す方法を示します。  
  
```  
public static void executeGetTablePrivileges(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getTablePrivileges("AdventureWorks", "Person", "Contact");  
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
  
  
