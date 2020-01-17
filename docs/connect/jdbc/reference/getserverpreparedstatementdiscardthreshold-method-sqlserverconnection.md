---
title: getServerPreparedStatementDiscardThreshold メソッド (SQLServerConnection) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getServerPreparedStatementDiscardThreshold
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 87d7f85799524e3ac7c0e4d99608ce1d82b8f2fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979935"
---
# <a name="getserverpreparedstatementdiscardthreshold-method-sqlserverconnection"></a>getServerPreparedStatementDiscardThreshold メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 **ServerPreparedStatementDiscardThreshold** connection プロパティの値を返します。 この設定は、サーバー上の未処理のハンドルをクリーンアップするための呼び出しが実行される前に、1つの接続に対して未処理の準備されたステートメント破棄操作 (sp_unprepare) の数を制御します。 設定が < = 1 の場合、unprepare のアクションは、準備されたステートメントの終了時に直ちに実行されます。 > 1 に設定されている場合は、sp_unprepare の呼び出しが頻繁に行われるオーバーヘッドを避けるために、これらの呼び出しがまとめてバッチ処理されます。 このオプションの既定値は、getDefaultServerPreparedStatementDiscardThreshold () を呼び出すことによって変更できます。

## <a name="syntax"></a>構文  
  
```  
  
public int getServerPreparedStatementDiscardThreshold()  
```  

## <a name="return-value"></a>戻り値
 **ServerPreparedStatementDiscardThreshold** connection プロパティの値を含む**int**です。

## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Remarks  
 このメソッドは、JDBC driver バージョン6.4 以降で使用できます。
 
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
