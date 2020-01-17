---
title: getMaxFieldSize メソッド (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9a1700cc8bb2bfb54dd9ddee52da54899f764650
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982106"
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの文字列やバイナリ列の値に対して返すことができる最大バイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>戻り値  
 列に格納できる最大バイト数を示す **int** です。制限しない場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getMaxFieldSize メソッドは、java. .sql. ステートメントインターフェイスの getMaxFieldSize メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメソッド](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
