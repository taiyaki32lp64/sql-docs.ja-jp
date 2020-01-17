---
title: getProcedures メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 66c9a8b0-dc4c-4cbb-8004-c7157368cab4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 054ce4f6f646f873d4aff05fbe1d31aa9903ded9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980742"
---
# <a name="getprocedures-method-sqlserverdatabasemetadata"></a>getProcedures メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたカタログ、スキーマ、またはストアド プロシージャ名のパターンで使用可能なストアド プロシージャの記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getProcedures(java.lang.String sCatalog,  
                                        java.lang.String sSchema,  
                                        java.lang.String proc)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCatalog*  
  
 カタログ名を含む**文字列**です。 このパラメーターに null を指定すると、カタログ名を使用する必要はありません。  
  
 *sSchema*  
  
 スキーマ名のパターンを含む**文字列**です。 このパラメーターに null を指定すると、スキーマ名を使用する必要はありません。  
  
 *proc*  
  
 プロシージャ名のパターンを含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getProcedures メソッドは、java メタデータインターフェイスの getProcedures メソッドによって指定されます。  
  
 getProcedures メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|PROCEDURE_CAT|**String**|指定したストアド プロシージャが存在するデータベースの名前です。|  
|PROCEDURE_SCHEM|**String**|ストアド プロシージャのスキーマです。|  
|PROCEDURE_NAME|**String**|ストアド プロシージャの名前です。|  
|NUM_INPUT_PARAMS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|NUM_OUTPUT_PARAMS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|NUM_RESULT_SETS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|REMARKS|**String**|プロシージャ列の記述です。<br /><br /> <br /><br /> **注:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、この列の値は返されません。|  
|PROCEDURE_TYPE|**smallint**|ストアド プロシージャの種類です。 次のいずれかの値を指定できます。<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
> [!NOTE]  
>  getProcedures メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_stored_procedures (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースで、getProcedures メソッドを使用して uspGetBillOfMaterials ストアド プロシージャに関する情報を返す方法を示します。  
  
```  
public static void executeGetProcedures(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getProcedures(null, null, "uspGetBillOfMaterials");  
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
  
  
