---
title: getApplicationName メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getApplicationName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3b7e55cbaa630a4c191eead93d3e016aa07ea5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954398"
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>getApplicationName メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  アプリケーション名を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>戻り値  
 アプリケーション名を含む**文字列**です。値が設定されていない場合は、"[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" です。  
  
## <a name="remarks"></a>Remarks  
 アプリケーション名は、個別のアプリケーションを識別するために、さまざまな [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] プロファイリング ツールおよびロギング ツールで使用されます。 アプリケーション名を設定しない場合は、getApplicationName メソッドによって非ローカライズ文字列 "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" が返されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
