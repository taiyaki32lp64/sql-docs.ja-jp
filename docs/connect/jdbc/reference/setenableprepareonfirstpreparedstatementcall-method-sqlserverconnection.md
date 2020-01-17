---
title: setEnablePrepareOnFirstPreparedStatementCall メソッド (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setEnablePrepareOnFirstPreparedStatementCall
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 187a195a831955b65f4af113fb80e5f99308e1a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974446"
---
# <a name="setenableprepareonfirstpreparedstatementcall-method-sqlserverconnection"></a>setEnablePrepareOnFirstPreparedStatementCall Method (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 特定の接続インスタンスの動作を指定します。 Value が false の場合、最初の実行では sp_executesql が呼び出され、ステートメントは準備されません。2回目の実行が行われると、sp_prepexec が呼び出され、実際には準備されたステートメントハンドルが設定されます。 次の実行では、sp_execute を呼び出します。 これにより、ステートメントが1回だけ実行された場合に、準備されたステートメントを閉じる必要がなくなります。

## <a name="syntax"></a>構文  
  
```  
  
public void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *enablePrepareOnFirstPreparedStatementCall*  
  
 **EnablePrepareOnFirstPreparedStatementCall** connection プロパティの新しい値です。  
 
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 このメソッドは、JDBC driver バージョン6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
