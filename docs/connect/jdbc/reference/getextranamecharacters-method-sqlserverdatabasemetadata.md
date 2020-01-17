---
title: getExtraNameCharacters メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExtraNameCharacters
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a22becfe-0f07-4a15-8d11-06d4054b2369
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a4aada79019aad4ae01729de8e018edd728b473
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67983320"
---
# <a name="getextranamecharacters-method-sqlserverdatabasemetadata"></a>getExtraNameCharacters メソッド (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  引用符で囲まれていない識別子名に使用できるすべての特殊文字 (a ～ z、A ～ Z、0 ～ 9、および _ 以外) を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getExtraNameCharacters()  
```  
  
## <a name="return-value"></a>戻り値  
 特殊文字を含む **String** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この getExtraNameCharacters メソッドは、getExtraNameCharacters メソッドによって、java メタデータインターフェイスで指定されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースで [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] を使用している場合、このメソッドは $、#、および \@ の特殊文字を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
