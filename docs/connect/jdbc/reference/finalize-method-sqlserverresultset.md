---
title: finalize メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7afb8728b92ac7460173950bf42e38f968e056af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954560"
---
# <a name="finalize-method-sqlserverresultset"></a>finalize メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを明示的に閉じます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>Remarks  
 アプリケーションが閉じていない場合は、結果セットを閉じます。 このメソッドは JDBC 仕様に準拠するためにだけ存在します。 Java 仮想マシン (JVM) ではファイナライザーがいつ実行されるかが保証されないため、明示的に結果セットを閉じてないアプリケーションは、別のステートメント (同じ接続を使用し、行ロックなどの共通のサーバー リソースでブロックされているステートメント) でもデッドロックする可能性があります。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
