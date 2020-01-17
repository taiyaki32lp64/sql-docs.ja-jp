---
title: Setn文字ストリームメソッドを java. io. Reader オブジェクト-long |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36396dc9-f109-4da0-bd64-726704046bbf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 76c59a5e367e3d3e8524a64f5ae7ac6dab85b529
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973948"
---
# <a name="setncharacterstream-method-int-javaioreader-long"></a>setNCharacterStream (int, java.io.Reader, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターを、指定された Reader オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setNCharacterStream(int parameterIndex,  
                                                  java.io.Reader value,  
                                                                long length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterIndex*  
  
 パラメーターのインデックスを示す **int** です。  
  
 *value*  
  
 パラメーター値を含む Reader オブジェクトです。  
  
 *length*  
  
 パラメーター値の文字数を示す **long** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この Setn; Stream メソッドは、PreparedStatement インターフェイスの Setn Stream メソッドによって指定されます。  
  
 このメソッドは、 **NCHAR**、 **NVARCHAR**、 **NTEXT**、および**XML**データ型に対して使用する必要があります。  
  
 ストリームの長さが、*length* パラメーターで指定された長さと異なる場合は、行の更新または挿入時に JDBC ドライバーが例外をスローします。  
  
 ストリームの長さが不明である場合、*length* パラメーターを -1 に設定して、ドライバーが長さに関係なくストリームを受け入れるように指定できます。 sqljdbc4.jar を使用する場合、アプリケーションで長さが不明なストリームを使用して列を更新するときには、JDBC 4.0 メソッドの [setNCharacterStream メソッド &#40;int, java.io.Reader&#41;](../../../connect/jdbc/reference/setncharacterstream-method-int-java-io-reader.md) を使用することをお勧めします。  
  
## <a name="see-also"></a>参照  
 [setNCharacterStream メソッド &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
