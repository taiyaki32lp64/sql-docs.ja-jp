---
title: getPropertyInfo メソッド (SQLServerDriver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d89a29af5aa3d2518f94101854371cea757e135c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980668"
---
# <a name="getpropertyinfo-method-sqlserverdriver"></a>getPropertyInfo メソッド (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースへの接続に必要なプロパティを検出するために使用します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.DriverPropertyInfo[] getPropertyInfo(java.lang.String Url,  
                                                     java.util.Properties Info)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Url*  
  
 データベースへの接続に使用される URL を含む **String** 値です。  
  
 *Info*  
  
 プロパティ値のペアの一覧です。初回使用時には null です。  
  
## <a name="return-value"></a>戻り値  
 DriverPropertyInfo オブジェクトの配列。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getPropertyInfo メソッドは、getPropertyInfo インターフェイスのメソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDriver のメソッド](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [SQLServerDriver のメンバー](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [SQLServerDriver クラス](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
