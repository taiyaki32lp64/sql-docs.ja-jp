---
title: getLastUpdateCount メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0d284e02be13af60bf7d8e7d447835f7eccd90a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982602"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>getLastUpdateCount メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  lastUpdateCount プロパティが有効であるかどうかを示す **Boolean** 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>戻り値  
 lastUpdateCount が有効な場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>Remarks  
 lastUpdateCount プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は、サーバーに渡された SQL ステートメントから最終的な更新数のみを返します。 lastUpdateCount プロパティが **false** に設定されている場合、ドライバーは、発生した可能性があるすべてのトリガーが返した更新数を含む、すべての更新数を返します。 lastUpdateCount プロパティが設定されていない場合、getLastUpdateCount メソッドは既定値の **true** を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
