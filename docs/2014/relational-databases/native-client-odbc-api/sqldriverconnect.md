---
title: SQLDriverConnect |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 22d560c8a65d5b9a7cebc4062ddd2d1ce936d5a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067748"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、接続文字列のキーワードを置き換えたり、拡張したりするための接続属性を定義します。 接続文字列のいくつかのキーワードには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが指定する既定値があります。  
  
 使用できるキーワードの一覧については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを参照してください[使用した Connection String Keywords with SQL Server Native Client を使用して](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)します。  
  
 詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]接続属性とドライバーの既定の動作を参照してください。 [SQLSetConnectAttr](sqlsetconnectattr.md)します。  
  
 有効な接続文字列キーワードの詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client を参照してください[使用した Connection String Keywords with SQL Server Native Client を使用して](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)します。  
  
 ときに、 `SQLDriverConnect` *DriverCompletion*パラメーター値が SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE、または sql_driver_complete_required の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーからキーワード値を取得します表示されるダイアログ ボックス。 接続文字列でキーワード値が渡され、ユーザーがダイアログ ボックスでキーワードの値を変更しなかった場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは接続文字列の値を使用します。 接続文字列で値が設定されていない場合、ユーザーがダイアログ ボックスで割り当てを行わないと、ドライバーは既定値を使用します。  
  
 `SQLDriverConnect` 有効なを指定する必要があります*WindowHandle*いずれかが*DriverCompletion*値が必要です (または必要があります)、ドライバーの接続 ダイアログ ボックスの表示。 無効なハンドルを指定すると、SQL_ERROR が返されます。  
  
 DRIVER キーワードまたは DSN キーワードを指定します。 ODBC は、これらの 2 つのキーワードが両方指定されている場合、左側に指定されているキーワードを使用し、他方を無視するように指示します。 ドライバーが指定されているか、2 つの場合、 `SQLDriverConnect` *DriverCompletion*パラメーター値が SQL_DRIVER_NOPROMPT、SERVER キーワードと、適切な値が必要です。  
  
 SQL_DRIVER_NOPROMPT が指定されているときは、ユーザー認証に関するキーワードに値が指定されている必要があります。 ドライバーは、文字列 "Trusted_Connection=yes" または UID キーワードと PWD キーワードの両方が指定されていることを確認します。  
  
 場合、 *DriverCompletion*パラメーター値が SQL_DRIVER_NOPROMPT または SQL_DRIVER_COMPLETE_REQUIRED と言語またはデータベースが接続文字列から取得し、いずれかが有効でない`SQLDriverConnect`SQL_ERROR を返します。  
  
 場合、 *DriverCompletion*パラメーター値が SQL_DRIVER_NOPROMPT または SQL_DRIVER_COMPLETE_REQUIRED と言語またはデータベースが ODBC データ ソースの定義から取得し、いずれかが有効でない`SQLDriverConnect`既定の使用言語またはデータベースの指定されたユーザー ID、SQL_SUCCESS_WITH_INFO を返します。  
  
 場合、 *DriverCompletion*パラメーター値が SQL_DRIVER_COMPLETE または SQL_DRIVER_PROMPT とかどうか、言語またはデータベースの無効な`SQLDriverConnect` ダイアログ ボックスを再表示します。  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>SQLDriverConnect の HADR サポート  
 使用しての詳細については`SQLDriverConnect`への接続に、[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]クラスターを参照してください[SQL Server Native Client のサポート高可用性、ディザスター リカバリー](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)します。  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>SQLDriverConnect によるサービス プリンシパル名 (SPN) のサポート  
 SQLDDriverConnect では、ダイアログ ボックスの確認が有効になっている ODBC のログインを使用します。 これにより、プリンシパル サーバーとそのフェールオーバー パートナーの両方に対して SPN を入力できます。  
  
 SQLDriverConnect が新しい接続文字列キーワードを受け入れる`ServerSPN`と`FailoverPartnerSPN`、し、新しい接続属性である SQL_COPT_SS_SERVER_SPN および SQL_COPT_SS_FAILOVER_PARTNER_SPN が認識されます。  
  
 接続属性の値が複数指定されている場合は、DSN の値や接続文字列の値より、プログラムによって設定された値が優先されます。 DSN の値は接続文字列の値より優先されます。  
  
 接続が開いている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client では、SQL_COPT_SS_MUTUALLY_AUTHENTICATED および SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD が、接続を開くときに使用された認証方式に設定されます。  
  
 Spn の詳細については、次を参照してください。[サービス プリンシパル名&#40;Spn&#41;クライアント接続で&#40;ODBC&#41;](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)します。  
  
## <a name="examples"></a>使用例  
 次の呼び出しに必要なデータ量が少なくを示しています`SQLDriverConnect`:。  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 次の接続文字列は、最低限必要なデータを示していますときに、 *DriverCompletion*パラメーター値が SQL_DRIVER_NOPROMPT:。  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>参照  
 [SQLDriverConnect 関数](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)  
  
  
