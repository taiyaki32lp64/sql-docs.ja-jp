---
title: Azure で SSIS パッケージをデプロイし、実行する | Microsoft Docs
description: SQL Server Integration Services (SSIS) プロジェクトを Azure SQL Database 上の SSIS カタログにデプロイして、パッケージを実行する方法について説明します
ms.date: 05/22/2018
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: swinarko
ms.author: sawinark
ms.reviewer: maghan
ms.openlocfilehash: 42250d8edbd646f9bd89f3663f2591b3404fe05f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68007941"
---
# <a name="tutorial-deploy-and-run-a-sql-server-integration-services-ssis-package-in-azure"></a>チュートリアル:Azure で SQL Server Integration Services (SSIS) パッケージをデプロイし、実行する

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


このチュートリアルでは、Azure SQL Database の SSIS カタログに SQL Server Integration Services (SSIS) プロジェクトをデプロイする方法、Azure-SSIS Integration Runtime でのパッケージの実行方法、および実行中のパッケージの監視方法を示します。

## <a name="prerequisites"></a>Prerequisites

始める前に、バージョン 17.2 以降の SQL Server Management Studio があることを確認します。 最新バージョンの SSMS をダウンロードするには、「[SQL Server Management Studio (SSMS) のダウンロード](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)」を参照してください。

また、Azure で SSISDB データベースを設定し、Azure SSIS 統合ランタイムをプロビジョニングしていることを確認してください。 Azure で SSIS をプロビジョニングする方法については、「[SQL Server Integration Services パッケージを Azure にデプロイする](https://docs.microsoft.com/azure/data-factory/tutorial-deploy-ssis-packages-azure)」を参照してください。

## <a name="for-azure-sql-database-get-the-connection-info"></a>Azure SQL Database の場合の接続情報の取得

Azure SQL Database でパッケージを実行するには、SSIS カタログ データベース (SSISDB) に接続するために必要な接続情報を取得します。 次の手順では、完全修飾サーバー名とログイン情報が必要です。

1. [Azure ポータル](https://portal.azure.com/)にログインします。
2. 左側のメニューから **[SQL Databases]** を選択し、 **[SQL データベース]** ページで SSISDB データベースを選びます。 
3. データベースの **[概要]** ページで、完全修飾サーバー名を確認します。 **[クリックしてコピー]** オプションを表示するには、サーバー名にマウス ポインターを移動します。 
4. Azure SQL Database サーバーのログイン情報を忘れた場合は、[SQL Database サーバー] ページに移動し、サーバーの管理者名を表示します。 必要に応じて、パスワードをリセットできます。

## <a name="connect-to-the-ssisdb-database"></a>SSISDB データベースに接続する

SQL Server Management Studio を使用して、Azure SQL Database サーバー上の SSIS カタログに接続します。 詳細とスクリーンショットについては、「[Azure 上の SSISDB カタログ データベースへの接続](ssis-azure-connect-to-catalog-database.md)」を参照してください。

ここで、覚えるべき重要事項が 2 点あります。 これらの点については、以下の手順で説明されます。
-   **mysqldbserver.database.windows.net** という形式で、Azure SQL Database サーバーの完全修飾名を入力します。
-   接続するデータベースとして `SSISDB` を選択します。

> [!IMPORTANT]
> Azure SQL Database サーバーは、ポート 1433 でリッスンします。 企業のファイアウォール内から Azure SQL Database サーバーに接続しようとする場合、正常に接続するには、このポートを企業のファイアウォールで開ける必要があります。

1. SQL Server Management Studio を開きます。

2. **サーバーに接続します**。 **[サーバーへの接続]** ダイアログ ボックスに次の情報を入力します。

   | 設定       | 提案される値 | [説明] | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **サーバーの種類** | データベース エンジン | この値は必須です。 |
   | **サーバー名** | 完全修飾サーバー名 | 名前は **mysqldbserver.database.windows.net** の形式である必要があります。 サーバー名が必要な場合は、「[Azure 上の SSISDB カタログ データベースへの接続](ssis-azure-connect-to-catalog-database.md)」を参照してください。 |
   | **[認証]** | SQL Server 認証 (SQL Server Authentication) | Windows 認証を使用して Azure SQL Database に接続することはできません。 |
   | **Login** | サーバー管理者アカウント | これはサーバーを作成したときに指定したアカウントです。 |
   | **パスワード** | サーバー管理者アカウントのパスワード | これはサーバーを作成したときに指定したパスワードです。 |

3. **SSISDB データベースに接続します**。 **[オプション]** を選択して、 **[サーバーへの接続]** ダイアログ ボックスを展開します。 展開した **[サーバーへの接続]** ダイアログ ボックスで、 **[接続プロパティ]** タブを選択します。 **[データベースへの接続]** フィールドで、`SSISDB` を選択または入力します。

4. **[接続]** を選択します。 [オブジェクト エクスプローラー] ウィンドウで、SSMS を開きます。 

5. オブジェクト エクスプローラーで、 **[Integration Services カタログ]** 、 **[SSISDB]** の順に展開し、SSIS カタログ データベース内のオブジェクトを表示します。

## <a name="deploy-a-project-with-the-deployment-wizard"></a>配置ウィザードを使用してプロジェクトを配置する

パッケージの配置と配置ウィザードについて詳しくは、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../packages/deploy-integration-services-ssis-projects-and-packages.md)」および「[Integration Services 配置ウィザード](../packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)」を参照してください。

> [!NOTE]
> Azure への配置では、プロジェクト配置モデルのみがサポートされます。

### <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 配置ウィザードを起動する
1. SSMS のオブジェクト エクスプローラーで、 **[Integration Services カタログ]** ノードと **[SSISDB]** ノードを展開した状態で、プロジェクト フォルダーを展開します。

2.  **[プロジェクト]** ノードを選びます。

3.  **[プロジェクト]** ノードを右クリックして、 **[プロジェクトの配置]** を選びます。 Integration Services 配置ウィザードが開きます。 SSIS カタログ データベースから、またはファイル システムから、プロジェクトを配置することができます。

    ![SSMS からプロジェクトを配置する](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project1.png)

    ![SSIS 配置ウィザード ダイアログ ボックスの表示](media/ssis-azure-deploy-run-monitor-tutorial/ssisdb-deploy-project2.png)

### <a name="deploy-a-project-with-the-deployment-wizard"></a>配置ウィザードを使用してプロジェクトを配置する
1. 配置ウィザードの **[概要]** ページで、概要を確認します。 **[次へ]** を選択して、 **[ソースの選択]** ページを開きます。

2. **[ソースの選択]** ページで、配置する既存の SSIS プロジェクトを選びます。
    -   作成したプロジェクト配置ファイルを配置するには、 **[プロジェクト配置ファイル]** を選択して .ispac ファイルのパスを入力します。
    -   SSIS カタログにあるプロジェクトを配置するには、 **[Integration Services カタログ]** を選び、サーバー名とカタログ内のプロジェクトのパスを入力します。
    -   **[次へ]** を選択して、 **[配置先の選択]** ページを表示します。
  
3.  **[配置先の選択]** ページで、プロジェクトの配置先を選びます。
    -   完全修飾サーバー名を `<server_name>.database.windows.net` の形式で入力します。
    -   認証情報を入力し、 **[接続]** を選択します。
    -   次に、 **[参照]** を選択し、SSISDB でターゲット フォルダーを選択します。
    -   **[次へ]** を選択し、 **[レビュー]** ページを開きます。 ( **[次へ]** ボタンは、 **[接続]** を選択した後でないと有効になりません。)
  
4.  **[レビュー]** ページで、選択した設定を確認します。
    -   選択内容を変更するには、 **[戻る]** を選択するか、左ペインで任意の手順を選択します。
    -   **[配置]** をクリックして、配置プロセスを開始します。

    > [!NOTE]
    > "**アクティブなワーカー エージェントがありません。(.Net SqlClient Data Provider)** " というエラー メッセージが表示される場合は、Azure-SSIS Integration Runtime が動いていることを確認してください。 Azure-SSIS IR が停止状態の間に配置しようとすると、このエラーが発生します。

5.  配置プロセスが完了すると、 **[結果]** ページが開きます。 このページでは、各アクションが成功したか、失敗したかを表示します。
    -   アクションが失敗した場合は、 **[結果]** 列の **[失敗]** を選択すると、エラーの説明が表示されます。
    -   必要に応じて、 **[レポートの保存]** を選択して結果を XML ファイルに保存します。
    -   **[閉じる]** を選択してウィザードを終了します。

## <a name="deploy-a-project-with-powershell"></a>PowerShell でプロジェクトを配置する

PowerShell を使って Azure SQL Database の SSISDB にプロジェクトを配置するには、次のスクリプトを要件に適合させます。 スクリプトが `$ProjectFilePath` の下の子フォルダーと各子フォルダー内のプロジェクトを列挙し、次に、SSISDB で同じフォルダーを作成し、それらのフォルダーにプロジェクトを展開します。

このスクリプトには、SQL Server Data Tools バージョン 17.x、またはスクリプトを実行するコンピューターにインストールされている SQL Server Management Studio が必要です。

```powershell
# Variables
$ProjectFilePath = "C:\<folder>"
$SSISDBServerEndpoint = "<servername>.database.windows.net"
$SSISDBServerAdminUserName = "<username>"
$SSISDBServerAdminPassword = "<password>"

# Load the IntegrationServices Assembly
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices") | Out-Null;

# Store the IntegrationServices Assembly namespace to avoid typing it every time
$ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"

Write-Host "Connecting to server ..."

# Create a connection to the server
$sqlConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID="+ $SSISDBServerAdminUserName +";Password="+ $SSISDBServerAdminPassword + ";Initial Catalog=SSISDB"
$sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString

# Create the Integration Services object
$integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection

# Get the catalog
$catalog = $integrationServices.Catalogs['SSISDB']

write-host "Enumerating all folders..."

$folders = ls -Path $ProjectFilePath -Directory

if ($folders.Count -gt 0)
{
    foreach ($filefolder in $folders)
    {
        Write-Host "Creating Folder " $filefolder.Name " ..."

        # Create a new folder
        $folder = New-Object $ISNamespace".CatalogFolder" ($catalog, $filefolder.Name, "Folder description")
        $folder.Create()

        $projects = ls -Path $filefolder.FullName -File -Filter *.ispac
        if ($projects.Count -gt 0)
        {
            foreach($projectfile in $projects)
            {
                $projectfilename = $projectfile.Name.Replace(".ispac", "")
                Write-Host "Deploying " $projectfilename " project ..."

                # Read the project file, and deploy it to the folder
                [byte[]] $projectFileContent = [System.IO.File]::ReadAllBytes($projectfile.FullName)
                $folder.DeployProject($projectfilename, $projectFileContent)
            }
        }
    }
}

Write-Host "All done." 
```

## <a name="run-a-package"></a>パッケージの実行

1. SSMS のオブジェクト エクスプローラーで、実行するパッケージを選択します。

2. 右クリックして **[実行]** を選択し、 **[パッケージの実行]** ダイアログ ボックスを開きます。

3.  **[パッケージの実行]** ダイアログ ボックスで、 **[パラメーター]** タブ、 **[接続マネージャー]** タブ、 **[詳細設定]** タブの設定を使用して、パッケージの実行を構成します。

4.  **[OK]** を選択してパッケージを実行します。

## <a name="monitor-the-running-package-in-ssms"></a>SSMS で実行中のパッケージを監視する

Integration Services サーバー上で現在実行されている Integration Services 操作 (配置、検証、パッケージの実行など) の状態を表示するには、SSMS の **[アクティブな操作]** ダイアログ ボックスを使用します。 **[アクティブな操作]** ダイアログ ボックスを開くには、 **[SSISDB]** を右クリックし、 **[アクティブな操作]** を選択します。

また、オブジェクト エクスプローラーでパッケージを選択し、右クリックして **[レポート]** を選択し、 **[標準レポート]** 、 **[すべての実行]** の順に選択することもできます。

SSMS で実行中のパッケージを監視する方法の詳細については、「[パッケージとその他の操作を実行するモニター](https://docs.microsoft.com/sql/integration-services/performance/monitor-running-packages-and-other-operations)」を参照してください。

## <a name="monitor-the-execute-ssis-package-activity"></a>SSIS パッケージの実行アクティビティを監視する

SSIS パッケージの実行アクティビティを使用して Azure Data Factory パイプラインの一部としてパッケージを実行している場合、Data Factory UI でパイプライン実行を監視できます。 その後、アクティビティ実行の出力から SSISDB 実行 ID を取得し、その ID を使用してさらに包括的な実行ログとエラー メッセージを SSMS で確認できます。

![Data Factory でパッケージ実行 ID を取得する](media/ssis-azure-deploy-run-monitor-tutorial/get-execution-id.png)

## <a name="monitor-the-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime の監視

パッケージが実行されている Azure SSIS 統合ランタイムに関する状態情報を取得するには、次の PowerShell コマンドを使用します。 コマンドごとに、データ ファクトリ、Azure SSIS IR、およびリソース グループの名前を入力します。

詳細については、[Azure SSIS 統合ランタイムの監視](https://docs.microsoft.com/azure/data-factory/monitor-integration-runtime#azure-ssis-integration-runtime)に関するページを参照してください。

### <a name="get-metadata-about-the-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime に関するメタデータを取得する

```powershell
Get-AzDataFactoryV2IntegrationRuntime -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

### <a name="get-the-status-of-the-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime の状態を取得する

```powershell
Get-AzDataFactoryV2IntegrationRuntime -Status -DataFactoryName $DataFactoryName -Name $AzureSsisIRName -ResourceGroupName $ResourceGroupName
```

## <a name="next-steps"></a>次の手順
- パッケージ実行をスケジュールする方法を説明します。 詳細については、「[Azure で SSIS パッケージの実行をスケジュールする](ssis-azure-schedule-packages.md)」を参照してください。
