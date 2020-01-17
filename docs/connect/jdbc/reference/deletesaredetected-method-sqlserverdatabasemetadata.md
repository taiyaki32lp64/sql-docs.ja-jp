---
title: deletesAreDetected メソッド (SQLServerDatabaseMetaData) |Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.deletesAreDetected
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 73f3d994-bbd7-43d2-8b64-50057e278983
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aef2ebd78b1aed2d03ba56ef3371d7f0dbfade31
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67955129"
---
# <a name="deletesaredetected-method-sqlserverdatabasemetadata"></a>deletesAreDetected メソッド (SQLServerDatabaseMetaData)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) メソッドを呼び出すことで可視の行が削除されたことを検出できるかどうかを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
public boolean deletesAreDetected(int type)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *type*  
  
 結果セットの種類を示す **int** です。java.sql.ResultSet または SQLServerResultSet での定義に従って、次のいずれかの値を指定できます。  
  
## <a name="javasqlresultset-types"></a>java.sql.ResultSet の種類  
 TYPE_FORWARD_ONLY  
  
 TYPE_SCROLL_SENSITIVE  
  
 TYPE_SCROLL_INSENSITIVE  
  
## <a name="sqlserverresultset-types"></a>SQLServerResultSet の種類  
 TYPE_SS_SCROLL_STATIC  
  
 TYPE_SS_SCROLL_KEYSET  
  
 TYPE_SS_DIRECT_FORWARD_ONLY  
  
 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY  
  
 TYPE_SS_SCROLL_DYNAMIC  
  
## <a name="return-value"></a>戻り値  
 削除された行がギャップに置き換わる場合は**true** 。 削除された行が削除された場合は**false** 。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースと共に使用している場合、このメソッドは TYPE_SS_SCROLL_KEYSET カーソルに対して **true** を返し、それ以外のすべての結果セットの種類に対して **false** が返されます。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この deletesAreDetected メソッドは、deletesAreDetected メソッドによって、java メタデータインターフェイスで指定されます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は更新可能なすべてのカーソルの種類の削除された行を検出しますが、順方向カーソルと動的カーソルについては、検出は一時的です。  
  
## <a name="see-also"></a>参照  
 [SQLServerDatabaseMetaData のメソッド](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [SQLServerDatabaseMetaData のメンバー](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [SQLServerDatabaseMetaData クラス](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
