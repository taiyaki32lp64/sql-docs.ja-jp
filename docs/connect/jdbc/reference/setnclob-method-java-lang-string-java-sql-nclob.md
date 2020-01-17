---
title: setNClob メソッド (java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cafa1124f193be1f747ad63e2024ea24d8fd5137
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973692"
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>setNClob (java.lang.String, java.sql.NClob) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、指定された NClob オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterName*  
  
 パラメーターの名前を含む**文字列**です。  
  
 *value*  
  
 NClob オブジェクトです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、 **NCHAR**、 **NVARCHAR**、 **NTEXT**、および**XML**の各パラメーターのデータ型に対して使用する必要があります。  
  
 この setNClob メソッドは、java.sql.CallableStatement インターフェイスの setNClob メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [setNClob メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
