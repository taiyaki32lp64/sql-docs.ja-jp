---
title: getMoreResults メソッド () |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: df89db50-0b2f-4094-820a-30be25ad72fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcbce9783641376ae142e94ab5e45dc47fe16fef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981737"
---
# <a name="getmoreresults-method-"></a>getMoreResults () メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの次の結果に移動します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final boolean getMoreResults()  
```  
  
## <a name="return-value"></a>戻り値  
 返された結果が結果セットである場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getMoreResults メソッドは、java. .sql. ステートメントインターフェイスの getMoreResults メソッドによって指定されます。  
  
 getMoreResults メソッドを呼び出すと、[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) メソッドを使用して取得された現在開いているすべての結果セット オブジェクトが暗黙的に閉じます。  
  
## <a name="see-also"></a>参照  
 [getMoreResults メソッド &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
