---
title: getTrustServerCertificate メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81d07743dfefe0b0305b1a094a9ae4632d4effd9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67978581"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>getTrustServerCertificate メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  trustServerCertificate プロパティが有効であるかどうかを示す**ブール**値が返されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>戻り値  
 trustServerCertificate が有効な場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>Remarks  
 trustServerCertificate プロパティが **true** に設定されている場合、通信レイヤーが SSL (Secure Sockets Layer) で暗号化されているときに、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の SSL 証明書が自動的に信頼されます。 つまり、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] によって [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の SSL 証明書は検証されません。 既定値は **false**です。  
  
 trustServerCertificate プロパティが **false** に設定されている場合は、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] によってサーバーの SSL 証明書が検証されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
