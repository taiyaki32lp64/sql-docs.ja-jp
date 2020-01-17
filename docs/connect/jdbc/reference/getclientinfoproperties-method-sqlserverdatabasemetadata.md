---
title: getClientInfoProperties メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08b919ec6b626cd61b757b380d24efffcada0d55
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953105"
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>getClientInfoProperties メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  ドライバーがサポートしているクライアント情報のプロパティの一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>戻り値  
 ResultSet オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getClientInfoProperties メソッドは、java メタデータインターフェイスの getClientInfoProperties メソッドによって指定されます。  
  
> [!NOTE]  
>  このメソッドでは、空の結果セットが返されます。 ドライバーは**applicationname**の設定のみをサポートし、 **applicationname**は接続時にのみ設定されます。 SQL Server では、接続が確立された後のクライアント アプリケーション情報の更新はサポートされていません。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
