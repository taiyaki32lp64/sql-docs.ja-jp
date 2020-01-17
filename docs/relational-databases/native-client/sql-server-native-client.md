---
title: SQL Server Native Client |Microsoft Docs
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 48a335f4cf3dc3990cbcf6bbf68e82ce76a9e54f
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73759353"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

SNAC (SQL Server Native Client) は、SQL Server の ODBC および OLE DB ドライバーを参照するために使用されていた用語です。

> [!IMPORTANT] 
> SQL Server Native Client (SQLNCLI) は非推奨とされます。新しい開発作業には使用しないことをお勧めします。 代わりに、新しい [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) を使用します。これは、最新のサーバー機能で更新されます。

> [!NOTE]
> SNAC または ODBC ドライバーの詳細とダウンロードについては、「 [SNAC ライフサイクル](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)」で説明されているブログ記事を参照してください。
> ODBC Driver for SQL Server の詳細については、「 [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)」を参照してください。  

 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]と共にリリースされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネイティブクライアント機能については、SQL Server native Client の最新バージョンを参照してください。

-   [SQL Server Native Client における LocalDB のサポート](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [メタデータの検出](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 での UTF-16 のサポート](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [SQL Server Native Client の HADR サポート](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [拡張イベント ログの診断情報へのアクセス](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の ODBC では、Windows 7 SDK の標準 ODBC に追加された3つの機能をサポートしています。  

-   接続関連の操作での非同期実行。 詳細については、「[非同期実行](https://go.microsoft.com/fwlink/?LinkID=191493)」を参照してください。  

-   C データ型の機能拡張。 詳細については、「 [ODBC の C データ型](https://go.microsoft.com/fwlink/?LinkID=191495)」を参照してください。  

     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client でこの機能をサポートするために、アプリケーションの場合、SQLGetDescField は**SQL_C_BINARY**ではなく**SQL_C_SS_TIME2** ( **time**型の場合) または**SQL_C_SS_TIMESTAMPOFFSET** ( **datetimeoffset**の場合) を返すことができます。ODBC 3.8 を使用します。 詳細については、「 [ODBC の日付と時刻の機能強化に関するデータ型のサポート](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)」を参照してください。  

-   小さいバッファーを使用して**SQLGetData**を複数回呼び出して、大きなパラメーター値を取得します。 詳細については、「 [SQLGetData を使用した出力パラメーターの取得](https://go.microsoft.com/fwlink/?LinkID=191494)」を参照してください。  

 次のトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] における [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client の動作の変更点について説明します。  

-   **ICommandWithParameters:: SetParameterInfo**を呼び出すときに、 *pwszName*パラメーターに渡される値は有効な識別子である必要があります。 詳細については、「 [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)」を参照してください。  

-   **SQLDescribeParam**は、常に ODBC 仕様に準拠した値を返します。 詳細については、「 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)」を参照してください。  

-   [文字変換処理での ODBC ドライバーの動作の変更](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>参照  
[SQL Server Native Client のインストール](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client の機能](../../relational-databases/native-client/features/sql-server-native-client-features.md)  
