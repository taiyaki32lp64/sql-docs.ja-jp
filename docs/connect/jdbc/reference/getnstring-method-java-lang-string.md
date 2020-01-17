---
title: getNString メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d9362a41e5a48400c1b63d52b2ff89095d119d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981401"
---
# <a name="getnstring-method-javalangstring"></a>getNString (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された**NCHAR**、 **NVARCHAR**、または**LONGNVARCHAR**パラメーターの値を Java プログラミング言語の文字列として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterName*  
  
 パラメーターの名前を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 AStringobject.  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getNString メソッドは、java.sql.CallableStatement インターフェイスの getNString メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [getNString メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメソッド](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
