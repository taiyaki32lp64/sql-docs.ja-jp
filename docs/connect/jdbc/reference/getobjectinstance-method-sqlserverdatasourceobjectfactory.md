---
title: getObjectInstance メソッド (SQLServerDataSourceObjectFactory) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de25e608c9fbdbdf6ff91d08e7a6502765bb590e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67981053"
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>getObjectInstance メソッド (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定したデータ ソース オブジェクトのインスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ref*  
  
 **Object** 値。  
  
 *name*  
  
 オブジェクトの名前。  
  
 *c*  
  
 指定した名前に関連するコンテキストです。  
  
 *h*  
  
 オブジェクトの作成に使用する環境です。  
  
## <a name="return-value"></a>戻り値  
 **Object** 値。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>Remarks  
 この getObjectInstance メソッドは、Javax.naming.spi.objectfactory インターフェイスの getObjectInstance メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSourceObjectFactory のメソッド](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [SQLServerDataSourceObjectFactory のメンバー](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [SQLServerDataSourceObjectFactory クラス](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
