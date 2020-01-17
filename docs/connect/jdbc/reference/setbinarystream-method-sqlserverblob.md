---
title: setBinaryStream メソッド (SQLServerBlob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerBlob.setBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: abcec31f-1a60-4765-9725-8cf7e9f1f8ab
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4555dfb9256f3ffe2ba61e82fe90307991a5a580
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975097"
---
# <a name="setbinarystream-method-sqlserverblob"></a>setBinaryStream メソッド (SQLServerBlob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB 値への書き込みに使用できるストリームを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.io.OutputStream setBinaryStream(long pos)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *Po*  
  
 書き込みを開始する BLOB 値内の位置です。  
  
## <a name="return-value"></a>戻り値  
 出力ストリームです。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この setBinaryStream メソッドは、java. Blob インターフェイスの setBinaryStream メソッドによって指定されます。  
  
 BLOB のデータは、指定された開始位置から出力ストリームによって上書きされ、BLOB の初期データの長さをオーバーランすることができます。 開始位置に BLOB の長さ + 1 の値を指定すると、バイトが追加されます。 開始位置に BLOB の長さ + 2 以上 (または 0 以下) の値を渡すと、位置のエラーがスローされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
