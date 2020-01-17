---
title: 検証を伴わない暗号化の使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], encryption
- cryptography [SQL Server Native Client]
- SQLNCLI, encryption
- encryption [SQL Server Native Client]
- SQL Server Native Client, encryption
ms.assetid: f4c63206-80bb-4d31-84ae-ccfcd563effa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 443c6e0c556a7e69510796b1d58ab0f7b2567e6e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63225494"
---
# <a name="using-encryption-without-validation"></a>検証を伴わない暗号化の使用
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、常に、ログインに関連するネットワーク パケットを暗号化します。 サーバーの起動時に証明書がサーバーに提供されないと、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] はログイン パケットの暗号化に使用される自己署名入りの証明書を生成します。  
  
 アプリケーションでは、接続文字列キーワードまたは接続プロパティを使用して、すべてのネットワーク トラフィックの暗号化を要求することもできます。 キーワードは、プロバイダー文字列を使用する場合、ODBC および OLE DB の"Encrypt"を**idbinitialize::initialize**、または"Use Encryption for Data"ADO および OLE DB 初期化文字列を使用する場合の**IDataInitialize**. これは、ことがありますで構成することも[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager を使用して、 **Force Protocol Encryption**オプション。 既定では、接続のネットワーク トラフィックをすべて暗号化するには、証明書をサーバーに提供する必要があります。  
  
 接続文字列キーワードについては、次を参照してください。[使用した Connection String Keywords with SQL Server Native Client を使用して](../applications/using-connection-string-keywords-with-sql-server-native-client.md)します。  
  
 証明書がサーバーに提供されていないときに暗号化を有効にするには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 構成マネージャーを使用して **[Force Protocol Encryption]** オプションと **[Trust Server Certificate]** オプションの両方を設定できます。 この場合、検証可能な証明書がサーバーに提供されなかった場合は、暗号化には検証を伴わない自己署名入りのサーバー証明書を使用します。  
  
 アプリケーションでは、暗号化が行われることを保証するために "TrustServerCertificate" キーワードまたはそれに関連する接続属性も使用できます。 アプリケーションの設定によって、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] クライアント構成マネージャーで設定されるセキュリティのレベルを緩和することはできません。ただし、厳密にすることはできます。 たとえば、クライアントに **[Force Protocol Encryption]** オプションが設定されていない場合、アプリケーションから暗号化自体を要求することができます。 サーバー証明書が提供されなかった場合でも暗号化を保証するには、アプリケーションから暗号化と "TrustServerCertificate" を要求できます。 ただし、クライアントの構成で "TrustServerCertificate" が有効になっていない場合は、サーバー証明書を提供する必要があります。 次の表ですべてのケースを説明します。  
  
|[Force Protocol Encryption] クライアント設定|[Trust Server Certificate] クライアント設定|接続文字列/接続属性 Encrypt/Use Encryption for Data|接続文字列/接続属性 Trust Server Certificate|結果|  
|----------------------------------------------|---------------------------------------------|------------------------------------------------------------------------------|----------------------------------------------------------------------|------------|  
|いいえ|なし|いいえ (既定値)|無視|暗号化は行われません。|  
|いいえ|なし|はい|いいえ (既定値)|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|いいえ|なし|はい|はい|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
|はい|いいえ|無視|無視|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|はい|はい|いいえ (既定値)|無視|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
|はい|[はい]|はい|いいえ (既定値)|暗号化は、検証可能なサーバー証明書が提供されている場合にのみ行われます。それ以外の場合は、接続試行が失敗します。|  
|はい|[はい]|[はい]|はい|暗号化は常に行われますが、自己署名入りのサーバー証明書を使用することがあります。|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーには、DBPROPSET_SQLSERVERDBINIT プロパティで実装されて SSPROP_INIT_TRUST_SERVER_CERTIFICATE データ ソース初期化プロパティの追加検証を伴わない暗号化がサポートしています設定します。 また、新しい接続文字列のキーワードとして "TrustServerCertificate" が追加されました。 "TrustServerCertificate" は、yes または no を値として受け取ります。既定値は no です。 サービス コンポーネントを使用しているときは、"TrustServerCertificate" は true または false を値として受け取ります。既定値は false です。  
  
 DBPROPSET_SQLSERVERDBINIT プロパティ セットに加えられた機能強化の詳細については、次を参照してください。[初期化プロパティと承認プロパティ](../../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)します。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーへの追加検証を伴わない暗号化のサポート、 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)と[SQLGetConnectAttr](../../native-client-odbc-api/sqlgetconnectattr.md)関数。 SQL_TRUST_SERVER_CERTIFICATE_YES または SQL_TRUST_SERVER_CERTIFICATE_NO を受け取る、SQL_COPT_SS_TRUST_SERVER_CERTIFICATE が追加されました。既定値は SQL_TRUST_SERVER_CERTIFICATE_NO です。 また、新しい接続文字列のキーワードとして "TrustServerCertificate" が追加されました。 "TrustServerCertificate" は、"yes" または "no" を値として受け取ります。既定値は "no" です。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](sql-server-native-client-features.md)  
  
  
