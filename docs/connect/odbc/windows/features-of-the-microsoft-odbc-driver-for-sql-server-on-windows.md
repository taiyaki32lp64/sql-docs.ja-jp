---
title: Windows での Microsoft ODBC Driver for SQL Server の機能 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76326eeb-1144-4b9f-85db-50524c655d30
author: v-makouz
ms.author: genemi
ms.openlocfilehash: 6e3f7929c17b161d3534474d3d9ad99e559714d2
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653804"
---
# <a name="features-of-the-microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows の機能
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

    
## <a name="microsoft-odbc-driver-174-for-sql-server-on-windows"></a>Windows の Microsoft ODBC Driver 17.4 for SQL Server

ODBC ドライバー17.4 には、TCP Keep-alive 設定を調整する機能が含まれています。 これらは、ドライバーまたは DSN のレジストリキーに値を追加することによって変更できます。 キーは、システムデータ`HKEY_LOCAL_MACHINE\Software\ODBC\`ソース`HKEY_CURRENT_USER\Software\ODBC\`の場合はに、ユーザーデータソースの場合はにあります。 DSN の場合は、 `...\Software\ODBC\ODBC.INI\<DSN Name>` `...\Software\ODBC\ODBCINST.INI\ODBC Driver 17 for SQL Server`ドライバーのに対して値をに追加する必要があります。

詳細については、「 [ODBC コンポーネントのレジストリエントリ](../../../odbc/reference/install/registry-entries-for-odbc-components.md)」を参照してください。

その値は `REG_SZ` で、次のとおりです。

- `KeepAlive`キープアライブパケットを送信して、アイドル状態の接続がまだ破損していないことを TCP が確認する頻度を制御します。 既定値は 30 秒です。

- `KeepAliveInterval`応答が受信されるまで、キープアライブの再送信を分離する間隔を決定します。 既定値は 1 秒です。



## <a name="microsoft-odbc-driver-131-for-sql-server-on-windows"></a>Windows の Microsoft ODBC Driver 13.1 for SQL Server

ODBC Driver 13.1 for SQL Server には、以前のバージョン (11) のすべての機能が含まれており、Microsoft SQL Server 2016 と組み合わせて使用する場合に Always Encrypted と Azure Active Directory 認証のサポートが追加されます。  
  
Always Encrypted を使用すると、クライアントは SQL Server に暗号化キーを開示することなく、クライアント アプリケーション内の機密データを暗号化することができます。 クライアント コンピューターにインストールされている、Always Encrypted が有効のドライバーは、SQL Server クライアント アプリケーション内の機密データを自動的に暗号化および暗号化解除することで、この処理を実行します。 ドライバーは、SQL Server にデータを渡す前に機密性の高い列のデータを暗号化し、アプリケーションに対するセマンティクスが維持されるように自動的にクエリを書き換えます。 同様に、ドライバーはクエリ結果に含まれている暗号化されたデータベース列に格納されているデータを透過的に暗号化解除します。 詳しくは、「[Using Always Encrypted with the ODBC Driver](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)」(ODBC ドライバーでの Always Encrypted の使用) をご覧ください。
 
Azure Active Directory を使用すると、ユーザー、DBA、およびアプリケーションのプログラマは、Azure Active Directory の id を使用して Microsoft Azure SQL Database および Microsoft SQL Server 2016 に接続するメカニズムとして Azure Active Directory 認証を使用できます (Azure AD). 詳細については、「 [ODBC ドライバーでの Azure Active Directory の使用](../../../connect/odbc/using-azure-active-directory.md)」および「 [Azure Active Directory 認証を使用した SQL Database または SQL Data Warehouse への接続](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)」を参照してください。   
  
## <a name="microsoft-odbc-driver-11-for-sql-server-on-windows"></a>Windows の Microsoft ODBC Driver 11 for SQL Server  

ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に付属の [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]Native Client ODBC ドライバーのすべての機能が含まれています。 詳細については、「 [SQL Server Native Client プログラミング](../../../relational-databases/native-client/sql-server-native-client-programming.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、Windows オペレーティング システムに付属の ODBC ドライバーに基づいています。 詳細については、「 [Windows Data Access Components SDK](https://msdn.microsoft.com/library/aa968814(VS.85).aspx)」を参照してください。  
  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のこのリリースには、次の新機能が含まれています。  
  
### <a name="bcpexe--l-option-for-specifying-a-login-timeout"></a>ログイン タイムアウトを指定するための bcp.exe -l オプション
 
\- l オプションでは、サーバーへの接続の試行時に、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への `bcp.exe` のログインがタイムアウトするまでの秒数を指定します。 既定のログインタイムアウトは15秒です。 ログイン タイムアウトは、0 から 65,534 の数値にする必要があります。 指定した値が数値以外の場合、または範囲外の場合、`bcp.exe` はエラー メッセージを生成します。 値が0の場合は、タイムアウトが無制限であることを示します。 (約) 10 秒未満のログイン タイムアウトは信頼できません。  
  
### <a name="driver-aware-connection-pooling"></a>ドライバー対応接続プール  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、[ドライバー対応の接続プール](https://msdn.microsoft.com/library/hh405031(VS.85).aspx)をサポートしています。 詳細については、「 [ODBC Driver for SQL Server のドライバー対応接続プール | Microsoft Docs](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)」を参照してください。  
  
### <a name="asynchronous-execution-notification-method"></a>非同期実行 (通知方法)  
ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、[非同期実行 (通知方法)](https://msdn.microsoft.com/library/hh405038(VS.85).aspx) をサポートしています。 使用例については、「[非同期実行 &#40;通知方法&#41; の例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)」を参照してください。  
  
### <a name="connection-resiliency"></a>接続の回復
アプリケーションを Microsoft Azure SQL データベースに接続されたままにするため、Windows 上の ODBC ドライバーは、アイドル状態の接続を復元できます。 詳細については、「 [Windows ODBC ドライバーの接続レジリエンシー](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)」を参照してください。  
  
## <a name="behavior-changes"></a>動作の変更

Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Clientでは`sqlcmd.exe` 、のオプションを指定すると、表示幅が0の場合、出力が1MBで切り捨てられます。`-y0`
  
ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 以降では、`-y0` を指定したときに、1 つの列で取得できるデータの量に制限がなくなりました。 `sqlcmd.exe` は、最大 2 GB ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のデータ型の最大値) の列をストリームするようになりました。  
  
もう1つの違いは`-h` 、 `-y0`との両方を指定すると、オプションに互換性がないというエラーを報告するようになりました。 列見出し間に出力する行数を指定する `-h` は、`-y0` と互換性がなく、ヘッダーは出力されませんでしたが、無視されました。
  
`-y0` を使用すると、返されるデータのサイズによっては、サーバーとネットワークの両方に重大なパフォーマンスの問題が発生する可能性があることに注意してください。

## <a name="see-also"></a>参照  
[Microsoft ODBC Driver for SQL Server on Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
