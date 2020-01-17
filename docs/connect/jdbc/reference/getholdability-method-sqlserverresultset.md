---
title: getHoldability メソッド (SQLServerResultSet) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4508d90f-c3c4-4eac-8001-fb0b93b66734
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57bf0cfc206319bf6afcb09435e8787499266c0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982926"
---
# <a name="getholdability-method-sqlserverresultset"></a>getHoldability メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの保持機能を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getHoldability()  
```  
  
## <a name="return-value"></a>戻り値  
 次のいずれかの保持機能レベルを含む **int** 値です。  
  
 HOLD_CURSORS_OVER_COMMIT  
  
 CLOSE_CURSORS_AT_COMMIT  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getHoldability メソッドは、getHoldability インターフェイスのメソッドによって指定されます。  
  
 結果セットの保持機能を設定するには、アプリケーションで [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) メソッドを使用できます。 [setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) メソッドが呼び出され、ステートメント オブジェクトとその結果セット オブジェクトが作成され、ステートメントが実行された後、アプリケーションで保持機能をもう一度変更しなければならない場合があります。  
  
 サーバー側のカーソルについては、SQL Server 2005 以降に接続されている場合に、保持機能の設定が、その接続でこれから作成される新しい結果セットの保持機能にのみ影響を与えます。 ただし、SQL Server 2000 の場合は、保持機能の設定が、既存の結果セットとその接続でこれから作成される新しい結果セットの両方の保持機能に影響を与えます。  
  
 保持機能がリセットされ、以前に作成された結果セットオブジェクトに対して getHoldability メソッドが呼び出されると、このメソッドによって返される値は、次のメソッドによって返される保持機能値とは異なる場合があります: getResultSetHoldability、GetHoldability、または getResultSetHoldability。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
