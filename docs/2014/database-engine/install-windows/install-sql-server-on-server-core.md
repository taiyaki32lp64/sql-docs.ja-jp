---
title: Server Core に SQL Server 2014 をインストールする |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3e244b2c4892d725e8e3ddf684b55a224138a50
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637675"
---
# <a name="install-sql-server-2014-on-server-core"></a>Server Core への SQL Server 2014 のインストール
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 または [!INCLUDE[win8srv](../../includes/win8srv-md.md)]の Server Core インストールにインストールできます。 このトピックでは、Server Core に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] をインストールする場合のセットアップに固有の詳細について説明します。  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] または [!INCLUDE[win8srv](../../includes/win8srv-md.md)] オペレーティング システムの Server Core インストール オプションでは、特定のサーバー ロールを実行するための最低限の環境が提供されます。 これにより、必要な保守と管理が減り、これらのサーバー ロールに対する攻撃の危険性が軽減されます。 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]に実装された Server Core の詳細については、「 [Windows server 2008 R2 の Server core](https://go.microsoft.com/fwlink/?LinkId=202439) 」 (https://go.microsoft.com/fwlink/?LinkId=202439)を参照してください。 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] に実装された Server Core の詳細については、[Windows Server 2012 の Server Core](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) に関するページ (https://msdn.microsoft.com/library/hh846323(VS.85).aspx) を参照してください。  
  
## <a name="prerequisites"></a>Prerequisites  
  
|要件|インストール方法|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 および [!INCLUDE[win8srv](../../includes/win8srv-md.md)]の Server Core インストールに含まれています。 有効になっていない場合、セットアップにおいて既定で有効になります。<br /><br /> コンピューター上で Version 2.0、3.0、および 3.5 を同時に実行することはできません。 .NET Framework 3.5 SP1 をインストールすると、2.0 と 3.0 のレイヤーが自動的に取得されます。|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 Full Profile|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 の Server Core インストールに含まれています。 有効になっていない場合、セットアップにおいて既定で有効になります。<br /><br /> Windows サーバー オペレーティング システム搭載のコンピューターで、.NET 3.5 SP1 に依存するコンポーネントをインストールするには、セットアップを実行する前に .NET Framework 3.5 SP1 をダウンロードしてインストールする必要があります。<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]で .NET Framework 3.5 を取得して有効にする方法に関する推奨事項とガイダンスの詳細については、 [Microsoft .NET Framework 3.5 の展開に関する考慮事項](https://msdn.microsoft.com/library/windows/hardware/hh975396)(https://msdn.microsoft.com/library/windows/hardware/hh975396)を参照してください。|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を除く [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]のすべてのエディションのセットアップで、 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile が前提条件としてインストールされます。<br /><br /> [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)]については、セットアップを続行する前に、 [server https://www.microsoft.com/download/details.aspx?id=17718)core の Microsoft .NET Framework 4 (スタンドアロンインストーラー)](https://www.microsoft.com/download/details.aspx?id=17718)から [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server core プロファイルをダウンロードし、インストールします。|  
|Windows インストーラー 4.5|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 および [!INCLUDE[win8srv](../../includes/win8srv-md.md)]の Server Core インストールに付属します。|  
|Windows PowerShell 2.0|[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 および [!INCLUDE[win8srv](../../includes/win8srv-md.md)]の Server Core インストールに付属します。|  
  
##  <a name="BK_SupportedFeatures"></a> Supported Features  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 および [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の Server Core インストールの [!INCLUDE[win8srv](../../includes/win8srv-md.md)]でサポートされている機能については、次の表を参照してください。  
  
|機能|Supported|  
|-------------|---------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] サービス|はい|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レプリケーション|はい|  
|フルテキスト検索|はい|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|はい|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|[いいえ]|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools (SSDT)|[いいえ]|  
|クライアント ツール接続|はい|  
|Integration Services サーバー<sup>[1]</sup>|はい|  
|クライアント ツールの旧バージョンとの互換性|[いいえ]|  
|クライアント ツール SDK|[いいえ]|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック|[いいえ]|  
|管理ツール - 基本|リモートのみ<sup>[2]</sup>|  
|管理ツール - 完全|リモートのみ<sup>[2]</sup>|  
|分散再生コントローラー|[いいえ]|  
|分散再生クライアント|リモートのみ<sup>[2]</sup>|  
|SQL クライアント接続 SDK|はい|  
|Microsoft Sync Framework|はい<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|[いいえ]|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|[いいえ]|  
  
 <sup>[1]</sup>新しい Integration Services サーバーと [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の機能の詳細については、「 [SSIS &#40;&#41;サーバーの Integration Services](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md)」を参照してください。  
  
 <sup>[2]</sup>Server Core へのこれらの機能のインストールはサポートされていません。 これらのコンポーネントは、 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 または [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core ではない別のサーバーにインストールし、Server Core にインストールされている [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスに接続できます。  
  
 <sup>[3]</sup>Microsoft Sync Framework は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストールパッケージには含まれていません。 適切なバージョンの Sync Framework は、この[Microsoft ダウンロードセンター](https://go.microsoft.com/fwlink/?LinkId=221788) (https://go.microsoft.com/fwlink/?LinkId=221788) ページからダウンロードし、[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 または [!INCLUDE[win8srv](../../includes/win8srv-md.md)]の Server Core インストールを実行しているコンピューターにインストールすることができます。  
  
## <a name="supported-scenario-matrix"></a>サポートされるシナリオのマトリックス  
 次の表では、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 および [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の Server Core インストールに [!INCLUDE[win8srv](../../includes/win8srv-md.md)]をインストールする場合のサポートされるシナリオのマトリックスを示します。  
  
|||  
|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディション|すべての [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64-bit エディション<sup>[1]</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の言語|すべての言語|  
|OS の言語とロケール (組み合わせ) での[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の言語|JPN (日本語) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> GER (ドイツ語) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> CHS (中国語 - 中国) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ARA (アラビア語 (SA)) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> THA (タイ語) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> TRK (トルコ語) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> pt-PT (ポルトガル語 - ポルトガル) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> ENG (英語) Windows への ENG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Windows のエディション|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 ビット x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 ビット x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 ビット x64 Data Center Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 ビット x64 Enterprise Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 ビット x64 Standard Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 ビット x64 Web Server Core|  
  
 <sup>[1]</sup>[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] エディションの32ビットバージョンのインストールは、Server Core ではサポートされていません。  
  
## <a name="upgrading"></a>アップグレード  
 Server Core インストールでは、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] へのアップグレードがサポートされています。  
  
## <a name="installation"></a>インストール  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、Server Core オペレーティング システムでのインストール ウィザードを使用したセットアップはサポートされていません。 Server Core にインストールする場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップでは、/Q パラメーターを使用した非表示モード、または /QS パラメーターを使用した簡易非表示モードがサポートされます。 詳細については、「[コマンド プロンプトからの SQL Server 2014 のインストール](install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Core SP1 または [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core を実行しているコンピューターに、以前のバージョンの [!INCLUDE[win8srv](../../includes/win8srv-md.md)] とサイド バイ サイドでインストールすることはできません。  
  
 どのインストール方法を使用するかにかかわらず、個人として、または組織を代表して、ソフトウェア ライセンス条項に同意するかどうかを確認する必要があります。ただし、ソフトウェアの使用に別の契約 ([!INCLUDE[msCoName](../../includes/msconame-md.md)] ボリューム ライセンス契約、ISV や OEM とのサード パーティ契約など) が適用される場合を除きます。  
  
 ライセンス条項は、セットアップのユーザー インターフェイスで確認し、同意することができます。 /Q または /QS パラメーターを使用した自動インストールでは、/IACCEPTSQLSERVERLICENSETERMS パラメーターを指定する必要があります。 ライセンス条項は、「 [マイクロソフト ソフトウェア ライセンス条項](https://go.microsoft.com/fwlink/?LinkId=148209)」で別途確認できます。  
  
> [!NOTE]  
>  ソフトウェアの入手方法 ([!INCLUDE[msCoName](../../includes/msconame-md.md)] のボリューム ライセンスを通じて入手した場合など) によっては、ソフトウェアの使用に追加の条件が課されることがあります。  
  
 特定の機能をインストールするには、/FEATURES パラメーターを使用して、親機能の値または機能の値を指定します。 機能パラメーターとその使用の詳細については、次のセクションを参照してください。  
  
### <a name="feature-parameters"></a>機能パラメーター  
  
|機能パラメーター|[説明]|  
|-----------------------|-----------------|  
|SQLENGINE|[!INCLUDE[ssDE](../../includes/ssde-md.md)]のみをインストールします。|  
|REPLICATION|[!INCLUDE[ssDE](../../includes/ssde-md.md)]と共にレプリケーション コンポーネントをインストールします。|  
|FULLTEXT|[!INCLUDE[ssDE](../../includes/ssde-md.md)]と共にフルテキスト コンポーネントをインストールします。|  
|AS|すべての [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コンポーネントをインストールします。|  
|IS|すべての [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントをインストールします。|  
|CONN|接続コンポーネントをインストールします。|  
  
 機能パラメーターの使い方の例を参照してください。  
  
|パラメーターおよび値|[説明]|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|[!INCLUDE[ssDE](../../includes/ssde-md.md)]のみをインストールします。|  
|/FEATURES=SQLEngine,FullText|[!INCLUDE[ssDE](../../includes/ssde-md.md)] とフルテキストをインストールします。|  
|/FEATURES=SQLEngine,Conn|[!INCLUDE[ssDE](../../includes/ssde-md.md)] および接続コンポーネントをインストールします。|  
|/FEATURES=SQLEngine,AS,IS,Conn|[!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、および接続コンポーネントをインストールします。|  
  
### <a name="installation-options"></a>インストール オプション  
 Server Core オペレーティング システムへの [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインストール中に、セットアップで次のインストール オプションをサポートします。  
  
1.  **コマンド ラインからのインストール**  
  
     コマンド プロンプトのインストール オプションを使用して特定の機能をインストールするには、/FEATURES パラメーターを使用して、親機能の値または機能の値を指定します。 コマンド ラインからパラメーターを使用する方法の例を次に示します。  
  
    ```cmd
    setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **構成ファイルを使用したインストール**  
  
     セットアップでは、コマンド プロンプトからのみ構成ファイルを使用できます。 構成ファイルは、パラメーター (名前と値のペア) と説明のコメントの基本構造を持つテキスト ファイルです。 コマンド プロンプトで指定した構成ファイルには、.INI のファイル名拡張子が必要です。 次の例の ConfigurationFile.INI を参照してください。  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインストール  
  
         次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] を含む新しいスタンドアロン インスタンスをインストールする方法を示します。  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"
        ```  
  
    -   接続コンポーネントのインストール  
  
         次の例では、接続コンポーネントをインストールする方法を示します。  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True
        ```  
  
    -   サポートされるすべての機能のインストール  
  
         次の例では、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のサポートされる全機能を Server Core にインストールする方法を示します。  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     次の例では、構成ファイルを使用してセットアップを起動する方法を示します。  
  
    -   [構成ファイル]  
  
         次に、構成ファイルの使用方法の例をいくつか示します。  
  
        -   コマンド プロンプトで構成ファイルを指定するには  
  
        ```cmd
        setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   構成ファイルの代わりにコマンド プロンプトでパスワードを指定するには  
  
        ```cmd
        setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ソース メディアのルート レベルの \x86 および \x64 フォルダーに DefaultSetup.ini ファイルがある場合は、DefaultSetup.ini ファイルを開き、*Features* パラメーターをファイルに追加します。  
  
         DefaultSetup.ini ファイルが存在しない場合は、作成し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ソース メディアのルート レベルの \x86 および \x64 フォルダーにコピーできます。  
  
## <a name="configuring-remote-access-of-includessnoversionincludesssnoversion-mdmd-running-on-server-core"></a>Server Core で実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート アクセスの構成  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SP1 または [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] の Server Core インストールで実行されている [!INCLUDE[win8srv](../../includes/win8srv-md.md)]インスタンスのリモート アクセスを構成するには、以下で説明する処理を実行します。  
  
### <a name="enable-remote-connections-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>のインスタンスでリモート接続を有効にする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 リモート接続を有効にするには、SQLCMD.exe をローカルで使用して、Server Core インスタンスに対して次のステートメントを実行します。  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-includessnoversionincludesssnoversion-mdmd-browser-service"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを有効にして開始する  
 Browser サービスは、既定では無効になっています。  Server Core で実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで無効になっている場合、このサービスを有効にするには、コマンド プロンプトから次のコマンドを実行します。  
  
 `sc config SQLBROWSER start= auto`  
  
 有効にした後は、コマンド プロンプトから次のコマンドを実行して、サービスを開始します。  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Windows ファイアウォールで例外を作成する  
 Windows ファイアウォールで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスの例外を作成するには、「[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」で指定されている手順に従います。  
  
### <a name="enable-tcpip-on-the-instance-of-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Server Core 上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して TCP/IP プロトコルを有効にするには、Windows PowerShell を使用します。 次の手順に従います。  
  
1.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 または [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core を実行しているコンピューターで、タスク マネージャーを起動します。  
  
2.  **[アプリケーション]** タブで、 **[新しいタスク]** をクリックします。  
  
3.  **[新しいタスクの作成]** ダイアログ ボックスで、 **[開く]** フィールドに **sqlps.exe** と入力して、 **[OK]** をクリックします。 **[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell** ウィンドウが開きます。  
  
4.  **[Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell]** ウィンドウで、次のスクリプトを実行して TCP/IP プロトコルを有効にします。  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = New-Object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>アンインストール  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 または [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core を実行しているコンピューターにログオンした後は、管理者コマンド プロンプトのデスクトップ環境に制限されます。 このコマンド プロンプトを使用して、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスのアンインストールを開始できます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスをアンインストールするには、/Q パラメーターを使用した非表示モード、または /QS パラメーターを使用した簡易非表示モードで、コマンド プロンプトからアンインストールを起動します。 /QS パラメーターを指定すると、UI に進捗状況が表示されますが、入力は受け付けられません。 /Q は、ユーザー インターフェイスのない非表示モードで実行します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存のインスタンスをアンインストールするには、次のコマンドを実行します。  
  
```cmd
setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 名前付きインスタンスを削除する場合は、前に示した例の "MSSQLSERVER" の代わりにインスタンス名を指定します。  
  
> [!WARNING]
>  誤ってコマンド プロンプトを閉じた場合は、次の手順で新しいコマンド プロンプトを開始できます。  
> 
>  1.  Ctrl + Shift + Esc キーを押して、タスク マネージャーを表示します。  
> 2.  **[アプリケーション]** タブで、 **[新しいタスク]** をクリックします。  
> 3.  **[新しいタスクの作成]** ダイアログ ボックスで、 **[名前]** フィールドに「 **cmd** 」と入力して、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]。  
  
## <a name="see-also"></a>参照  
 [構成ファイルを使用して SQL Server 2014 をインストール](install-sql-server-using-a-configuration-file.md)   
 [コマンドプロンプトから SQL Server 2014 をインストール](install-sql-server-from-the-command-prompt.md)   
 [SQL Server 2014  の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
 [Server Core Installation Option Getting Started Guide (Server Core インストール オプションの開始ガイド)](https://go.microsoft.com/fwlink/?LinkId=221422)   
 [Configuring a Server Core installation: Overview (Server Core インストールの構成: 概要)](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [Failover Cluster Cmdlets in Windows PowerShell Listed by Task Focus (タスク フォーカスによって一覧表示される Windows PowerShell でのフェールオーバー クラスター コマンドレット)](https://go.microsoft.com/fwlink/?LinkId=221419)   
 [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters (フェールオーバー クラスターの Windows PowerShell コマンドレットへの Cluster.exe コマンドのマッピング)](https://go.microsoft.com/fwlink/?LinkId=221421)  
