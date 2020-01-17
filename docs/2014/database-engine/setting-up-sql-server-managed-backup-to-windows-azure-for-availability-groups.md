---
title: 可用性グループのための Azure への SQL Server マネージバックアップの設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 0c4553cd-d8e4-4691-963a-4e414cc0f1ba
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 75ab1892641fa3bf805d52c649a8526e256d14b7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228204"
---
# <a name="setting-up-sql-server-managed-backup-to-azure-for-availability-groups"></a>可用性グループに対する Azure への SQL Server マネージド バックアップの設定
  このトピックは、AlwaysOn 可用性グループに参加しているデータベースの [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の構成に関するチュートリアルです。  
  
## <a name="availability-group-configurations"></a>可用性グループの構成  
 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は、可用性グループデータベースに対してサポートされています。レプリカがすべてオンプレミスで構成されているか、完全に Azure で構成されているか、またはオンプレミスと1つ以上の Azure 仮想マシンの間のハイブリッド実装であるかは関係ありません。 ただし、1 つ以上の実装に関して、次のことを考慮する必要が生じる可能性があります。  
  
-   ログ バックアップ頻度: ログ バックアップ頻度に応じて、時間とログの両方が増加します。 たとえば、2 時間という期間で使用されるログ領域が 5 MB に達しない場合は、2 時間ごとにログ バックアップを作成するとします。 この方針を、内部設置型、クラウド、またはハイブリッドというすべての実装に適用します。  
  
-   ネットワーク帯域幅: これは、ハイブリッドクラウドなどの異なる物理的な場所にあるレプリカが配置されている場合、またはクラウドのみの構成の異なる Azure リージョンにある場合に適用されます。 ネットワーク帯域幅は、セカンダリの待機時間に影響する可能性があります。セカンダリが同期レプリケーションに設定されている場合は、プライマリ ログの増加が引き起こされる可能性があります。 セカンダリ レプリカが同期レプリケーションに設定されている場合は、ネットワーク待機時間が原因でセカンダリは同期を維持できない可能性があり、その結果、セカンダリ レプリカへのフェールオーバー イベントが発生したときにデータが失われる可能性があります。  
  
### <a name="configuring-includess_smartbackupincludesss-smartbackup-mdmd-for-availability-databases"></a>可用性データベースに対する [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の構成  
 **許可**  
  
-   **Db_backupoperator**データベースロールのメンバーシップ、 **ALTER ANY CREDENTIAL**権限、および`EXECUTE` **sp_delete_backuphistory**ストアドプロシージャに対する権限が必要です。  
  
-   **Smart_admin fn_get_current_xevent_settings**関数に対する**SELECT**権限が必要です。  
  
-   `EXECUTE` **Smart_admin sp_get_backup_diagnostics**ストアドプロシージャに対する権限が必要です。 さらに、`VIEW SERVER STATE` 権限も必要です (この権限を必要とする他のシステム オブジェクトを内部的に呼び出すため)。  
  
-   ストアド`EXECUTE`プロシージャ`smart_admin.sp_set_instance_backup`および`smart_admin.sp_backup_master_switch`ストアドプロシージャに対する権限が必要です。  
  
 次に、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]で AlwaysOn 可用性グループを設定する基本的な手順を説明します。 詳細手順のチュートリアルについては、このトピックの後半で説明します。  
  
1.  可用性グループを作成したら、優先されるバックアップ レプリカを構成します。 可用性グループに対するこの設定は、バックアップに使用するレプリカを決定するために [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]でも使用されます。 バックアップ設定をセットアップする方法の詳細な手順については、「[可用性レプリカのバックアップの構成」 &#40;SQL Server&#41;](availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)を参照してください。  新しい AlwaysOn 可用性グループを作成する場合は、「[はじめに AlwaysOn 可用性グループ &#40;SQL Server&#41;](availability-groups/windows/getting-started-with-always-on-availability-groups-sql-server.md)」を参照してください。  
  
2.  セカンダリ レプリカへの読み取り専用接続アクセスを構成します。 読み取り専用アクセスを構成する方法の詳細な手順については、「[可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md) 」を参照してください&#41;  
  
3.  バックアップ レプリカを指定します。 優先されるバックアップ レプリカの設定は、バックアップのスケジュール設定に使用するデータベースを決定するために [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]で使用されます。  現在のレプリカが推奨されるバックアップレプリカであるかどうかを判断するには、 [fn_hadr_backup_is_preferred_replica &#40;transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)関数を使用します。  
  
4.  各レプリカで、 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] **smart admin. sp_set_db_backup**ストアドプロシージャを使用してデータベースの構成を実行します。  
  
     **フェールオーバー後の動作: は、フェールオーバーイベント後も引き続き機能し、バックアップコピーと回復性を維持します。 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] フェールオーバー後に特別な操作は必要ありません。  
  
#### <a name="considerations-and-requirements"></a>注意点と要件:  
 AlwaysOn 可用性グループに参加しているデータベースに対して [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を構成する場合は、特定の注意点と要件があります。 次に、考慮事項と要件の一覧を示します。  
  
-   
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の構成設定は、同じ可用性グループに参加している [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のすべてのノード上にあるすべてのデータベースに対して同じである必要があります。 これを実現するには、データベース レベルでプライマリとすべてのレプリカに対して同じ [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]構成を設定するか、可用性グループに参加しているすべてのノードで同じ既定の [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]設定を使用します。 データベース レベルで [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を設定することをお勧めします。データベース レベルで [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を構成すると、データベースに対する設定を分離でき、既定の設定に対する変更は、インスタンス上の他のデータベースすべてに反映されます。  
  
-   バックアップ レプリカを指定します。 
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]では、優先されるバックアップ レプリカの設定がバックアップのスケジュール設定に使用されます。 現在のレプリカが推奨されるバックアップレプリカであるかどうかを判断するには、 [fn_hadr_backup_is_preferred_replica &#40;transact-sql&#41;](/sql/relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql)関数を使用します。  
  
-   優先されるレプリカとしてセカンダリ レプリカが構成されている場合は、少なくとも読み取り専用接続アクセスを持つように構成する必要があります。 セカンダリ データベースへの接続アクセスがない可用性グループはサポートされません。  詳細については、「 [可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)が存在する必要があります。  
  
-   可用性グループの構成後に [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を構成すると、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は、構成に基づいて既存のバックアップをコピーし、それをストレージ コンテナーに格納することを試みます。  
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]は、既存のバックアップが見つからない場合や既存のバックアップにアクセスできない場合に、データベースの完全バックアップをスケジュールします。 この処理は、特に、可用性グループのデータベースのバックアップ操作を最適化するために行われます。  
  
-   新しい可用性データベースを作成するときに、インスタンスレベルの設定をデータベースに適用しない場合は、インスタンスレベルの設定を無効にすることを検討してください。  
  
-   暗号化を使用する場合は、すべてのレプリカで同じ証明書を使用します。 この結果、フェールオーバー イベントが発生した場合や、別のレプリカへの復元を行う場合に、継続的で途切れることのないバックアップ操作が容易になります。  
  
#### <a name="enable-and-configure-includess_smartbackupincludesss-smartbackup-mdmd-for-an-availability-database"></a>可用性データベースに対する [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]の有効化と構成  
 このチュートリアルでは、Node1 と Node2 の[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]コンピューターでデータベース (agtestdb 対し) を有効にして構成する手順について説明し[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 、その後、正常性状態の監視を有効にする手順について説明します。  
  
1.  **Azure ストレージアカウントを作成します。** バックアップは、Azure Blob ストレージサービスに格納されます。 Azure ストレージアカウントをまだ作成していない場合は、最初に作成する必要があります。 詳細については、「 [Azure Storage アカウントの作成](https://www.windowsazure.com/manage/services/storage/how-to-create-a-storage-account/)」を参照してください。 ストレージ アカウントの名前、アクセス キー、および URL をメモしておきます。 ストレージ アカウント名およびアクセス キー情報は、SQL 資格情報の作成に使用します。 SQL 資格情報は、バックアップ操作中にストレージ アカウントへの認証を行うために [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]によって使用されます。  
  
2.  **SQL 資格情報を作成します。** Id としてストレージアカウントの名前を使用し、パスワードとしてストレージアクセスキーを使用して、SQL 資格情報を作成します。  
  
3.  **SQL Server エージェントサービスが開始され、実行されていることを確認します。** 現在実行されていない場合は SQL Server エージェントを開始します。 
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] でバックアップ操作を実行するには、SQL Server エージェントがインスタンスで実行されている必要があります。  バックアップ操作を定期的に実行できるように、SQL エージェントの自動的な実行を設定できます。  
  
4.  **保有期間を決定します。** バックアップファイルに必要な保有期間を決定します。 保有期間は日数で指定し、その範囲は 1 ～ 30 になります。 保有期間によって、データベースの復旧時間の期間が決まります。  
  
5.  **バックアップ中の暗号化に使用する証明書または非対称キーを作成します。** 最初のノード Node1 で証明書を作成してから、バックアップ証明書を使用してファイルにエクスポートします。これには、 [transact-sql&#41;&#40;](/sql/t-sql/statements/backup-certificate-transact-sql)ます。 Node 2 で、Node 1 からエクスポートしたファイルを使用して証明書を作成します。 ファイルから証明書を作成する方法の詳細については、「 [CREATE certificate &#40;transact-sql&#41;](/sql/t-sql/statements/create-certificate-transact-sql)」の例を参照してください。  
  
6.  **Node1 で agtestdb 対し[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を有効にして構成します。** SQL Server Management Studio を起動し、可用性データベースがインストールされている Node1 上のインスタンスに接続します。 要件に合わせて、データベース名、ストレージ URL、SQL 資格情報、および保有期間の値を変更した後、クエリ ウィンドウから次のステートメントを実行します。  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     暗号化用の証明書の作成の詳細については、「[暗号化されたバックアップを作成](../relational-databases/backup-restore/create-an-encrypted-backup.md)する」の「**バックアップ証明書**の作成」を参照してください。  
  
7.  **Node2 で agtestdb 対し[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を有効にして構成します。** SQL Server Management Studio を起動し、可用性データベースがインストールされている Node2 上のインスタンスに接続します。 要件に合わせて、データベース名、ストレージ URL、SQL 資格情報、および保有期間の値を変更した後、クエリ ウィンドウから次のステートメントを実行します。  
  
    ```  
    Use msdb;  
    GO  
    EXEC smart_admin.sp_set_db_backup   
                    @database_name='AGTestDB'   
                    ,@retention_days=30   
                    ,@credential_name='MyCredential'  
                    ,@encryption_algorithm ='AES_128'  
                    ,@encryptor_type= 'Certificate'  
                    ,@encryptor_name='MyBackupCert'  
                    ,@enable_backup=1;  
    GO  
  
    ```  
  
     
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] は、指定したデータベースで有効になります。 データベースでのバックアップ操作の実行が開始されるまで最大 15 分かかる場合があります。 バックアップは、優先されるバックアップ レプリカに対して実行されます。  
  
8.  **拡張イベントの既定の構成を確認します。** を使用してバックアップのスケジュールを設定するレプリカ[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]で、次の transact-sql ステートメントを実行して、拡張イベントの構成を確認します。 これは、通常、データベースが属している可用性グループの優先されるバックアップ レプリカの設定です。  
  
    ```  
    SELECT * FROM smart_admin.fn_get_current_xevent_settings()  
    ```  
  
     管理、運用、および分析のチャネル イベントは既定で有効になっていて、無効にできないことに注意してください。 手動の介入を必要とするイベントを監視するには、これで十分です。  デバッグ イベントを有効にすることはできますが、これらのチャネルには、[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]が問題の検出および解決に使用する情報イベントとデバッグ イベントが含まれています。 詳細については、「 [Monitor SQL Server Managed Backup To Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
9. **正常性状態の通知を有効にして構成する:** [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]には、注意が必要なエラーまたは警告の電子メール通知を送信するエージェントジョブを作成するストアドプロシージャがあります。  このような通知を受信するには、SQL Server エージェント ジョブを作成するストアド プロシージャの実行を有効にする必要があります。 次の手順では、電子メール通知を有効にして構成するためのプロセスを示します。  
  
    1.  データベース メールがインスタンス上でまだ有効になっていない場合は設定します。 詳細については、「 [Configure Database Mail](../relational-databases/database-mail/configure-database-mail.md)」を参照してください。  
  
    2.  データベース メールを使用するように SQL Server エージェント通知を構成します。 詳細については、「[データベースメールを使用するように SQL Server エージェントメールを構成する](../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)」を参照してください。  
  
    3.  **電子メール通知によるバックアップエラーと警告の受信を有効にする:** クエリウィンドウで、次の Transact-sql ステートメントを実行します。  
  
        ```  
        EXEC msdb.smart_admin.sp_set_parameter  
        @parameter_name = 'SSMBackup2WANotificationEmailIds',  
        @parameter_value = '<email>'  
  
        ```  
  
         詳細と完全なサンプルスクリプトについては、「 [Monitor SQL Server Managed Backup To Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。  
  
10. **Azure Storage アカウントでバックアップファイルを表示します。** SQL Server Management Studio または Azure 管理ポータルからストレージアカウントに接続します。 
  [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を使用するように構成したデータベースをホストする SQL Server インスタンスのコンテナーが表示されます。 また、データベースに対して [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]を有効にしてから 15 分以内のデータベースとログ バックアップも表示される場合があります。  
  
11. **正常性状態の監視:** 以前に構成した電子メール通知を使用して監視したり、ログに記録されたイベントを積極的に監視したりできます。 イベントを表示するための Transact-SQL ステートメントのいくつかの例を示します。  
  
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
    event varchar (512),  
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
  
 このセクションで説明した手順は、データベースで初めて [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] を構成するための特別な手順です。 同じシステムストアドプロシージャ**smart_admin sp_set_db_backup**を使用して既存の構成を変更し、新しい値を指定することができます。 詳細については、「 [Azure へのマネージバックアップ-保有期間とストレージの設定の SQL Server](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)」を参照してください。  
  
### <a name="considerations-when-removing-a-database-from-alwayson-availability-group-configuration"></a>AlwaysOn 可用性グループの構成からデータベースを削除する際の注意点  
 データベースが AlwaysOn 可用性グループの構成から削除され、スタンドアロンデータベースになった場合は、smart_admin を使用してバックアップを実行することをお勧めし[ます。 transact-sql&#41;&#40;sp_backup_on_demand ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)。 データベースのバックアップをこのように作成すると、新しいバックアップ チェーンが確立され、データベースが可用性グループに含まれていたときにバックアップが格納された可用性コンテナーではなく、インスタンス固有のコンテナーにファイルが配置されます。  
  
> [!WARNING]  
>  このシナリオのデータベースについては、可用性グループの状態が変更される前のバックアップからの復旧性は保証されません。  
  
