---
title: Azure への SQL Server マネージバックアップの設定 |Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 68ebb53e-d5ad-4622-af68-1e150b94516e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b69439226b55965e37f24f2131c77340ae833590
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154720"
---
# <a name="setting-up-sql-server-managed-backup-to-azure"></a>Azure への SQL Server マネージバックアップの設定
  このトピックには、次の 2 つのチュートリアルが含まれています。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]をデータベース レベルで設定し、電子メール通知を有効にして、バックアップ処理を監視します。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]をインスタンス レベルで設定し、電子メール通知を有効にして、バックアップ処理を監視します。  
  
 可用性グループ[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の設定に関するチュートリアルについては、「[可用性グループの Microsoft Azure するための SQL Server マネージバックアップの設定](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)」を参照してください。  
  
## <a name="setting-up-includess_smartbackupincludesss-smartbackup-mdmd"></a>[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の設定  
  
### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-a-database"></a>データベースに対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にして構成する  
 このチュートリアルでは、データベース (TestDB) に対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にして構成するために必要な手順の後、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の正常性状態の監視を有効にする手順について説明します。  
  
 **権限:**  
  
-   **Db_backupoperator**データベースロールのメンバーシップ、 **ALTER ANY CREDENTIAL**権限、および`EXECUTE` **sp_delete_backuphistory**ストアドプロシージャに対する権限が必要です。  
  
-   **Fn_get_current_xevent_settings**関数に対する**SELECT**権限が必要です。  
  
-   Smart_admin `EXECUTE`ストアドプロシージャに対する権限が必要です。 さらに、`VIEW SERVER STATE` 権限も必要です (この権限を必要とする他のシステム オブジェクトを内部的に呼び出すため)。  
  
-   ストアド`EXECUTE`プロシージャ`smart_admin.sp_set_instance_backup`およびストアドプロシージャに対する権限が必要です。`smart_admin.sp_backup_master_switch`  


1.  **Microsoft Azure ストレージアカウントを作成します。** バックアップは Microsoft Azure ストレージサービスに格納されます。 まだアカウントを持っていない場合は、まず Microsoft Azure ストレージアカウントを作成する必要があります。
    - SQL Server 2014 では、ブロック blob と追加 blob とは異なるページ blob が使用されます。 そのため、blob アカウントではなく、汎用アカウントを作成する必要があります。 詳細については、「 [Azure ストレージアカウントについて](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」を参照してください。
    - ストレージ アカウント名およびアクセス キーをメモしておきます。 ストレージ アカウント名およびアクセス キー情報は、SQL 資格情報の作成に使用します。 ストレージアカウントに対する認証には、SQL 資格情報が使用されます。  
 
2.  **SQL 資格情報を作成します。** Id としてストレージアカウントの名前を使用し、パスワードとしてストレージアクセスキーを使用して、SQL 資格情報を作成します。  
  
3.  **SQL Server エージェント サービスが開始され、実行されていることを確認する:** SQL Server エージェントを開始します (現在実行されていない場合)。  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] でバックアップ操作を実行するには、SQL Server エージェントがインスタンスで実行されている必要があります。  バックアップ操作を定期的に実行できるように、SQL Server エージェントの自動的な実行を設定できます。  
  
4.  **保有期間を決定する:** バックアップ ファイルに必要な保有期間を決定します。 保有期間は日数で指定し、その範囲は 1 ～ 30 になります。  
  
5.  **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にして構成する:** SQL Server Management Studio を起動し、データベースがインストールされているインスタンスに接続します。 要件に合わせて、データベース名、SQL 資格情報、保有期間、および暗号化オプションの値を変更した後、クエリ ウィンドウから次のステートメントを実行します。  
  
     暗号化用の証明書の作成の詳細については、「[暗号化されたバックアップを作成](create-an-encrypted-backup.md)する」の「**バックアップ証明書**の作成」を参照してください。  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='TestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、指定したデータベースで有効になります。 データベースでのバックアップ操作の実行が開始されるまで最大 15 分かかる場合があります。  
  
6.  **拡張イベントの既定の構成を確認する:** 次の Transact-SQL ステートメントを実行して、拡張イベントの設定を確認します。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     管理、運用、および分析のチャネル イベントは既定で有効になっていて、無効にできないことに注意してください。 手動の介入を必要とするイベントを監視するには、これで十分です。  デバッグ イベントを有効にすることはできますが、デバッグ チャネルには、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] が問題の検出および解決に使用する情報イベントとデバッグ イベントが含まれています。 詳細については、「 [Monitor SQL Server Managed Backup to Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
7.  **正常性状態の通知を有効化し、構成する:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] には、注意を要するエラーまたは警告の電子メール通知を送信するためにエージェント ジョブを作成するストアド プロシージャがあります。 次の手順では、電子メール通知を有効にして構成するためのプロセスを示します。  
  
    1.  データベース メールがインスタンス上でまだ有効になっていない場合は設定します。 詳細については、「 [Configure Database Mail](../database-mail/configure-database-mail.md)」を参照してください。  
  
    2.  データベース メールを使用するように SQL Server エージェント通知を構成します。 詳細については、「 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)」を参照してください。  
  
    3.  **電子メール通知を有効にして、バックアップ エラーおよび警告を受け取る:** クエリ ウィンドウから、次の Transact-SQL ステートメントを実行します。  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email1;email2>'  
  
        ```  
  
         詳細と完全なサンプルスクリプトについては、「 [Monitor SQL Server Managed Backup to Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
8.  **Microsoft Azure ストレージ アカウントでバックアップ ファイルを表示する:** SQL Server Management Studio または Azure 管理ポータルから、ストレージ アカウントに接続します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を使用するように構成したデータベースをホストする SQL Server インスタンスのコンテナーが表示されます。 また、データベースに対して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にしてから 15 分以内のデータベースとログ バックアップも表示される場合があります。  
  
9. **正常性状態を監視する:** 前の手順で構成した電子メール通知から監視するか、ログに記録されているイベントをアクティブに監視することができます。 イベントを表示するための Transact-SQL ステートメントのいくつかの例を示します。  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    -- to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 このセクションで説明した手順は、データベースで初めて [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を構成するための特別な手順です。 同じシステムストアドプロシージャ**smart_admin**を使用して既存の構成を変更し、新しい値を指定することができます。 詳細については、「SQL Server 管理されている[バックアップから Microsoft Azure-保有期間とストレージの設定](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)」を参照してください。  
  
### <a name="enable-includess_smartbackupincludesss-smartbackup-mdmd-for-the-instance-with-default-settings"></a>既定の設定を使用してインスタンスの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にする  
 このチュートリアルでは、インスタンス ' myinstance [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] \\' に対してを有効にして構成する手順について説明します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の正常性状態の監視を有効にするための手順も含まれています。  
  
 **権限:**  
  
-   **Db_backupoperator**データベースロールのメンバーシップ、 **ALTER ANY CREDENTIAL**権限、および`EXECUTE` **sp_delete_backuphistory**ストアドプロシージャに対する権限が必要です。  
  
-   **Fn_get_current_xevent_settings**関数に対する**SELECT**権限が必要です。  
  
-   Smart_admin `EXECUTE`ストアドプロシージャに対する権限が必要です。 さらに、`VIEW SERVER STATE` 権限も必要です (この権限を必要とする他のシステム オブジェクトを内部的に呼び出すため)。  


1.  **Microsoft Azure ストレージアカウントを作成します。** バックアップは Microsoft Azure ストレージサービスに格納されます。 まだアカウントを持っていない場合は、まず Microsoft Azure ストレージアカウントを作成する必要があります。
    - SQL Server 2014 では、ブロック blob と追加 blob とは異なるページ blob が使用されます。 そのため、blob アカウントではなく、汎用アカウントを作成する必要があります。 詳細については、「 [Azure ストレージアカウントについて](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」を参照してください。
    - ストレージ アカウント名およびアクセス キーをメモしておきます。 ストレージ アカウント名およびアクセス キー情報は、SQL 資格情報の作成に使用します。 ストレージアカウントに対する認証には、SQL 資格情報が使用されます。  
  
2.  **SQL 資格情報を作成します。** Id としてストレージアカウントの名前を使用し、パスワードとしてストレージアクセスキーを使用して、SQL 資格情報を作成します。  
  
3.  **SQL Server エージェント サービスが開始され、実行されていることを確認する:** SQL Server エージェントを開始します (現在実行されていない場合)。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] でバックアップ操作を実行するには、SQL Server エージェントがインスタンスで実行されている必要があります。  バックアップ操作を定期的に実行できるように、SQL Server エージェントの自動的な実行を設定できます。  
  
4.  **保有期間を決定する:** バックアップ ファイルに必要な保有期間を決定します。 保有期間は日数で指定し、その範囲は 1 ～ 30 になります。 インスタンス レベルで既定値を使用して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にすると、その後作成されたすべての新しいデータベースに、設定が継承されます。 完全または一括ログ復旧モデルに設定されているデータベースのみがサポートされており、自動的に構成されます。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成する必要がなければ、特定のデータベースの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]をいつでも無効にすることができます。 また、データベース レベルで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成することで、特定のデータベースの構成を変更することもできます。  
  
5.  **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効にして構成する:** SQL Server Management Studio を起動し、SQL Server のインスタンスに接続します。 要件に応じて、データベース名、SQL 資格情報、保有期間、および暗号化オプションの値を変更した後、クエリウィンドウから次のステートメントを実行します。  
  
     暗号化用の証明書の作成の詳細については、「[暗号化されたバックアップを作成](create-an-encrypted-backup.md)する」の「**バックアップ証明書**の作成」を参照してください。  
  
    ```  
    Use msdb;  
    Go  
       EXEC smart_admin.sp_set_instance_backup  
                     @enable_backup=1  
                    ,@retention_days=30   
                    ,@credential_name='sqlbackuptoURL'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert';  
    GO  
  
    ```  
  
     これで、インスタンス上で [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]が有効になります。  
  
6.  次の Transact-SQL ステートメントを実行して、構成設定を確認します。  
  
    ```  
    Use msdb;  
    GO  
    SELECT * FROM smart_admin.fn_backup_instance_config ();  
  
    ```  
  
7.  インスタンス上に新しいデータベースを作成します。 次の Transact-SQL ステートメントを実行して、データベースの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の構成設定を表示します。  
  
    ```  
    Use msdb  
    GO  
    SELECT * FROM smart_admin.fn_backup_db_config('NewDB')  
    ```  
  
     設定が表示され、データベースでのバックアップ操作の実行が開始されるまで最大 15 分かかる場合があります。  
  
8.  **正常性状態の通知を有効化し、構成する:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] には、注意を要するエラーまたは警告の電子メール通知を送信するためにエージェント ジョブを作成するストアド プロシージャがあります。  このような通知を受信するには、SQL Server エージェント ジョブを作成するストアド プロシージャの実行を有効にする必要があります。 次の手順では、電子メール通知を有効にして構成するためのプロセスを示します。  
  
    1.  データベース メールがインスタンス上でまだ有効になっていない場合は設定します。 詳細については、「 [Configure Database Mail](../database-mail/configure-database-mail.md)」を参照してください。  
  
    2.  データベース メールを使用するように SQL Server エージェント通知を構成します。 詳細については、「 [Configure SQL Server Agent Mail to Use Database Mail](../database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)」を参照してください。  
  
    3.  **電子メール通知を有効にして、バックアップ エラーおよび警告を受け取る:** クエリ ウィンドウから、次の Transact-SQL ステートメントを実行します。  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email address>'  
  
        ```  
  
         監視方法の詳細と完全なサンプルスクリプトについては、「 [monitor SQL Server Managed Backup to Microsoft Azure](sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
9. **Microsoft Azure ストレージ アカウントでバックアップ ファイルを表示する:** SQL Server Management Studio または Azure 管理ポータルから、ストレージ アカウントに接続します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を使用するように構成したデータベースをホストする SQL Server インスタンスのコンテナーが表示されます。 また、新しいデータベースを作成してから 15 分以内のデータベースとログ バックアップも表示される場合があります。  
  
10. **正常性状態を監視する:** 前の手順で構成した電子メール通知から監視するか、ログに記録されているイベントをアクティブに監視することができます。 イベントを表示するための Transact-SQL ステートメントのいくつかの例を示します。  
  
    ```  
    --  view all admin events  
    Use msdb;  
    Go  
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
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek  
  
    SELECT * from @eventresult  
    WHERE event_type LIKE '%admin%'  
  
    ```  
  
    ```  
    --  to enable debug events  
    Use msdb;  
    Go  
             EXEC smart_admin.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
    ```  
  
    ```  
    --  View all events in the current week  
    Use msdb;  
    Go  
    DECLARE @startofweek datetime  
    DECLARE @endofweek datetime  
    SET @startofweek = DATEADD(Day, 1-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)   
    SET @endofweek = DATEADD(Day, 7-DATEPART(WEEKDAY, CURRENT_TIMESTAMP), CURRENT_TIMESTAMP)  
  
    EXEC smart_admin.sp_get_backup_diagnostics @begin_time = @startofweek, @end_time = @endofweek;  
  
    ```  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の既定の設定は、明示的にデータベース レベルで設定を構成することで、特定のデータベースに対してオーバーライドすることができます。 また、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] サービスを一時停止および再開することもできます。 詳細については、「 [Microsoft Azure への管理](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)されたバックアップの SQL Server」を参照してください。  
  
  
