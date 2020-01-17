---
title: updateBinaryStream (int, java.io.InputStream) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1db3a975-c108-45d1-8c0d-14a094f391bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8a1b69d4f4e1845b4ec86297c06298c1302becea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985375"
---
# <a name="updatebinarystream-method-int-javaioinputstream"></a>updateBinaryStream (int, java.io.InputStream) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列をバイナリ ストリーム値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateBinaryStream(int columnIndex,  
                               java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
 *x*  
  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この updateBinaryStream メソッドは、java.sql.ResultSet インターフェイスの updateBinaryStream メソッドで規定されています。  
  
 **Image**、 **text**、および**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型に対してこのメソッドを使用すると、パフォーマンスに影響を与える可能性があります。  
  
 このメソッドは、InputStream オブジェクトからのバイトを、binary、varbinary、varbinary(max)、image、xml、udt など、選択した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] バイナリ列に渡します。 このメソッドでは、文字型の列の更新はサポートされていません。 InputStream で文字型の列を更新するには、[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) メソッドを使用します。  
  
## <a name="see-also"></a>参照  
 [updateBinaryStream メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
