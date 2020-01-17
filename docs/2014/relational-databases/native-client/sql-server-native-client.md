---
title: どのような&#39;s New in SQL Server Native Client |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2a01b9d9d13bf5e9135d287553beb8b87c2dcd5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62638843"
---
# <a name="what39s-new-in-sql-server-native-client"></a>どのような&#39;s New in SQL Server Native Client
  [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] は、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client をインストールします。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client は存在しません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の ODBC ドライバーにはこれ以上の更新プログラムがありません。 Windows の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC Driver 11 for [!INCLUDE[msCoName](../../includes/msconame-md.md)] と呼ばれる、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の ODBC ドライバーに代わるものが [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] と共にインストールされます。 詳細については、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Windows を参照してください。 [for SQL Server - Windows の Microsoft ODBC Driver 11](https://www.microsoft.com/download/details.aspx?id=36434)します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の OLE DB プロバイダーは、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client で最終更新されています。 開発者が OLE DB プロバイダーを使用して最新バージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するには、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client に付属している OLE DB プロバイダーを使用する必要があります。  
  
 次のトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] における [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client の重要な新機能について説明します。  
  
-   [SQL Server Native Client における LocalDB のサポート](features/sql-server-native-client-support-for-localdb.md)  
  
-   [メタデータの検出](features/metadata-discovery.md)  
  
-   [SQL Server Native Client 11.0 での UTF-16 のサポート](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [SQL Server Native Client の HADR サポート](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [拡張イベント ログの診断情報へのアクセス](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 さらに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の ODBC では、Windows 7 SDK の標準 ODBC に追加された 3 つの機能もサポートされるようになりました。  
  
-   接続関連の操作での非同期実行。 詳細については、次を参照してください。[非同期実行](https://go.microsoft.com/fwlink/?LinkID=191493)します。  
  
-   C データ型の機能拡張。 詳細については、次を参照してください。 [ODBC における C データ型](https://go.microsoft.com/fwlink/?LinkID=191495)します。  
  
     この機能をサポートする[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client、SQLGetDescField が返すことができます`SQL_C_SS_TIME2`(の`time`型) または`SQL_C_SS_TIMESTAMPOFFSET`(の`datetimeoffset`) の代わりに`SQL_C_BINARY`アプリケーションで ODBC 3.8 が使用する場合は、します。 詳細については、次を参照してください。 [ODBC の日付と時刻の強化に対するデータ型のサポート](features/date-and-time-improvements.md)します。  
  
-   小さなバッファーを伴う `SQLGetData` を複数回呼び出すことによる、大きなパラメーター値の取得。 詳細については、次を参照してください。 [SQLGetData を使用して出力パラメーターを取得する](https://go.microsoft.com/fwlink/?LinkID=191494)します。  
  
 次のトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] における [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client の動作の変更点について説明します。  
  
-   呼び出すときに`ICommandWithParameters::SetParameterInfo`に渡される値、 *pwszName*パラメーターは、有効な識別子である必要があります。 詳細については、次を参照してください。 [ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md)します。  
  
-   `SQLDescribeParam` は、ODBC 仕様に準拠した値を一貫して返すようになりました。 詳細については、次を参照してください。 [SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md)します。  
  
-   [文字変換処理での ODBC ドライバーの動作の変更](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](features/sql-server-native-client-features.md)  
  
  
