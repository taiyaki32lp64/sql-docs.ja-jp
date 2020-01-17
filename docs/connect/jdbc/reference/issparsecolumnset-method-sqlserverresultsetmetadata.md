---
title: isSparseColumnSet メソッド (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ac363670-78ae-49f1-aeda-4fba3329a258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2b902ddf8e9e05900e55492116ee9e22a3dbbccc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977223"
---
# <a name="issparsecolumnset-method-sqlserverresultsetmetadata"></a>isSparseColumnSet メソッド (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  結果セットの列がスパース列セットであるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```scr  
public boolean isSparseColumnSet(int column)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *column*  
  
 列の (1 から始まる) インデックス。  
  
## <a name="return-value"></a>戻り値  
 結果セットの列がスパース列セットである場合は **true**、それ以外の場合は **false**。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、データベースから情報を取得しません。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSetMetaData メソッド](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [SQLServerResultSetMetaData メンバー](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [SQLServerResultSetMetaData クラス](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
