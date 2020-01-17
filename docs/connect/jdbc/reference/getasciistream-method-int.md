---
title: getAsciiStream (int) メソッドMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getAsciiStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1ec7e246-4b91-4420-9a4c-0ebd98e2e38b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f7bc5b4729e071f2a65670522735654e550a453
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954207"
---
# <a name="getasciistream-method-int"></a>getAsciiStream (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値を、ASCII 文字のストリームとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.io.InputStream getAsciiStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getAsciiStream メソッドは、java.sql.ResultSet インターフェイスの getAsciiStream メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [getAsciiStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
