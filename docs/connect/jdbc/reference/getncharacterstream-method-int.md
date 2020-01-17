---
title: Getnキャラクターストリームメソッド (int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6ae704f5-823c-4dfe-8c08-07b547c61a3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ed91df645edd7083e0d91346dfdf6d39bebd91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981655"
---
# <a name="getncharacterstream-method-int"></a>getNCharacterStream (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡されたインデックスを使用して、指定されたパラメーターの値を Reader オブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final java.io.Reader getNCharacterStream(int parameterIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterIndex*  
  
 パラメーターのインデックスを示す **int** です。  
  
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
  
  
