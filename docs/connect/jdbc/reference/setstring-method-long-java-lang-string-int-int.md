---
title: setString (long, java.lang.String, int, int) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerClob.setString (long, java.lang.String, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fb59b09-e825-46a6-ba5d-85d4a8dc143a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5741f8ba74009327befc8f940e1d3b37df6ef1ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972702"
---
# <a name="setstring-method-long-javalangstring-int-int"></a>setString (long, java.lang.String, int, int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された文字列を、渡されたオフセットと長さに基づいて CLOB の指定された位置から書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int setString(long pos,  
                     java.lang.String str,  
                     int offset,  
                     int len)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *po*  
  
 CLOB への書き込みを開始する位置です。  
  
 *str*  
  
 CLOB に書き込む文字列です。  
  
 *offset*  
  
 文字の読み取りを開始する文字列内のオフセットです。  
  
 *len*  
  
 書き込む文字数です。  
  
## <a name="return-value"></a>戻り値  
 書き込まれる文字数です。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この setString メソッドは、java.sql.Clob インターフェイスの setString メソッドで規定されています。  
  
 文字データは、指定された開始位置から上書きされ、CLOB の初期データの長さを上書きできます。 開始位置に CLOB の長さ + 1 の値を指定すると、文字列が追加されます。 開始位置に CLOB の長さ + 2 以上 (または 0 以下) の値を指定すると、位置エラーがスローされます。  
  
## <a name="see-also"></a>参照  
 [setString メソッド&#40;SQLServerClob&#41;](../../../connect/jdbc/reference/setstring-method-sqlserverclob.md)   
 [SQLServerClob のメソッド](../../../connect/jdbc/reference/sqlserverclob-methods.md)   
 [SQLServerClob メンバー](../../../connect/jdbc/reference/sqlserverclob-members.md)   
 [SQLServerClob クラス](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
