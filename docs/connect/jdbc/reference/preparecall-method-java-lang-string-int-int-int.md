---
title: prepareCall メソッド (java.lang.String, int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareCall (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 81104fd5-75b0-4540-9f48-c3dbf59a8564
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0839fb735431adcdc4d1e3d0e7820ca2253cc121
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976239"
---
# <a name="preparecall-method-javalangstring-int-int-int"></a>prepareCall (java.lang.String, int, int, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された結果セットの種類、コンカレンシー、および保持機能の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを生成する [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.CallableStatement prepareCall(java.lang.String sql,  
                                              int nType,  
                                              int nConcur,  
                                              int nHold)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sql*  
  
 SQL ステートメントを含む**文字列**です。  
  
 *nType*  
  
 結果セットの種類を示す **int** です。  
  
 *nConcur*  
  
 結果セットのコンカレンシーの種類を示す **int** です。  
  
 *nHold*  
  
 結果セットの保持機能を示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 CallableStatement オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この prepareCall メソッドは、prepareCall インターフェイスのメソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [prepareCall メソッド &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)   
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
