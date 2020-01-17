---
title: rsconfig ユーティリティ (SSRS) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 38c2cd6242e9515872ef086ec4851bf6cec103ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571526"
---
# <a name="rsconfig-utility-ssrs"></a>rsconfig ユーティリティ (SSRS)
  **rsconfig.exe** ユーティリティは、接続値とアカウント値を RSReportServer.config ファイルへ暗号化して格納します。 暗号化される値は、自動レポート処理に使用される、レポート サーバー データベースの接続情報とアカウント値です。  
  
## <a name="syntax"></a>構文  
  
```  
  
rsconfig {-?}  
{-cconnection}  
{-eunattendedaccount}  
{-mcomputername}  
{-iinstancename}  
{-sservername}  
{-ddatabasename}  
{-aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>引数  
  
|項目|省略可/必須|定義|  
|----------|------------------------|----------------|  
|**-?**|省略可。|Rsconfig.exe の引数の構文を表示します。|  
|**-c**|**-e** 引数を使用しない場合は必須。|レポート サーバーをレポート サーバー データベースに接続するために使用する、接続文字列、資格情報、データ ソース値を指定します。<br /><br /> この引数は値を取りません。 ただし、必須の接続値をすべて指定する場合は、この引数と共に追加の引数を指定する必要があります。<br /><br /> **-c** と共に指定する引数には、 **-m**、 **-s**、 **-i**、 **-d**、 **-a**、 **-u**、 **-p**、および **-t**があります。|  
|**-e**|**-c** 引数を使用しない場合は必須。|自動的にレポートを実行する場合のアカウントを指定します。<br /><br /> この引数は値を取りません。 ただし、構成ファイルで暗号化されている値を指定する場合は、コマンド ラインに追加の引数を追加する必要があります。<br /><br /> **-e** と共に指定する引数には、 **-u** および **-p**があります。 **-t**を設定することもできます。|  
|**-m**  *computername*|リモート レポート サーバー インスタンスを構成する場合は必須。|レポート サーバーをホストするコンピューターの名前を指定します。 この引数が省略された場合、既定は **localhost**です。|  
|**-s**  *servername*|必須。|レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定します。|  
|**-i**  *instancename*|名前付きインスタンスを使用する場合は必須。|名前付きの Reporting Services インスタンスを使用した場合、この値により、Reporting Services インスタンスの名前が指定されます。|  
|**-d**  *databasename*|必須。|レポート サーバー データベースの名前を指定します。|  
|**-a**  *authmethod*|必須。|レポート サーバーがレポート サーバー データベースへの接続に使用する認証方法を指定します。 有効な値は、 **Windows** または **SQL** です (この引数は大文字と小文字を区別しません)。<br /><br /> **Windows** は、レポート サーバーが Windows 認証を使用することを指定します。<br /><br /> **SQL** は、レポート サーバーが SQL Server 認証を使用することを指定します。|  
|**-u**  *[domain\\]username*|**-e** の場合は必須。 **-c**の場合は省略可。|レポート サーバー データベース接続または自動アカウントのためのユーザー アカウントを指定します。<br /><br /> **rsconfig -e**では、この引数は必須です。 引数はドメイン ユーザー アカウントであることが必要です。<br /><br /> **rsconfig -c** および **-a SQL**では、この引数には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定する必要があります。<br /><br /> **rsconfig -c** および **-a Windows**では、この引数には、ドメイン ユーザー、組み込みアカウント、またはサービス アカウント資格情報を指定できます。 ドメイン アカウントを指定している場合は、 *domain* と *username* を *domain\username*の形式で指定します。 組み込みアカウントを使用する場合、この引数は省略可能です。 サービス アカウント資格情報を使用する場合、この引数は省略してください。|  
|**-p**  *password*|**-u** を指定した場合は必須。|*username* 引数と共に使用するパスワードを指定します。 アカウントがパスワードを必要としない場合、この引数を空白に設定できます。 この値は、ドメイン アカウントの大文字と小文字を区別します。|  
|**-t**|省略可。|エラー メッセージをトレース ログに出力します。 この引数は値を取りません。 詳細については、「 [Report Server Service Trace Log](../../reporting-services/report-server/report-server-service-trace-log.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 構成中のレポート サーバーをホストするコンピューターのローカル管理者であることが必要です。  
  
## <a name="file-location"></a>ファイルの場所  
 rsconfig.exe は **\Program Files\Microsoft SQL Server\110\Tools\Binn**にあります。 このユーティリティは、ファイル システム上の任意のフォルダーから実行できます。  
  
## <a name="remarks"></a>Remarks  
 Rsconfig.exe は次の 2 つの目的で使用します。  
  
-   レポート サーバー データベースへの接続でレポート サーバーが使用する接続情報の修正。  
  
-   他の資格情報が利用できない場合に、リモート データベース サーバーへのログオンでレポート サーバーが使用する特別なアカウントの構成。  
  
**rsconfig** ユーティリティは、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のローカル インスタンスまたはリモート インスタンスで実行できます。 **rsconfig** ユーティリティは、既に設定されている値の暗号化解除または参照に使用することはできません。  
  
このユーティリティを実行する前に、構成中のコンピューターに、Windows Management Instrumentation (WMI) をインストールしておく必要があります。  
  
## <a name="examples"></a>使用例  
 次の例は、 **rsconfig**の使用方法を示しています。  
  
#### <a name="specifying-a-domain-user-account"></a>ドメイン ユーザー アカウントの指定  
 次の例では、ローカルのレポート サーバー データベースに接続する場合に、ドメイン ユーザー アカウントを使用するようにレポート サーバーを構成します。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>SQL Server データベース ユーザー アカウントの指定  
 次の例では、リモートのレポート サーバー データベースに接続する場合に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを使用するようにレポート サーバーを構成します。  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>組み込みアカウントの指定  
 次の例では、ローカルのレポート サーバー データベースに接続する場合に、組み込みアカウントを使用するようにレポート サーバーを構成します。 **-u** は使用されないことに注意してください。 サポートされる組み込みアカウント値の例として、ローカル システムの NT AUTHORITY\SYSTEM、およびネットワーク サービスの NT AUTHORITY\NETWORKSERVICE ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] のみ) などがあります。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>サービス アカウントの指定  
 次の例では、ローカルのレポート サーバー データベースに接続する場合に、レポート サーバー Windows サービス アカウントと Web サービス アカウントを使用するようにレポート サーバーを構成します。 **-u** は使用されず、アカウント情報が指定されないことに注意してください。 コマンドでアカウント値を指定しなかった場合、 **rsconfig** ユーティリティは、各サービスの実行に使用する統合セキュリティおよびサービス アカウントを使用します。  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>ローカル サーバーの自動アカウントの指定  
 次の例では、外部データ ソースに資格情報を渡すことのできないレポートに対して、自動的にレポートを実行する場合に使用されるアカウントを構成します。 アカウントは Windows ドメイン アカウントであることが必要です。 ユーザー名とパスワードに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを指定することはできません。 アカウントは、ローカルのレポート サーバー インスタンス上に構成されます。 エラー メッセージは、ReportingServices\LogFiles フォルダーのトレース ログにキャプチャされます。  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>リモート サーバーの自動アカウントの指定  
 次の例では、リモートのレポート サーバー インスタンス上にアカウントを構成します。このインスタンスは、Rsconfig.exe と同じバージョンになっています (レポート サーバーと Rsconfig.exe が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 バージョンの場合など)。 エラー メッセージ情報は、リモート サーバーのトレース ログにキャプチャされます。  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>参照  
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services レポート サーバー (ネイティブ モード)](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [レポート サーバーのコマンド プロンプト ユーティリティ &#40;SSRS&#41;](../../reporting-services/tools/report-server-command-prompt-utilities-ssrs.md)   
 [RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
