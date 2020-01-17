---
title: getObject メソッド (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getObject (jnt)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c4b8366b-c065-48e1-b712-19e2d9834228
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db0b8768c599ebf8fcef127139b9fb8bd6d8ec50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981226"
---
# <a name="getobject-method-int"></a>getObject (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  パラメーターに渡されたインデックスを使用して、指定されたパラメーターの値を Java プログラミング言語のオブジェクトとして取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.Object getObject(int index)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *index*  
  
 パラメーターのインデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 **Object** 値。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getObject メソッドは、java.sql.CallableStatement インターフェイスの getObject メソッドで規定されています。  
  
 このメソッドは、指定された列の値を Java オブジェクトとして返します。 この Java オブジェクトの型は、JDBC 仕様に指定されている組み込み型のマッピングに基づく、列の SQL 型に対応する既定の Java オブジェクト型です。 値が SQL NULL の場合、ドライバーは Java の null を返します。  
  
 このメソッドは、データベース固有の抽象データ型を読み取る場合にも使用できます。 JDBC 2.0 では、SQL のユーザー定義型のデータを具体化するよう、getObject メソッドの動作が拡張されました。 列に構造化された値または個別の値が含まれている場合、このメソッドの動作は `getObject(columnIndex, this.getStatement().getConnection().getTypeMap())` を呼び出した場合と同様です。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 以降:  
  
-   **date** 型の値は java.sql.Date オブジェクトとして返されます。  
  
-   **time** 型の値は java.sql.Time オブジェクトとして返されます。  
  
-   **datetime2** 型の値は java.sql.Timestamp オブジェクトとして返されます。  
  
-   **datetimeoffset** 型の値は microsoft.sql.DateTimeOffset オブジェクトとして返されます。  
  
## <a name="see-also"></a>参照  
 [getObject メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getobject-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
