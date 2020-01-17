---
title: レポート データ ソースに関する資格情報と接続情報を指定する | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2d1e804282459972b21303cf795a9c3a88ea93d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107035"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>レポート データ ソースに関する資格情報と接続情報を指定する
  レポート サーバーは、資格情報を使用して、レポートにコンテンツを提供したり、データ ドリブン サブスクリプションに受信者の情報を提供する外部データ ソースに接続します。 Windows 認証、データベース認証、認証なし、またはカスタム認証を使用する資格情報を指定できます。 ネットワーク経由で接続要求を送信するときに、レポート サーバーはユーザー アカウントまたは自動実行アカウントのいずれかの権限を借用します。 接続要求の実行時に使用されるセキュリティ コンテキストの詳細については、このトピックの「 [データ ソースの構成とネットワーク接続](#DataSourceConfigurationConnections) 」をご覧ください。  
  
> [!NOTE]  
>  資格情報は、レポート サーバーにアクセスするユーザーを認証するためにも使用されます。 レポート サーバーへのユーザーの認証に関する情報については、別のトピックで説明します。  
  
 レポートを作成すると、外部データ ソースへの接続が定義されます。 レポートをパブリッシュした後は、この接続を個別に管理できます。 動的な一覧からデータ ソースを選択できるようになる静的な接続文字列または式を指定できます。 データ ソースの種類と接続文字列を指定する方法の詳細については、次を参照してください。[データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)します。  
  
## <a name="using-remote-data-sources"></a>リモート データ ソースの使用  
 リモートのデータベース サーバーのデータをレポートに取得する場合、次の点を確認します。  
  
-   データベース サーバーに提供される資格情報が有効かどうか。 Windows ユーザー資格情報を使用している場合、ユーザーがサーバーとデータベースに対するアクセス許可を持っていることを確認してください。  
  
-   データベース サーバーで使用するポートが開いている。 外部コンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベースにアクセスする場合、またはレポート サーバー データベースが外部の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに置かれている場合は、外部コンピューターのポート 1433 および 1434 を開く必要があります。 ポートを開いた後、サーバーを必ず再起動してください。 詳しくは、「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)」をご覧ください。  
  
-   リモート接続を有効にする。 外部コンピューター上の SQL Server リレーショナル データベースにアクセスする場合、SQL Server 構成マネージャーを使用して、TCP によるリモート接続が有効であることを確認できます。  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>リモート データ ソースへの接続に使用する資格情報の指定方法  
 レポートにコンテンツを提供するデータ ソースは、通常リモート サーバーにホストされます。 レポートのデータを取得するには、ユーザーが事前に提供する一連の資格情報、または実行時に取得される一連の資格情報を使用して、レポート サーバーがリモート サーバーに接続する必要があります。 データ ソースを構成するときには、次の方法で資格情報を指定できます。  
  
-   ユーザーに資格情報を要求する。  
  
-   資格情報を保存する。  
  
-   Windows 統合セキュリティを使用する。  
  
-   資格情報を使用しない。  
  
 ネットワーク環境によって、ユーザーがサポートできる接続の種類が決まります。 たとえば、Kerberos Version 5 プロトコルが有効になっている場合、Windows 認証で利用できる委任機能と権限の借用機能を使用して、複数のサーバーにまたがって接続をサポートできます。 このようなセキュリティ機能がネットワークでサポートされていない場合は、接続の制限を回避する必要があります。 委任機能と権限の借用機能が有効でない場合、Windows 資格情報の有効期限が切れる前に、1 つのコンピューター接続で Windows 資格情報を渡すことができます。 クライアント コンピューターからレポート サーバー コンピューターへのユーザー接続は、最初の接続としてカウントされます。 リモート サーバーからデータを取得するレポートをユーザーが開いた場合、そのログインは 2 回目の接続としてカウントされます。接続で統合セキュリティを使用するように指定している場合、委任機能が無効になっていると、そのログインが失敗します。  
  
 クライアント コンピューターから外部レポート データ ソースへのラウンドトリップを遂行するために複数の接続が必要な場合は、次の方法の中から選択して接続を正常に行います。  
  
-   ドメインの委任機能と権限の借用機能を有効にして、資格情報を無制限に他のコンピューターに委任できるようにします。  
  
-   保存されている資格情報または要求された資格情報を使用して、レポート データの外部データ ソースに対してクエリを実行します。 資格情報には Windows ドメイン アカウントまたはデータベース ログインのいずれかを指定できます。  
  
### <a name="prompted-credentials"></a>資格情報の要求  
 要求された資格情報を使用するようにレポートのデータ ソース接続を構成した場合、レポートにアクセスするユーザーがデータを取得するには、それぞれがユーザー名とパスワードを入力する必要があります。 機密データを含むレポートには、この方法を使用することをお勧めします。 要求時に実行されるレポートでのみ、要求された資格情報を使用できます。 要求される資格情報は、Windows アカウントまたはデータベース ログインのいずれかです。 Windows 認証を使用するには、 **[データ ソースへの接続時に Windows 資格情報として使用する]** チェック ボックスをオンにする必要があります。 それ以外の場合、ユーザー認証のためにレポート サーバーからデータベース サーバーに資格情報が渡されます。 指定された資格情報をデータベース サーバーで認証できない場合、接続が失敗します。  
  
### <a name="windows-integrated-security"></a>Windows 統合セキュリティ  
 **[Windows 統合セキュリティ]** オプションがオンになっている場合、レポート サーバーから外部データ ソースをホストしているサーバーに、レポートにアクセスしているユーザーのセキュリティ トークンが渡されます。 この場合、ユーザーはユーザー名やパスワードを入力することを要求されません。 権限の借用機能と委任機能が有効な場合、この方法をお勧めします。 これらの機能が無効な場合、アクセスするすべてのサーバーが同じコンピューターに配置されている場合にのみ、この方法を使用してください。  
  
### <a name="stored-credentials"></a>保存された資格情報  
 外部データ ソースへのアクセスに使用する資格情報を保存することができます。 資格情報は、暗号化を元に戻せる状態でレポート サーバー データベースに保存されます。 レポートで使用されるデータ ソースごとに、1 セットの保存された資格情報を指定できます。 提供する資格情報によって、どのユーザーがレポートを実行しても同じデータが取得されます。  
  
 リモート データベース サーバーにアクセスするための戦略の一環として、保存された資格情報を使用することをお勧めします。 サブスクリプションをサポートする場合、またはレポート履歴の生成やレポート スナップショットの更新をスケジュールする場合は、保存された資格情報が必要です。 レポートをバックグラウンド処理として実行する場合は、レポート サーバーがレポートを実行するエージェントです。 指定されたユーザー コンテキストがないため、レポート サーバーはデータ ソースに接続するためにレポート サーバー データベースから資格情報を取得する必要があります。  
  
 指定するユーザー名とパスワードは、Windows 認証またはデータベース ログインのいずれかです。 Windows 資格情報を指定する場合、レポート サーバーによって、後続の認証用に Windows に資格情報が渡されます。 それ以外の場合、認証用にデータベース サーバーに資格情報が渡されます。  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>ドメイン ユーザー アカウントに "ローカル ログオンを許可する" 権限を付与する方法  
 保存済みの資格情報を使用して外部データ ソースに接続する場合、Windows ドメイン ユーザー アカウントにローカル ログオン権限が必要です。 レポート サーバーはこの権限を利用して、レポート サーバー上のユーザーの権限を借用し、その借用元ユーザーとして外部データ ソースに要求を送信します。  
  
 この権限を付与するには、次の手順に従います。  
  
1.  レポート サーバー コンピューターで、 **[管理ツール]** の **[ローカル セキュリティ ポリシー]** を開きます。  
  
2.  **[セキュリティの設定]** の下の **[ローカル ポリシー]** を展開し、 **[ユーザー権利の割り当て]** をクリックします。  
  
3.  詳細ペインで **[ローカル ログオンを許可する]** を右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ユーザーまたはグループの追加]** をクリックします。  
  
5.  **[場所]** をクリックし、検索するドメインまたは別の場所を指定して、 **[OK]** をクリックします。  
  
6.  対話的なログインを許可する Windows アカウントを入力し、 **[OK]** をクリックします。  
  
7.  **[ローカル ログオンを許可するのプロパティ]** ダイアログ ボックスで、 **[OK]** をクリックします。  
  
8.  選択したアカウントに、拒否する権限がないことを確認します。  
  
    1.  **[ローカルでログオンを拒否する]** を右クリックし、 **[プロパティ]** を右クリックします。  
  
    2.  該当するアカウントが表示されている場合は、そのアカウントを選択して **[削除]** をクリックします。  
  
#### <a name="using-impersonation-with-stored-credentials"></a>保存された資格情報での権限借用の使用  
 資格情報を使用して、別のユーザーの ID の権限を借用することもできます。 SQL Server データベースの場合、権限借用のオプションを使用すると、 [SETUSER](/sql/t-sql/statements/setuser-transact-sql) 関数が設定されます。  
  
> [!IMPORTANT]  
>  サブスクリプションをサポートするレポート、またはスケジュールを使用してレポート履歴を生成したりレポート実行スナップショットを更新するレポートには権限の借用を使用しないでください。  
  
### <a name="no-credentials"></a>資格情報を使用しない  
 資格情報を使用しないようにデータ ソース接続を構成できます。 常に資格情報を使用してデータ ソースにアクセスすることが推奨の方法です。資格情報を使用しない方法はお勧めしません。 ただし、以下の場合、資格情報を使用しないでレポートを実行することができます。  
  
-   リモート データ ソースで資格情報が必要とされない。  
  
-   資格情報が接続文字列で渡される (接続がセキュリティで保護されている場合にのみお勧めします)。  
  
-   レポートが、親レポートの資格情報を使用するサブレポートである。  
  
 このような条件下では、レポート サーバーは、事前に定義する必要がある自動実行アカウントを使用して、リモート データ ソースに接続します。 レポート サーバーはそのサービス資格情報を使用してリモート サーバーに接続しないため、レポート サーバーが接続のために使用できるアカウントを指定する必要があります。 このアカウントの作成の詳細については、「[自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
##  <a name="DataSourceConfigurationConnections"></a> データ ソースの構成とネットワーク接続  
 次の表は、資格情報の種類とデータ処理拡張機能の特定の組み合わせにおける接続方法を示しています。 カスタム データ処理拡張機能を使用している場合は、「 [カスタム データ処理拡張機能の接続を指定する](specify-connections-for-custom-data-processing-extensions.md)」をご覧ください。  
  
|**型**|**ネットワーク接続のコンテキスト**|**データ ソースの種類**<br /><br /> **(SQL Server、Oracle、ODBC、OLE DB、Analysis Services、XML、SAP NetWeaver BI、Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|統合セキュリティ|現在のユーザーを借用します。|すべてのデータ ソースの種類で、現在のユーザー アカウントを使用して接続します。|  
|Windows 資格情報|指定したユーザーの権限を借用します。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC、および OLE DB の場合 : 権限を借用したユーザー アカウントを使用して接続します。|  
|データベース資格情報|自動実行アカウントまたはサービス アカウントの権限を借用します。<br /><br /> (Reporting Services は、サービス ID を使用して接続要求を送信する際に管理者権限を削除します。)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC、OLE DB の場合:<br /><br /> ユーザー名とパスワードを接続文字列に追加します。<br /><br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の場合:<br /><br /> TCP/IP プロトコルを使用している場合は、接続が正常に行われます。それ以外の場合は、失敗します。<br /><br /> XML の場合 :<br /><br /> データベース資格情報を使用している場合は、レポート サーバーで接続に失敗します。|  
|なし|自動実行アカウントの権限を借用します。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Oracle、ODBC、OLE DB の場合:<br /><br /> 接続文字列で定義されている資格情報を使用します。 自動実行アカウントが未定義の場合は、レポート サーバーで接続に失敗します。<br /><br /> [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]の場合:<br /><br /> 自動実行アカウントが定義されていても、資格情報が指定されていない場合は、必ず接続に失敗します。<br /><br /> XML の場合 :<br /><br /> 自動実行アカウントが定義されている場合は、匿名ユーザーとして接続します。それ以外の場合は、接続に失敗します。|  
  
## <a name="setting-credentials-programmatically"></a>プログラム上での資格情報の設定  
 コード内で資格情報を設定して、レポートおよびレポート サーバーへのアクセスを制御できます。 詳しくは、「 [データ ソースと接続のメソッド](../report-server-web-service/methods/data-sources-and-connection-methods.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services でサポートされるデータ ソース &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [レポート データ ソースを管理する](../../integration-services/connection-manager/data-sources.md)   
 [レポート マネージャー &#40;SSRS ネイティブ モード&#41;](../report-manager-ssrs-native-mode.md)   
 [共有データ ソースを作成、削除、または変更する &#40;レポート マネージャー&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [レポートのデータ ソースのプロパティを構成する (レポート マネージャー)](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
