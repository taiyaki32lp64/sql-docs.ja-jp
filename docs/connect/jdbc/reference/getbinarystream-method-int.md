---
title: getBinaryStream (int) メソッドMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0add171861f2ea9e021b9f9342968baf1601557
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953707"
---
# <a name="getbinarystream-method-int"></a>getBinaryStream (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値を、未解釈のバイトのバイナリ ストリームとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getBinaryStream メソッドは、java.sql.ResultSet インターフェイスの getBinaryStream メソッドで規定されています。  
  
 このメソッドを使用できる [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型は、binary、varbinary、varbinary(max)、および image だけです。 他のデータ型で使用すると、例外がスローされます。  
  
 このメソッドで値をストリームとして取得した後は、ストリームからこの値をチャンク単位で読み取ることができます。 このメソッドは、大きな LONGVARBINARY 値を取得する場合に適しています。  
  
> [!NOTE]  
>  返されたストリーム内のデータはすべて、他の列の値を取得する前に読み取る必要があります。 次に getter メソッドを呼び出すと、ストリームは暗黙的に閉じます。 また、メソッド InputStream.available を呼び出した場合、使用可能なデータがあるかどうかにかかわらず、ストリームから 0 が返される可能性があります。  
  
## <a name="see-also"></a>参照  
 [getBinaryStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
