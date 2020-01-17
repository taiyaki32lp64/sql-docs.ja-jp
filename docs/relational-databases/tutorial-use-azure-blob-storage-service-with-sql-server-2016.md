---
title: チュートリアル:Azure Blob Storage サービスと SQL Server 2016 データベースの使用
ms.custom: seo-dt-2019
ms.date: 01/10/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aba8d7e3dc7aaf48523303ad6f63682c888b3c46
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095693"
---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>チュートリアル:Azure Blob Storage サービスと SQL Server 2016 データベースの使用

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Microsoft Azure Blob Storage サービスでの SQL Server 2016 の使用に関するチュートリアルへようこそ。 このチュートリアルは、Microsoft Azure Blob Storage サービスを SQL Server データ ファイルや SQL Server バックアップに使用する方法を理解するのに役立ちます。  
  
SQL Server による Microsoft Azure Blob Storage サービスの統合のサポートは、SQL Server 2012 Service Pack 1 CU2 の拡張機能として開始され、SQL Server 2014 および SQL Server 2016 でさらに強化されました。 この機能の概要と使用した場合の利点については、「[Microsoft Azure 内の SQL Server データ ファイル](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)」をご覧ください。 ライブ デモについては、 [特定の時点での復元に関するデモ](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)を参照してください。  

このチュートリアルでは、複数のセクションに分けて、Microsoft Azure Blob Storage サービス上で SQL Server データ ファイルを使用する方法を説明します。 各セクションでは特定のタスクに重点を置いており、セクションは順番に完了する必要があります。 まず、格納済みアクセス ポリシーと Shared Access Signature で Blob ストレージに新しいコンテナーを作成する方法を学習します。 次に、SQL Server を Azure Blob Storage と統合するための SQL Server 資格情報を作成する方法を学習します。 さらに、Blob ストレージにデータベースをバックアップし、Azure の仮想マシンに復元します。 SQL Server 2016 のファイル スナップショットのトランザクション ログ バックアップを使用して、特定の時点、または新しいデータベースに復元することができます。 最後に、このチュートリアルでは、ファイル スナップショットのバックアップについて理解し、使用できるようにするために、メタ データ システムのストアド プロシージャと関数の使用方法を紹介します。
  
## <a name="prerequisites"></a>Prerequisites

このチュートリアルを完了するには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバックアップと復元の概念と T-SQL 構文についての知識が必要です。 このチュートリアルを使用するには、Azure ストレージ アカウント、SQL Server Management Studio (SSMS)、オンプレミスの SQL Server のインスタンスへのアクセス、SQL Server 2016 を実行している Azure 仮想マシン (VM) へのアクセス、および AdventureWorks2016 データベースが必要です。 また、BACKUP コマンドと RESTORE コマンドの実行に使用するアカウントは、**alter any credential** 権限を持つ **db_backup operator** データベース ロールに属している必要があります。 

- 無料の [Azure アカウント](https://azure.microsoft.com/offers/ms-azr-0044p/)を取得する。
- [Azure ストレージ アカウント](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)を作成する。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールする。
- [SQL Server を実行している Azure VM](https://azure.microsoft.com/documentation/articles/virtual-machines-provision-sql-server/) をプロビジョニングする
- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールする。
- [AdventureWorks2016 サンプル データベース](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)をダウンロードする。
- ユーザー アカウントを [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) のロールに割り当て、[alter any credential](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql) 権限を付与する。 

## <a name="1---create-stored-access-policy-and-shared-access-storage"></a>1 - 格納済みアクセス ポリシーと共有アクセス ストレージを作成する

このセクションでは [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) スクリプトを使用して、Azure BLOB コンテナーに格納済みアクセス ポリシーを使用した Shared Access Signature を作成します。  
  
> [!NOTE]  
> このスクリプトは、Azure PowerShell 5.0.10586 を使用して作成されています。  
  
Shared Access Signature とは、コンテナー、BLOB、キュー、またはテーブルに対する制限付きアクセス権を付与する URI です。 格納済みアクセス ポリシーによって、取り消し、期限切れ、アクセス権の拡張などのサーバー側の Shared Access Signatures のコントロールのレベルが追加されます。 この新しい機能強化を使用する場合は、少なくとも読み取り、書き込み、一覧表示の権限のあるコンテナーに対してポリシーを作成する必要があります。  
  
格納済みアクセス ポリシーと Shared Access Signature を作成するには、Azure PowerShell、Azure Storage SDK、Azure REST API、またはサードパーティのユーティリティを使用します。 このチュートリアルでは、Azure PowerShell スクリプトを使用して、このタスクを実行する方法について説明します。 スクリプトは、Resource Manager デプロイ モデル ルを使用して、次の新しいリソースを作成します  
  
-   リソース グループ   
-   [ストレージ アカウント]  
-   Azure BLOB コンテナー   
-   SAS ポリシー    

このスクリプトでは、まず前述のリソースの名前と次の必要な入力値の名前を指定するための多くの変数を宣言します。  
  
-   その他のリソース オブジェクトの名前付けで使用されるプレフィックス名    
-   サブスクリプション名    
-   データ センターの場所  

  
このスクリプトでは、最後に「[2 - Shared Access Signature を使用して SQL Server 資格情報を作成する](#2---create-a-sql-server-credential-using-a-shared-access-signature)」で使用する適切な CREATE CREDENTIAL ステートメントを生成します。 このステートメントは、自動的にクリップボードにコピーされ、コンソールに出力されるので、確認できます。  
  
コンテナーのポリシーを作成し、Shared Access Signature (SAS) キーを生成するには、次の手順に従います。  
  
1.  Window PowerShell または Windows PowerShell ISE (前述のバージョン要件を参照してください) を開きます。  
  
2.  以下のスクリプトを編集してから、実行します。  
  
    ```powershell
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionID = '<your subscription ID>'   # the ID  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy 

    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # Add an authenticated Azure account for use in the session   
    Connect-AzAccount    
  
    # Set the tenant, subscription and environment for use in the rest of   
    Set-AzContext -SubscriptionId $subscriptionID   
  
    # Create a new resource group - comment out this line to use an existing resource group  
    New-AzResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new Azure Resource Manager storage account - comment out this line to use an existing Azure Resource Manager storage account  
    New-AzStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the Azure Resource Manager storage account  
    $accountKeys = Get-AzStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an Azure Resource Manager storage account  
    $storageContext = New-AzStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value

    # Creates a new container in blob storage  
    $container = New-AzStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  

    # Sets the variables for the new container you just created
    $container = Get-AzStorageContainer -Context $storageContext -Name $containerName
    $cbc = $container.CloudBlobContainer 
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql 

    # Once you're done with the tutorial, remove the resource group to clean up the resources. 
    # Remove-AzResourceGroup -Name $resourceGroupName  
    ```  

3.  スクリプトが完了すると、CREATE CREDENTIAL ステートメントがクリップボード上にあるため、次のセクションで使用できます。  


## <a name="2---create-a-sql-server-credential-using-a-shared-access-signature"></a>2 - Shared Access Signature を使用して SQL Server 資格情報を作成する

このセクションでは、前の手順で作成した Azure コンテナーに対して読み書きを行うために SQL Server で使用するセキュリティ情報を格納するための資格情報を作成します。  
  
SQL Server 資格情報は、SQL Server の外部にあるリソースへの接続に必要な認証情報を保存するために使用されるオブジェクトです。 資格情報には、ストレージ コンテナーの URI パスと、このコンテナーの Shared Access Signature が格納されます。  

SQL Server 資格情報を作成するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。  
2.  新しいクエリ ウィンドウを開き、オンプレミスの環境内にあるデータベース エンジンの SQL Server インスタンスに接続します。  
  
3.  新しいクエリ ウィンドウで、セクション 1 で取得した Shared Access Signature を指定した CREATE CREDENTIAL ステートメントを貼り付けて、そのスクリプトを実行します。  
  
    スクリプトは、次のコードのようになります。  
  
    ```sql   
    /* Example:
    USE master  
    CREATE CREDENTIAL [https://msfttutorial.blob.core.windows.net/containername] 
    WITH IDENTITY='SHARED ACCESS SIGNATURE'   
    , SECRET = 'sharedaccesssignature' 
    GO */
    
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] 
      -- this name must match the container path, start with https and must not contain a forward slash at the end
    WITH IDENTITY='SHARED ACCESS SIGNATURE' 
      -- this is a mandatory string and should not be changed   
     , SECRET = 'sharedaccesssignature' 
       -- this is the shared access signature key that you obtained in section 1.   
    GO    
    ```  
  
4.  使用可能なすべての資格情報を表示するには、インスタンスに接続されたクエリ ウィンドウで次のステートメントを実行できます。  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
5.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server インスタンスに接続します。  
  
6.  新しいクエリ ウィンドウで、セクション 1 で取得した Shared Access Signature を指定した CREATE CREDENTIAL ステートメントを貼り付けて、そのスクリプトを実行します。  
  
7.  Azure コンテナーにアクセスするようにしたい SQL Server インスタンスが他にもある場合は、手順 5. と手順 6. を繰り返します。  

## <a name="3---database-backup-to-url"></a>3 - URL にデータベースをバックアップする

このセクションでは、オンプレミスの SQL Server 2016 インスタンス内の AdventureWorks2016 データベースを、[セクション 1](#1---create-stored-access-policy-and-shared-access-storage) で作成した Azure コンテナーにバックアップします。
  
> [!NOTE]  
> この Azure コンテナーに SQL Server 2012 SP1 CU2 以降のデータベースまたは SQL Server 2014 データベースをバックアップする場合、 [こちら](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url?view=sql-server-2014) に記載されている非推奨の構文を使用すれば、WITH CREDENTIAL 構文で URL へのバックアップを行うことができます。  
  
BLOB ストレージにデータベースをバックアップするには、次の手順に従います。  
  
1.  SQL Server Management Studio に接続します。  
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。  
3.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて適宜 URL を変更し、次のスクリプトを実行します。  
  
    ```sql  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2016  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2016 database to the container that you created in section 1  
    BACKUP DATABASE AdventureWorks2016   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_onprem.bak'  
  
    ```  
  
4.  オブジェクト エクスプローラーを開き、ストレージ アカウントとアカウント キーを使用して Azure ストレージに接続します。 
    1.  [Containers] を展開します。セクション 1 で作成されたコンテナーを展開し、前述の手順 3 で作成されたバックアップがこのコンテナー内に表示されているかどうかを確認します。  
  
   ![Azure ストレージ アカウントに接続する](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/connect-to-azure-storage.png)


## <a name="4----restore-database-to-virtual-machine-from-url"></a>4 - URL から仮想マシンにデータベースを復元する

このセクションでは、Azure 仮想マシン内の SQL Server 2016 インスタンスに AdventureWorks2016 データベースを復元します。
  
> [!NOTE]  
> このチュートリアルではわかりやすくするために、データ ファイルおよびログ ファイル用のコンテナーとして、データベースのバックアップの場合と同じものを使用します。 運用環境では、多くの場合、複数のコンテナーを使用し、データ ファイルも複数を頻繁に使用することになります。 SQL Server 2016 では、大規模なデータベースをバックアップする場合にそのパフォーマンスを向上させるために、バックアップを複数の BLOB でストライプ化することも検討可能です。  
  
Azure Blob Storage から Azure 仮想マシン内の SQL Server 2016 インスタンスに AdventureWorks2016 データベースを復元するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。   
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。   
3.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて適宜 URL を変更し、次のスクリプトを実行します。  
  
    ```sql  
    -- Restore AdventureWorks2016 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2016_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Data.mdf'  
         ,MOVE 'AdventureWorks2016_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  オブジェクト エクスプローラーを開き、Azure SQL Server 2016 インスタンスに接続します。   
5.  オブジェクト エクスプローラーで、[データベース] ノードを展開し、AdventureWorks2016 データベースが復元されていることを確認します (必要に応じてノードを更新する)    
    1. AdventureWorks2016 を右クリックし、[プロパティ] を選択します。
    1. [ファイル] を選択して、2 つのデータベース ファイルのパスが、Azure ブログ コンテナー内の BLOB を指す URL であることを確認します (完了したら [キャンセル] を選択します)。
    
     ![Azure VM 上の AdventureWorks db](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/adventureworks-on-azure-vm.png)

    
8.  オブジェクト エクスプローラーで、Azure Storage に接続します。
    1. [Containers] を展開します。セクション 1 で作成したコンテナーを展開して、このコンテナーの中に、上記の手順 3. で作成した AdventureWorks2016_Data.mdf と AdventureWorks2016_Log.ldf が、セクション 3 で作成したバックアップ ファイルと一緒に表示されていることを確認します (必要に応じてノードを更新する)。  
  
   ![Azure 上のコンテナー内のデータ ファイル](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/data-files-in-container.png)

## <a name="5---backup-database-using-file-snapshot-backup"></a>5 - ファイル スナップショット バックアップを使用してデータベースをバックアップする

このセクションでは、Azure のスナップショットを使用して、ファイル スナップショット バックアップによって AdventureWorks2016 データベースを Azure 仮想マシンにバックアップし、ほぼ瞬時にバックアップを行います。 ファイル スナップショット バックアップの詳細については、「 [Azure でのデータベース ファイルのスナップショット バックアップ](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
ファイル スナップショット バックアップを使用して AdventureWorks2016 データベースをバックアップするには、次の手順に従います。  
  
1.  SQL Server Management Studio に接続します。   
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。  
3.  次の Transact-SQL スクリプトをコピーして、クエリ ウィンドウに貼り付け、実行します (このクエリ ウィンドウは閉じないでください。このスクリプトは、手順 5. でもう一度実行します)。 このシステム ストアド プロシージャでは、指定したデータベースを構成する既存のファイル スナップショット バックアップの各ファイルを確認できます。 このデータベースのファイル スナップショット バックアップはありません。  
  
    ```sql  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
    ```  
  
4.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて適宜 URL を変更し、次のスクリプトを実行します。 非常に早くバックアップされます。  
  
    ```sql  
    -- Backup the AdventureWorks2016 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2016   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Azure.bak'   
       WITH FILE_SNAPSHOT;    
    ```  
  
5.  手順 4 のスクリプトが正常に実行されたことを確認した後、次のスクリプトを再度実行します。 手順 4 のファイル スナップショット バックアップ操作で、データとログ ファイルの両方のファイル スナップショットが生成されました。  
  
    ```sql  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
  
    ```  
  
    ![スナップショットを示す fn_db_backup_file_snapshots の結果](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/results-showing-snapshot.png) 
  
6.  Azure 仮想マシンの SQL Server 2016 インスタンスのオブジェクト エクスプローラーで、[データベース] ノードを展開し、AdventureWorks2016 データベースがこのインスタンスに復元されたことを確認します (必要に応じてノードを更新する)。  
7.  オブジェクト エクスプローラーで、Azure Storage に接続します。   
8.  [Containers] を展開します。セクション 1 で作成したコンテナーを展開して、上記の手順 4 で作成した AdventureWorks2016_Azure.bak が、セクション 3 で作成したバックアップ ファイルおよびセクション 4 で作成したデータベース ファイルと一緒にこのコンテナーの中に表示されていることを確認します (必要に応じてノードを更新する)。  
  
    ![Azure へのスナップショット バックアップ](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/snapshot-backup-on-azure.PNG)

## <a name="6----generate-activity-and-backup-log-using-file-snapshot-backup"></a>6 - アクティビティを生成し、ファイル スナップショット バックアップを使用してログをバックアップする

このセクションでは、AdventureWorks2016 データベースにアクティビティを生成し、ファイル スナップショット バックアップを使用してトランザクション ログ バックアップを定期的に作成します。 ファイル スナップショット バックアップの使用の詳細については、 [「Azure でのデータベース ファイルのスナップショット バックアップ」](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)を参照してください。  
  
AdventureWorks2016 データベースにアクティビティを生成し、ファイル スナップショット バックアップを使用してトランザクション ログ バックアップを定期的に作成するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。   
2.  新しい 2 つのクエリ ウィンドウを開き、それぞれのクエリ ウィンドウを、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。   
3.  次の Transact-SQL スクリプトをコピーし、いずれかのクエリ ウィンドウに貼り付けて、実行します。 手順 4. で新しい行を追加する前に、Production.Location テーブルには 14 の行があります。  
  
    ```sql 
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2016.Production.Location;    
    ```  
  
4.  次の 2 つの Transact-SQL スクリプトをコピーして 2 つの個別のクエリ ウィンドウに貼り付けます。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて適宜 URL を変更し、個別のクエリ ウィンドウ内でこれらのスクリプトを同時に実行します。 これらのスクリプトは、完了まで約 7 分かかります。  
  
    ```sql  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2016.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;    
    ```  
  
    ```sql  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2016.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2016 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  1 番目のスクリプトの出力を確認します。最終的な行カウントは 29,939 になっています。  
  
    ![29,939 の行数が表示される](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/29-thousand-rows.png)
  
6.  2 番目のスクリプトの出力を確認します。BACKUP LOG ステートメントが実行されるたびに 2 つの新しいファイル スナップショットが作成されています。ログ ファイルのファイル スナップショットが 1 つと、データ ファイルのファイル スナップショットが 1 つです (データベース ファイルごとに、合計 2 つのファイル スナップショット)。 2 番目のスクリプトが完了すると、ファイル スナップショットは合計で 16 個になっています。データベース ファイルごとに 8 個です (BACKUP DATABASE ステートメントで 1 つ、BACKUP LOG ステートメントの実行のたびに 1 つ)。  
  
   ![バックアップ スナップショットの結果](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/snapshot-back-results.png)
  
7.  オブジェクト エクスプローラーで、Azure Storage に接続します。  
  
8.  [Containers] を展開します。セクション 1 で作成したコンテナーを展開し、新しいバックアップ ファイルが 7 つと、前のセクションで生成されたデータ ファイルが表示されていることを確認します (必要に応じてノードを更新)。  
  
    ![Azure コンテナー内の複数のスナップショット](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/tutorial-snapshots-in-container.png)

## <a name="7---restore-a-database-to-a-point-in-time"></a>7 - 特定の時点にデータベースを復元する

このセクションでは、2 つのトランザクション ログ バックアップ間の特定の時点に AdventureWorks2016 データベースを復元します。  
  
従来のバックアップの場合、ポイント イン タイム リストアを実行するには、復元する時点までの、およびその直後の完全なデータベース バックアップ (場合によっては差分バックアップ) とすべてのトランザクション ログ ファイルを使用する必要がありました。 ファイルスナップショット バックアップの場合、復元先の時点を枠内に入れたゴール ポストを設定する 2 つの隣接するログ バックアップ ファイルを必要とするだけです。 各ログ バックアップによって各データベース ファイルのファイル スナップショット (各データ ファイルとログ ファイル) が作成されるので、ログ ファイル スナップショット バックアップ セットが 2 つ必要なだけです。  
  
ファイル スナップショット バックアップ セットから、指定した時点にデータベースを復元するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。  
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。   
3.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けて実行します。 Production.Location テーブルの行数が 29,939 行であることを確認してから、手順 5 で示すこれより行数が少なかった特定の時点にこのテーブルを復元します。  
  
    ```sql
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2016.Production.Location   
    ```  
  
    ![29,939 の行数が表示される](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/29-thousand-rows.png) 
  
4.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 2 つの隣接するログ バックアップ ファイルを選択し、そのファイル名を、次のスクリプトで必要となる日付と時刻に変換します。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて URL を適切に変更し、1 番目と 2 番目のバックアップ ファイルの名前を指定し、STOPAT 時間を "June 26, 2018 01:48 PM" の形式で指定し、このスクリプトを実行します。 このスクリプトは完了するまで数分かかります  
  
    ```sql  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2016 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2018 01:48 PM';  
    ALTER DATABASE AdventureWorks2016 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2016.Production.Location ;
    ```  
  
5.  出力を確認します。 復元後、行数は 18,389 行になっています。この値は、ログ バックアップ 5 の行数 ～ ログ バックアップ 6 の行数の範囲内の値です (行数は変動します)。  
  
    ![18-thousand-rows.JPG](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/18-thousand-rows.png)

## <a name="8----restore-as-new-database-from-log-backup"></a>8 - ログ バックアップから新しいデータベースとして復元する

このセクションでは、ファイル スナップショットのトランザクション ログ バックアップから、新しいデータベースとして AdventureWorks2016 データベースを復元します。  
  
このシナリオでは、ビジネス分析やレポートのために、別の仮想マシン上の SQL Server インスタンスに復元を実行します。 別の仮想マシン上の別のインスタンスに復元することによって、この目的に合わせてサイズ調整された専用の仮想マシンにワークロードをオフロードし、トランザクション システムからリソース要件を削除することができます。  
  
ファイル スナップショット バックアップを使用したトランザクション ログ バックアップからの復元は非常に高速で、従来のストリーミング バックアップよりも大幅に高速です。 従来のストリーミング バックアップでは、データベースの完全バックアップ、必要に応じて差分バックアップ、一部またはすべてのトランザクション ログ バックアップ (または新しいデータベースの完全バックアップ) を使用する必要があります。 一方、スナップショット ファイルのログ バックアップでは、最新のログ バックアップ (2 つのログ バックアップ時点間の特定の時点に復元する場合は、もう 1 つのログ バックアップまたは 2 つの隣接するログ バックアップ) のみが必要です。 簡単に言うと、各ファイルスナップショットのログ バックアップによって各データベース ファイルのファイル スナップショット (各データ ファイルとログ ファイル) が作成されるので、ログ ファイル スナップショット バックアップ セットが 1 つだけ必要です。  
  
ファイル スナップショット バックアップを使用して、トランザクション ログ バックアップから新しいデータベースにデータベースを復元するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。   
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシン内にあるデータベース エンジンの SQL Server 2016 インスタンスに接続します。  
  
    > [!NOTE]  
    > 前のセクションで使用していたものとは別の Azure 仮想マシンを使用する場合は、「[2 - Shared Access Signature を使用して SQL Server 資格情報を作成する](#2---create-a-sql-server-credential-using-a-shared-access-signature)」の手順に従っていることを確認します。 別のコンテナーに復元する場合は、新しいコンテナーについて「[1 - 格納済みアクセス ポリシーと共有アクセス ストレージを作成する](#1---create-stored-access-policy-and-shared-access-storage)」の手順に従います。  
  
3.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 使用するログ バックアップ ファイルを選択します。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて適宜 URL を変更し、ログ バックアップ ファイルの名前を指定して、このスクリプトを実行します。  
  
    ```sql  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2016_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2016_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2016_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE   
    ```  
  
4.  出力を調べて復元が正常に行われたことを確認します。   
5.  オブジェクト エクスプローラーで、Azure ストレージに接続します。    
6.  [Containers] を展開します。セクション 1 で作成したコンテナーを展開し (必要に応じて表示を更新して)、コンテナー内に新しいデータ ファイルとログ ファイルが、前のセクションで生成された BLOB と共に表示されていることを確認します。  
  
    ![新しいデータベースのデータとログ ファイルを表示している Azure コンテナー](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/new-db-in-azure-container.png)

## <a name="9---manage-backup-sets-and-file-snapshot-backups"></a>9 - バックアップ セットとファイル スナップショット バックアップを管理する

このセクションでは、[sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) システム ストアド プロシージャを使用してバックアップ セットを削除します。 このシステム ストアド プロシージャは、このバックアップ セットに関連付けられている各データベース ファイルのバックアップ ファイルおよびスナップショット ファイルを削除します。  
  
> [!NOTE]  
> 単にバックアップ ファイルを Azure BLOB コンテナーから削除することでバックアップ セットを削除しようとした場合は、バックアップ ファイル自体が削除されるだけで、関連付けられているスナップショット ファイルは残ってしまいます。 そのような状況になった場合は、 [sys.fn_db_backup_file_snapshots (Transact-SQL)](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) システム関数を使用して孤立したファイル スナップショットの URL を特定し、 [sp_delete_backup_file_snapshot (Transact-SQL)](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) システム ストアド プロシージャを使用して孤立した各ファイル スナップショットを削除します。 詳細については、「  [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。  
  
ファイル スナップショット バックアップ セットを削除するには、次の手順のようにします。  
  
1.  SQL Server Management Studio に接続します。  
2.  新しいクエリ ウィンドウを開き、Azure 仮想マシンのデータベース エンジンの SQL Server 2016 インスタンス (または、このコンテナーでの読み取りおよび書き込みアクセス許可を持つ任意の SQL Server 2016 インスタンス) に接続します。   
3.  次の Transact-SQL スクリプトをコピーしてクエリ ウィンドウに貼り付けます。 関連付けられているファイル スナップショットと共に削除するログ バックアップを選択します。 セクション 1 で指定したコンテナーとストレージ アカウント名に合わせて適宜 URL を変更し、ログ バックアップ ファイルの名前を指定して、このスクリプトを実行します。  
  
  ```sql
  sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-21764-20181003205236.bak';  
  ```  
  
4.  オブジェクト エクスプローラーで、Azure Storage に接続します。  
5.  [Containers] を展開します。セクション 1 で作成したコンテナーを展開し、手順 3 で使用したバックアップ ファイルがこのコンテナーに表示されなくなっていることを確認します (必要に応じてノードを更新する)。  
  
    ![ログ バックアップ BLOB の削除を示している Azure コンテナー](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/deleted-backup-snapshot.png)
  
6.  次の Transact-SQL スクリプトをコピーし、クエリ ウィンドウに貼り付け、実行して、2 つのファイル スナップショットが削除されたことを確認します。  
  
    ```sql  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016');   
    ```  
    ![2 つのファイル スナップショットが削除されたことを示す詳細ウィンドウ](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/results-of-two-deleted-snapshot-files.png)

## <a name="10---remove-resources"></a>10 - リソースの削除

このチュートリアルを完了したら、リソースを節約するために、このチュートリアルで作成したリソース グループを削除してください。 

リソース グループを削除するには、次の powershell コードを実行します。

  ```powershell
  # Define global variables for the script  
  $prefixName = '<prefix name>'  # should be the same as the beginning of the tutorial
  
  # Set a variable for the name of the resource group you will create or use  
  $resourceGroupName=$prefixName + 'rg'   
  
  # Adds an authenticated Azure account for use in the session   
  Connect-AzAccount    
  
  # Set the tenant, subscription and environment for use in the rest of   
  Set-AzContext -SubscriptionId $subscriptionID    
    
  # Remove the resource group
  Remove-AzResourceGroup -Name $resourceGroupName   
  ```


  
## <a name="see-also"></a>参照

[Microsoft Azure 内の SQL Server データ ファイル](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Azure でのデータベース ファイルのファイル スナップショット バックアップ](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[SQL Server Backup to URL](../relational-databases/backup-restore/sql-server-backup-to-url.md) 
[Shared Access Signature, 第 1 部: SAS モデルについて](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[コンテナーの作成](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[コンテナー ACL の設定](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[コンテナー ACL の取得](https://msdn.microsoft.com/library/azure/dd179469.aspx)
[資格情報 &#40;データベース エンジン&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
[sp_delete_backup (Transact-SQL)](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots (Transact-SQL)](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) [Azure でのデータベース ファイルのスナップショット バックアップ](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
