---
title: getString メソッド (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getString (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f67371e0-e879-4188-85fc-ecb85f0be2a9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4ff58d1a2f58e044b49767f8fb2982b669a7b78
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979430"
---
# <a name="getstring-method-javalangstring"></a>getString (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡された名前を使用して、指定されたパラメーターの値が Java プログラミング言語の **String** として取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getString(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sCol*  
  
 パラメーターの名前を含む**文字列**です。  
  
## <a name="return-value"></a>戻り値  
 **文字列**値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getString メソッドは、java.sql.CallableStatement インターフェイスの getString メソッドで規定されています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内のすべての列を文字列として返すことができます。 つまり、数値ベースと文字ベースのすべての型の文字列表現、および binary、varbinary、varbinary(max)、image、timestamp、uniqueidentifier などのバイナリ列の 16 進形式の文字列表現を返すことができます。  
  
 money、smallmoney、datetime、smalldatetime、float、real、decimal、numeric などの地域依存の型では、その型の基になる値に対する標準の toString() 形式が返されます。  
  
 ユーザー定義型は、16 進形式の文字列値として返されます。  
  
## <a name="see-also"></a>参照  
 [getString メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
