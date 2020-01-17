---
title: getBytes メソッド (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBytes (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1385d7d4-9288-4cbd-8606-4b919e9b07b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d328a2b1f092686403ba4cbcddf1ad22d733ea06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213736"
---
# <a name="getbytes-method-int-sqlserverresultset"></a>getBytes (int) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  この [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値が、Java プログラミング言語の **byte** 配列として取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public byte[] getBytes(int columnIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 **バイト**値の配列。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getBytes メソッドは、java.sql.ResultSet インターフェイスの getBytes メソッドで規定されています。  
  
 このメソッドでは、サーバーからバイトの生データを読み取ることにより、すべての列を取得できます。 byte 配列が、サーバーに格納されている形式のまま、サーバーから直接返されます。  
  
 以前のバージョンの [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、SQLServerResultSet.getBytes を使用してバイト配列と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型の **date**、**time**、**datetime2**、または **datetimeoffset** との間の変換を実行できました。 新しいバージョンでは、これらのデータ型に対してこのメソッドを使用すると、変換がサポートされていないことを示す例外が発生します。  
  
## <a name="see-also"></a>参照  
 [getBytes メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
