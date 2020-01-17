---
title: getVersionColumns メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getVersionColumns
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6dd275d3-d9b2-4db7-938a-d4406c940a7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3e2cf823a6c1cd33d647472a2e709517175ddce7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978159"
---
# <a name="getversioncolumns-method-sqlserverdatabasemetadata"></a>getVersionColumns メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  行の任意の値が更新された場合に自動的に更新されるテーブルの列の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getVersionColumns(java.lang.String catalog,  
                                            java.lang.String schema,  
                                            java.lang.String table)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 カタログ名を含む**文字列**です。  
  
 *schema*  
  
 スキーマ名のパターンを含む**文字列**です。  
  
 *テーブル*  
  
 テーブル名を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getVersionColumns メソッドは、java.sql.DatabaseMetaData インターフェイスの getVersionColumns メソッドで規定されています。  
  
 getVersionColumns メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|SCOPE|**short**|JDBC ドライバーではサポートされていません。|  
|COLUMN_NAME|**String**|列名。|  
|DATA_TYPE|**short**|java.sql.Types の SQL データ型です。|  
|TYPE_NAME|**String**|データ型の名前です。|  
|COLUMN_SIZE|**int**|列の完全桁数です。|  
|BUFFER_LENGTH|**int**|列の長さです (バイト)。|  
|DECIMAL_DIGITS|**short**|列の小数点以下の桁数です。|  
|PSEUDO_COLUMN|**short**|列が擬似列かどうかを示します。 次のいずれかの値を指定できます。<br /><br /> versionColumnUnknown (0)<br /><br /> versionColumnNotPseudo (1)<br /><br /> versionColumnPseudo (2)|  
  
> [!NOTE]  
>  getVersionColumns メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_datatype_info (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getVersionColumns メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースの Person.Contact テーブルで自動的に更新される列に関する情報を返す方法を示します。  
  
```  
public static void executeGetVersionColumns(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getVersionColumns("AdventureWorks", "Person", "Contact");  
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
  
  
