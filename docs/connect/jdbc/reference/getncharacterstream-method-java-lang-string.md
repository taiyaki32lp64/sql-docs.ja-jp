---
title: Getn; Stream メソッド (java. lang. String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cc5e5e72c4b1aedcc9e10ef74ff2946f2fb2d588
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981618"
---
# <a name="getncharacterstream-method-javalangstring"></a>getNCharacterStream (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡された名前を使用して、指定されたパラメーターの値を Reader オブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 AReaderobject。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 **NCHAR**、 **NVARCHAR** 、および**LONGNVARCHAR**パラメーターにアクセスするときは、このメソッドを使用する必要があります。  
  
 この Getn; Stream メソッドは、java. sql. CallableStatement インターフェイスの getNCharacterStream メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [getNCharacterStream メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
