---
title: ODBC サービス プロバイダー インターフェイス (SPI) リファレンス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88053620fa413c50a8faff4cc47cbbe1457249f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073835"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>ODBC サービス プロバイダー インターフェイス (SPI) リファレンス
これまでは、ODBC アプリケーション プログラミング インターフェイス (API) を定義します。 アプリケーションは、API 内の関数を呼び出すことができるし、ドライバー マネージャーとドライバーの両方で実装する必要があります。  
  
 ドライバー対応接続プール機能の追加により、ODBC には、サービス プロバイダー インターフェイス (SPI) が導入されています。 SPI 内の関数は、ドライバー マネージャーとドライバーの間の通信に使用されます。 SPI 関数は、ドライバーによって実装されます。ドライバー マネージャーは、アプリケーションに SPI 関数を公開しません。 アプリケーションでは、これらの関数を直接呼び出さないでください。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
 このセクションには、次のトピックが含まれています。  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>関連項目  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [ドライバー マネージャーの接続プール](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
