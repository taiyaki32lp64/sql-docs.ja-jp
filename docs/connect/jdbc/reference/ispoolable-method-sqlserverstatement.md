---
title: isPoolable メソッド (SQLServerStatement) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8a12ac5-57cb-4288-9973-c7d5cebd197c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 225584f3c60f0494af987581574d8f4205e04e2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977509"
---
# <a name="ispoolable-method-sqlserverstatement"></a>isPoolable メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ユーザー指定のステートメント プールにステートメントを追加できるかどうかを示す値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean isPoolable() throws SQLException  
```  
  
## <a name="return-value"></a>戻り値  
 ユーザー指定のステートメント プールにステートメントを追加できる場合は **true**、それ以外の場合は **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md) により、オブジェクトをプールできるかどうかを変更します。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
