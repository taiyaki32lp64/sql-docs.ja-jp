---
title: Backup to URL に関するベスト プラクティスとトラブルシューティング
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: de676bea-cec7-479d-891a-39ac8b85664f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 149c351796af7741c4bd3ef512fe27ebcbdcf35a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245440"
---
# <a name="sql-server-backup-to-url-best-practices-and-troubleshooting"></a>SQL Server Backup to URL に関するベスト プラクティスとトラブルシューティング

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  このトピックでは、Azure Blob service との間の SQL Server のバックアップと復元に関するベスト プラクティスとトラブルシューティングのヒントを示します。  
  
 SQL Server のバックアップ操作または復元操作に Azure Blob Storage サービスを使用する方法の詳細については、次のトピックを参照してください。  
  
-   [Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
-   [チュートリアル:Azure Blob Storage サービスへの SQL Server のバックアップと復元](../../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="managing-backups-mb1"></a> バックアップの管理  
 バックアップを管理するための一般的な推奨事項を次に示します。  
  
-   BLOB を誤って上書きしないように、各バックアップに一意なファイル名を付けることをお勧めします。  
  
-   コンテナーを作成する際は、アクセス レベルを **private**に設定し、必要な認証情報を指定できるユーザーまたはアカウントだけがコンテナー内の BLOB の読み取りや書き込みを実行できるようにすることをお勧めします。  
  
-   Azure 仮想マシンで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの場合、仮想マシンと同じリージョンのストレージ アカウントを使用して、リージョン間のデータ転送のコストがかからないようにします。 また、同じ地域を使用すると、バックアップ操作と復元操作で最適なパフォーマンスを得ることができます。  
  
-   バックアップ処理に失敗すると、無効なバックアップ ファイルが生成されます。 失敗したバックアップを定期的に確認し、BLOB ファイルを削除することをお勧めします。 詳細については、「 [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)」をご覧ください。  
  
-   バックアップ中に `WITH COMPRESSION` オプションを使用すると、ストレージ コストとストレージのトランザクション コストを最小限に抑えることができます。 また、バックアップ プロセスが完了するまでにかかる時間を短縮することもできます。  

- 「[SQL Server Backup to URL](./sql-server-backup-to-url.md)」で推奨されているように、`MAXTRANSFERSIZE` と `BLOCKSIZE` の引数を設定します。
  
## <a name="handling-large-files"></a>大きなファイルの処理  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバックアップ操作では、複数のスレッドを使用して、Azure Blob Storage サービスへのデータ転送が最適化されます。  ただし、パフォーマンスは ISV の帯域幅やデータベースのサイズなどのさまざまな要因によって異なります。 内部設置型の SQL Server データベースから大きなデータベースまたはファイル グループをバックアップする場合は、最初にスループットのテストを行うことをお勧めします。 [SLA for Storage](https://azure.microsoft.com/support/legal/sla/storage/v1_0/) には BLOB の最大処理時間が示されているため、考慮に入れておくことができます。  
  
-   「[バックアップの管理](#managing-backups-mb1)」セクションで推奨されているように `WITH COMPRESSION` オプションを使用することは、大きなファイルをバックアップするときに非常に重要です。  
  
## <a name="troubleshooting-backup-to-or-restore-from-url"></a>BACKUP TO URL または RESTORE FROM URL のトラブルシューティング  
 ここでは、Azure Blob Storage サービスへのバックアップまたは Azure Blob Storage サービスからの復元を実行するときに発生するエラーを簡単にトラブルシューティングする方法をいくつか示します。  
  
 サポートされないオプションまたは制限事項によるエラーを回避するには、「 [Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 」の記事で、制限事項の一覧および BACKUP コマンドと RESTORE コマンドのサポート情報を確認してください。  
  
 **認証エラー:**  
  
-   `WITH CREDENTIAL` は新しいオプションで、Azure Blob Storage サービスへのバックアップまたは Azure Blob Storage サービスからの復元に必要です。 資格情報に関連するエラーには、次のようなものがあります。  
  
     **BACKUP** コマンドまたは **RESTORE** コマンドで指定された資格情報が存在しません。 この問題を回避するには、資格情報が BACKUP ステートメントに存在しない場合に資格情報を作成する T-SQL ステートメントを含めることができます。 使用可能な例を次に示します。  
  
    ```sql  
    IF NOT EXISTS  
    (SELECT * FROM sys.credentials   
    WHERE credential_identity = 'mycredential')  
    CREATE CREDENTIAL <credential name> WITH IDENTITY = 'mystorageaccount'  
    ,SECRET = '<storage access key> ;  
    ```  
  
-   資格情報は存在しますが、BACKUP コマンドの実行に使用されるログイン アカウントに資格情報へのアクセス権限がありません。 **Alter any credential** 権限がある ***db_backupoperator*** ロールのログイン アカウントを使用してください。  
  
-   ストレージ アカウントの名前とキーの値を確認してください。 資格情報に格納されている情報は、バックアップ操作と復元操作で使用する Azure ストレージ アカウントのプロパティの値と一致する必要があります。  
  
 **バックアップ エラー/障害:**  
  
-   同じ BLOB への並列バックアップを実行すると、バックアップの 1 つが " **初期化に失敗しました** " エラーで失敗します。  
  
-   ページ BLOB (`BACKUP... TO URL... WITH CREDENTIAL` など) を使用している場合は、次のエラー ログを使用して、バックアップ エラーのトラブルシューティングに役立ててください。  
  
    -   トレース フラグ 3051 を設定して、次の形式の特定のエラー ログへの記録を有効にします。  
  
        `BackupToUrl-\<instname>-\<dbname>-action-\<PID>.log` ここで `\<action>` は、次のいずれかです。  
  
        -   **DB (DB)**  
        -   **FILELISTONLY**  
        -   **LABELONLY**  
        -   **HEADERONLY**  
        -   **VERIFYONLY**  
  
    -   Windows イベント ログ (`SQLBackupToUrl` という名前のアプリケーション ログ) を確認することで情報を見つけることもできます。  

    -   大規模なデータベースをバックアップする場合には、COMPRESSION、MAXTRANSFERSIZE、BLOCKSIZE、および複数の URL 引数を検討してください。  「[Backing up a VLDB to Azure Blob Storage](https://blogs.msdn.microsoft.com/sqlcat/2017/03/10/backing-up-a-vldb-to-azure-blob-storage/)」(VLDB を Azure Blob Storage にバックアップする) を参照してください
  
        ```console
        Msg 3202, Level 16, State 1, Line 1
        Write on "https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak" failed: 1117(The request could not be performed because of an I/O device error.)
        Msg 3013, Level 16, State 1, Line 1
        BACKUP DATABASE is terminating abnormally.
        ```

        ```sql  
        BACKUP DATABASE TestDb
        TO URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_1.bak',
        URL = 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_2.bak'
        WITH COMPRESSION, MAXTRANSFERSIZE = 4194304, BLOCKSIZE = 65536;  
        ```  

-   圧縮されたバックアップから復元するときに、次のエラーが表示される場合があります。  
  
    -   `SqlException 3284 occurred. Severity: 16 State: 5  
        Message Filemark on device 'https://mystorage.blob.core.windows.net/mycontainer/TestDbBackupSetNumber2_0.bak' is not aligned.           Reissue the Restore statement with the same block size used to create the backupset: '65536' looks like a possible value.`  
  
        このエラーを解決するには、**BLOCKSIZE = 65536** を指定した **RESTORE** ステートメントを再実行してください。  
  
-   アクティブなリースを保持している BLOB が原因でバックアップ中に発生するエラー:バックアップ処理に失敗すると、アクティブなリースを保持する BLOB が生成されます。  
  
     BACKUP ステートメントが再実行されると、バックアップ操作が次のようなエラーで失敗することがあります。  
  
     `Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (412) There is currently a lease on the blob and no lease ID was specified in the request.`  
  
     アクティブなリースを保持しているバックアップ BLOB ファイルに対して RESTORE ステートメントが実行されると、復元操作は次のようなエラーで失敗します。  
  
     `Exception Message: The remote server returned an error: (409) Conflict..`  
  
     このようなエラーが発生した場合は、BLOB ファイルを削除する必要があります。 このシナリオの詳細とこの問題の解決方法については、「 [Deleting Backup Blob Files with Active Leases](../../relational-databases/backup-restore/deleting-backup-blob-files-with-active-leases.md)」を参照してください。  
  
## <a name="proxy-errors"></a>プロキシ エラー  
 インターネットへのアクセスにプロキシ サーバーを使用している場合、以下の問題が発生することがあります。  
  
 **プロキシ サーバーによる接続数の設定:**  
  
 プロキシ サーバーで、1 分あたりの接続数を制限する設定が使用されている場合があります。 Backup to URL プロセスはマルチスレッド プロセスであるため、この制限を超える可能性があります。 制限を超えた場合、プロキシ サーバーは接続を切断します。 この問題を解決するには、プロキシ設定を変更し、SQL Server がプロキシを使用しないようにします。 エラー ログに表示される可能性のある種類またはエラー メッセージの例を次に示します。  
  
```console
Write on "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak" failed: Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
```console
A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Error could not be gathered from Remote Endpoint.  
  
Msg 3013, Level 16, State 1, Line 2  
  
BACKUP DATABASE is terminating abnormally.  
```

```console
BackupIoRequest::ReportIoError: write failure on backup device https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak'. Operating system error Backup to URL received an exception from the remote endpoint. Exception Message: Unable to read data from the transport connection: The connection was closed.
```  
  
トレース フラグ 3051 を使用して詳細ログを有効にすると、ログに次のメッセージが表示される場合もあります。  
  
`HTTP status code 502, HTTP Status Message Proxy Error (The number of HTTP requests per minute exceeded the configured limit. Contact your ISA Server administrator.)` 
  
 **選択されていない既定のプロキシ設定:**  
  
場合によっては、既定の設定が選択されず、次のようなプロキシ認証エラーが発生します。
 
 `A nonrecoverable I/O error occurred on file "https://storageaccount.blob.core.windows.net/container/BackupAzurefile.bak:" Backup to URL received an exception from the remote endpoint. Exception Message: The remote server returned an error: (407)* **Proxy Authentication Required.`  
  
この問題を解決するには、次の手順に従って、Backup to URL プロセスで既定のプロキシ設定を使用できるようにするための構成ファイルを作成します。  
  
1.  次の xml コンテンツを使用して、`BackuptoURL.exe.config` という名前の構成ファイルを作成します。  
  
    ```xml  
    <?xml version ="1.0"?>  
    <configuration>   
                    <system.net>   
                                    <defaultProxy enabled="true" useDefaultCredentials="true">   
                                                    <proxy usesystemdefault="true" />   
                                    </defaultProxy>   
                    </system.net>  
    </configuration>  
    ```  
  
2.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの Binn フォルダーに構成ファイルを配置します。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がコンピューターの C ドライブにインストールされている場合は、構成ファイルを `C:\Program Files\Microsoft SQL Server\MSSQL13.\<InstanceName>\MSSQL\Binn` に配置します。  
  
## <a name="see-also"></a>参照  
 [Microsoft Azure に格納されたバックアップからの復元](../../relational-databases/backup-restore/restoring-from-backups-stored-in-microsoft-azure.md)  
[BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)  
[RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)
  
