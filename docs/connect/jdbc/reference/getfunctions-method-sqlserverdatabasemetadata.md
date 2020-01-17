---
title: getFunctions メソッド (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 44335cbd-c84d-4ef3-a6a1-fca7eb7ec768
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b799fb56207294041c52fe455ad2acceff508d3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982954"
---
# <a name="getfunctions-method-sqlserverdatabasemetadata"></a>getFunctions メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  システム関数およびユーザー関数の記述を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public ResultSet getFunctions(java.lang.String catalog,  
                       java.lang.String schemaPattern,  
                       java.lang.String functionNamePattern)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *catalog*  
  
 データベース内のカタログの名前です。 空の文字列 "" の場合、結果にはカタログのない関数が含まれます。 **null** の場合、カタログ名は検索に使用されません。  
  
 *schemaPattern*  
  
 スキーマの名前です。 空の文字列 "" の場合、結果にはスキーマのない関数が含まれます。 **null** の場合、スキーマ名は検索に使用されません。  
  
 *functionNamePattern*  
  
 関数の名前。  
  
## <a name="return-value"></a>戻り値  
 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getFunctions メソッドは、java.sql.DatabaseMetaData インターフェイスの getFunctions メソッドで規定されています。  
  
 このメソッドは、指定されたスキーマ名および関数名に一致するシステム関数およびユーザー関数だけを返します。  
  
> [!IMPORTANT]  
>  返される結果セットには、呼び出し元のユーザーに、実行するためのアクセス許可がない関数が含まれることがあります。  
  
 各関数の記述には、次の列が含まれます。  
  
|[オブジェクト名]|型|[説明]|  
|----------|----------|-----------------|  
|FUNCTION_CAT|**String**|関数が存在するデータベースの名前です。|  
|FUNCTION_SCHEM|**String**|関数が存在するスキーマの名前です。|  
|FUNCTION_NAME|**String**|関数の名前です。|  
|NUM_INPUT_PARAMS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|NUM_OUTPUT_PARAMS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|NUM_RESULT_SETS|**int**|今後の使用のために予約されています。現在は -1 の値を返します。|  
|REMARKS|**String**|関数についてのコメントです。|  
|FUNCTION_TYPE|**short**|関数の種類です。 次のいずれかの値を指定できます。<br /><br /> SQL_PT_UNKNOWN (0)<br /><br /> SQL_PT_PROCEDURE (1)<br /><br /> SQL_PT_FUNCTION (2)|  
  
 返される結果セット内のすべての記述は、FUNCTION_CAT、FUNCTION_SCHEM、FUNCTION_NAME、および SPECIFIC_NAME で順序付けされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
