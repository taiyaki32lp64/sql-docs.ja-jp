---
title: updateAsciiStream メソッド (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d800d385d1df3b9cea8c8c0f4eccb29b90f64147
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985453"
---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>updateAsciiStream (java.lang.String, java.io.InputStream) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された列を ASCII ストリーム値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnLabel*  
  
 列ラベルを含む**文字列**です。  
  
 *x*  
  
 InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この updateAsciiStream メソッドは、java.sql.ResultSet インターフェイスの updateAsciiStream メソッドで規定されています。  
  
 このメソッドは、ASCII 文字 (バイト) を、InputStream オブジェクトから変換可能な文字型の列へ渡します。これは、Unicode の ASCII の範囲 [0x00 - 0x7F] と、874、932、936、949、950、1250 から 1258 のコード ページです。 このメソッドは、対象となる照合順序ページへの変換を実行します。 変換できない変換先列を更新しようとすると、例外がスローされます。 バイナリ列の場合、そのままのバイトが渡されます。  
  
 **Image**、 **text**、および**ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]データ型に対してこのメソッドを使用すると、パフォーマンスが低下する可能性があります。  
  
## <a name="see-also"></a>参照  
 [updateAsciiStream メソッド (SQLServerResultSet)](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
