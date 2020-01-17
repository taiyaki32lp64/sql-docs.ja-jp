---
title: Setワークステーション Id メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08b09958276a5cc7f7cc3de6e56f7d7336ca9e64
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67972036"
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>setWorkstationID メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データ ソースへの接続に使用されるクライアント コンピューターの名前を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *workstationID*  
  
 クライアント コンピューターの名前を含む **String** です。  
  
## <a name="remarks"></a>Remarks  
 workstationID は、クライアント コンピューターまたはワークステーションの名前です。 "ワークステーション Id" プロパティが設定されていない場合、既定値は、InetAddress () メソッドを呼び出すことによって作成されます。 GetHostName が空の値を返す場合は、getHostAddress (). toString () メソッドが呼び出されます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
