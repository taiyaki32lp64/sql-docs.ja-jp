---
title: getImportedKeys メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getImportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: dc8c1a5e-700e-4059-a5ed-5013bbb87fb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2418bd5e62f00e46ddc329c1c7ba987505fb5a7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982827"
---
# <a name="getimportedkeys-method-sqlserverdatabasemetadata"></a>getImportedKeys メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  テーブル内の外部キー列によって参照される、主キー列の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getImportedKeys(java.lang.String cat,  
                                          java.lang.String schema,  
                                          java.lang.String table)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *cat*  
  
 カタログ名を含む**文字列**です。  
  
 *schema*  
  
 スキーマ名を含む**文字列**です。  
  
 *テーブル*  
  
 テーブル名を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getImportedKeys メソッドは、java メタデータインターフェイスの getImportedKeys メソッドによって指定されます。  
  
 getImportedKeys メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|PKTABLE_CAT|**String**|主キー テーブルを含むカタログの名前です。|  
|PKTABLE_SCHEM|**String**|主キー テーブルのスキーマの名前です。|  
|PKTABLE_NAME|**String**|主キー テーブルの名前です。|  
|PKCOLUMN_NAME|**String**|主キーの列名です。|  
|FKTABLE_CAT|**String**|外部キー テーブルを含むカタログの名前です。|  
|FKTABLE_SCHEM|**String**|外部キー テーブルのスキーマの名前です。|  
|FKTABLE_NAME|**String**|外部キー テーブルの名前です。|  
|FKCOLUMN_NAME|**String**|外部キーの列名です。|  
|KEY_SEQ|**short**|複数列の主キーにおける列のシーケンス番号です。|  
|UPDATE_RULE|**short**|SQL の操作が更新であるとき、外部キーに適用される動作です。 次のいずれかの値を指定できます。<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|DELETE_RULE|**short**|SQL の操作が削除であるとき、外部キーに適用される動作です。 次のいずれかの値を指定できます。<br /><br /> importedKeyNoAction (3)<br /><br /> importedKeyCascade (0)<br /><br /> importedKeySetNull (2)<br /><br /> importedKeySetDefault (4)<br /><br /> importedKeyRestrict (1)|  
|FK_NAME|**String**|外部キーの名前です。|  
|PK_NAME|**String**|主キーの名前です。|  
|DEFERRABILITY|**short**|外部キーの制限の評価を、コミット時まで遅延できるかどうかを示します。 次のいずれかの値を指定できます。<br /><br /> importedKeyInitiallyDeferred (5)<br /><br /> importedKeyInitiallyImmediate (6)<br /><br /> importedKeyNotDeferrable (7)|  
  
> [!NOTE]  
>  getImportedKeys メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_fkeys (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getImportedKeys メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースの Person.Address テーブルにある外部キーを参照するすべての主キーに関する情報を返す方法を示します。  
  
```  
public static void executeGetImportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getImportedKeys("AdventureWorks", "Person", "Address");  
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
  
  
