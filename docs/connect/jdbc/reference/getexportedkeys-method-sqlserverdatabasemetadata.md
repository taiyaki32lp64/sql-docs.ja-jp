---
title: getExportedKeys メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExportedKeys
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 26888e61-b243-4a1b-922c-c0a451dcff4d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e89d65955c5637bcd566d48b6e54bcae50397d88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983303"
---
# <a name="getexportedkeys-method-sqlserverdatabasemetadata"></a>getExportedKeys メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたテーブルの主キー列を参照する外部キー列の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getExportedKeys(java.lang.String cat,  
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
 この getExportedKeys メソッドは、getExportedKeys メソッドによって、java メタデータインターフェイスで指定されます。  
  
 getExportedKeys メソッドによって返される結果セットには、次の情報が含まれます。  
  
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
>  getExportedKeys メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_fkeys (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getExportedKeys メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースの Person.Contact テーブルにある主キーを参照するすべての外部キーに関する情報を返す方法を示します。  
  
```  
public static void executeGetExportedKeys(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getExportedKeys("AdventureWorks", "Person", "Contact");  
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
  
  
