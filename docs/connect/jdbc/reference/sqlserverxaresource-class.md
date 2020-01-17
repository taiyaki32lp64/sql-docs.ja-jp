---
title: SQLServerXAResource クラス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: df957b79-536f-4db7-b6ac-3d59343559fc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 282201b7ff3f5b2ebfe4d8a1224d4d1b39285c53
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970083"
---
# <a name="sqlserverxaresource-class"></a>SQLServerXAResource クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XA 分散トランザクション管理用の XAResource を表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **拡張:** java.lang.Object  
  
 **実装:** javax.transaction.xa.XAResource  
  
## <a name="syntax"></a>構文  
  
```  
  
public class SQLServerXAResource  
```  
  
## <a name="remarks"></a>Remarks  
 XA トランザクションは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分散トランザクション マネージャー (DTC) を使用して [!INCLUDE[msCoName](../../../includes/msconame_md.md)] に実装されます。 SQLServerXAResource クラスは、DTC とのインターフェイスになる sqljdbc_xa.dll という名前の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 拡張 DLL を呼び出します。 SQLServerXAResource が受信する XA 呼び出し (XA_START、XA_END、XA_PREPARE など) は、対応する DTC 関数の呼び出しにマップされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerXAResource のメンバー](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
