---
title: getSchemas メソッド () |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSchemas
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: adba0ee6-ff6d-4215-b646-62c735be3fe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0a5f453e6300258cacffa6606259f85cdd25977
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980082"
---
# <a name="getschemas-method-"></a>getSchemas () メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  現在のデータベースで使用できるスキーマ名を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getSchemas()  
```  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getSchemas メソッドは、java.sql.DatabaseMetaData インターフェイスの getSchemas メソッドで規定されています。  
  
 GetSchemas メソッドによって返される結果セットには、次の情報が含まれています。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|TABLE_SCHEM|**String**|スキーマの名前です。|  
|TABLE_CATALOG|**String**|スキーマのカタログ名です。|  
  
 結果は、TABLE_CATALOG および TABLE_SCHEM で順序付けされます。 各行の最初の列は TABLE_SCHEM、次の列は TABLE_CATALOG です。  
  
> [!NOTE]  
>  getSchemas メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sys.schemas (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、使用するデータベースが接続の引数で指定されている場合に、getSchemas メソッドを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のカタログおよびそれに関連付けられているスキーマ名に関する情報を返す方法を示します。  
  
```  
public static void executeGetSchemas(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getSchemas();  
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
  
  
