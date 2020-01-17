---
title: getBytes メソッド (SQLServerBlob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bea1b810-b5c1-466d-bdc4-561468214632
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c4c7891c6d7454e0397406f9391fdfb60d0f0fc7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213716"
---
# <a name="getbytes-method-sqlserverblob"></a>getBytes メソッド (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB データを byte 配列として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public byte[] getBytes(long pos,  
                       int length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *po*  
  
 開始位置です。1 から始まります (0 ではありません)。  
  
 *length*  
  
 取得するデータの長さです。  
  
## <a name="return-value"></a>戻り値  
 要求されたデータを含む **byte** 配列です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getBytes メソッドは、java.sql.Blob インターフェイスの getBytes メソッドで指定されています。  
  
 null または長さが 0 の BLOB があり、位置 1 で正確に 0 バイトを取得しようとすると、空の **byte** 配列が返されます (長さが 0 の byte 配列)。  
  
 null または長さが 0 の BLOB があり、位置 1 以外の場所で任意の長さのバイトを取得しようとすると、位置の例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
