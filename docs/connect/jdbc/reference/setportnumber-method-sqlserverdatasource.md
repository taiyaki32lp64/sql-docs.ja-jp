---
title: setPortNumber メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c171e8fb78553275d6a1f5d4bcce485a470f94a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67973192"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>setPortNumber メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用されるポート番号を設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *portNumber*  
  
 ポート番号を含む **int** 値です。  
  
## <a name="remarks"></a>Remarks  
 このポート番号は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] へのソケット接続を開くときに使用される TCP/IP ポート番号です。 portNumber プロパティが設定されていない場合、[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) メソッドは既定値の 1433 が返されます。  
  
> [!NOTE]  
>  SetPortNumber メソッドでは、渡されたポート値に対する範囲チェックは行われません。 エラーをトリガーすることなく、99999のように、無効なポート番号を渡すことができます。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
