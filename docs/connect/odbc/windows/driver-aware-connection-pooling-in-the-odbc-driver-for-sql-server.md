---
title: ODBC Driver for SQL Server のドライバー対応接続プール | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 455ab165-8e4d-4df9-a1d7-2b532bfd55d6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97ddd5aa4abf926ecd4e68e89bef63b8f25ce323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009973"
---
# <a name="driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server"></a>OLE DB Provider for SQL Server のドライバー対応接続プール
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、[ドライバー対応の接続プール](https://msdn.microsoft.com/library/hh405031(VS.85).aspx)をサポートしています。 このトピックでは、Windows 上の Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のドライバー対応接続プールに追加された機能強化について説明します。  
  
-   `SQLDriverConnect` を使用する接続は、接続のプロパティに関係なく、`SQLConnect` を使用する接続とは別のプールに移動されます。
- [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証とドライバー対応接続プールを使用する場合、ドライバーでは、現在のスレッドでプール内の接続を分離するために Windows ユーザーのセキュリティ コンテキストが使用されません。 つまり、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証での Windows での権限借用シナリオでの接続と、接続パラメーターが同じで、バックエンドとの接続に同じ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証資格証明を使用する場合、別の Windows ユーザーが同じプール接続を使用できる可能性があります。 Windows 認証とドライバー対応接続プールを使用する場合、ドライバーでは、プール内の接続を分離するために現在の Windows ユーザーのセキュリティ コンテキストが使用されます。 つまり、Windows での権限借用のシナリオでは、接続で同じパラメーターを使用していても、別の Windows ユーザーは同じ接続を使用しません。
- Azure Active Directory とドライバー対応の接続プールを使用する場合、ドライバーは、認証値を使用して接続プールのメンバーシップを決定します。
  
-   ドライバー対応接続プールは、無効な接続がプールから返されないようにします。  
  
-   ドライバー対応接続プールは、ドライバーに固有の接続属性を認識します。 そのため、接続`SQL_COPT_SS_APPLICATION_INTENT`が読み取り専用に設定されている場合、その接続は独自の接続プールを取得します。
-   属性を`SQL_COPT_SS_ACCESS_TOKEN`設定すると、接続が個別にプールされます。 
  
次のいずれかの接続属性 ID または接続文字列キーワードが、接続文字列と、プールされた接続文字列の間で異なる場合、ドライバーはプールされた接続を使用します。 ただし、すべての接続属性 ID または接続文字列キーワードが一致する場合、パフォーマンスは向上します。 (プール内で接続を一致させるために、ドライバーは属性をリセットします。 次のパラメーターをリセットする場合、ネットワーク呼び出しを追加で実行する必要があるので、パフォーマンスは低下します。  
  
-    次の接続属性または接続キーワードの 2 つ以上が異なる場合、プールされた接続は使用されません。  
  
  - `Language`  
  - `QuoteId`  
  - `SQL_ATTR_TXN_ISOLATION` 
  - `SQL_COPT_SS_QUOTED_IDENT`  
  
-   接続文字列とプールされた接続文字列の次のいずれかの接続キーワードの間に違いがある場合、プールされた接続は使用されません。  
  
    |Keyword|ODBC ドライバー 13|ODBC ドライバー 11|
    |-|-|-|
    |`Address`|はい|はい|
    |`AnsiNPW`|はい|はい|
    |`App`|はい|はい|
    |`ApplicationIntent`|はい|はい|  
    |`Authentication`|はい|いいえ|
    |`ColumnEncryption`|はい|いいえ|
    |`Database`|はい|はい|
    |`Encrypt`|はい|はい|  
    |`Failover_Partner`|はい|はい|
    |`FailoverPartnerSPN`|はい|はい|
    |`MARS_Connection`|はい|はい|
    |`Network`|はい|はい|
    |`PWD`|はい|はい|
    |`Server`|はい|はい|
    |`ServerSPN`|はい|はい|
    |`TransparentNetworkIPResolution`|はい|はい|
    |`Trusted_Connection`|はい|はい|
    |`TrustServerCertificate`|はい|はい|
    |`UID`|はい|はい|
    |`WSID`|はい|はい|
    
- 接続文字列とプールされた接続文字列の次のいずれかの接続属性の間に違いがある場合、プールされた接続は使用されません。  
  
    |属性|ODBC ドライバー 13|ODBC ドライバー 11|  
    |-|-|-|  
    |`SQL_ATTR_CURRENT_CATALOG`|はい|はい|
    |`SQL_ATTR_PACKET_SIZE`|はい|はい|
    |`SQL_COPT_SS_ANSI_NPW`|はい|はい|
    |`SQL_COPT_SS_ACCESS_TOKEN`|はい|いいえ|
    |`SQL_COPT_SS_AUTHENTICATION`|はい|いいえ|
    |`SQL_COPT_SS_ATTACHDBFILENAME`|はい|はい|
    |`SQL_COPT_SS_BCP`|はい|はい|
    |`SQL_COPT_SS_COLUMN_ENCRYPTION`|はい|いいえ|
    |`SQL_COPT_SS_CONCAT_NULL`|はい|はい|
    |`SQL_COPT_SS_ENCRYPT`|はい|はい|
    |`SQL_COPT_SS_FAILOVER_PARTNER`|はい|はい|
    |`SQL_COPT_SS_FAILOVER_PARTNER_SPN`|はい|はい|
    |`SQL_COPT_SS_INTEGRATED_SECURITY`|はい|はい|
    |`SQL_COPT_SS_MARS_ENABLED`|はい|はい|
    |`SQL_COPT_SS_OLDPWD`|はい|はい|
    |`SQL_COPT_SS_SERVER_SPN`|はい|はい|
    |`SQL_COPT_SS_TRUST_SERVER_CERTIFICATE`|はい|はい|
    |`SSPROP_AUTH_REPL_SERVER_NAME`|はい|はい|
    |`SQL_COPT_SS_TNIR`|はい|いいえ|
 
-   ドライバーは追加でネットワーク呼び出しを行うことなく、次の接続キーワードと属性をリセットおよび調整できます。 ドライバーは接続に誤った情報が含まれないように、これらのパラメーターをリセットします。  
  
     これらの接続キーワードは、ドライバー マネージャがプール内の接続とユーザーの接続を一致させるときには考慮されません (これらのいずれかのパラメーターを変更した場合でも、既存の接続を再利用できます。 必要に応じて、ドライバーによりこれらのオプションがリセットされます。)これらの属性は、追加でネットワーク呼び出しを行わずに、クライアント側でリセットできます。  
  
    |Keyword|ODBC ドライバー 13|ODBC ドライバー 11|  
    |-|-|-|  
    |`AutoTranslate`|はい|はい|
    |`Description`|はい|はい|
    |`MultisubnetFailover`|はい|はい|  
    |`QueryLog_On`|はい|はい|
    |`QueryLogFile`|はい|はい|
    |`QueryLogTime`|はい|はい|
    |`Regional`|はい|はい|
    |`StatsLog_On`|はい|はい|
    |`StatsLogFile`|  はい|はい|
  
     次のいずれかの接続属性を変更した場合、既存の接続を再利用できます。  必要に応じて、ドライバーによって値がリセットされます。 ドライバーは追加のネットワーク呼び出しを行うことなく、クライアントでこれらの属性をリセットできます。  
  
    |属性|ODBC ドライバー 13|ODBC ドライバー 11|  
    |-|-|-|  
    |すべてのステートメント属性|はい|はい|
    |`SQL_ATTR_AUTOCOMMIT`|はい|はい|
    |`SQL_ATTR_CONNECTION_TIMEOUT`|  はい|はい|
    |`SQL_ATTR_DISCONNECT_BEHAVIOR SQL_ATTR_CONNECTION_TIMEOUT`|はい|はい|
    |`SQL_ATTR_LOGIN_TIMEOUT`|はい|はい|
    |`SQL_ATTR_ODBC_CURSORS`|  はい|はい|
    |`SQL_COPT_SS_PERF_DATA`|はい|はい|
    |`SQL_COPT_SS_PERF_DATA_LOG`|はい|はい|
    |`SQL_COPT_SS_PERF_DATA_LOG_NOW`| はい|はい| 
    |`SQL_COPT_SS_PERF_QUERY`|はい|はい|
    |`SQL_COPT_SS_PERF_QUERY_INTERVAL`|はい|はい|
    |`SQL_COPT_SS_PERF_QUERY_LOG`|  はい|はい|
    |`SQL_COPT_SS_PRESERVE_CURSORS`|はい|はい|
    |`SQL_COPT_SS_TRANSLATE`|はい|はい|
    |`SQL_COPT_SS_USER_DATA`|  はい|はい|
    |`SQL_COPT_SS_WARN_ON_CP_ERROR`|はい|はい|  
  
## <a name="see-also"></a>参照  
 [Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
