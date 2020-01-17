---
title: RsReportServer.config 構成ファイル | Microsoft Docs
ms.date: 06/12/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 60e0a0b2-8a47-4eda-a5df-3e5e403dbdbc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 351ca36275fbd782e3bf3e8d098aaf6a49287430
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500410"
---
# <a name="rsreportserverconfig-configuration-file"></a>RSReportServer Configuration File
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**RsReportServer.config** ファイルには、レポート サーバー Web サービスおよびバックグラウンド処理で使用される設定が格納されます。 すべての [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションは、RSReportServer.config ファイルに格納された構成設定を読み取る単一のプロセス内で実行されます。 ネイティブ モードのレポート サーバーと SharePoint モードのレポート サーバーはどちらも RSReportServer.config を使用しますが、両方のモードで構成ファイル内のまったく同じ設定が使用されるわけではありません。 SharePoint モードの設定の多くは、ファイルではなく SharePoint 構成データベースに格納されるため、SharePoint モード バージョンのファイルは、より小さくなります。 このトピックでは、ネイティブ モードおよび SharePoint モード用にインストールされる既定の構成ファイル、いくつかの重要な設定、および構成ファイルによって制御される動作について説明します。  

SharePoint モードでは、そのコンピューターで実行されているすべてのサービス アプリケーション インスタンスに適用される設定が、構成ファイルに含まれています。 SharePoint 構成データベースには、特定のサービス アプリケーションに適用される構成設定が含まれています。 構成データベースに格納され、SharePoint 管理ページを通じて管理される設定は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のサービス アプリケーションごとに異なるものにすることができます。  
  
 以下に各設定を、既定でインストールされる構成ファイル内に出現する順で示します。 このファイルを編集する方法については、「 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
 
##  <a name="bkmk_file_location"></a> ファイルの場所  

RSReportServer.config は、レポート サーバーのモードに応じて、次のフォルダーにあります。  


  
### <a name="native-mode-report-server"></a>ネイティブ モードのレポート サーバー 

 
**[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)]** [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)]

```  
C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer  
```

**[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)]** [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

```  
C:\Program Files\Microsoft SQL Server Reporting Services\RSServer\ReportServer
```  
  
### <a name="sharepoint-mode-report-server"></a>SharePoint モードのレポート サーバー 

> [!NOTE]
> SharePoint 統合モードは、SQL Server Reporting Services の Power BI レポートの 2017 年 1 月 Technical Preview バージョンでは使用できません。
  
```  
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting  
```  
 
このファイルの編集の詳細については、「 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
##  <a name="bkmk_generalconfiguration"></a> 全般構成設定 (rsreportserver.config)  
 次の表では、ファイルの最初の部分に出現する全般的な構成設定について説明します。 構成ファイルに出現する順に、設定を示します。 表の最後の列は、設定がネイティブ モードのレポート サーバーに適用されるか **(N)** 、SharePoint モードのレポート サーバーに適用されるか **(S)** 、両方に適用されるかを示しています。  
  
> [!NOTE]  
>  このトピックの "最大値" は INT_MAX の値 (2147483647) を示します。  詳細については、「[整数の制限](https://msdn.microsoft.com/library/296az74e\(v=vs.110\).aspx)」(https://msdn.microsoft.com/library/296az74e(v=vs.110).aspx) を参照してください。  
  
|設定|[説明]|モード|  
|-------------|-----------------|----------|  
|**Dsn**|レポート サーバー データベースをホストするデータベース サーバーへの接続文字列を指定します。 この値は、レポート サーバー データベースの作成時に、暗号化されて構成ファイルに追加されます。 SharePoint では、SharePoint 構成データベースからデータベース接続情報が取得されます。|N、S|  
|**ConnectionType**|レポート サーバーがレポート サーバー データベースへの接続に使用する資格情報のタイプを指定します。 有効な値は、 **Default** および **Impersonate**です。 **Default** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログインまたはサービス アカウントを使用してレポート サーバー データベースに接続するようにレポート サーバーを構成する場合に指定します。 **Impersonate** は、レポート サーバーが Windows アカウントを使用してレポート サーバー データベースに接続する場合に指定します。|×|  
|**LogonUser、LogonDomain、LogonCred**|レポート サーバーがレポート サーバー データベースに接続するときに使用するドメイン アカウントのドメイン、ユーザー名、およびパスワードを格納します。 **LogonUser**、 **LogonDomain**、および **LogonCred** の値は、レポート サーバー接続がドメイン アカウントを使用するように構成されていると作成されます。 レポート サーバーのデータベース接続の詳細については、「[レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。|×|  
|**InstanceID**|レポート サーバーのインスタンス用の識別子です。 レポート サーバー インスタンスの名前は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前に基づいています。 この値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス名を指定します。 既定値は **MSRS12** _\<インスタンス名>_ です。 この設定は変更しないでください。 完全な値の例を次に示します: `<InstanceId>MSRS13.MSSQLSERVER</InstanceId>`<br /><br /> SharePoint モードの例を次に示します:<br /><br /> `<InstanceId>MSRS12.@Sharepoint</InstanceId>`|N、S|  
|**InstallationID**|セットアップによって作成されるレポート サーバーのインストール用の識別子です。 この値は GUID に設定されます。 この設定は変更しないでください。|×|  
|**SecureConnectionLevel**|Web サービス呼び出しにおける SSL (Secure Sockets Layer) の使用レベルを指定します。 この設定は、レポート サーバー Web サービスと Web ポータルの両方で使用されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで、HTTP または HTTPS を使用するように URL を構成すると、この値が設定されます。 SQL Server 2008 R2 で、SecureConnectionLevel はオン/オフのスイッチとして使用されます。 SQL Server 2008 R2 より前のバージョンの場合、有効な値の範囲は 0 から 3 で、0 はセキュリティ レベルが最も低くなります。 詳細については、「[ConfigurationSetting メソッド - SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)」、「[セキュリティで保護された Web サービス メソッドの使用](../../reporting-services/report-server-web-service/net-framework/using-secure-web-service-methods.md)」および「[ネイティブ モードのレポート サーバーでの SSL 接続の構成](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)」を参照してください。|N、S|
|**DisableSecureFormsAuthenticationCookie**|既定値は False です。<br /><br /> フォーム認証とカスタム認証をセキュリティで保護されているものとしてマークするために使用するクッキーの強制を無効にするかどうかを指定します。 SQL Server 2012 以降、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] によって、カスタム認証拡張機能と共に使用されるフォーム認証クッキーが、クライアントへの送信時にセキュリティで保護されたクッキーとして自動的にマークされます。 このプロパティを変更することで、レポート サーバー管理者およびカスタム セキュリティ拡張機能の作成者は、カスタム セキュリティ拡張機能の作成者がクッキーをセキュリティで保護されたクッキーとしてマークするかどうかを指定できた以前の動作に戻すことができます。 ネットワーク スニッフィングや再生攻撃を防止するため、フォーム認証にはセキュリティで保護されたクッキーを使用することをお勧めします。|×|  
|**CleanupCycleMinutes**|レポート サーバー データベースから古いセッションと期限切れのスナップショットを削除するまでの保持期間を分単位で指定します。 有効な値は、0 から整数型の最大値までです。 既定値は 10 です。 値を 0 に設定すると、データベースによる処理のクリーンアップが無効になります。|N、S|  
|**MaxActiveReqForOneUser**|ユーザーが同時に処理できる最大レポート数を指定します。 最大数に達すると、それ以降のレポート処理要求は拒否されます。 有効値は、1 から整数型の最大値までです。 既定値は 20 です。<br /><br /> 要求の大半はきわめて迅速に処理されるため、1 人のユーザーが任意の時点で 20 より多くの接続を開くということはまずありません。 ユーザーが 15 より多い処理集中型のレポートを同時に開く場合は、この値を増やす必要があります。<br /><br /> この設定は、SharePoint 統合モードで動作するレポート サーバーでは無視されます。|N、S|  
|**MaxActiveReqForAnonymous**|同時に処理できる匿名要求の最大数を指定します。 最大数に達すると、それ以降の処理要求は拒否されます。 有効値は、1 から整数型の最大値までです。 既定値は 200 です。
|**DatabaseQueryTimeout**|レポート サーバー データベースへの接続がタイムアウトするまでの期間を秒単位で指定します。この値は、System.Data.SQLClient.SQLCommand.CommandTimeout プロパティに渡されます。 有効な値の範囲は 0 ～ 2147483647 です。 既定値は 120 です。 値を 0 に設定することはお勧めできません。0 にすると待ち時間が無制限になります。|×|  
|**AlertingCleanupCycleMinutes**|既定値は 20 です。<br /><br /> 警告データベースに格納されている一時データのクリーンアップが発生する頻度を指定します。|S|  
|**AlertingDataCleanupMinutes**|既定値は 360 です。<br /><br /> 警告の定義を作成または編集するために使用するセッション データを警告データベース内で保持する期間を指定します。 既定値は 6 時間です。|S|  
|**AlertingExecutionLogCleanup**Minutes|既定値は 10080 です。<br /><br /> 警告実行ログの値を保持する期間を指定します。 既定の日数は 7 日です。|S|  
|**AlertingMaxDataRetentionDays**|既定値は 180 です。<br /><br /> 警告データが変更されていない場合、警告メッセージの重複を防ぐために必要な警告データを保持する期間を指定します。|S|  
|**RunningRequestsScavengerCycle**|孤立し、期限の切れた要求を取り消す頻度を指定します。 この値は秒単位で指定します。 有効な値は、0 から整数型の最大値までです。 既定値は 60 です。|N、S|  
|**RunningRequestsDbCycle**|レポート サーバーが実行中のジョブを評価する頻度を指定します。この評価の目的は、実行中のジョブがレポート実行のタイムアウト値を超えているかどうか、および、いつ Web ポータルの [ジョブの管理] ページに実行中のジョブ情報を表示するかを確認することです。 この値は秒単位で指定します。 有効な値の範囲は 0 ～ 2147483647 です。 既定値は 60 です。|N、S|  
|**RunningRequestsAge**|実行中のジョブの状態を新規から実行中に変更するまでの間隔を秒単位で指定します。 有効な値の範囲は 0 ～ 2147483647 です。 既定値は 30 です。|N、S|  
|**MaxScheduleWait**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 次の実行時刻 **が要求されたときに、レポート サーバー Windows サービスが** エージェント サービスによるスケジュールの更新を待機する期間を秒単位で指定します。 有効な値の範囲は 1 ～ 60 です。<br /><br /> 既定の構成ファイルでは、MaxScheduleWait は **5**に設定されます。<br /><br /> レポート サーバーが構成ファイルを見つけられないか読み取れない場合、MaxScheduleWait は既定で 1 に設定されます。|N、S|  
|**DisplayErrorLink**|エラーが発生した場合に [!INCLUDE[msCoName](../../includes/msconame-md.md)] ヘルプとサポート サイトへのリンクを表示するかどうかを示します。 このリンクはエラー メッセージに表示されます。 該当するリンクをクリックすることで、サイト上の最新のエラー メッセージの内容を表示できます。 有効な値は、 **True** (既定) および **False**です。|N、S|  
|**WebServiceuseFileShareStorage**|キャッシュされたレポート、およびユーザー セッション中にレポート サーバー Web サービスにより作成された一時スナップショットをファイル システムに格納するかどうかを指定します。 有効な値は、 **True** および **False** (既定) です。 値を False に設定すると、一時データは reportservertempdb データベースに格納されます。|N、S|  
|**WatsonFlags**|[!INCLUDE[msCoName](../../includes/msconame-md.md)]にレポートするエラー状態をログに記録する際の情報量を指定します。<br /><br /> 0x0430 = 完全なダンプ<br /><br /> 0x0428 = ミニダンプ<br /><br /> 0x0002 = ダンプなし|N、S|  
|**WatsonDumpOnExceptions**|エラー ログでレポートする例外のリストを指定します。 特定の問題が繰り返し発生するような場合は、この設定を使って分析に必要な情報のダンプを作成し、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] に送信することができます。 ダンプを作成するとパフォーマンスに悪影響が生じるため、問題を診断するとき以外は、この設定を変更しないでください。|N、S|  
|**WatsonDumpExcludeIfContainsExceptions**|エラー ログでレポートしない例外のリストを指定します。 問題を診断するときに、特定の例外についてはダンプが作成されないように設定できます。|N、S|  
  
##  <a name="bkmk_URLReservations"></a> URLReservations (RSReportServer.config ファイル)  
 **URLReservations** は、現在のインスタンスについて、レポート サーバー Web サービスおよび Web ポータルへの HTTP アクセスを定義します。 URL は、レポート サーバーの構成時に予約されて HTTP.SYS に格納されます。  
  
> [!WARNING]  
>  SharePoint モードでは、SharePoint サーバーの全体管理で URL 予約が構成されます。 詳細については、「[代替アクセス マッピングを構成する」(https://technet.microsoft.com/library/cc263208(office.12).aspx)](https://technet.microsoft.com/library/cc263208\(office.12\).aspx) を参照してください。  
  
 URL 予約を構成ファイル内で直接編集することは避けてください。 ネイティブ モードのレポート サーバーの URL 予約を作成または変更する場合は、必ず [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーまたはレポート サーバー WMI プロバイダーを使用します。 構成ファイルで値を変更すると、予約が破損して実行時にサーバー エラーが発生する場合や、HTTP.SYS 内に予約が取り残されて、ソフトウェアをアンインストールしても削除されなくなる場合があります。 詳細については、「[レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)」と「[構成ファイル内の URL &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)」を参照してください。  
  
 **URLReservations** は省略可能な要素です。 この要素が RSReportServer.config ファイルに存在しない場合、サーバーが構成されていない可能性があります。 指定されている場合、 **AccountName** を除くすべての子要素が必要となります。  
  
 表の最後の列は、設定がネイティブ モードのレポート サーバーに適用されるか (N)、SharePoint モードのレポート サーバーに適用されるか (S)、両方に適用されるかを示しています。  
  
|設定|[説明]|モード|  
|-------------|-----------------|----------|  
|**アプリケーション**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションの設定を格納します。|×|  
|**[名前]**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] アプリケーションを指定します。 有効な値は ReportServerWebService または ReportManager です。|×|  
|**VirtualDirectory**|アプリケーションの仮想ディレクトリ名を指定します。|×|  
|**URLs、URL**|アプリケーションの 1 つまたは複数の URL 予約を格納します。|×|  
|**UrlString**|HTTP.SYS の有効な URL 構文を指定します。 構文の詳細については、「[URL 予約の構文 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/url-reservation-syntax-ssrs-configuration-manager.md)」を参照してください。|×|  
|**AccountSid**|URL 予約の作成対象となったアカウントのセキュリティ ID (SID) を指定します。 これは、Report Server サービスの実行に使用されているアカウントである必要があります。 SID がサービス アカウントと一致しない場合、レポート サーバーが、その URL で要求をリッスンできない場合があります。|×|  
|**AccountName**|**AccountSid**に対応するわかりやすいアカウント名を指定します。 実際に使用されることはありませんが、URL 予約に使用されたアカウントのサービス アカウントを容易に判別できるようにファイルに表示されます。|×|  
  
##  <a name="bkmk_Authentication"></a> Authentication (RSReportServer.config ファイル)  
 **Authentication** は、レポート サーバーで使用できる認証の種類 (複数可) を指定します。 既定の設定および値は、このセクションで定義できる設定と値のサブセットです。 既定の設定のみが自動的に追加されます。 他の設定を追加するには、テキスト エディターを使用して RSReportServer.config ファイルに要素構造を追加し、値を設定する必要があります。  
  
 既定値には **RSWindowsNegotiate** と **RSWindowsNTLM** が含まれており、 **EnableAuthPersistance** は **True**に設定されます。  
  
```  
   <Authentication>  
      <AuthenticationTypes>  
         <RSWindowsNegotiate/>  
         <RSWindowsNTLM/>  
      </AuthenticationTypes>  
      <EnableAuthPersistence>true</EnableAuthPersistence>  
   </Authentication>  
```  
  
 その他の値はすべて手動で追加する必要があります。 詳細については、「 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)」を参照してください。  
  
 次の表の最後の列は、設定がネイティブ モードのレポート サーバーに適用されるか (N)、SharePoint モードのレポート サーバーに適用されるか (S)、両方に適用されるかを示しています。  
  
|設定|[説明]|モード|  
|-------------|-----------------|----------|  
|**AuthenticationTypes**|1 つまたは複数の認証の種類を指定します。 有効な値は、 **RSWindowsNegotiate**、 **RSWindowsKerberos**、 **RSWindowsNTLM**、 **RSWindowsBasic**、および **Custom**です。<br /><br /> **RSWindows** タイプと **Custom** は、相互に排他的です。<br /><br /> **RSWindowsNegotiate**、 **RSWindowsKerberos**、 **RSWindowsNTLM**、および **RSWindowsBasic** は累積的に設定されるため、前述の既定値の例に示したように、組み合わせて指定することができます。<br /><br /> 認証の種類が異なる複数のクライアント アプリケーションまたはブラウザーから要求を受け取る場合は、認証の種類を複数指定する必要があります。<br /><br /> **RSWindowsNTLM**は削除しないでください。削除した場合、サポートされるブラウザーの種類が制限されます。 詳細については、「 [Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。|×|  
|**RSWindowsNegotiate**|レポート サーバーは、Kerberos または NTLM のいずれかのセキュリティ トークンを受け付けます。 これは、レポート サーバーがネイティブ モードで実行され、サービス アカウントが Network Service である場合の既定の設定です。 レポート サーバーがネイティブ モードで実行され、サービス アカウントがドメイン ユーザー アカウントとして構成されている場合、この設定は省略されます。<br /><br /> レポート サーバー サービス アカウントに対してドメイン アカウントが構成されており、レポート サーバーに対してサービス プリンシパル名 (SPN) が構成されていない場合、この設定により、ユーザーがサーバーにログオンできないことがあります。|×|  
|**RSWindowsNTLM**|サーバーは、NTLM のセキュリティ トークンを受け付けます。<br /><br /> この設定を削除した場合、サポートされるブラウザーの種類が制限されます。 詳細については、「 [Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)」を参照してください。|N、S|  
|**RSWindowsKerberos**|サーバーは、Kerberos のセキュリティ トークンを受け付けます。<br /><br /> 制約付き委任の認証スキームで Kerberos 認証を使用する場合は、この設定か RSWindowsNegotiate を使用してください。|×|  
|**RSWindowsBasic**|サーバーは基本資格情報を受け付けます。資格情報なしで接続が試みられた場合、チャレンジ/レスポンスを発行します。<br /><br /> 基本認証では、HTTP 要求において、資格情報がクリア テキストで渡されます。 基本認証を使用する場合は、レポート サーバーとの間でやり取りされるネットワーク トラフィックを SSL で暗号化してください。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で基本認証を構成するための構文例については、「 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)」を参照してください。|×|  
|**Custom**|レポート サーバー コンピューターにカスタム セキュリティ拡張機能を配置した場合は、この値を指定します。 詳細については、「 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)」を参照してください。|×|  
|**LogonMethod**|この値は、 **RSWindowsBasic**におけるログオンの種類を指定します。 **RSWindowsBasic**を指定した場合、この値は省略できません。 有効な値は 2 または 3 で、それぞれ次の意味になります。<br /><br /> **2** = ネットワーク ログオン。プレーンテキスト パスワードを認証する高パフォーマンス サーバー向けです。<br /><br /> **3** = クリア テキスト ログオン。各 HTTP 要求と一緒に送信される認証パッケージにログオン資格情報が保持されます。これにより、ネットワーク内の他のサーバーに接続する際に、サーバーがユーザーの権限を借用できます。<br /><br /> <br /><br /> 注: 値 0 (対話型ログオン) と値 1 (バッチ ログオン) は、 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]ではサポートされません。|×|  
|**Realm**|この値は、 **RSWindowsBasic**で使用されます。 組織内の保護されたリソースへのアクセスを制御するための承認機能や認証機能を含んだリソース パーティションを指定します。|×|  
|**DefaultDomain**|この値は、 **RSWindowsBasic**で使用されます。 サーバーがユーザーを認証する際のドメインを決定するために使用されます。 この値はオプションです。ただし、省略した場合、レポート サーバーでは、コンピューター名がドメインとして使用されます。 レポート サーバーをドメイン コントローラーにインストールした場合、そのコンピューターによって制御されるドメインを指定します。|×|  
|**RSWindowsExtendedProtectionLevel**|既定値は **off**です。 詳細については、「 [Extended Protection for Authentication with Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)」をご覧ください。|×|  
|**RSWindowsExtendedProtectionScenario**|既定値は **Proxy**です。|×|  
|**EnableAuthPersistence**|要求ごとに接続の認証を実行するかどうかを指定します。<br /><br /> 有効な値は **True** (既定) または **False**です。 **True**に設定した場合、同じ接続の 2 回目以降の要求は、最初の要求の権限借用コンテキストと見なされます。<br /><br /> プロキシ サーバー ソフトウェア (ISA Server など) を使用してレポート サーバーにアクセスする場合は、この値を **False** に設定する必要があります。 プロキシ サーバーを使用すると、プロキシ サーバーからの単一接続を複数のユーザーが使用できるようになります。 このシナリオでは、認証の永続化を無効にして、各ユーザー要求が個別に認証されるようにする必要があります。 **EnableAuthPersistence** を **False**に設定しなかった場合、すべてのユーザーが、最初の要求の権限借用コンテキストで接続するようになります。|N、S|  
  
##  <a name="bkmk_service"></a> Service (RSReportServer.config ファイル)  
 **Service** は、サービス全体に適用されるアプリケーション設定を指定します。  
  
 次の表の最後の列は、設定がネイティブ モードのレポート サーバーに適用されるか (N)、SharePoint モードのレポート サーバーに適用されるか (S)、両方に適用されるかを示しています。  
  
|設定|[説明]|モード|  
|-------------|-----------------|----------|  
|**IsSchedulingService**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザーによって作成されたスケジュールおよびサブスクリプションに対応する一連の [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] エージェント ジョブをレポート サーバーが維持するかどうかを指定します。 有効な値は、 **True** (既定) および **False**です。<br /><br /> ポリシー ベースの管理の [Reporting Services のセキュリティ構成] ファセットを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能を有効または無効にすると、この設定に影響します。 詳細については、「 [レポート サーバー サービスの開始と停止](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)」を参照してください。|N、S|  
|**IsNotificationService**|レポート サーバーが通知および配信を処理するかどうかを指定します。 有効な値は、 **True** (既定) および **False**です。 この値が **False**の場合、サブスクリプションは配信されません。<br /><br /> ポリシー ベースの管理の [Reporting Services のセキュリティ構成] ファセットを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能を有効または無効にすると、この設定に影響します。 詳細については、「 [レポート サーバー サービスの開始と停止](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)」を参照してください。|N、S|  
|**IsEventService**|サービスがイベント キュー内のイベントを処理するかどうかを指定します。 有効な値は、 **True** (既定) および **False**です。 この値が **False**の場合、レポート サーバーは、スケジュールまたはサブスクリプションの処理を実行しません。<br /><br /> ポリシー ベースの管理の [Reporting Services のセキュリティ構成] ファセットを使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の機能を有効または無効にすると、この設定に影響します。 詳細については、「 [レポート サーバー サービスの開始と停止](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)」を参照してください。|N、S|  
|**IsAlertingService**|既定値は **True**です。|S|  
|**PollingInterval**|レポート サーバーによるイベント テーブルへのポーリング間隔を、秒単位で指定します。 有効な値は、0 から整数型の最大値までです。 既定値は 10 です。|N、S|  
|**WindowsServiceUseFileShareStorage**|キャッシュされたレポート、およびユーザー セッション中にレポート サーバー サービスにより作成された一時スナップショットをファイル システムに格納するかどうかを指定します。 有効な値は、 **True** および **False** (既定) です。|N、S|  
|**MemorySafetyMargin**|**WorkingSetMaximum** を上限として、メモリ圧迫の度合いを中レベルと低レベルに分けたとき、その境界を定義するパーセンテージを指定します。 既定値は 80 です。 **WorkingSetMaximum** と利用可能なメモリの構成の詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。|N、S|  
|**MemoryThreshold**|**WorkingSetMaximum** を上限として、メモリ圧迫の度合いを高レベルと中レベルに分けたとき、その境界を定義するパーセンテージを指定します。 既定値は **90**です。 この値は、 **MemorySafetyMargin**で設定する値より大きくする必要があります。 詳細については、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。|N、S|  
|**RecycleTime**|アプリケーション ドメインのリサイクル時間を分単位で指定します。 有効な値は、0 から整数型の最大値までです。 既定値は 720 です。|N、S|  
|**MaxAppDomainUnloadTime**|リサイクル中に、アプリケーション ドメインがアンロードを許可される間隔を指定します。 この間にリサイクルが完了しない場合、アプリケーション ドメインのすべての処理が停止します。 詳細については、「 [Application Domains for Report Server Applications](../../reporting-services/report-server/application-domains-for-report-server-applications.md)」を参照してください。<br /><br /> この値は分単位で指定します。 有効な値は、0 から整数型の最大値までです。 既定値は **30**です。|N、S|  
|**MaxQueueThreads**|レポート サーバー Windows サービスがサブスクリプションと通知を同時に処理するために使用するスレッド数を指定します。 有効な値は、0 から整数型の最大値までです。 既定値は 0 です。 0 を選択した場合は、レポート サーバーによってスレッドの最大数が決定されます。 整数を指定した場合は、指定した値が、一度に作成できるスレッド数の上限に設定されます。 レポート サーバー Windows サービスがプロセスを実行するためにメモリをどのように管理するかについては、「 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)」を参照してください。|N、S|  
|**UrlRoot**|電子メール サブスクリプションやファイル共有サブスクリプションで配信されたレポート用の URL を構築するために、レポート サーバーの配信拡張機能で使用されます。 パブリッシュされたレポートが置かれているレポート サーバーの有効な URL アドレスを指定する必要があります。 レポート サーバーは、この設定を使って、オフライン アクセスまたは自動アクセスに必要な URL を生成します。 これらの URL は、エクスポートされたレポートで使用されるほか、配信拡張機能が、リンクや電子メールなど、配信メッセージに追加される URL を構築する際に使用されます。 レポート サーバーは、次のようにして、レポート内の URL を決定します。<br /><br /> **[UrlRoot]** が空 (既定値) であり、URL 予約が存在する場合、レポート サーバーは、ListReportServerUrls メソッドによる URL 生成と同様の方法で、自動的に URL を決定します。 ListReportServerUrls メソッドで返される最初の URL が使用されます。 SecureConnectionLevel がゼロ (0) よりも大きい場合は、最初の SSL URL が使用されます。<br /><br /> **[UrlRoot]** が特定の値に設定された場合は、明示的な値が使用されます。<br /><br /> **[UrlRoot]** が空であり、URL 予約が構成されていない場合、レンダリングされたレポートや電子メール リンク内の URL に誤りが生じることになります。|N、S|  
|**UnattendedExecutionAccount**|レポートを実行するために、レポート サーバーで使用されるユーザー名、パスワード、およびドメインを指定します。 これらの値は暗号化されます。 これらの値を設定するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールまたは **rsconfig** ユーティリティを使用します。 詳細については、「[自動実行アカウントを構成する &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。<br /><br /> SharePoint モードでは、SharePoint サーバーの全体管理を使用して [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションの実行アカウントを設定します。 詳細については、「 [Reporting Services SharePoint サービス アプリケーションの管理](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md)｣を参照してください|×|  
|**PolicyLevel**|セキュリティ ポリシーの構成ファイルを指定します。 有効な値は Rssrvrpolicy.config です。詳細については、「 [Using Reporting Services Security Policy Files](../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)」を参照してください。|N、S|  
|**IsWebServiceEnabled**|レポート サーバー Web サービスが SOAP および URL アクセス要求に応答するかどうかを指定します。 ポリシー ベースの管理の [Reporting Services のセキュリティ構成] ファセットを使用してサービスを有効または無効にすると、この値が設定されます。|N、S|  
|**IsReportManagerEnabled**|この設定は、SQL Server 2016 Reporting Services 累積更新プログラム 2 の時点で非推奨とされました。 Web ポータルは常に有効になります。|×|  
|**FileShareStorageLocation**|一時スナップショットの格納先となるファイル システム上のフォルダーを 1 つ指定します。 UNC パスとしてフォルダー パスを指定することはできますが、これはお勧めできません。 既定値は空です。<br /><br /> `<FileShareStorageLocation>`<br /><br /> `<Path>`<br /><br /> `</Path>`<br /><br /> `</FileShareStorageLocation>`|N、S|  
|**IsRdceEnabled**|RDCE (Report Definition Customization Extension) が有効かどうかを指定します。 有効値は **True** および **False**です。|N、S|  
  
##  <a name="bkmk_UI"></a> UI (RSReportServer.config ファイル)  
 **UI** は、Web ポータル アプリケーションに適用される構成設定を指定します。  
  
 次の表の最後の列は、設定がネイティブ モードのレポート サーバーに適用されるか (N)、SharePoint モードのレポート サーバーに適用されるか (S)、両方に適用されるかを示しています。  
  
|設定|[説明]|モード|  
|-------------|-----------------|----------|  
|**ReportServerUrl**|Web ポータルの接続先となるレポート サーバーの URL を指定します。 この値は、Web ポータルを他のインスタンス上またはリモート コンピューター上のレポート サーバーに接続する場合にのみ変更します。|N、S|  
|**ReportBuilderTrustLevel**|この値は変更しないでください。この値を構成することはできません。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 以降のバージョンでは、レポート ビルダーは **FullTrust**でのみ実行されます。 部分信頼モードの廃止の詳細については、「 [SQL Server 2016 で廃止された SQL Server Reporting Services の機能](../../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)」を参照してください。|N、S|  
|**PageCountMode**|Web ポータルでのみ使用されます。この設定は、レポート サーバーでページ数の値をレポートの表示前に計算するか、表示中に計算するかを指定します。 有効な値は **Estimate** (既定値) および **Actual**です。 ユーザーがレポートを閲覧している間にページ数情報を計算する場合は、 **Estimate** を使用します。 ページ数の初期値は 2 (現在のページの他にもう 1 ページ) で、ユーザーがレポートを読み進める間にページ数が調整されます。 レポートが表示される前にページ数を計算する場合は、 **Actual** を使用します。 **Actual** は旧バージョンとの互換性を維持するために用意されています。 **PageCountMode** を **Actual**に設定した場合、有効なページ数を取得する関係上、レポート全体を処理する必要があるため、レポートが表示されるまでの待ち時間が長くなる点に注意してください。|N、S|  
  
##  <a name="bkmk_extensions"></a> Extensions (RSReportServer.config ファイル) (ネイティブ モード)  
 Extensions セクションは、 **ネイティブ モード レポート サーバーの** rsreportserver.config ファイルでのみ表示されます。 SharePoint モード レポート サーバーの拡張機能の情報は、SharePoint 構成データベースに格納され、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションごとに構成されます。  
  
 **Extensions** は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 環境に対する以下の拡張モジュールの構成設定を指定します。  
  
-   配信拡張機能  
  
-   DeliveryUI 拡張機能  
  
-   表示拡張機能  
  
-   データ処理拡張機能  
  
-   セマンティック クエリ拡張機能 (内部使用のみ)  
  
-   モデル生成拡張機能 (内部使用のみ)  
  
-   セキュリティ拡張機能  
  
-   認証拡張機能  
  
-   イベント処理拡張機能 (内部使用のみ)  
  
-   レポート定義カスタマイズ拡張機能  
  
 上記の一部の拡張機能は、厳密には内部的にのみレポート サーバーによって使用されます。 内部使用のみを目的とした拡張機能の構成設定には触れません。 以降のセクションでは、既定の拡張機能の構成設定について説明します。 カスタム拡張機能を備えたレポート サーバーを使用している場合、実際の構成ファイルには、ここに記載されていない設定が含まれている可能性もあります。 このセクションでは、各拡張機能を出現順に列挙しています。 同じ種類の複数の拡張機能で繰り返し出現する設定については、一度だけ記載するものとします。  
  
###  <a name="bkmk_extensionsgeneral"></a> 配信拡張機能の全般構成  
 レポートの配信時にサブスクリプションによって使用される、既定 (またはカスタム) の配信拡張機能を指定します。 RSReportServer.config ファイルには、次の 4 つの配信拡張機能に対応したアプリケーション設定が含まれています。  
  
1.  レポート サーバーの電子メール  
  
2.  ファイル共有配信  
  
3.  SharePoint 統合モードで動作するレポート サーバー用のレポート サーバー ドキュメント ライブラリ  
  
4.  レポートを事前にキャッシュする NULL 配信プロバイダー  
  
 配信拡張機能の詳細については「[サブスクリプションと配信 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)」を参照してください。  
  
 **Extension Name**、 **MaxRetries**、 **SecondsBeforeRetry**、 **Configuration**の各設定は、すべての配信拡張機能に存在します。 まず、これらの共通の設定について説明します。 それぞれの拡張機能に固有の設定については、2 つ目以降の表を参照してください。  
  
|設定|[説明]|  
|-------------|-----------------|  
|**Extension Name**|配信拡張機能のフレンドリ名とアセンブリを指定します。 この値は変更しないでください。|  
|**MaxRetries**|1 回で配信できなかった場合に、レポート サーバーが再試行を行う回数を指定します。 既定値は、3 です。|  
|**SecondsBeforeRetry**|再試行の間隔 (秒) を指定します。 既定値は 900 です。|  
|**Configuration**|各配信拡張機能に固有の構成設定が含まれます。|  
  
####  <a name="bkmk_fileshare_extension"></a> ファイル共有配信拡張機能の構成設定  
 ファイル共有配信では、アプリケーション ファイル形式でエクスポートされたレポートが、ネットワーク上の共有フォルダーに送信されます。 詳細については、「 [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)」を参照してください。  
  
|設定|[説明]|  
|-------------|-----------------|  
|**ExcludedRenderFormats**、 **RenderingExtension**|ファイル共有配信でうまく使用できないエクスポート形式を意図的に除外する場合に使用します。 通常、これらの形式は、対話型のレポートやプレビューに使用されるほか、レポートを事前にキャッシュする場合に使用されます。 デスクトップ アプリケーションから簡単に閲覧できるアプリケーション ファイルは生成されません。<br /><br /> HTMLOWC<br /><br /> RGDI<br /><br /> [Null]|  
  
####  <a name="bkmk_email_extension"></a> レポート サーバーの電子メール拡張機能の構成設定  
 レポート サーバーの電子メールでは、SMTP ネットワーク デバイスを使用して、レポートを電子メール アドレスに送信します。 使用するには、この配信拡張機能があらかじめ構成されている必要があります。 詳細については、「 [Reporting Services の電子メール配信](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)」を参照してください。  
  
|設定|[説明]|  
|-------------|-----------------|  
|**SMTPServer**|リモート SMTP サーバーまたは転送サーバーのアドレスを示す文字列値を指定します。 この値は、リモート SMTP サービスに対して必要です。 IP アドレス、企業イントラネット上のコンピューターの UNC 名、または完全修飾ドメイン名を使用できます。|  
|**SMTPServerPort**|メールを送信するために SMTP サービスで使用されるポートを示す整数値を指定します。 通常、ポート 25 が電子メールの送信に使用されます。|  
|**SMTPAccountName**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook Express のアカウント名を割り当てる文字列値が含まれています。 SMTP サーバーがなんらかの処理にこのアカウントを使用するよう構成されている場合に、この値を設定できます。それ以外の場合は、空のままにしてください。 **From** を使用して、レポートの送信に使用される電子メール アカウントを指定します。|  
|**SMTPConnectionTimeout**|SMTP サービスを使用した有効なソケット接続に対する、タイムアウトまでの秒単位の待ち時間を示す整数値を指定します。既定値は 30 秒ですが、 **SendUsing** が 2 に設定されている場合、この値は無視されます。|  
|**SMTPServerPickupDirectory**|ローカル SMTP サービス用のピックアップ ディレクトリを示す文字列値を指定します。 この値には、完全修飾のローカル フォルダー パス (たとえば、d:\rs-emails) を指定する必要があります。|  
|**SMTPUseSSL**|ネットワークを介した SMTP メッセージの送信時に SSL (Secure Sockets Layer) を使用するよう設定できる、ブール値を指定します。 既定値は 0 (または False) です。 この設定は、 **SendUsing** 要素が 2 に設定されている場合に使用できます。|  
|**SendUsing**|メッセージの送信に使用する方法を指定します。 有効な値は、<br /><br /> 1 = ローカル SMTP サービスのピックアップ ディレクトリからメッセージを送信します。<br /><br /> 2 = ネットワークの SMTP サービスからメッセージを送信します。|  
|**SMTPAuthenticate**|TCP/IP 接続経由での SMTP サービスへのメッセージ送信に使用する認証の種類を示す整数値を指定します。 有効な値は、<br /><br /> 0 = 認証を行いません。<br /><br /> 1 = (サポートされていません)。<br /><br /> 2 = NTLM (NT LanMan) 認証を行います。 ネットワーク SMTP サーバーへの接続には、レポート サーバー Windows サービスのセキュリティ コンテキストが使用されます。|  
|**From**|レポートの送信元の電子メール アドレスを、 *abc@host.xyz* 」を参照してください。 アドレスは、送信する電子メール メッセージの **[差出人]** 行に表示されます。 リモート SMTP サーバーを使用している場合に、この値が必要です。 メールを送信する権限を持つ有効な電子メール アカウントを指定する必要があります。|  
|**EmbeddedRenderFormats、RenderingExtension**|電子メール メッセージ本文内のレポートのカプセル化に使用する表示形式を指定します。 続いて、レポート内の画像がレポートに埋め込まれます。 有効な値は、MHTML および HTML4.0 です。|  
|**PrivilegedUserRenderFormats**|"すべてのサブスクリプションを管理" タスクを使用してサブスクライブが有効になっている場合に、ユーザーがレポートのサブスクリプション用に選択できる表示形式を指定します。 この値が設定されていない場合は、意図的に除外されたものを除く、すべての表示形式を使用できます。|  
|**ExcludedRenderFormats、RenderingExtension**|指定の配信拡張機能で適切に処理されない形式を意図的に除外します。 同じ表示拡張機能の複数のインスタンスは除外できません。 複数のインスタンスを除外すると、レポート サーバーが構成ファイルを読み取るときにエラーが発生します。 既定では、電子メール配信に対し、次の拡張機能は除外されます。<br /><br /> HTMLOWC<br /><br /> [Null]<br /><br /> RGDI|  
|**SendEmailToUserAlias**|この値は、 **DefaultHostName**と連動します。<br /><br /> **SendEmailToUserAlias** を **True**に設定すると、個々のサブスクリプションを定義したユーザーが、レポートの受信者として自動的に指定されます。 **[宛先]** フィールドは非表示になります。 この値が **False**に設定されている場合、 **[宛先]** フィールドが表示されます。 レポートの配信を最大限に制御する場合は、この値を **True** に設定します。 有効な値は次のとおりです。<br /><br /> **True**= サブスクリプションを作成しているユーザーの電子メール アドレスが使用されます。 これが既定値です。<br /><br /> **False**= 任意の電子メール アドレスを指定できます。|  
|**DefaultHostName**|この値は、 **SendEmailToUserAlias**と連動します。<br /><br /> **SendEmailToUserAlias** が True に設定されている場合に、ホスト名を示す文字列値を指定して、ユーザーの別名に追加します。 この値には、ドメイン ネーム システム (DNS) 名または IP アドレスを指定できます。|  
|**PermittedHosts**|電子メール配信を受信できるホストを明示的に指定することにより、レポートの配信を制限します。 **PermittedHosts**内で、各ホストは **HostName** 要素として指定されます。この値は、IP アドレスまたは DNS 名のいずれかです。<br /><br /> ホストに定義された電子メール アカウントのみが、有効な受信者です。 **DefaultHostName**を指定した場合、そのホストが **PermittedHosts** の **HostName**要素として含まれていることを確認してください。 この値は、1 つ以上の DNS 名または IP アドレスである必要があります。 既定では、この値は設定されていません。 値が設定されていない場合は、電子メール化されたレポートを受信できるユーザーは制限されません。|  
  
####  <a name="bkmk_documentlibrary_extension"></a> レポート サーバー SharePoint ドキュメント ライブラリ拡張機能の構成  
 レポート サーバー ドキュメント ライブラリでは、アプリケーション ファイル形式にエクスポートされたレポートがドキュメント ライブラリに送信されます。 この配信拡張機能を使用できるのは、SharePoint 統合モードで実行するように構成されたレポート サーバーだけです。 詳細については、「 [SharePoint Library Delivery in Reporting Services](../../reporting-services/subscriptions/sharepoint-library-delivery-in-reporting-services.md)」を参照してください。  
  
|設定|[説明]|  
|-------------|-----------------|  
|**ExcludedRenderFormats、RenderingExtension**|ドキュメント ライブラリ配信でうまく使用できないエクスポート形式を意図的に除外する場合に使用します。 HTMLOWC、RGDI、Null の各配信拡張機能が除外されます。 通常、これらの形式は、対話型のレポートやプレビューに使用されるほか、レポートを事前にキャッシュする場合に使用されます。 デスクトップ アプリケーションから簡単に閲覧できるアプリケーション ファイルは生成されません。|  
  
####  <a name="bkmk_null_extension"></a> Null 配信拡張機能の構成  
 NULL 配信プロバイダーは、個々のユーザー用にあらかじめ生成されたレポートを事前にキャッシュに格納しておく場合に使用します。 この配信拡張機能には構成設定はありません。 詳細については、「 [レポートのキャッシュ (SSRS)](../../reporting-services/report-server/caching-reports-ssrs.md)でキャッシュを事前に読み込む唯一の方法でした。  
  
###  <a name="bkmk_ui"></a> 配信 UI 拡張機能の全般構成  
 Web ポータルで個別のサブスクリプションを定義する際に使用されるサブスクリプション定義ページに表示されるユーザー インターフェイス コンポーネントを含んだ配信拡張機能を指定します。 ユーザー定義のオプションを持ったカスタム配信拡張機能を作成して配置する場合、Web ポータルを使用する必要がある場合は、その配信拡張機能をこのセクションに登録する必要があります。 既定では、レポート サーバーの電子メールおよびレポート サーバーのファイル共有の構成設定が存在します。 このセクションには、データ ドリブン サブスクリプションまたは SharePoint アプリケーション ページでのみ使用される配信拡張機能の設定は存在しません。  
  
|設定|[説明]|  
|-------------|-----------------|  
|**DefaultDeliveryExtension**|サブスクリプション定義ページの配信の種類一覧で、どの配信拡張機能を先頭に表示するかを決定します。 この設定は 1 つの配信拡張機能だけが保持できます。 有効な値は **True** または **False**です。 この値を **True**に設定した場合、その拡張機能が既定で選択されます。|  
|**Configuration**|配信拡張機能の構成オプションを指定します。 配信拡張機能ごとに、既定の表示形式を設定できます。 有効な値は、rsreportserver.config ファイルの表示セクションに記述されている表示拡張機能の名前です。|  
|**DefaultRenderingExtension**|配信拡張機能が既定かどうかを指定します。 "レポート サーバーの電子メール" は、既定の配信拡張機能です。 有効な値は **True** または **False**です。 複数の拡張機能の値が **True**の場合、最初の拡張機能が既定の拡張機能と見なされます。|  
  
###  <a name="bkmk_rendering"></a> 表示拡張機能の全般構成  
 レポート プレゼンテーションで使用される、既定 (またはカスタム) の表示拡張機能を指定します。  
  
 カスタム表示拡張機能を配置する場合以外は、このセクションを変更しないでください。 詳細については、「 [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)」を参照してください。  
  
 既定の表示拡張機能は、次のとおりです。  
  
-   XML  
  
-   [Null]  
  
-   CSV  
  
-   PDF  
  
-   RGDI  
  
-   HTML4.0  
  
-   MHTML  
  
-   EXCEL  
  
-   RPL  
  
-   IMAGE  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] リリース以降では、MHTML および HTML 4.0 での表示に、サイズ指定データ ビジュアライゼーションの動作を制御するための次のデバイス情報設定が既定で含まれます。  
  
```  
<DeviceInfo><DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing></DeviceInfo>  
```  
  
 DeviceInfo 設定の詳細については、以下を参照してください。  
  
-   [MHTML デバイス情報設定](../../reporting-services/mhtml-device-information-settings.md)  
  
-   [HTML デバイス情報設定](../../reporting-services/html-device-information-settings.md)  
  
-   [表示拡張機能のデバイス情報設定 (Reporting Services)](../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)  
  
 **\<Render>** の **\<Extension>** 子要素の属性の詳細については、以下を参照してください。  
  
-   [RSReportServer.Config で表示拡張機能パラメーターをカスタマイズする](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)  
  
-   [表示拡張機能の配置](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
 カスタム表示拡張機能を配置する場合以外は、このセクションを変更しないでください。 詳細については、「 [Implementing a Rendering Extension](../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)」を参照してください。  
  
###  <a name="bkmk_data"></a> データ拡張機能の全般構成  
 クエリの処理に使用される、既定 (またはカスタム) のデータ処理拡張機能を指定します。 既定のデータ処理拡張機能は、次のとおりです。  
  
-   SQL  
  
-   SQLAZURE  
  
-   SQLPDW  
  
-   OLEDB  
  
-   OLEDB-MD  
  
-   ORACLE  
  
-   ODBC  
  
-   XML  
  
-   SHAREPOINTLIST  
  
-   SAPBW  
  
-   ESSBASE  
  
-   TERADATA  
  
 カスタム データ処理拡張機能を追加する場合以外は、このセクションを変更しないでください。 詳細については、「 [Implementing a Data Processing Extension](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)」を参照してください。  
  
###  <a name="bkmk_semantic"></a> セマンティック クエリ拡張機能の全般構成  
 レポート モデルの処理に使用するセマンティック クエリ処理拡張機能を指定します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に含まれるセマンティック クエリ処理拡張機能では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データ、Oracle、および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の多次元データをサポートしています。 このセクションは変更しないでください。 クエリ処理は拡張できません。  
  
###  <a name="bkmk_model"></a> モデル生成の構成  
 レポート サーバーにパブリッシュされた既存の共有データ ソースからレポート モデルを作成するためのモデル生成拡張機能を指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データ、Oracle、および [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の多次元データ ソースのモデルを生成できます。 このセクションは変更しないでください。 モデル生成は拡張できません。  
  
###  <a name="bkmk_security"></a> セキュリティ拡張機能の構成  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]によって使用される承認コンポーネントを指定します。 このコンポーネントは、RSReportServer.config ファイルの **Authentication** 要素に登録されている認証拡張機能で使用されます。 カスタム認証拡張機能を実装する場合以外は、このセクションを変更しないでください。 カスタム セキュリティ機能の追加の詳細については、「 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)」を参照してください。 承認の詳細については、「 [Authorization in Reporting Services](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)」を参照してください。  
  
###  <a name="bkmk_authentication"></a> 認証拡張機能の構成  
 レポート サーバーによって使用される、既定およびカスタムの認証拡張機能を指定します。 既定の拡張機能は、Windows 認証に基づいています。 カスタム認証拡張機能を実装する場合以外は、このセクションを変更しないでください。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]での認証の詳細については、「 [Reporting Services での認証](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md) 」と「 [レポート サーバーでの認証](../../reporting-services/security/authentication-with-the-report-server.md)」を参照してください。 カスタム セキュリティ機能の追加の詳細については、「 [Implementing a Security Extension](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)」を参照してください。  
  
###  <a name="bkmk_eventprocessing"></a> イベント処理  
 既定のイベント ハンドラーを指定します。 このセクションは変更しないでください。 このセクションは拡張できません。  
  
###  <a name="bkmk_reportdefinition"></a> レポート定義カスタマイズ  
 レポート定義を変更するカスタム拡張機能の名前と種類を指定します。  
  
###  <a name="bkmk_rdlsandboxing"></a> RDL サンドボックス  
 RDL (レポート定義言語) モードを指定します。このモードでは、複数のテナントが 1 つのレポート サーバー Web ファームを共有している状況で、個々のテナントによる特定の種類のレポート リソースの使用を検出および制限できます。 詳細については、 [「RDL サンドボックスの有効化と無効化」](../../reporting-services/report-server-sharepoint/enable-and-disable-rdl-sandboxing.md)を参照してください。  
  
##  <a name="bkmk_MapTileServer"></a> MapTileServerConfiguration (RSReportServer.config ファイル)  
 **MapTileServerConfiguration** は、レポート サーバーでパブリッシュされるレポート内のマップ レポート アイテムに対してタイル背景を提供する、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bing Maps Web サービス用の構成の設定を定義します。 すべての子要素が必須です。  
  
|設定|[説明]|  
|-------------|-----------------|  
|**MaxConnections**|Bing Maps Web サービスに対する接続の最大数を指定します。|  
|**Timeout**|Bing Maps Web サービスからの応答を待つ時間のタイムアウトを秒数で指定します。|  
|**AppID**|Bing Maps Web サービスに使用するアプリケーション識別子 (AppID) を指定します。 **(Default)** は、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の既定の AppID を指定します。<br /><br /> レポート内での Bing のマップ タイルの使用については、「 [追加使用条件](https://go.microsoft.com/fwlink/?LinkId=151371)」を参照してください。<br /><br /> 固有の Bing Maps 使用許諾契約書にカスタム AppID を指定する必要があるとき以外は、この値を変更しないでください。 AppID を変更する場合は、変更を有効にするために [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を再起動する必要はありません。|  
|**CacheLevel**|System.Net.Cache の HttpRequestCacheLevel 列挙から値を指定します。 既定値は **Default**です。 詳細については、「 [HttpRequestCacheLevel 列挙体](https://go.microsoft.com/fwlink/?LinkId=153353)」を参照してください。|  
  
##  <a name="bkmk_nativedefaultfile"></a> ネイティブ モード レポート サーバーの既定の構成ファイル  
 既定では、rsreportserver.config ファイルは次の場所にインストールされます。  
  
 **C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer**  
  
```  
<Configuration>
    <Dsn>AQAAANCMnd8BFdERjHoAwE/Cl+sBAAAAR58DMGebHUeMvyR6HR04kQQAAAAiAAAAUgBlAHAAbwBy
AHQAaQBuAGcAIABTAGUAcgB2AGUAcgAAAANmAADAAAAAEAAAADczfLRgZ4GF44iBHkLrKY4AAAAA
BIAAAKAAAAAQAAAAJ9wQOmDNauH+LS30rboJ2OAAAAAp0kiFFBrc3r3ypKaldZJtjCORX9LTZRzt
0/JCSVIZc4GXx0peGKqd+f85UyrY/KOyUSHogOC/XoBp9Ppxv6ITbdunsS/LXEcMUBVqEdQD4ylh
x6K1NTC/u8hl9v0MgK+xMQKaiV7BuNYbgGgkaViABcNH0xVzcc5rMTHUkrABbGDFGKyAFniGQ1qu
/rqHibNNyvYbP/2uiqvgC0tQl6u8VkVbXpWrkvO+bFCqxlaJlCoDc2f3rIO321SZEvoFbsYNgPLd
+mIAkSCnH3Z3gm/bI8bqVkFaHblKyQuSfFsi6RQAAACb87b26dV0GjHmMJnE0Tk8CzNmhg==</Dsn>
    <ConnectionType>Default</ConnectionType>
    <LogonUser></LogonUser>
    <LogonDomain></LogonDomain>
    <LogonCred></LogonCred>
    <InstanceId>MSRS13.MSSQLSERVER</InstanceId>
    <InstallationID>{cd920604-a5c7-4554-b2a0-aadc04312fe5}</InstallationID>
    <Add Key="SecureConnectionLevel" Value="0"/>
    <Add Key="DisableSecureFormsAuthenticationCookie" Value="false"/>
    <Add Key="CleanupCycleMinutes" Value="10"/>
    <Add Key="MaxActiveReqForOneUser" Value="20"/>
    <Add Key="DatabaseQueryTimeout" Value="120"/>
    <Add Key="RunningRequestsScavengerCycle" Value="60"/>
    <Add Key="RunningRequestsDbCycle" Value="60"/>
    <Add Key="RunningRequestsAge" Value="30"/>
    <Add Key="MaxScheduleWait" Value="5"/>
    <Add Key="DisplayErrorLink" Value="true"/>
    <Add Key="WebServiceUseFileShareStorage" Value="false"/>
    <!--  <Add Key="ProcessTimeout" Value="150" /> -->
    <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->
    <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->
    <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->
    <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->
    <Add Key="WatsonFlags" Value="0x0428"/>
    <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException"/>
    <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException,System.AppDomainUnloadedException"/>
    <URLReservations>
        <Application>
            <Name>ReportServerWebService</Name>
            <VirtualDirectory>ReportServer</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>https://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
        <Application>
            <Name>ReportServerWebApp</Name>
            <VirtualDirectory>Reports</VirtualDirectory>
            <URLs>
                <URL>
                    <UrlString>https://+:80</UrlString>
                    <AccountSid>S-1-5-80-2885764129-887777008-271615777-1616004480-2722851051</AccountSid>
                    <AccountName>NT SERVICE\ReportServer</AccountName>
                </URL>
            </URLs>
        </Application>
    </URLReservations>
    <Authentication>
        <AuthenticationTypes>
            <RSWindowsNTLM/>
        </AuthenticationTypes>
        <RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>
        <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>
        <EnableAuthPersistence>true</EnableAuthPersistence>
    </Authentication>
    <Service>
        <IsSchedulingService>True</IsSchedulingService>
        <IsNotificationService>True</IsNotificationService>
        <IsEventService>True</IsEventService>
        <PollingInterval>10</PollingInterval>
        <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>
        <MemorySafetyMargin>80</MemorySafetyMargin>
        <MemoryThreshold>90</MemoryThreshold>
        <RecycleTime>720</RecycleTime>
        <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>
        <MaxQueueThreads>0</MaxQueueThreads>
        <UrlRoot>
        </UrlRoot>
        <UnattendedExecutionAccount>
            <UserName></UserName>
            <Password></Password>
            <Domain></Domain>
        </UnattendedExecutionAccount>
        <PolicyLevel>rssrvpolicy.config</PolicyLevel>
        <IsWebServiceEnabled>True</IsWebServiceEnabled>
        <IsReportManagerEnabled>True</IsReportManagerEnabled>
        <FileShareStorageLocation>
            <Path>
            </Path>
        </FileShareStorageLocation>
        <DefaultFileShareAccount>
            <Domain></Domain>
            <UserName></UserName>
            <Password></Password>
        </DefaultFileShareAccount>
    </Service>
    <UI>
        <ReportServerUrl>
        </ReportServerUrl>
        <PageCountMode>Estimate</PageCountMode>
    </UI>
    <Extensions>
        <Delivery>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareProvider,ReportingServicesFileShareDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <FileShareConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </FileShareConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailProvider,ReportingServicesEmailDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <SMTPServer></SMTPServer>
                        <SMTPServerPort>
                        </SMTPServerPort>
                        <SMTPAccountName>
                        </SMTPAccountName>
                        <SMTPConnectionTimeout>
                        </SMTPConnectionTimeout>
                        <SMTPServerPickupDirectory>
                        </SMTPServerPickupDirectory>
                        <SMTPUseSSL>False</SMTPUseSSL>
                        <SendUsing>2</SendUsing>
                        <SMTPAuthenticate>0</SMTPAuthenticate>
                        <SendUserName></SendUserName>
                        <SendPassword></SendPassword>
                        <From></From>
                        <EmbeddedRenderFormats>
                            <RenderingExtension>MHTML</RenderingExtension>
                        </EmbeddedRenderFormats>
                        <PrivilegedUserRenderFormats>
                        </PrivilegedUserRenderFormats>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                        <SendEmailToUserAlias>True</SendEmailToUserAlias>
                        <DefaultHostName>
                        </DefaultHostName>
                        <PermittedHosts>
                        </PermittedHosts>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server DocumentLibrary" Type="Microsoft.ReportingServices.SharePoint.SharePointDeliveryExtension.DocumentLibraryProvider,ReportingServicesSharePointDeliveryExtension">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <DocumentLibraryConfiguration>
                        <ExcludedRenderFormats>
                            <RenderingExtension>HTMLOWC</RenderingExtension>
                            <RenderingExtension>NULL</RenderingExtension>
                            <RenderingExtension>RGDI</RenderingExtension>
                        </ExcludedRenderFormats>
                    </DocumentLibraryConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.NullDeliveryProvider.NullProvider,ReportingServicesNullDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryProvider,ReportingServicesPowerBIDeliveryProvider">
                <MaxRetries>3</MaxRetries>
                <SecondsBeforeRetry>900</SecondsBeforeRetry>
                <Configuration>
                    <PowerBIDeliveryConfiguration>
                    </PowerBIDeliveryConfiguration>
                </Configuration>
            </Extension>
        </Delivery>
        <DeliveryUI>
            <Extension Name="Report Server Email" Type="Microsoft.ReportingServices.EmailDeliveryProvider.EmailDeliveryProviderControl,ReportingServicesEmailDeliveryProvider">
                <DefaultDeliveryExtension>True</DefaultDeliveryExtension>
                <Configuration>
                    <RSEmailDPConfiguration>
                        <DefaultRenderingExtension>MHTML</DefaultRenderingExtension>
                    </RSEmailDPConfiguration>
                </Configuration>
            </Extension>
            <Extension Name="Report Server FileShare" Type="Microsoft.ReportingServices.FileShareDeliveryProvider.FileShareUIControl,ReportingServicesFileShareDeliveryProvider"/>
            <Extension Name="Report Server PowerBI" Type="Microsoft.ReportingServices.PowerBIDeliveryProvider.PowerBIDeliveryUIControl,ReportingServicesPowerBIDeliveryProvider"/>
        </DeliveryUI>
        <Render>
            <Extension Name="WORDOPENXML" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordOpenXmlRenderer.WordOpenXmlDocumentRenderer,Microsoft.ReportingServices.WordRendering"/>
            <Extension Name="WORD" Type="Microsoft.ReportingServices.Rendering.WordRenderer.WordDocumentRenderer,Microsoft.ReportingServices.WordRendering" Visible="false"/>
            <Extension Name="EXCELOPENXML" Type="Microsoft.ReportingServices.Rendering.ExcelOpenXmlRenderer.ExcelOpenXmlRenderer,Microsoft.ReportingServices.ExcelRendering"/>
            <Extension Name="EXCEL" Type="Microsoft.ReportingServices.Rendering.ExcelRenderer.ExcelRenderer,Microsoft.ReportingServices.ExcelRendering" Visible="false"/>
            <Extension Name="PPTX" Type="Microsoft.ReportingServices.Rendering.PowerPointRendering.PptxRenderingExtension,Microsoft.ReportingServices.PowerPointRendering"/>
            <Extension Name="PDF" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.PDFRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="IMAGE" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.ImageRenderer,Microsoft.ReportingServices.ImageRendering"/>
            <Extension Name="MHTML" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.MHtmlRenderingExtension,Microsoft.ReportingServices.HtmlRendering">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="CSV" Type="Microsoft.ReportingServices.Rendering.DataRenderer.CsvReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.Rendering.DataRenderer.XmlDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="ATOM" Type="Microsoft.ReportingServices.Rendering.DataRenderer.AtomDataReport,Microsoft.ReportingServices.DataRendering"/>
            <Extension Name="NULL" Type="Microsoft.ReportingServices.Rendering.NullRenderer.NullReport,Microsoft.ReportingServices.NullRendering" Visible="false"/>
            <Extension Name="RGDI" Type="Microsoft.ReportingServices.Rendering.ImageRenderer.RGDIRenderer,Microsoft.ReportingServices.ImageRendering" Visible="false"/>
            <Extension Name="HTML4.0" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html40RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="HTML5" Type="Microsoft.ReportingServices.Rendering.HtmlRenderer.Html5RenderingExtension,Microsoft.ReportingServices.HtmlRendering" Visible="false">
                <Configuration>
                    <DeviceInfo>
                        <DataVisualizationFitSizing>Approximate</DataVisualizationFitSizing>
                    </DeviceInfo>
                </Configuration>
            </Extension>
            <Extension Name="RPL" Type="Microsoft.ReportingServices.Rendering.RPLRendering.RPLRenderer,Microsoft.ReportingServices.RPLRendering" Visible="false" LogAllExecutionRequests="false"/>
        </Render>
        <!--
        For the SQLPDW extension to work, install the SQL Server PDW Client Tools on the report server.
        NOTE: The SQLPDW extension is deprecated. It supports old versions of SQL Server Parallel Data Warehouse (PDW).        
        To connect to Analytics Platform System, use the SQL (SQL Server) extension.        
        For the ORACLE extension to work, install the Oracle Data Provider for NET (ODP.NET) on the report server.
        For TERADATA extension to work, install the .NET Provider for Teradata on the report server.
      -->
        <Data>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.DataExtensions.SqlConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.DataExtensions.SqlAzureConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.DataExtensions.SqlDwConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.ReportingServices.DataExtensions.AdoMdConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="SHAREPOINTLIST" Type="Microsoft.ReportingServices.DataExtensions.SharePointList.SPListConnection,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.DataExtensions.OracleClientConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ESSBASE" Type="Microsoft.ReportingServices.DataExtensions.Essbase.EssbaseConnection,Microsoft.ReportingServices.DataExtensions.Essbase"/>
            <Extension Name="SAPBW" Type="Microsoft.ReportingServices.DataExtensions.SapBw.SapBwConnection,Microsoft.ReportingServices.DataExtensions.SapBw"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.DataExtensions.TeradataConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="OLEDB" Type="Microsoft.ReportingServices.DataExtensions.OleDbConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="ODBC" Type="Microsoft.ReportingServices.DataExtensions.OdbcConnectionWrapper,Microsoft.ReportingServices.DataExtensions"/>
            <Extension Name="XML" Type="Microsoft.ReportingServices.DataExtensions.XmlDPConnection,Microsoft.ReportingServices.DataExtensions"/>
        </Data>
        <SemanticQuery>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MSSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="SQLPDW" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQLADW.MSSqlAdwSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>False</EnableMathOpCasting>
                </Configuration>
            </Extension>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <DisableNO_MERGEInLeftOuters>False</DisableNO_MERGEInLeftOuters>
                    <EnableUnistr>False</EnableUnistr>
                    <DisableTSTruncation>False</DisableTSTruncation>
                </Configuration>
            </Extension>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlSQCommand,Microsoft.ReportingServices.SemanticQueryEngine">
                <Configuration>
                    <EnableMathOpCasting>True</EnableMathOpCasting>
                    <ReplaceFunctionName>oREPLACE</ReplaceFunctionName>
                </Configuration>
            </Extension>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.QueryExecution.ASSemanticQueryCommand,Microsoft.AnalysisServices.Modeling"/>
        </SemanticQuery>
        <ModelGeneration>
            <Extension Name="SQL" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="SQLAZURE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.MSSQL.MsSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="ORACLE" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Oracle.OraSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="TERADATA" Type="Microsoft.ReportingServices.SemanticQueryEngine.Sql.Teradata.TdSqlModelGenerator,Microsoft.ReportingServices.SemanticQueryEngine"/>
            <Extension Name="OLEDB-MD" Type="Microsoft.AnalysisServices.Modeling.Generation.ModelGeneratorExtention,Microsoft.AnalysisServices.Modeling"/>
        </ModelGeneration>
        <Security>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authorization.WindowsAuthorization, Microsoft.ReportingServices.Authorization"/>
        </Security>
        <Authentication>
            <Extension Name="Windows" Type="Microsoft.ReportingServices.Authentication.WindowsAuthentication, Microsoft.ReportingServices.Authorization"/>
        </Authentication>
        <EventProcessing>
            <Extension Name="SnapShot Extension" Type="Microsoft.ReportingServices.Library.HistorySnapShotCreatedHandler,ReportingServicesLibrary">
                <Event>
                    <Type>ReportHistorySnapshotCreated</Type>
                </Event>
            </Extension>
            <Extension Name="Timed Subscription Extension" Type="Microsoft.ReportingServices.Library.TimedSubscriptionHandler,ReportingServicesLibrary">
                <Event>
                    <Type>TimedSubscription</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Refresh Plan Extension" Type="Microsoft.ReportingServices.Library.CacheRefreshPlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>RefreshCache</Type>
                </Event>
            </Extension>
            <Extension Name="Shared Dataset Cache Update Extension" Type="Microsoft.ReportingServices.Library.SharedDatasetCacheUpdatePlanHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SharedDatasetCacheUpdate</Type>
                </Event>
            </Extension>
            <Extension Name="Cache Update Extension" Type="Microsoft.ReportingServices.Library.ReportExecutionSnapshotUpdateEventHandler,ReportingServicesLibrary">
                <Event>
                    <Type>SnapshotUpdated</Type>
                </Event>
            </Extension>
        </EventProcessing>
    </Extensions>
    <MapTileServerConfiguration>
        <MaxConnections>2</MaxConnections>
        <Timeout>10</Timeout>
        <AppID>(Default)</AppID>
        <CacheLevel>Default</CacheLevel>
    </MapTileServerConfiguration>
</Configuration> 
```  
  
##  <a name="bkmk_sharepointdefaultfile"></a> SharePoint モード レポート サーバーの既定の構成ファイル  
 既定では、rsreportserver.config ファイルは次の場所にインストールされます。  
  
 **C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting**  
  
```  
<Configuration>  
  <Dsn />  
  <ConnectionType>Default</ConnectionType>  
  <LogonUser>  
  </LogonUser>  
  <LogonDomain>  
  </LogonDomain>  
  <LogonCred>  
  </LogonCred>  
  <InstanceId>MSRS12.@Sharepoint</InstanceId>  
  <Add Key="SecureConnectionLevel" Value="0" />  
  <Add Key="CleanupCycleMinutes" Value="10" />  
  <Add Key="MaxActiveReqForOneUser" Value="20" />  
  <Add Key="AlertingCleanupCycleMinutes" Value="20" />  
  <Add Key="AlertingDataCleanupMinutes" Value="360" />  
  <Add Key="AlertingExecutionLogCleanupMinutes" Value="10080" />  
  <Add Key="AlertingMaxDataRetentionDays" Value="180" />  
  <Add Key="RunningRequestsScavengerCycle" Value="60" />  
  <Add Key="RunningRequestsDbCycle" Value="60" />  
  <Add Key="RunningRequestsAge" Value="30" />  
  <Add Key="MaxScheduleWait" Value="5" />  
  <Add Key="DisplayErrorLink" Value="true" />  
  <Add Key="WebServiceUseFileShareStorage" Value="false" />  
  <!--  <Add Key="ProcessTimeout" Value="150" /> -->  
  <!--  <Add Key="ProcessTimeoutGcExtension" Value="30" /> -->  
  <!--  <Add Key="WatsonFlags" Value="0x0430" /> full dump-->  
  <!--  <Add Key="WatsonFlags" Value="0x0428" /> minidump -->  
  <!--  <Add Key="WatsonFlags" Value="0x0002" /> no dump-->  
  <Add Key="WatsonFlags" Value="0x0428" />  
  <Add Key="WatsonDumpOnExceptions" Value="Microsoft.ReportingServices.Diagnostics.Utilities.InternalCatalogException,Microsoft.ReportingServices.Modeling.InternalModelingException,Microsoft.ReportingServices.ReportProcessing.UnhandledReportRenderingException" />  
  <Add Key="WatsonDumpExcludeIfContainsExceptions" Value="System.Threading.ThreadAbortException,System.Web.UI.ViewStateException,System.OutOfMemoryException,System.Web.HttpException,System.IO.IOException,System.IO.FileLoadException,Microsoft.SharePoint.SPException,Microsoft.ReportingServices.WmiProvider.WMIProviderException" />  
  <RStrace>  
    <add name="FileName" value="ReportServerService" />  
    <add name="FileSizeLimitMb" value="32" />  
    <add name="KeepFilesForDays" value="14" />  
    <add name="Prefix" value="tid, time" />  
    <add name="TraceListeners" value="file" />  
    <add name="TraceFileMode" value="unique" />  
    <add name="Components" value="all:3" />  
  </RStrace>  
  <URLReservations>  
    <Application>  
      <Name>ReportServerWebService</Name>  
      <VirtualDirectory>ReportServer</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>https://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
    <Application>  
      <Name>ReportManager</Name>  
      <VirtualDirectory>Reports</VirtualDirectory>  
      <URLs>  
        <URL>  
          <UrlString>https://+:80</UrlString>  
          <AccountSid>  
          </AccountSid>  
          <AccountName>  
          </AccountName>  
        </URL>  
      </URLs>  
    </Application>  
  </URLReservations>  
  <Authentication>  
    <AuthenticationTypes>  
      <RSWindowsNTLM />  
    </AuthenticationTypes>  
    <EnableAuthPersistence>true</EnableAuthPersistence>  
  </Authentication>  
  <Service>  
    <IsSchedulingService>True</IsSchedulingService>  
    <IsNotificationService>True</IsNotificationService>  
    <IsEventService>True</IsEventService>  
    <IsAlertingService>True</IsAlertingService>  
    <PollingInterval>10</PollingInterval>  
    <WindowsServiceUseFileShareStorage>False</WindowsServiceUseFileShareStorage>  
    <MemorySafetyMargin>80</MemorySafetyMargin>  
    <MemoryThreshold>90</MemoryThreshold>  
    <RecycleTime>720</RecycleTime>  
    <MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>  
    <MaxQueueThreads>0</MaxQueueThreads>  
    <UrlRoot>  
    </UrlRoot>  
    <PolicyLevel>rssrvpolicy.config</PolicyLevel>  
    <IsWebServiceEnabled>True</IsWebServiceEnabled>    
    <FileShareStorageLocation>  
      <Path>  
      </Path>  
    </FileShareStorageLocation>  
  </Service>  
  <UI>  
    <ReportServerUrl>  
    </ReportServerUrl>  
    <PageCountMode>Estimate</PageCountMode>  
  </UI>  
  <MapTileServerConfiguration>  
    <MaxConnections>2</MaxConnections>  
    <Timeout>10</Timeout>  
    <AppID>(Default)</AppID>  
    <CacheLevel>Default</CacheLevel>  
  </MapTileServerConfiguration>  
</Configuration>  
```  
  
## <a name="see-also"></a>参照  
 [Reporting Services の構成ファイル &#40;RSreportserver.config&#41; の変更](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [レポート サーバー アプリケーションで利用可能なメモリの構成](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services 構成ファイル](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
 その他のご不明な点は、 [Reporting Services のフォーラムにアクセスします](https://go.microsoft.com/fwlink/?LinkId=620231)
  
  
