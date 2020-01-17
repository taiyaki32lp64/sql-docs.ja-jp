---
title: setAsciiStream (int, java.io.InputStream, long) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 9dfa7781-d72f-407a-a8d4-1c78c9446d09
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc093dbd271a03f2efe4641986ced16ae1471f31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975516"
---
# <a name="setasciistream-method-int-javaioinputstream-long"></a>setAsciiStream (int, java.io.InputStream, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターの番号を、指定されたバイト数を持つ指定された java.io.InputStream オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x,  
                                    long length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterIndex*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 InputStream オブジェクトです。  
  
 *length*  
  
 バイト数を示す **long** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setAsciiStream メソッドは、PreparedStatement インターフェイスの setAsciiStream メソッドによって指定されます。  
  
 ストリームの長さが、*length* パラメーターで指定された長さと異なる場合は、行の更新または挿入時に JDBC ドライバーが例外をスローします。  
  
 ストリームの長さが不明である場合、*length* パラメーターを -1 に設定して、ドライバーが長さに関係なくストリームを受け入れるように指定できます。 sqljdbc4.jar を使用する場合、アプリケーションで長さが不明なストリームを使用して列を更新するときには、JDBC 4.0 メソッドの [setAsciiStream &#40;int, java.io.InputStream&#41;](../../../connect/jdbc/reference/setasciistream-method-int-java-io-inputstream.md) メソッドを使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [setAsciiStream メソッド &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
