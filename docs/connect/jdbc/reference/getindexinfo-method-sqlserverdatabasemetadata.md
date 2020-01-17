---
title: getIndexInfo メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getIndexInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8a677cc6-8e33-4e57-8678-0849345aa8d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8dd512236aa3070ce299756d4e4294c79ac2e94a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982791"
---
# <a name="getindexinfo-method-sqlserverdatabasemetadata"></a>getIndexInfo メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡されたテーブルのインデックスと統計情報についての記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getIndexInfo(java.lang.String cat,  
                                       java.lang.String schema,  
                                       java.lang.String table,  
                                       boolean unique,  
                                       boolean approximate)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *cat*  
  
 カタログ名を含む**文字列**です。  
  
 *schema*  
  
 スキーマ名を含む**文字列**です。  
  
 *テーブル*  
  
 テーブル名を含む**文字列**です。  
  
 *unique*  
  
 一意の値のインデックスのみが返される場合は**true** 。 すべてのインデックスが返される場合は**false** 。  
  
 *approximate*  
  
 結果に概数または古い値が反映されている場合は**true** 。 結果が正確である場合は**false** 。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getIndexInfo メソッドは、java.sql.DatabaseMetaData インターフェイスの getIndexInfo メソッドで規定されています。  
  
 getIndexInfo メソッドによって返される結果セットには、次の情報が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|TABLE_CAT|**String**|指定したテーブルが含まれているデータベースの名前です。|  
|TABLE_SCHEM|**String**|テーブルのスキーマです。|  
|TABLE_NAME|**String**|テーブルの名前です。|  
|NON_UNIQUE|**boolean**|インデックス値が重複可能であるかどうかを示します。|  
|INDEX_QUALIFIER|**String**|インデックス所有者の名前です。 TYPE が tableIndexStatistic の場合は null になります。|  
|INDEX_NAME|**String**|インデックスの名前です。|  
|TYPE|**short**|インデックスの型です。 次のいずれかの値を指定できます。<br /><br /> tableIndexStatistic (0)<br /><br /> tableIndexClustered (1)<br /><br /> tableIndexHashed (2)<br /><br /> tableIndexOther (3)|  
|ORDINAL_POSITION|**short**|インデックス内での列の位置を示す序数です。 インデックスの最初の列は 1 です。|  
|COLUMN_NAME|**String**|列の名前です。|  
|ASC_OR_DESC|**String**|インデックスの照合で使用される順序です。 次のいずれかの値を指定できます。<br /><br /> A (昇順)<br /><br /> D (降順)<br /><br /> NULL (適用なし)<br /><br /> **注:**  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] からは常に "A" が返されます。|  
|CARDINALITY|**int**|テーブル内の行数またはインデックス内の一意の値の個数です。|  
|PAGES|**int**|インデックスまたはテーブルの格納に使用するページ数です。|  
|FILTER_CONDITION|**String**|フィルター条件です。<br /><br /> **注:**  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] からは常に "null" が返されます。|  
  
> [!NOTE]  
>  getIndexInfo メソッドによって返されるデータの詳細については、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] オンライン ブックの「sp_indexes (Transact-SQL)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、getIndexInfo メソッドを使用して、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースにある Person.Contact テーブルのインデックスと統計情報に関する情報を返す方法を示します。  
  
```  
public static void executeGetIndexInfo(Connection con) {  
   try {  
      DatabaseMetaData dbmd = con.getMetaData();  
      ResultSet rs = dbmd.getIndexInfo("AdventureWorks", "Person", "Contact", false, true);  
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
  
  
