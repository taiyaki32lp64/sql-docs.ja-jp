---
title: getXopenStates メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de6fdf6b-8345-4490-b35e-7115b61e782e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5c263a94b8df0337d05cc8f3ee41df4e2f30fc72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67977933"
---
# <a name="getxopenstates-method-sqlserverdatasource"></a>getXopenStates メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  XOPEN 互換の状態への SQL 状態の変換が有効になっているかどうかを示す **boolean** 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getXopenStates()  
```  
  
## <a name="return-value"></a>戻り値  
 XOPEN 互換の状態への SQL 状態の変換が有効になっている場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="remarks"></a>Remarks  
 xopenStates プロパティが **true** に設定されている場合、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は SQL 状態を XOPEN 互換の状態に変換します。 既定値は **false** です。この場合、JDBC ドライバーは SQL 99 の状態コードを生成します。 xopenStates が設定されていない場合、getXopenStates メソッドは既定値の **false** を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
