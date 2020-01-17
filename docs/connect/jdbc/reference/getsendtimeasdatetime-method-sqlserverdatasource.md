---
title: getSendTimeAsDatetime メソッド (SQLServerDataSource) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e1396ac28a7e41dbf530f7e4a251876f6c340871
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67979943"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>getSendTimeAsDatetime メソッド (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  このメソッドは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 で追加されました。  
  
 **SendTimeAsDatetime**接続プロパティの設定を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>戻り値  
 値が**datetime**型として[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]サーバーに送信される場合は**true**を指定します。 値が**time**型として[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]サーバーに送信される場合は**false** 。  
  
## <a name="remarks"></a>Remarks  
 **SendTimeAsDatetime**接続プロパティの詳細については、「[接続プロパティの設定](../../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) を使用すると、**sendTimeAsDatetime** 接続プロパティをプログラムから設定することができます。  
  
 詳細については、「 [java .sql の時刻値をサーバーに送信する方法の構成](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource のメンバー](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
