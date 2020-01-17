---
title: position メソッド (byte, long) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.position (byte[], long)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 787412c2-4342-49c8-9ca2-7a9ddcd3277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf8cfa3bb6aed74c7689639698715dc24803d46d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67976474"
---
# <a name="position-method-byte-long"></a>position (byte, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された **byte** 配列パターンと開始インデックスに基づいて、BLOB 内の指定されたパターンの位置を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public long position(byte[] bPattern,  
                     long start)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *bPattern*  
  
 検索するパターンです。  
  
 *start*  
  
 検索の開始インデックスです。  
  
## <a name="return-value"></a>戻り値  
 パターンが見つかった場合は位置の **long** 値で、見つからなかった場合は -1 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この位置メソッドは、java. Blob インターフェイスの position メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [position メソッド&#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/position-method-sqlserverblob.md)   
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
