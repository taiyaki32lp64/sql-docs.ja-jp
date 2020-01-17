---
title: getClientInfo メソッド (java. lang. String) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8e632c4-d6cc-4c5e-b6ad-873579343b19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d3005e2b5ae8628ab31ceeb6314159afd796e83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953134"
---
# <a name="getclientinfo-method-javalangstring"></a>getClientInfo (java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたクライアント情報のプロパティの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getClientInfo (java.lang.String name)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *name*  
  
 取得するクライアント情報のプロパティの名前を含む String です。  
  
## <a name="return-value"></a>戻り値  
 設定するクライアント情報のプロパティの値を含む String です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getClientInfo メソッドは、java. .sql. 接続インターフェイスの getClientInfo メソッドによって指定されます。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] では、クライアント情報のプロパティはサポートされていません。 そのため、このメソッドでは **null** が返されます。  
  
 同様に、アプリケーションでは、[SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) クラスの [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) メソッドを使用して、ドライバーがサポートするクライアント情報プロパティの一覧を取得できます。 [getClientInfoProperties](../../../connect/jdbc/reference/getclientinfoproperties-method-sqlserverdatabasemetadata.md) メソッドでは、空の結果セットが返されます。  
  
## <a name="see-also"></a>参照  
 [getClientInfo メソッド &#40;SQLServerConnection&#41;](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
