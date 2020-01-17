---
title: Azure へのマネージド バックアップを使用する "
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.description: Enable SQL Server managed backup to Azure
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 07bb9cf8f0fc697e1d31a80e22a72cd5a0ea484a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257951"
---
# <a name="enable-sql-server-managed-backup-to-azure"></a>Azure への SQL Server マネージド バックアップを有効にする

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、データベース レベルとインスタンス レベルの両方で、既定の設定を使用して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にする方法について説明します。 また、電子メール通知を有効にする方法と、バックアップ処理を監視する方法についても説明します。  
  
 このチュートリアルでは、Azure PowerShell を使用します。 チュートリアルを開始する前に、 [Azure PowerShell をダウンロードしてインストールします](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。  
  
> [!IMPORTANT]  
>  また、高度なオプションを有効にする場合やカスタムのスケジュールを使用する場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にする前にまずその設定を構成します。 詳細については、「[Microsoft Azure への SQL Server マネージド バックアップの詳細設定オプションの構成](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
## <a name="create-the-azure-blob-container"></a>Azure Blob コンテナーを作成する

このプロセスには、Azure アカウントが必要です。 既にアカウントがある場合は、次の手順に進みます。 ない場合は、 [無料評価版](https://azure.microsoft.com/pricing/free-trial/) から始めるか、 [購入オプション](https://azure.microsoft.com/pricing/purchase-options/)を調べることができます。

ストレージ アカウントの詳細については、「 [Azure ストレージ アカウントについて](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」を参照してください。 

#### <a name="azure-clitabazure-cli"></a>[Azure CLI](#tab/azure-cli)

1. Azure アカウントにサインインします。

    ```azurecli-interactive
    az login
    ```
  
1. Azure ストレージ アカウントを作成します。 既にストレージ アカウントがある場合は、次の手順に進みます。 次のコマンドを実行すると、米国東部リージョンに `<backupStorage>` というストレージ アカウントが作成されます。  
  
    ```azurecli-interactive
    az storage account create -n <backupStorage> -l "eastus" --resource-group <resourceGroup>
    ```  
    
1. バックアップ ファイル用に `<backupContainer>` という名前の BLOB コンテナーを作成します。
  
    ```azurecli-interactive
    $keys = az storage account keys list --account-name <backupStorage> --resource-group <resourceGroup> | ConvertFrom-Json
    az storage container create --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value 
    ```  
  
1. コンテナーにアクセスするために Shared Access Signature (SAS) を生成します。 次のコマンドを実行すると、1 年後に期限切れになる SAS トークンが `<backupContainer>` BLOB コンテナーに作成されます。  
  
    ```azurecli-interactive 
    az storage container generate-sas --name <backupContainer> --account-name <backupStorage> --account-key $keys[0].value
    ```

#### <a name="powershelltabazure-powershell"></a>[PowerShell](#tab/azure-powershell)

1. 次のコマンドで Azure アカウントにログ インします。

    ```azurepowershell-interactive
    Connect-AzAccount
    Set-AzContext -SubscriptionId "<subscriptionId>"
    ```
  
1. Azure ストレージ アカウントを作成します。 既にストレージ アカウントがある場合は、次の手順に進みます。 次のコマンドを実行すると、米国東部リージョンに `<backupStorage>` というストレージ アカウントが作成されます。  
  
    ```azurepowershell-interactive
    New-AzStorageAccount -StorageAccountName <backupStorage> -Location "EAST US" -ResourceGroupName <resourceGroup> -SkuName Standard_GRS
    ```   
  
1. バックアップ ファイル用に `<backupContainer>` という名前の BLOB コンテナーを作成します。  
  
    ```azurepowershell-interactive
    $context = New-AzStorageContext -StorageAccountName <backupStorage> -StorageAccountKey (Get-AzStorageAccountKey -Name <backupStorage> -ResourceGroupName <resourceGroup>).Value[0]  
    New-AzStorageContainer -Name <backupContainer> -Context $context  
    ```  
  
1. コンテナーにアクセスするために Shared Access Signature (SAS) を生成します。 次のコマンドを実行すると、1 年後に期限切れになる SAS トークンが `<backupContainer>` BLOB コンテナーに作成されます。
  
    ```azurepowershell-interactive 
    New-AzStorageContainerSASToken -Name <backupContainer> -Permission rwdl -ExpiryTime (Get-Date).AddYears(1) -FullUri -Context $context 
    ```

* * *

> [!NOTE]
> 以上の手順は [Azure portal](https://portal.azure.com/) でも行うことができます。

出力には、コンテナーの URL と SAS トークンの両方または一方が含まれます。 以下に例を示します。  
  
  `https://managedbackupstorage.blob.core.windows.net/backupcontainer?sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl`
  
URL が含まれている場合、疑問符で SAS トークンから区切ります (疑問符は含めないでください)。 たとえば、前の出力結果は、次の 2 つの値になります。  
  
|||  
|-|-|  
|**コンテナー URL**|https://managedbackupstorage.blob.core.windows.net/backupcontainer|  
|**SAS トークン**|sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl|  
|||
  
SQL 資格情報の作成に使用するコンテナーの URL と SAS を記録します。 SAS の詳細については、[Shared Access Signature に関する記事のパート 1 の SAS モデル](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)に関するページを参照してください。  
  
## <a name="enable-managed-backup-to-azure"></a>Azure へのマネージド バックアップを有効にする
  
1.  **SAS URL の SQL 資格情報を作成する**: SAS トークンを使用して、BLOB コンテナーの URL の SQL 資格情報を作成します。 SQL Server Management Studio で、次の Transact-SQL クエリを使用して、次の例に基づいて BLOB コンテナーの資格情報を作成します。  
  
    ```sql  
    CREATE CREDENTIAL [https://managedbackupstorage.blob.core.windows.net/backupcontainer]   
    WITH IDENTITY = 'Shared Access Signature',  
    SECRET = 'sv=2014-02-14&sr=c&sig=xM2LXVo1Erqp7LxQ%9BxqK9QC6%5Qabcd%9LKjHGnnmQWEsDf%5Q%se=2015-05-14T14%3B93%4V20X&sp=rwdl'  
    ```  
  
2.  **SQL Server エージェント サービスが開始され、実行されていることを確認する:** SQL Server エージェントを開始します (現在実行されていない場合)。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] でバックアップ操作を実行するには、SQL Server エージェントがインスタンスで実行されている必要があります。  バックアップ操作を定期的に実行できるように、SQL Server エージェントの自動的な実行を設定できます。  
  
3.  **保有期間を決定する:** バックアップ ファイルに必要な保有期間を決定します。 保有期間は日数で指定し、その範囲は 1 ～ 30 になります。  
  
4.  **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にして構成する:** SQL Server Management Studio を起動し、対象の SQL Server インスタンスに接続します。 要件に合わせて、データベース名、コンテナーの URL、および保有期間の値を変更した後、クエリ ウィンドウから次のステートメントを実行します。  
  
    > [!IMPORTANT]  
    >  インスタンス レベルで管理対象バックアップを有効にするには、`database_name` パラメーターに `NULL` を指定します。  
  
    ```sql  
    USE msdb;  
    GO  
    EXEC msdb.managed_backup.sp_backup_config_basic   
     @enable_backup = 1,   
     @database_name = 'yourdatabasename',  
     @container_url = 'https://managedbackupstorage.blob.core.windows.net/backupcontainer',   
     @retention_days = 30  
    GO  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、指定したデータベースで有効になります。 データベースでのバックアップ操作の実行が開始されるまで最大 15 分かかる場合があります。  
  
5.  **拡張イベントの既定の構成を確認する:** 次の Transact-SQL ステートメントを実行して、拡張イベントの設定を確認します。  
  
    ```sql
    SELECT * FROM msdb.managed_backup.fn_get_current_xevent_settings()  
    ```  
  
     管理、運用、および分析のチャネル イベントは既定で有効になっていて、無効にできないことに注意してください。 手動の介入を必要とするイベントを監視するには、これで十分です。  デバッグ イベントを有効にすることはできますが、デバッグ チャネルには、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] が問題の検出および解決に使用する情報イベントとデバッグ イベントが含まれています。  
  
6.  **正常性状態の通知を有効化し、構成する:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]Microsoft Azure への SQL Server マネージド バックアップには、注意を要するエラーまたは警告の電子メール通知を送信するためにエージェント ジョブを作成するストアド プロシージャがあります。 次の手順では、電子メール通知を有効にして構成するためのプロセスを示します。  
  
    1.  データベース メールがインスタンス上でまだ有効になっていない場合は設定します。 詳細については、「 [Configure Database Mail](../../relational-databases/database-mail/configure-database-mail.md)」を参照してください。  
  
    2.  データベース メールを使用するように SQL Server エージェント通知を構成します。 詳細については、「 [Configure SQL Server Agent Mail to Use Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)」を参照してください。  
  
    3.  **電子メール通知を有効にして、バックアップ エラーおよび警告を受け取る:** クエリ ウィンドウから、次の Transact-SQL ステートメントを実行します。  
  
        ```sql
        EXEC msdb.managed_backup.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
        ```  
  
7.  **Azure Storage アカウントでバックアップ ファイルを表示する:** SQL Server Management Studio または Azure portal からストレージ アカウントに接続します。 指定したコンテナー内のすべてのバックアップが表示されます。 データベースに対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にしてから 5 分以内のデータベースとログ バックアップが表示される場合があります。  
  
8.  **正常性状態を監視する:** 前の手順で構成した電子メール通知から監視するか、ログに記録されているイベントをアクティブに監視することができます。 イベントを表示するための Transact-SQL ステートメントのいくつかの例を示します。  
  
    ```sql  
    --  view all admin events  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    DECLARE @eventresult TABLE  
    (event_type nvarchar(512),  
    event nvarchar (512),  
    timestamp datetime  
    )  
  
    INSERT INTO @eventresult  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
    ```  
  
    ```sql  
    -- to enable debug events  
    USE msdb;  
    GO  
    EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
    ```  
  
    ```sql  
    --  View all events in the current week  
    USE msdb;  
    GO  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC managed_backup.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
    ```
  
このセクションで説明した手順は、データベースで初めて [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を構成するための特別な手順です。 同じシステム ストアド プロシージャを使用して既存の構成を変更し、新しい値を指定することができます。  
  
## <a name="see-also"></a>参照  
 [Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
