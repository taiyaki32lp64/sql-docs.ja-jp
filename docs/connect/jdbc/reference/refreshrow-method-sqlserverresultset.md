---
title: refreshRow メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.refreshRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 048fe245-157f-4fd8-be75-ce54b83e02b3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 570a9185a83ecf1af0e47ee25cce5445dca1b958
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975980"
---
# <a name="refreshrow-method-sqlserverresultset"></a>refreshRow メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベース内の最新の値を使用して、現在の行を更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void refreshRow()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この refreshRow メソッドは、java. ResultSet インターフェイスの refreshRow メソッドによって指定されます。  
  
 カーソルが挿入行にあるときは、このメソッドを呼び出すことができません。  
  
 アプリケーションでこのメソッドを使用すると、データベースから行を再フェッチするよう、JDBC ドライバーに明示的に指示できます。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] がキャッシュまたはプレフェッチを行っているときには、行の最新の値をデータベースからフェッチするために、場合によってはアプリケーションでこのメソッドを呼び出す必要があります。 フェッチ サイズが 1 よりも大きい場合、JDBC ドライバーが複数行を同時に更新することがあります。  
  
 すべての値は、トランザクション分離レベルとカーソルの応答性に応じて再フェッチされます。 updater メソッドを呼び出した後、[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) メソッドを呼び出す前にこのメソッドを呼び出すと、行に加えた更新が失われます。 このメソッドを頻繁に呼び出すと、パフォーマンスが低下することがあります。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
