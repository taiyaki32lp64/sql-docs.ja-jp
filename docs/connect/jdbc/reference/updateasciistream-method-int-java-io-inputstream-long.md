---
title: updateAsciiStream メソッド (java.io.InputStream, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 143bff3e-2b5c-485d-9529-1c2387560094
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3e75b36daaccb0526674da64591b409f5c9856e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985514"
---
# <a name="updateasciistream-method-int-javaioinputstream-long"></a>updateAsciiStream (int, java.io.InputStream, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を ASCII ストリーム値で更新します。ASCII ストリーム値は、指定されたバイト数を持ちます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x,  
                              long length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *x*  
  
 InputStream オブジェクト。  
  
 *length*  
  
 ストリームの長さです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この updateAsciiStream メソッドは、java.sql.ResultSet インターフェイスの updateAsciiStream メソッドで規定されています。  
  
 このメソッドは、ASCII 文字 (バイト) を、InputStream オブジェクトから変換可能な文字型の列へ渡します。これは、Unicode の ASCII の範囲 [0x00 - 0x7F] と、874、932、936、949、950、1250 から 1258 のコード ページです。 このメソッドは、対象となる照合順序ページへの変換を実行します。 変換できない変換先列を更新しようとすると、例外がスローされます。 バイナリ列の場合、そのままのバイトが渡されます。  
  
 ストリームの長さが、*length* パラメーターで指定された長さと異なる場合は、行の更新または挿入時に JDBC ドライバーが例外をスローします。  
  
 ストリームの長さが不明である場合、*length* パラメーターを -1 に設定して、ドライバーが長さに関係なくストリームを受け入れるように指定できます。 sqljdbc4.jar を使用する場合、アプリケーションで長さが不明なストリームを使用して列を更新するときには、JDBC 4.0 メソッドの [updateAsciiStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/updateasciistream-method-int-java-io-inputstream.md) メソッドを使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [updateAsciiStream メソッド (SQLServerResultSet)](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
