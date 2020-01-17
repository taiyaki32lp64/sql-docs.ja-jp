---
title: レポート サーバー データベース接続の構成 (SSRS 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services]
- report servers [Reporting Services], connections
- report server database
- databases [Reporting Services], connections
- security [Reporting Services], database connections
ms.assetid: 9759a9fb-35e9-4215-969b-a9f1fea18487
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 8b6f1fa1697898432479b524659383d81fc8836a
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952629"
---
# <a name="configure-a-report-server-database-connection--ssrs-configuration-manager"></a>レポート サーバー データベース接続の構成 (SSRS 構成マネージャー)
  レポート サーバーの各インスタンスには、レポート サーバーの管理対象であるレポート、レポート モデル、共有データ ソース、リソース、およびメタデータが保存された、レポート サーバー データベースへの接続が必要です。 既定の構成をインストールする場合、最初の接続はレポート サーバーのインストール中に作成することができます。 ほとんどの場合は、セットアップの完了後に、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して接続を構成します。 この接続は、いつでも変更して、アカウントの種類を変更したり資格情報をリセットしたりできます。 データベースを作成し、接続を構成する実行手順については、「[ネイティブ モードのレポート サーバー データベース &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)」を参照してください。  
  
 レポート サーバー データベース接続を構成する必要があるのは、次の状況です。  
  
-   レポート サーバーを初めて使用するために構成する。  
  
-   別のレポート サーバー データベースを使用するようにレポート サーバーを構成する。  
  
-   データベース接続に使用するユーザー アカウントまたはパスワードを変更する。 データベース接続を更新する必要があるのは、アカウント情報が RSReportServer.config ファイルに保存されている場合だけです。 接続にサービス アカウントを使用している (資格情報の種類として Windows 統合セキュリティを使用する) 場合は、パスワードが保存されないので、接続情報を更新する必要はありません。 アカウント変更の詳細については、「 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
-   レポート サーバー スケールアウト配置を構成する。 スケールアウト配置を構成するには、レポート サーバー データベースへの複数の接続を作成する必要があります。 この複数段階に分かれた操作の実行方法の詳細については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
## <a name="how-reporting-services-connects-to-the-database-engine"></a>Reporting Services によるデータベース エンジンへの接続方法  
 レポート サーバーからレポート サーバー データベースへのアクセスは、資格情報や接続情報に依存します。また、そのデータベースを使用するレポート サーバー インスタンスに対して有効な暗号化キーにも依存します。 機密データの保存や取得には、有効な暗号化キーが必要です。 暗号化キーは、最初にデータベースを構成したときに自動的に作成されます。 レポート サーバー サービス ID を変更する場合、キーの作成後にキーを更新する必要があります。 暗号化キーを使用した作業の詳細については、「[暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。  
  
 レポート サーバー データベースは、レポート サーバーのみがアクセスする内部コンポーネントです。 レポート サーバー データベースに対して指定した資格情報および接続情報は、レポート サーバーによって排他的に使用されます。 レポートを要求するユーザーに、レポート サーバー データベースに対するデータベース権限やデータベース ログインは不要です。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、`System.Data.SqlClient` を使用して、レポート サーバー データベースをホストする[!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のローカル インスタンスを使用する場合、レポート サーバーは共有メモリを使用して接続を確立します。 リモートのデータベース サーバーをレポート サーバー データベースとして使用する場合は、使用中のエディションに応じてリモート接続を有効にする必要が生じる場合があります。 Enterprise Edition を使用している場合は、TCP/IP でのリモート接続が既定で有効になっています。  
  
 インスタンスがリモート接続を受け入れることを確認するには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックし、各サービスで TCP/IP プロトコルが有効になっていることを確認します。  
  
 リモート接続を有効にすると、クライアント プロトコルおよびサーバー プロトコルも有効になります。 プロトコルが有効になっていることを確認するには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。次に、 **[SQL Server ネットワークの構成]** をクリックし、 **[MSSQLSERVER のプロトコル]** をクリックします。 詳細については、 [オンライン ブックの「](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) サーバー ネットワーク プロトコルの有効化または無効化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
## <a name="defining-a-report-server-database-connection"></a>レポート サーバー データベース接続の定義  
 接続を構成するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャー ツールまたは **rsconfig** コマンド ライン ユーティリティを使用する必要があります。 レポート サーバーには、次の接続情報が必要です。  
  
-   レポート サーバー データベースをホストする [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの名前。  
  
-   レポート サーバー データベースの名前。 接続を初めて作成する場合、新しいレポート サーバー データベースを作成することも、既存のデータベースを選択することもできます。 詳細については、 [レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)」を参照してください。  
  
-   資格情報の種類。 サービス アカウント、Windows ドメイン アカウント、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ログインを使用できます。  
  
-   ユーザー名およびパスワード (Windows ドメイン アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを使用した場合のみ必要です)。  
  
 使用する資格情報は、レポート サーバー データベースへのアクセス権が許可されている必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用する場合、この手順は自動的に実行されます。 データベースのアクセスに必要な権限の詳細については、このトピックの「データベース権限」のセクションを参照してください。  
  
### <a name="storing-database-connection-information"></a>データベース接続情報の保存  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 次の RSreportserver.config 設定に接続情報が格納され暗号化されています。 これらの設定の暗号化された値を作成するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールまたは rsconfig ユーティリティを使用する必要があります。  
  
 すべての値がどの種類の接続に対しても設定されるとは限りません。 既定値を使用して接続を構成した場合 (つまり、サービスアカウントを使用して接続を確立した場合)、<`LogonUser`>、<`LogonDomain`>、および <`LogonCred`> は次のように空になります。  
  
```  
<Dsn></Dsn>  
<ConnectionType></ConnectionType>  
<LogonUser></LogonUser>  
<LogonDomain></LogonDomain>  
<LogonCred></LogonCred>  
```  
  
 特定の Windows アカウントまたはデータベース ログインを使用する接続を構成する場合、続いてアカウントまたはログインを変更した場合に格納される値を更新することを忘れないでください。  
  
### <a name="choosing-a-credential-type"></a>資格情報の種類の選択  
 レポート サーバー データベースへの接続に使用できる資格情報には、3 つの種類があります。  
  
-   レポート サーバー サービス アカウントを使用する Windows 統合セキュリティ。 レポート サーバーは単一のサービスとして実装されているため、サービスの実行に使用するアカウントのみにデータベース アクセスが必要になります。  
  
-   Windows ユーザー アカウント。 レポート サーバーおよびレポート サーバー データベースが同じコンピューターにインストールされている場合、ローカル アカウントを使用できます。 それ以外の場合、ドメイン アカウントを使用する必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインです。  
  
> [!NOTE]  
>  レポート サーバー データベースへの接続には、カスタム認証拡張機能を使用できません。 カスタム認証拡張機能は、レポート サーバーにプリンシパルを認証するためにのみ使用します。 レポート サーバー データベースへの接続や、レポートにコンテンツを提供する外部データ ソースへの接続に対しては、効力がありません。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが Windows 認証用に構成されており、レポート サーバー コンピューターと同じドメインまたは信頼関係のあるドメインにある場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールで接続プロパティとして管理するサービス アカウントまたはドメイン ユーザー アカウントを使用するように接続を構成できます。 データベース サーバーが別のドメインにある場合、またはワークグループ セキュリティを使用している場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ログインを使用するように接続を構成する必要があります。 この場合、必ず接続を暗号化してください。  
  
##### <a name="using-service-accounts-and-integrated-security"></a>サービス アカウントと統合セキュリティの使用  
 Windows 統合セキュリティを使用すると、レポート サーバー サービス アカウント経由で接続できます。 レポート サーバー サービス アカウントには、レポート サーバー データベースへのログイン権限が与えられます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を既定の構成でインストールした場合、セットアップは、Windows 統合セキュリティを既定の資格情報の種類として選択します。  
  
 サービス アカウントは信頼されたアカウントであり、レポート サーバー データベース接続の管理に対するメンテナンスが軽減されます。 サービス アカウントでは Windows 統合セキュリティを使用して接続を行うため、資格情報の格納は不要です。 ただし、後でサービス アカウントのパスワードまたは ID を変更する場合 (たとえば、ビルトイン アカウントからドメイン アカウントに切り替える場合など) は、必ず [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して変更を行ってください。 このツールを使用すると、データベース権限が自動的に更新され、変更したアカウント情報が使用されるようになります。 詳細については、「[レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
 サービス アカウントを使用するようにデータベース接続を構成するとき、レポート サーバー データベースがリモート コンピューター上にある場合には、アカウントにネットワーク アクセス許可が必要になります。 レポート サーバー データベースが別のドメインつまりファイアウォールの背後にある場合や、ドメイン セキュリティではなくワークグループ セキュリティを使用している場合は、サービス アカウントを使用しないでください。 代わりに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ユーザー アカウントを使用してください。  
  
##### <a name="using-a-domain-user-account"></a>ドメイン ユーザー アカウントの使用  
 レポート サーバー データベースへのレポート サーバー接続には、Windows ユーザー アカウントを指定できます。 ローカル アカウントまたはドメイン アカウントを使用する場合、パスワードまたはアカウントを変更するたびにレポート サーバー データベース接続を更新する必要があります。 接続を更新するには、必ず [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用してください。  
  
##### <a name="using-a-sql-server-login"></a>SQL Server ログインの使用  
 レポート サーバー データベースに接続する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを 1 つだけ指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用しており、レポート サーバー データベースがリモート コンピューター上にある場合は、サーバー間のデータ転送をセキュリティで保護するため、IPSec を使用してください。 データベース ログインを使用する場合、パスワードまたはアカウントを変更するたびにレポート サーバー データベース接続を更新する必要があります。  
  
### <a name="database-permissions"></a>データベース権限  
 レポート サーバー データベースへの接続に使用するアカウントには、次のロールが与えられます。  
  
-   **ReportServer** データベースに対する **public** ロールおよび **RSExecRole** ロール。  
  
-   **master** データベース、 **msdb**データベース、および **ReportServerTempDB**データベースに対する **RSExecRole** ロール。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用して接続を作成または変更するときには、これらの権限が自動的に与えられます。 rsconfig ユーティリティを使用しており、接続に別のアカウントを指定する場合は、その新しいアカウント用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを更新する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールでスクリプト ファイルを作成して、レポート サーバー用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを更新することもできます。  
  
### <a name="verifying-the-database-name"></a>データベース名の確認  
 特定のレポート サーバー インスタンスで使用されているレポート サーバー データベースを確認するには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用します。 名前を確認するには、レポート サーバー インスタンスに接続して、[データベースのセットアップ] ページを開きます。  
  
## <a name="using-a-different-report-server-database-or-moving-a-report-server-database"></a>別のレポート サーバー データベースの使用、またはレポート サーバー データベースの移動  
 接続情報を変更することによって、レポート サーバー インスタンスで別のレポート サーバー データベースを使用するように構成できます。 データベースの切り替えが生じる一般的なケースとして、運用レポート サーバーを配置する場合があります。 テストレポートサーバーデータベースから運用レポートサーバーデータベースへの切り替えは、通常、実稼働サーバーのロールアウトによって実行されます。また、レポートサーバーデータベースを別のコンピューターに移動することもできます。 詳細については、 [オンライン ブックの「](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) Reporting Services のアップグレードと移行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
## <a name="configuring-multiple-reports-servers-to-use-the-same-report-server-database"></a>複数のレポート サーバーで同じレポート サーバー データベースを使用するための構成  
 複数のレポート サーバーで同じレポート サーバー データベースを使用するように構成できます。 この配置構成はスケールアウト配置と呼ばれます。 サーバー クラスター内で複数のレポート サーバーを実行する場合は、この構成が前提条件となります。 ただし、この構成は、サービス アプリケーションを分割する場合や、新しいレポート サーバー インスタンスのインストールと設定をテストして既存のレポート サーバーのインストールと比較する場合にも使用できます。 詳細については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー データベースの作成 &#40;SSRS構成マネージャー&#41;](../../../2014/sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)  
  
  
