---
title: Data Quality Services のインストール
ms.date: 09/11/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 486e4216-a946-4c6e-828c-61bc905f7ec1
author: swinarko
ms.author: sawinark
ms.openlocfilehash: b7a9d9ce36a3419883adae9050ffabd0d1f9b012
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75252189"
---
# <a name="install-data-quality-services"></a>Data Quality Services のインストール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversionLong](../../includes/ssdqsnoversionlong-md.md)](DQS) には、 **[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]** と**[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]** の2つのコンポーネントが含まれています。  
  
|DQS コンポーネント|説明|  
|-------------------|-----------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] は、 [!INCLUDE[ssNoversion](../../includes/ssNoVersion-md.md)] データベース エンジンの上にインストールされ、DQS_MAIN、DQS_PROJECTS、および DQS_STAGING_DATA の 3 つのデータベースを含んでいます。 DQS_MAIN には、DQS ストアド プロシージャ、DQS エンジン、パブリッシュ済みナレッジ ベースが含まれています。 DQS_PROJECTS には、データ品質プロジェクトの情報が含まれています。 DQS_STAGING_DATA は、ソース データをコピーし、DQS 操作を実行して処理後のデータをエクスポートするためのステージング領域です。|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|
  [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] は、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]に接続するスタンドアロン アプリケーションであり、高度に直感的なグラフィカル ユーザー インターフェイスを使用して、データ品質に関する操作、および DQS に関連するその他の管理タスクを実行できます。|  
  
> [!IMPORTANT]  
>  上記の 2 種類の DQS コンポーネントとは別に、以下の作業も実行できます。  
>   
>  Integration Services 内にある、Integration Services パッケージ化プロセス内で DQS クレンジングを実行するデータ クレンジング変換を使用します。この機能は Integration Services のインストール時に自動的にインストールされます。 Integration Services のインストールの詳細については、「 [Integration Services のインストール](../../integration-services/install-windows/install-integration-services.md)」を参照してください。  
>   
>  マスター データ サービスの DQS 統合を有効にして、Excel 用マスター データ サービス アドインの DQS 照合機能を使用します。 詳細については、「 [マスター データ サービスを使用した Data Quality Services 統合の有効化](../../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md)」を参照してください。  
  
 DQS インストール プロセスは、3 つの部分から成ります。  
  
-   [インストール前の作業](#PreInstallationTasks): DQS をインストールする前に、システム要件を確認します。  
  
-   [Data Quality Services のインストールタスク](#DQSInstallation): SQL Server セットアップを使用して DQS をインストールします。  
  
-   [インストール後の作業](#PostInstallationTasks): SQL Server のセットアップを完了した後に、これらのタスクを実行して DQS のインストールを完了します。  
  
> [!NOTE]  
>  コマンド ラインからのセットアップの実行の手順については、ここでは扱いません。 
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] とクライアントをインストールするコマンドライン オプションの詳細については、「 [コマンド プロンプトからの SQL Server のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Feature) 」の「 [機能パラメーター](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
##  <a name="PreInstallationTasks"></a>インストール前の作業  
 DQS をインストールする前に、コンピューターが最小システム要件を満たしていることを確認します。 次の表は、DQS コンポーネントの最小システム要件に関する情報を示しています。  
  
|DQS コンポーネント|最小システム要件|  
|-------------------|---------------------------------|  
|[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]|メモリ (RAM): 最小: 2 GB / 推奨: 4 GB 以上<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]データベース エンジン。 詳細については、「 [SQL Server データベース エンジンのインストール](../../database-engine/install-windows/install-sql-server-database-engine.md)」を参照してください。|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|.NET Framework 4.0 (インストールされていない場合は、 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] のインストール時にインストールされます)<br /><br /> Internet Explorer 6.0 SP1 以降|  
  
> [!IMPORTANT]  
>  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] と [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] は、同じコンピューターにインストールすることも、別のコンピューターにインストールすることもできます。 両方のコンポーネントは、それぞれ個別に任意の順序でインストールできます。 ただし、 [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]を使用するには、接続先の [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] をインストールする必要があります。  
>   
>  
  [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] の現在または以前のバージョンと、DQS クレンジング変換を使用して、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] の [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] バージョンに接続できます。 既存のバージョンの DQS を [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]にアップグレードする方法の詳細については、「 [Data Quality Services のアップグレード](../../database-engine/install-windows/upgrade-data-quality-services.md)」を参照してください。  
>   
>  Microsoft Excel は Data Quality Client のインストールの前提条件ではありませんが、Excel ファイルからのドメイン値のインポートやナレッジ検出のための Excel ファイル内のソース データへのマッピング、クレンジング、照合アクティビティなどのさまざまな操作をクライアント アプリケーションで実行するには、Microsoft Excel 2003 以降が Data Quality Client コンピューターにインストールされている必要があります。  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]のインストールに必要な最小システム要件の詳細については、「 [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」を参照してください。  
  
##  <a name="DQSInstallation"></a>Data Quality Services のインストールタスク  
 DQS のコンポーネントをインストールするには、 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] セットアップを使用する必要があります。 SQL Server セットアップを実行するときは、インストール ウィザードの一連のページに従いながら、要件に基づいて適切なオプションを選択する必要があります。 インストール ウィザードのページのうち、選択するオプションによって DQS のインストールに影響するページのみを次の表に示します。  
  
|ページ|操作|  
|----------|------------|  
|特徴選択|選択肢:<br /><br /> **データベースエンジン Services**の**Data Quality services**をインストールする[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]には、をインストールします。 <br />
  **[Data Quality Services]** チェック ボックスをオンにすると、SQL Server セットアップでインストーラー ファイル DQSInstaller.exe がコンピューターの SQL Server インスタンス ディレクトリにコピーされます。 
  *のインストールを完了*[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] するには、SQL Server セットアップを完了した後で、このファイルを実行する必要があります。 また、使用する前に、いくつかの追加の手順を実行して [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] を構成する必要があります。 詳細については、「 [インストール後の作業](#PostInstallationTasks)」を参照してください。<br /><br /> **** インストール[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]する Data Quality Client。<br /><br /> (推奨) **[管理ツール - 基本]** の下の **[管理ツール - 完全]** を選択して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] をインストールします。 これにより、グラフィカル ユーザー インターフェイスを使用して SQL Server のインスタンスを管理できるようになり、次のセクションで示すインストール後の追加の作業の実行が容易になります。|  
|データベース エンジンの構成|
  **[現在のユーザーの追加]** をクリックして、ユーザー Windows アカウントを sysadmin 固定サーバー ロールに追加します。 これは、後で DQSInstaller.exe ファイルを実行して [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールを完了するために必要です。|  
  
##  <a name="PostInstallationTasks"></a>インストール後の作業  
 SQL Server のインストール ウィザードを完了した後で、このセクションで説明する追加手順を実行して、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールを実行し、構成して、使用する必要があります。  
  
1.  
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールを完了するには、DQSInstaller.exe ファイルを実行します。 DQSInstaller.exe ファイルを実行すると、次の操作が行われます。  
  
    -   DQS_MAIN, DQS_PROJECTS, および DQS_STAGING_DATA データベースが作成されます。  
  
    -   ##MS_dqs_db_owner_login## ログインと ##MS_dqs_service_login## ログインが作成されます。  
  
    -   DQS_MAIN データベースに dqs_administrator, dqs_kb_editor ロールと dqs_kb_operator ロールが作成されます。  
  
    -   DQInitDQS_MAIN ストアド プロシージャがマスター データベースに作成されます。  
  
    -   DQS_install.log ファイルは通常 C:\Program Files\Microsoft SQL Server\MSSQL13.*<instance_name>* \MSSQL\Log フォルダーに作成されます。 このファイルには、DQSInstaller.exe ファイルの実行時に行われた操作に関する情報が含まれます。  
  
    -   マスター データ サービス データベースが [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]と同じ SQL Server インスタンス上に存在する場合は、マスター データ サービス ログインにマップされたユーザーが作成され、DQS_MAIN データベースに対する dqs_administrator ロールが付与されます。  
  
     これにより [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のインストールが完了します。  
  
     詳細については、「 [Data Quality Server のインストールを完了するための DQSInstaller の実行」を](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md)参照してください。  
  
2.  ユーザーに DQS ロールを付与します。  
  
     
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] を使用して [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]にログオンするには、DQS_MAIN データベースに対して、次の 3 つのロールのいずれかが必要です。  
  
    -   **dqs_administrator**  
  
    -   **dqs_kb_editor**  
  
    -   **dqs_kb_operator**  
  
     既定では、ユーザー アカウントが sysadmin 固定サーバー ロールのメンバーである場合、DQS ロールがユーザー アカウントに付与されていない場合でも [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] を使用して [!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)] にログオンできます。 3 つの DQS ロールの詳細については、「 [DQS のセキュリティ](../../data-quality-services/dqs-security.md)」を参照してください。  
  
     詳細については、「 [ユーザーに DQS ロールを付与する](../../data-quality-services/install-windows/grant-dqs-roles-to-users.md)」を参照してください。  
  
    > [!NOTE]  
    >  DQS_PROJECTS および DQS_STAGING_DATA データベースについては、3 つの DQS ロールは使用できません。  
  
3.  データに対する DQS 操作を可能にします。 ソース データにアクセスして DQS 操作を実行できることと、処理後のデータをデータベース内のテーブルにエクスポートできることを確認します。  
  
     詳細情報の参照先  
                    [DQS 操作のデータにアクセス](../../data-quality-services/install-windows/access-data-for-the-dqs-operations.md)します。  
  
## <a name="see-also"></a>参照  
 [ビデオ: DQS をインストールして構成する](https://go.microsoft.com/fwlink/?LinkId=238241)   
 [.NET Framework の更新後に SQLCLR アセンブリをアップグレードする](../../data-quality-services/install-windows/upgrade-sqlclr-assemblies-after-net-framework-update.md)   
 [DQSInstaller を使用した DQS ナレッジベースのエクスポートとインポート](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)   
 [Data Quality Services のアップグレード](../../database-engine/install-windows/upgrade-data-quality-services.md)   
 [Data Quality Server オブジェクトの削除](../../sql-server/install/remove-data-quality-server-objects.md)   
 [ビジネスインテリジェンス機能のインストール SQL Server](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
 [アンインストール SQL Server](../../sql-server/install/uninstall-sql-server.md)   
 [Data Quality Services](../../data-quality-services/data-quality-services.md)   
 [DQS でのインストールと構成に関する問題のトラブルシューティング](https://social.technet.microsoft.com/wiki/contents/articles/3776.aspx)  
  
  
