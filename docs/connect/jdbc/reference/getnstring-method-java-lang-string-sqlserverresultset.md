---
title: getNString メソッド (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 546d77e2-723a-42ac-ba3f-fabf2395d376
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0a76052ccf05927ebd598e2baa37fbf0229bf54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981394"
---
# <a name="getnstring-method-javalangstring-sqlserverresultset"></a>getNString (java.lang.String) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列の値が、java.lang.String オブジェクトとして取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getNString(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む文字列です。  
  
## <a name="return-value"></a>戻り値  
 文字列オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getNString メソッドは、java.sql.SQLServerResultSet インターフェイスの getNString メソッドで規定されています。  
  
 このメソッドを使用すると、この[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)オブジェクトの現在の行にある**nvarchar**、 **nchar**、 **nvarchar (max)** 、 **ntext**、または**xml**列の値を取得できます。 このメソッドを使用して他のデータ型の値を取得しようとすると、例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [getNString メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)  
  
  
