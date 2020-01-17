---
title: SQLServerException コンストラクター (Java.lang.throwable、java. lang.) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14984450507b5eea63d2fbe88bb2e7f957f61868
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971078"
---
# <a name="sqlserverexception-constructor-javalangstring-javalangthrowable"></a>SQLServerException コンストラクター (Java.lang.throwable、java. lang.)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **文字列**オブジェクトと**java.lang.throwable**オブジェクトが指定された場合に、 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)クラスの新しいインスタンスを初期化します。

## <a name="syntax"></a>構文  
  
```  
public SQLServerException(java.lang.String errText,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>パラメーター  
 *errText*  
  
 エラーテキストを表す文字列です。
 
 *cause*  
  
 例外の原因を格納している java.lang.throwable オブジェクト。
  
## <a name="see-also"></a>参照  
 [SQLServerException のコンストラクター](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException のメンバー](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException クラス](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
