---
title: SQLServerException コンストラクター (java.lang.Object, java.lang.String, java.lang.String, int, boolean) | Microsoft Docs
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
ms.openlocfilehash: 72ae0e8ed3c65a795723326d7ca49e2f5a909f18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971147"
---
# <a name="sqlserverexception-constructor-javalangobject-javalangstring-javalangstring-int-boolean"></a>SQLServerException コンストラクター (java.lang.Object, java.lang.String, java.lang.String, int, boolean)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **オブジェクト**、**文字列**オブジェクト、**文字列**オブジェクト、 **int**、および**ブール値**が指定された場合に、 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)クラスの新しいインスタンスを初期化します。

## <a name="syntax"></a>構文  
  
```  

public SQLServerException(java.lang.Object obj,
            java.lang.String errText,
            java.lang.String errState,
            int errNum,
            boolean bStack)

            
```  
  
#### <a name="parameters"></a>パラメーター  
 *obj*  
  
 例外を生成した IO バッファー。

 *errText*  
  
 エラーテキストを表す文字列です。
  
 *sqlState*  
  
 SQL 状態を格納している列挙オブジェクト。
 
 *errNum*  
  
 例外のエラーコードを格納している int。
 
 *bStack*  
  
 スタックトレースを生成する必要があるかどうかを示すブール値。
  
## <a name="see-also"></a>参照  
 [SQLServerException のコンストラクター](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException のメンバー](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException クラス](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
