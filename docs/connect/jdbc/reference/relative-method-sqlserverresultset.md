---
title: relative メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.relative
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2bcdbb69-95fd-4ae8-8488-1a75a91fe2e0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b2e644feff3cd2787cc6bd80bce54562ad20794
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975783"
---
# <a name="relative-method-sqlserverresultset"></a>relative メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  カーソルを指定された行数分、現在の行を基準に正または負の方向に移動します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean relative(int nRows)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *nRows*  
  
 移動する行数を示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 カーソルが行にある場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この相対メソッドは、java. ResultSet インターフェイスの相対メソッドによって指定されます。  
  
 結果セット内の先頭行または最終行を越えて移動しようとすると、先頭行の前または最終行の後にカーソルが配置されます。 `relative(0)` の呼び出しは有効ですが、カーソルの位置は変更されません。  
  
 `relative(1)` メソッドを呼び出すことは、[next](../../../connect/jdbc/reference/next-method-sqlserverresultset.md) メソッドを呼び出すことと同じです。 `relative(-1)` メソッドを呼び出すことは、[previous](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md) メソッドを呼び出すことと同じです。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
