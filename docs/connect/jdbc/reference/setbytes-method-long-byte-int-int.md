---
title: setBytes メソッド (long、byte、int、int) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBytes (long.byte[], int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7def226c-b211-459e-8c1a-08592d75d4a4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee4ab641ede4d4ec614a306f9c0e08c9f16aa5ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974946"
---
# <a name="setbytes-method-long-byte-int-int"></a>setBytes (long, byte, int, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された byte 配列全体またはその一部を、渡された開始位置やオフセットおよび長さを使用して BLOB に書き込み、書き込んだバイト数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes,  
                    int offset,  
                    int len)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *po*  
  
 データの書き込みを開始する BLOB 内の位置 (1 から開始) です。  
  
 *bytes*  
  
 BLOB に書き込む byte 配列です。  
  
 *offset*  
  
 **byte** 配列からのデータの読み取りを開始する byte 配列内のオフセットです。  
  
 *len*  
  
 byte 配列から BLOB に読み込むバイト数です。  
  
## <a name="return-value"></a>戻り値  
 書き込んだバイト数を含む **int** です。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この setBytes メソッドは、java.sql.Blob インターフェイスの setBytes メソッドで指定されています。  
  
 データは指定された開始位置から上書きされ、BLOB の初期データの長さをオーバーランすることができます。 開始位置に BLOB の長さ + 1 の値を指定すると、バイトが追加されます。 開始位置に BLOB の長さ + 2 以上 (または 0 以下) の値を渡すと、位置のエラーがスローされます。 長さ 0 の **byte** 配列を渡すと、0 が返されます。これはバイトが書き込まれなかったためです。  
  
## <a name="see-also"></a>参照  
 [setBytes メソッド&#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
