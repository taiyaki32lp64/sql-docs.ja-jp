---
title: getBytes メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getBytes (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d0dac7f-7f39-47a2-953e-80ab03688d82
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35476869b1e083e66c349439563b4fed5fd8be2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953378"
---
# <a name="getbytes-method-javalangstring"></a>getBytes (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡された名前を使用して、指定されたパラメーターの値を byte 配列として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public byte[] getBytes(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCol*  
  
 パラメーターの名前を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 **バイト**値の配列。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 以前のバージョンの [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、SQLServerCallableStatement.getBytes を使用してバイト配列と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データ型の **date**、**time**、**datetime2**、または **datetimeoffset** との間の変換を実行できました。 新しいバージョンでは、これらのデータ型に対してこのメソッドを使用すると、変換がサポートされていないことを示す例外が発生します。  
  
 この getBytes メソッドは、java.sql.CallableStatement インターフェイスの getBytes メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [getBytes メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getbytes-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
