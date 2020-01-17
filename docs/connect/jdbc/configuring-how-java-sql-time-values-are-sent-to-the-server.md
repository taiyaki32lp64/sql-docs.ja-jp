---
title: java.sql.Time の値をサーバーに送信する方法の構成 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 07eb00dd-621a-46f9-a5a5-8cab4d6058b5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fe6969d51834d0798a530b9cc9926af1b27fec2
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028235"
---
# <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>java.sql.Time の値をサーバーに送信する方法の構成
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  パラメーターを設定するために java.sql.Time オブジェクトまたは java.sql.Types.TIME JDBC 型を使用する場合、サーバーに対して java.sql.Time 値をどのように送信するか ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **time** 型として送信するか、**datetime** 型として送信するか) を構成することができます。  
  
 次のいずれかのメソッドを使用するケースが、このシナリオに該当します。  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int.md)  
  
-   [SQLServerCallableStatement.registerOutParameter(int, int, int)](../../connect/jdbc/reference/registeroutparameter-method-int-int-int.md)  
  
-   [SQLServerCallableStatement.setTime](../../connect/jdbc/reference/settime-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setTime](../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)  
  
-   [SQLServerCallableStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlservercallablestatement.md)  
  
-   [SQLServerPreparedStatement.setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)  
  
 java.sql.Time 値の送信方法を構成するには **sendTimeAsDatetime** 接続プロパティを使用します。 詳細については、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」を参照してください。  
  
 **sendTimeAsDatetime** 接続プロパティの値は、[SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) を使用してプログラムから変更できます。  
  
 より[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前のバージョンのでは、**time** データ型がサポートされていないため、**smalldatetime** を使用するアプリケーションでは、通常、**datetime** またはデータ型として java.sql.time 値を格納します。 [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)]  
  
 **Smalldatetime** 値を使用するときに**datetime**データ型と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型を使用する場合は、 **sendTimeAsDatetime**接続プロパティを**true**に設定する必要があります。 **SendTimeAsDatetime**接続プロパティを**false**に設定して、 **time** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型を使用する場合は、time データ型を使用する必要があります。  
  
 日付と時刻の両方を格納できるパラメーターに java.sql.Time 値を送信した場合、java.sql.Time 値の送信方法によって、既定の日付は異なる点に注意してください。**datetime** 値として送信された場合は 1/1/1970 に、**time** 値として送信された場合は 1/1/1900 になります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にデータを送信する際のデータ変換の詳細については、「[日時データの使用](https://go.microsoft.com/fwlink/?LinkID=145211)」を参照してください。  
  
 JDBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Driver 3.0 では、 **sendTimeAsDatetime**は既定で true に設定されています。 今後のリリースでは、**sendTimeAsDatetime** 接続プロパティの既定値が false になる予定です。  
  
 アプリケーションの動作が **sendTimeAsDatetime** 接続プロパティの既定値に左右されないようにするための対策としては、次のような方法があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の **time** データ型を使用する場合は java.sql.Time を使用する。  
  
-   **Datetime**、 **smalldatetime**、および**datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型を操作する場合は、java. Timestamp を使用します。  
  
暗号化された列が time から datetime への変換をサポートしていないため、SendTimeAsDatetime は false である必要があります。 Microsoft JDBC Driver 6.0 for SQL Server の場合、SQLServerConnection クラスには、sendTimeAsDatetime プロパティの値を設定/取得する次の2つのメソッドがあります。

```java
  public boolean getSendTimeAsDatetime()
  public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)
```
  
## <a name="see-also"></a>参照
 [JDBC ドライバーのデータ型について](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
