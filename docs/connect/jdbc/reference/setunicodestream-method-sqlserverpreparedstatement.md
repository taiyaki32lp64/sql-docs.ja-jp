---
title: setUnicodeStream メソッド (SQLServerPreparedStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.setUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a413e83-e0a4-41f8-9fe0-33ce4d368ee4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a80dddc28fbca156fe31a7620f1d1b0460359a75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972162"
---
# <a name="setunicodestream-method-sqlserverpreparedstatement"></a>setUnicodeStream メソッド (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターの番号を、渡された入力ストリームに設定します。入力ストリームは、指定されたバイト数を持ちます。  
  
> [!NOTE]  
>  このメソッドは、JDBC 仕様で非推奨とされます。このメソッドを呼び出すと、"未実装" 例外がスローされます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setUnicodeStream(int n,  
                                   java.io.InputStream x,  
                                   int length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *n*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 InputStream オブジェクト。  
  
 *length*  
  
 バイト数です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setUnicodeStream メソッドは、PreparedStatement インターフェイスの setUnicodeStream メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [SQLServerPreparedStatement クラス](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
