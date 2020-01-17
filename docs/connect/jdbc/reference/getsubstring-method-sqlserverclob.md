---
title: getSubString メソッド (SQLServerClob) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.getSubString
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bf915590-a883-4403-befa-5b5bb42f34d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73b82c550c78d409accd423b485fc7b9825dbc8c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979333"
---
# <a name="getsubstring-method-sqlserverclob"></a>getSubString メソッド (SQLServerClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された開始位置とコピーする文字数に基づいて、指定された CLOB の部分文字列のコピーを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getSubString(long pos,  
                                     int length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *po*  
  
 抽出する部分文字列の先頭の文字です。 先頭の文字の位置は 1 です。  
  
 *length*  
  
 コピーする連続した文字の文字数です。  
  
## <a name="return-value"></a>戻り値  
 CLOB 内の指定された部分文字列である **String** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getSubString メソッドは、java. Clob インターフェイスの getSubString メソッドによって指定されます。  
  
 null または長さが 0 の CLOB から 0 文字を取得しようとすると、空の文字列が返されます。 長さが 0 の CLOB で、位置 1 以外の場所で任意の長さの文字を取得しようとすると、位置の例外がスローされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerClob のメソッド](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob メンバー](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
