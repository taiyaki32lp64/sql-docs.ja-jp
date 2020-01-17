---
title: レポート サーバー データベースを作成する、SSRS Configuration Manager | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
ms.custom: seodec18
ms.date: 08/28/2019
ms.openlocfilehash: d8bbc1436b3615259248598a9fa19346d4f2a43f
ms.sourcegitcommit: a1ddeabe94cd9555f3afdc210aec5728f0315b14
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2019
ms.locfileid: "70123017"
---
# <a name="create-a-report-server-database"></a>レポート サーバー データベースを作成する 

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のネイティブ モードでは、レポート サーバーのメタデータとオブジェクトを格納するため、2 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベースが使用されます。 データベースの 1 つは主要な記憶域として使用され、もう 1 つは一時データの格納に使用されます。 

この 2 つのデータベースは同時に作成され、データベース名によってバインドされます。 既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでは、データベース名がそれぞれ **reportserver** と **reportservertempdb**になります。 2 つのデータベースをまとめて、**レポート サーバー データベース**または**レポート サーバー カタログ**と呼びます。

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の **SharePoint モード**には、データ警告メタデータに使用する 3 つ目のデータベースが含まれています。 SSRS サービス アプリケーションごとに、3 つのデータベースが作成されます。 データベース名には、既定で、サービス アプリケーションを表す GUID が含まれます。 

SharePoint モードの 3 つのデータベースの名前の例を次に示します。

- ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  

::: moniker-end
  
> [!IMPORTANT]  
> レポート サーバー データベースに対してクエリを実行するアプリケーションは作成しないでください。 レポート サーバー データベースは、パブリック スキーマではありません。 テーブル構造は、リリースごとに変更される可能性があります。 レポート サーバー データベースにアクセスする必要のあるアプリケーションを作成する場合、常に SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] API を使用して、レポート サーバー データベースにアクセスします。  
>
> 実行ログ ビューは、この規則の例外です。 詳細については、「 [レポート サーバー実行ログと ExecutionLog3 ビュー](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)」を参照してください。  
  
## <a name="ways-to-create-the-report-server-database"></a>レポート サーバー データベースを作成する方法

 ### <a name="native-mode"></a>ネイティブ モード
 ネイティブ モードのレポート サーバー データベースは、次の方法で作成できます。  
  
- **[自動]** 。 インストールに対して既定の構成オプションを選択する場合は、SQL Server セットアップ ウィザードを使用します。 SQL Server インストール ウィザードでは、このオプションは **[Report Server Installation Options]\(レポート サーバー インストール オプション\)** ページの **[Install and configure]\(インストールと構成\)** です。 **[Install only]\(インストールのみ\)** オプションを選択する場合は、SQL Server Reporting Services Configuration Manager を使用してデータベースを作成する必要があります。  
  
- **[手動]** 。 SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager を使用します。 リモート環境の [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]を使用してデータベースをホストする場合は、レポート サーバー データベースを手動で作成します。 詳しくは、「[ネイティブ モードのレポート サーバー データベースの作成](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)」をご覧ください。  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
### <a name="sharepoint-mode"></a>SharePoint モード 
**[Report Server Installation Options]\(レポート サーバー インストール オプション\)** ページにある SharePoint モード用のオプションは、 **[Install only]\(インストールのみ\)** の 1 つだけです。 このオプションを選択すると、SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のすべてのファイルと SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 共有サービスがインストールされます。 次に、次のいずれかの方法で SSRS サービス アプリケーションを少なくとも 1 つ作成します。  
  
- SharePoint Server のサーバーの全体管理に移動して、SSRS サービス アプリケーションを作成します。 詳しくは、「[SharePoint モードでの最初のレポート サーバーのインストール](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication)」の**サービス アプリケーションの作成**に関するセクションをご覧ください。  
  
- SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の PowerShell コマンドレットを使用して、サービス アプリケーションとレポート サーバー データベースを作成します。 詳しくは、「[Reporting Services SharePoint モード用の PowerShell コマンドレット](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md)」トピックでサービス アプリケーション作成のサンプルをご覧ください。  

::: moniker-end
  
## <a name="database-server-version-requirements"></a>データベース サーバーのバージョンの要件

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レポート サーバー データベースをホストするために使用されます。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] インスタンスは、ローカルでもリモートでもかまいません。 以下のサポートされているバージョンの [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]で、レポート サーバー データベースをホストできます。  
::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

- Azure SQL Managed Instance

- SQL Server 2019

::: moniker-end
::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

- SQL Server 2017  
::: moniker-end

- [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
- [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  

リモート コンピューターにレポート サーバー データベースを作成する場合は、ネットワークにアクセスできるドメイン ユーザー アカウントまたはサービス アカウントを使用するように接続を構成します。 リモートの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを使用する場合は、レポート サーバーがインスタンスに接続するときに使用する必要がある資格情報を検討します。 詳しくは、「[レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」をご覧ください。  
  
> [!IMPORTANT]  
> レポート サーバーと、レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、同じドメインに属していなくてもかまいません。 インターネット配置では、ファイアウォール内にあるサーバーを使用するのが一般的です。 
>
> レポート サーバーをインターネット アクセス用に構成する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の資格情報を使用してファイアウォール内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。 IPSec を使用して接続をセキュリティ保護します。  
  
## <a name="edition-requirements-for-a-database-server"></a>データベース サーバーのエディションの要件 

 レポート サーバー データベースを作成するときは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションでデータベースをホストできるわけではないことに注意してください。 詳しくは、「[SQL Server の各エディションでサポートされる SQL Server Reporting Services の機能](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)」の「[レポート サーバー データベースのエディションの要件](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md#edition-requirements-for-the-report-server-database)」をご覧ください。  

## <a name="next-steps"></a>次の手順

[Reporting Services Configuration Manager](https://msdn.microsoft.com/63519ef4-e68a-42fb-9cf7-31228ea4e434) について読みます。  

その他の質問 [Reporting Services フォーラム](https://go.microsoft.com/fwlink/?LinkId=620231)で質問してください。
