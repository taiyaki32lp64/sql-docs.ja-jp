---
title: getDouble (int) メソッドMicrosoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDouble (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c0ed63bb-5ebe-4155-9f91-8fbfeac9c3b2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b02292225d0f0be0529537f369c2fa760d677486
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983593"
---
# <a name="getdouble-method-int"></a>getDouble (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡されたインデックスを使用して、指定されたパラメーターの値を Java プログラミング言語の **double** として取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public double getDouble(int index)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *index*  
  
 パラメーターのインデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 **Double**値。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getDouble メソッドは、java.sql.CallableStatement インターフェイスの getDouble メソッドで規定されています。  
  
 このメソッドは、数値ベースのすべてのデータ型を、Java の**double** の忠実性を使用して返します。  
  
## <a name="see-also"></a>参照  
 [getDouble メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdouble-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
