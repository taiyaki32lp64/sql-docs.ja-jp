---
title: getLockTimeout メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9c94e0c69bd528f1c579f41319a4db18b7d4d3c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67982562"
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>getLockTimeout メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  データベースがロック タイムアウトを通知するまでに待機する時間 (ミリ秒) を示す **int** 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>戻り値  
 データベースが待機する時間 (ミリ秒) を含む **int** 値です。  
  
## <a name="remarks"></a>Remarks  
 ロック タイムアウトは、データベースがロック タイムアウトを通知するまでに待機する時間 (ミリ秒) です。既定値の -1 は、無制限に待機することを意味します。 値を指定した場合、接続上のすべてのステートメントに対する既定値になります。  
  
> [!NOTE]  
>  値 0 を指定した場合、待機が行われません。 lockTimeout プロパティが設定されていない場合、getLockTimeout メソッドは既定値の -1 を返します。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
