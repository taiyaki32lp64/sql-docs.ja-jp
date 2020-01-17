---
title: isWrapperFor メソッド (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 71156863-3588-453e-b5a5-0573b2c1bebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5b1a572d3ab2dfba9d0aa0b8284fc770f3422782
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977105"
---
# <a name="iswrapperfor-method-sqlservercallablestatement"></a>isWrapperFor メソッド (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ステートメント オブジェクトが指定されたインターフェイスのラッパーであるかどうかを示します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean isWrapperFor(Class iface)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *iface*  
  
 インターフェイスを定義する**クラス**。  
  
## <a name="return-value"></a>戻り値  
 このオブジェクトがインターフェイスを実装しているか、インターフェイスを実装しているオブジェクトをラップしている場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlservercallablestatement.md) メソッドと [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md) メソッドは、JDBC 4.0 で導入された java.sql.Wrapper インターフェイスで定義されています。  
  
 このメソッドが **true** を返す場合、同じ引数を使用した [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md) の呼び出しは成功します。  
  
 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [unwrap メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
