---
title: Reporting Services でのサーバーとデータベースの接続に関する問題のトラブルシューティング | Microsoft Docs
ms.date: 05/28/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: 8bbb88df-72fd-4c27-91b7-b255afedd345
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: eda9f349cf53d77af14df10c842c9619fb6d370a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66403171"
---
# <a name="troubleshoot-server-and-database-connection-problems-with-reporting-services"></a>Reporting Services でのサーバーとデータベースの接続に関する問題のトラブルシューティング
このトピックでは、レポート サーバーへの接続時に発生する問題のトラブルシューティングを行います。 また、"予期しないエラー" メッセージについての情報も提供します。 データ ソースの構成と、レポート サーバーの接続情報の構成については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 」と「 [レポート サーバー データベース接続の構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="cannot-create-a-connection-to-data-source-datasourcename-rserroropeningconnection"></a>データ ソース 'datasourcename' への接続を作成できません (rsErrorOpeningConnection)。  
レポートにデータを提供する外部データ ソースに、レポート サーバーが接続できなかったときに発生する、一般的なエラーです。 このエラーと共に、根本原因を示したもう 1 つのエラー メッセージが表示されます。 **rsErrorOpeningConnection**では、その他のエラーが表示される場合があります。  
  
### <a name="login-failed-for-user-username"></a>ユーザー 'UserName' はログインできませんでした。  
ユーザーにはデータ ソースにアクセスする権限がありません。 SQL Server データベースを使用している場合は、ユーザーが使用しているデータベース ユーザー ログインが有効であるかどうかを確認してください。 データベース ユーザーまたは SQL Server ログインを作成する方法については、「 [データベース ユーザーの作成](../../relational-databases/security/authentication-access/create-a-database-user.md) 」と「 [ログインの作成](../../relational-databases/security/authentication-access/create-a-login.md)」を参照してください。  
  
### <a name="login-failed-for-user-nt-authorityanonymous-logon"></a>ユーザー 'NT AUTHORITY\ANONYMOUS LOGON' はログインできませんでした。  
複数のコンピューター接続を通じて資格情報が渡されたときに発生するエラーです。 Kerberos Version 5 プロトコルが有効でない環境で Windows 認証を使用している場合、複数のコンピューター接続を通じて資格情報が渡されると、このエラーが発生します。 このエラーを回避するには、保存された資格情報または要求された資格情報を使用することを検討してください。 この問題を回避する方法については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
### <a name="an-error-has-occurred-while-establishing-a-connection-to-the-server"></a>サーバーへの接続を確立中にエラーが発生しました。  
SQL Server に接続している場合、既定の設定では SQL Server によるリモート接続が許可されていないために、このエラーが発生した可能性があります。 (プロバイダー: 名前付きパイプ プロバイダー、エラー: 40 - SQL Server への接続を開けませんでした)。 このエラーは、レポート サーバー データベースをホストするデータベース エンジンのインスタンスによって返されます。 ほとんどの場合、このエラーが発生すると SQL Server サービスが停止します。 また、SQL Server Express with Advanced Services または名前付きインスタンスを使用している場合、レポート サーバーの URL かレポート サーバー データベースの接続文字列に誤りがあるとこのエラーが発生します。 これらの問題を解決するには、次のことを行います。  
  
* SQL Server (**MSSQLSERVER**) サービスが開始されていることを確認します。 データベース エンジンのインスタンスをホストするコンピューターで、[スタート] ボタンをクリックします。次に、[管理ツール] をクリックして、[サービス] をクリックし、[SQL Server (**MSSQLSERVER**)] までスクロールします。 まだ開始していなかった場合は、サービスを右クリックして [プロパティ] を選択し、[スタートアップの種類] で [自動] をクリックして、[適用]、[開始]、[OK] の順にクリックします。   
* レポート サーバーの URL およびレポート サーバー データベースの接続文字列が正しいことを確認します。 Reporting Services またはデータベース エンジンが名前付きインスタンスとしてインストールされている場合、セットアップ中に作成された既定の接続文字列にインスタンス名が含まれています。 たとえば、DEVSRV01 というサーバー上に SQL Server Express with Advanced Services の既定のインスタンスをインストールした場合、Web ポータルの URL は DEVSRV01\Reports$SQLEXPRESS になります。 さらに、接続文字列内のデータベース サーバー名は、DEVSRV01\SQLEXPRESS のようになります。 SQL Server Express の URL とデータ ソース接続文字列については、「 [SQL Server Express with Advanced Services の Reporting Services](https://technet.microsoft.com/library/ms365166(v=sql.105).aspx)」を参照してください。 レポート サーバー データベースの接続文字列を確認するには、Reporting Services 構成ツールを起動し、[データベースのセットアップ] ページを確認します。  
  
### <a name="a-connection-cannot-be-made-ensure-that-the-server-is-running"></a>接続できません。 サーバーが実行中であることを確認してください。  
このエラーは ADOMD.NET プロバイダーから返されます。 このエラーの発生原因はいくつかあります。 サーバーを "localhost" と指定した場合は、代わりにサーバー名を指定してください。 新しい接続にメモリを割り当てることができない場合にも、このエラーが発生します。 詳細については、サポート技術情報の記事 912017「 [Error message when you connect to an instance of SQL Server 2005 Analysis Services (SQL Server 2005 Analysis Services のインスタンスに接続するときのエラー メッセージ)](https://support.microsoft.com/kb/912017)」を参照してください。  
  
エラーに "そのようなホストは不明です" が含まれている場合は、Analysis Services サーバーが使用できないか接続が拒否されています。 Analysis Services サーバーが名前付きインスタンスとしてリモート コンピューター上にインストールされている場合は、このインスタンスが使用するポート番号を取得するために、SQL Server Browser サービスを実行する必要が生じることがあります。  
  
### <a name="report-services-soap-proxy-source"></a>(Report Services SOAP プロキシ ソース)  
レポート モデルの生成中にこのエラーが発生し、追加情報のセクションに "SQL Server が存在しないかアクセスが拒否されました" と表示される場合は、次の状況が発生している可能性があります。  
* データ ソースの接続文字列に "localhost" が含まれています。  
* SQL Server サービスの場合、TCP/IP は無効です。  
  
このエラーを解決するには、サーバー名を使用するよう接続文字列を変更するか、SQL Server サービスで TCP/IP を有効にします。 TCP/IP を有効にするには、次の手順を実行します。  
  
1. SQL Server 構成マネージャーを起動します。  
2. **[SQL Server ネットワークの構成]** を展開します。  
3. **[MSSQLSERVER のプロトコル]** を選択します。  
4. **[TCP/IP]** を右クリックし、 **[有効化]** を選択します。  
5. **[SQL Server のサービス]** を選択します。  
6. **[SQL Server (MSSQLSERVER)]** を右クリックし、 **[再起動]** をクリックします。  
  
## <a name="wmi-error-when-connecting-to-a-report-server-in-management-studio"></a>Management Studio でレポート サーバーに接続したときの WMI エラー  
Management Studio がレポート サーバーとの接続を確立する際、既定では、Reporting Services Windows Management Instrumentation (WMI) プロバイダーが使用されます。 WMI プロバイダーが正しくインストールされていない場合、レポート サーバーに接続しようとしたときに次のエラーが表示されます。  
  
\<サーバー名> に接続できません。 Reporting Services WMI プロバイダーがインストールされていないか、正しく構成されていません (Microsoft.SqlServer.Management.UI.RSClient)。  
  
このエラーを解決するにはソフトウェアを再インストールする必要があります。 それ以外の場合、一時的な回避策として、レポート サーバーに SOAP エンドポイント経由で接続する方法があります。  
  
* Management Studio の **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバー名]** にレポート サーバーの URL を入力します。 既定では `https://<your server name>/reportserver`です。 または、SQL Server 2008 Express with Advanced Services を使用している場合は、 `https://<your server name>/reportserver$sqlexpress`です。  
  
エラーを解決して、WMI プロバイダーを使って接続できるようにするには、セットアップを実行して Reporting Services を修復するか、Reporting Services を再インストールする必要があります。  
  
## <a name="connection-error-where-login-failed-due-to-unknown-user-name-or-bad-password"></a>不明なユーザー名または不正なパスワードが原因のログイン失敗による接続エラー  
レポート サーバーからレポート サーバー データベースへの接続にドメイン アカウントを使用しているときに、ドメイン アカウントのパスワードが変更された場合、 **rsReportServerDatabaseLogonFailed** エラーが発生することがあります。   
  
エラーのフルテキストは、"レポート サーバーでレポート サーバー データベースへの接続を開始できません。 ログオンに失敗しました (**rsReportServerDatabaseLogonFailed**)。 ファイル共有へのアクセス中にログオン エラーが発生しました。ユーザー アカウントまたはパスワードが無効です" です。  
  
パスワードを再設定する場合、接続を更新する必要があります。 詳細については、「 [レポート サーバー データベース接続の構成 (SSRS 構成マネージャー)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="the-report-server-cannot-open-a-connection-to-the-report-server-database-rsreportserverdatabaseunavailable"></a>レポート サーバーでレポート サーバー データベースへの接続を開始できません。 (rsReportServerDatabaseUnavailable)。  
エラーの全文: レポート サーバーでレポート サーバー データベースへの接続を開始できません。 すべての要求および処理でデータベースに接続する必要があります (rsReportServerDatabaseUnavailable)  
サーバーの内部ストレージである SQL Server リレーショナル データベースにレポート サーバーから接続できないときに発生するエラーです。 レポート サーバー データベースへの接続は、Reporting Services 構成ツールを使用して管理します。 このツールを実行し、[データベースのセットアップ] ページで接続情報を修正できます。 接続情報の更新には、このツールを使用することをお勧めします。このツールを使用すると、依存する設定の更新とサービスの再起動を確実に行えます。 詳細については、「 [レポート サーバー データベース接続の構成](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) 」と「 [レポート サーバー サービス アカウントの構成](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
このエラーは、レポート サーバー データベースをホストしているデータベース エンジン インスタンスがリモート接続用に構成されていない場合にも発生します。 SQL Server の一部のエディションでは、リモート接続が既定で有効になります。 使用している SQL Server データベース エンジン インスタンスで有効かどうかを確認するには、SQL Server 構成マネージャー ツールを実行します。 TCP/IP および名前付きパイプの両方を有効にする必要があります。 レポート サーバーでは両方のプロトコルを使用します。 リモート接続を有効にする方法については、「 [リモート管理用のレポート サーバーの構成](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)」の「レポート サーバー データベースへのリモート接続を構成する方法」を参照してください。  
  
データベース エンジン インスタンスの実行に使用したアカウントのパスワードの有効期限が切れている場合、エラーには "サーバーへの接続を確立中にエラーが発生しました。 SQL Server に接続している場合、既定の設定では SQL Server によるリモート接続が許可されていないために、このエラーが発生した可能性があります。 (**provider: SQL Server Network Interfaces, error: 26 - Error Locating Server/Instance Specified (プロバイダー: SQL Server ネットワーク インターフェイス、エラー: 26 - 指定されたサーバー/インスタンスの特定エラー))** "。 このエラーを解決するには、パスワードを再設定してください。   
  
## <a name="rpc-server-is-not-listening"></a>"RPC サーバーが受信待ちしていない"  
レポート サーバー サービスでは、いくつかの操作にリモート プロシージャ コール (RPC) サーバーを使用します。 "RPC サーバーが受信待ちしていない" エラーが発生した場合、レポート サーバー サービスが実行されていることを確認してください。  
  
## <a name="unexpected-error-general-network-error"></a>予期しないエラー (一般的なネットワーク エラーです)  
データ ソースの接続エラーを示すエラーです。 接続文字列をチェックし、データ ソースにアクセスするための権限があることを確認してください。 Windows 認証を使用してデータ ソースにアクセスしている場合、データ ソースをホストするコンピューターにアクセスするための権限が必要です。  
  
## <a name="unable-to-grant-database-access-in-sharepoint-central-administration"></a>SharePoint サーバーの全体管理でデータベースへのアクセスを許可できない  
Windows Vista または Windows Server 2008 上の SharePoint 製品やテクノロジと連携するように Reporting Services を構成した場合、SharePoint サーバーの全体管理の **[データベース アクセスの許可]** ページでアクセス権を付与しようとすると、"コンピューターへの接続を確立できません。" というエラー メッセージが表示されることがあります。  
  
これは、Windows Vista と Windows Server 2008 のユーザー アカウント制御 (UAC) が原因です。管理者権限が要求される作業では、管理者からの明示的な許可を得て権限を昇格し、管理者トークンを使用する必要があります。 ただしこの場合、Reporting Services サービス アカウントに SharePoint の構成データベースとコンテンツ データベースに対するアクセス権を付与するために、Windows SharePoint Services Administration サービスの権限を昇格させることはできません。  
  
SQL Server 2008 Reporting Services では、データベースへのアクセス権を必要とするのはレポート サーバー サービス アカウントだけですが、SQL Server 2005 Reporting Services SP2 では、レポート サーバー Windows サービス アカウントとレポート サーバー Web サービス アカウントの両方に、データベースへのアクセス権が必要です。 SQL Server 2008 のレポート サーバー サービス アカウントについては、「サービス アカウント (Reporting Services 構成)」を参照してください。  
  
この問題には、2 つの回避策があります。   
1.  1 つ目は、UAC を一時的に無効にし、SharePoint サーバーの全体管理を使ってアクセス権を付与する方法です。  
> [!IMPORTANT]  
> UAC を無効にすることによってこの問題を回避する場合は注意が必要です。SharePoint サーバーの全体管理でデータベースへのアクセス権を付与したら、直ちに UAC を有効にしてください。 UAC を無効にしないでこの問題を回避する場合は、このセクションで取り上げる 2 つ目の回避策を使用することになります。 UAC の詳細については、Windows の製品ドキュメントを参照してください。  
2. 2 つ目の回避策は、データベースへのアクセス権を Reporting Services サービス アカウントに対して手動で付与する方法です。 次の手順に従い、Reporting Services サービス アカウントを適切な Windows グループおよび適切なデータベース ロールに追加することによってアクセス権を付与できます。 この手順は、SQL Server 2008 Reporting Services のレポート サーバー サービス アカウントに適用されるものです。SQL Server 2005 Reporting Services を実行している場合は、レポート サーバー Windows サービス アカウントおよびレポート サーバー Web サービス アカウント向けの手順に従ってください。   
  
### <a name="to-manually-grant-database-access"></a>データベースへのアクセス権を手動で付与するには  
  
1. レポート サーバー サービス アカウントを Reporting Services コンピューターの WSS_WPG Windows グループに追加します。  
2. SharePoint の構成データベースとコンテンツ データベースをホストするデータベース インスタンスに接続し、レポート サーバー サービス アカウント用の SQL データベース ログインを作成します。  
3. 次のデータベース ロールに SQL データベース ログインを追加します。  
  
* WSS Content データベースの db_owner ロール  
* SharePoint_Config データベースの WSS_Content_Application_Pools ロール  
  
## <a name="unable-to-connect-to-the-reports-and-reportserver-directories-when-the-report-server-databases-are-created-on-a-virtual-sql-server-that-runs-in-a-microsoft-cluster-services-mscs-cluster"></a>レポート サーバーのデータベースを Microsoft Cluster Services (MSCS) クラスター上で実行されている仮想 SQL Server 上に作成した場合、/reports ディレクトリと /reportserver ディレクトリに接続できない  
レポート サーバーのデータベース ( **ReportServer** および **ReportServerTempDB**) を、MSCS クラスターの仮想 SQL Server 上に作成した場合、 `<domain>\<computer_name>$` 形式のリモート名が、SQL Server にログインとして登録されていない可能性があります。 このような形式のリモート名が接続で必要となるように、レポート サーバー サービス アカウントを構成した場合、ユーザーは Reporting Services の /reports ディレクトリおよび /reportserver ディレクトリに接続できません。 たとえば、組み込みの Windows アカウントである NetworkService では、このようなリモート名が必要になります。 この問題を回避するには、明示的なドメイン アカウントまたは SQL Server ログインを使用して、レポート サーバーのデータベースに接続するようにします。  
    
  ## <a name="see-also"></a>参照  
[Reporting Services と Power View のブラウザー サポート](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[エラーとイベント (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Reporting Services レポートのデータ取得に関する問題のトラブルシューティング](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Reporting Services のサブスクリプションと配信に関するトラブルシューティング](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

