---
title: prepareStatement メソッド (java.lang.String, int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.prepareStatement (java.lang.String, int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b78d2192-f315-4c45-9051-c77059e2c3f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a47ac1202ec73c15198b9b6f3c87ee53e027c83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976181"
---
# <a name="preparestatement-method-javalangstring-int-int-int"></a>prepareStatement (java.lang.String, int, int, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された結果セットの種類、コンカレンシー、および保持機能の [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを生成する [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.PreparedStatement prepareStatement(java.lang.String sql,  
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
 PreparedStatement オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この指定されたステートメントメソッドは、java. .sql. 接続インターフェイスの "ドステートメント" メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [prepareStatement メソッド &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)   
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
