---
title: getFetchSize メソッド (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8115ca58-8ae9-46ce-8515-7905d7bb25fe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22ba06688fb402fdbcd5e9afd951a668ef9c440d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983217"
---
# <a name="getfetchsize-method-sqlserverstatement"></a>getFetchSize メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  結果セットの行数を取得します。この行数は、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトから生成される結果セット オブジェクトの既定のフェッチ サイズとなります。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getFetchSize()  
```  
  
## <a name="return-value"></a>戻り値  
 [setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md) メソッドによって指定されるフェッチ サイズを示す **int** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getFetchSize メソッドは、java. .sql. ステートメントインターフェイスの getFetchSize メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
