---
title: setString メソッド (long, java.lang.String) - NClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 698073b2-3f0c-449c-ad68-48144698fe8f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9c549d3e1b7b9b63663333a59b263a2aa6ad4113
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972669"
---
# <a name="setstring-method-long-javalangstring-sqlservernclob"></a>setString (long, java.lang.String) メソッド (SQLServerNClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定した**文字列**を**NCLOB**の指定した位置から書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int setString(long pos,  
              java.lang.String str)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *po*  
  
 **NCLOB** 値への書き込みを開始する位置です。最初の位置は 1 です。  
  
 *str*  
  
 **NCLOB** に書き込む文字列です。  
  
## <a name="return-value"></a>戻り値  
 書き込まれる文字数です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この setString メソッドは、java.sql.NClob インターフェイスの setString メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerNClob のメソッド](../../../connect/jdbc/reference/sqlservernclob-methods.md)   
 [SQLServerNClob のメンバー](../../../connect/jdbc/reference/sqlservernclob-members.md)   
 [SQLServerNClob クラス](../../../connect/jdbc/reference/sqlservernclob-class.md)  
  
  
