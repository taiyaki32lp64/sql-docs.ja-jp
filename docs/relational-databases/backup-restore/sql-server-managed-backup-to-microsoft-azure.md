---
title: Microsoft Azure への SQL Server マネージド バックアップ | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 49016b1b4ff391c1b1f533a2bf716f39a40b4dbe
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245432"
---
# <a name="sql-server-managed-backup-to-microsoft-azure"></a>Microsoft Azure への SQL Server マネージド バックアップ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は Microsoft Azure BLOB ストレージへの SQL Server バックアップを管理および自動化します。 SQL Server でデータベースのトランザクション ワークロードに基づいて、バックアップ スケジュールを決定するように選択できます。 また、詳細オプションを使用して、スケジュールを定義することもできます。 保有期間の設定で、Azure BLOB ストレージでのバックアップの保存期間を決定します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] では、指定された保有期間の特定の時点への復元がサポートされています。  
  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] のプロシージャと基になる動作が変更されています。 詳細については、[SQL Server 2014 マネージド バックアップの設定の SQL Server 2016 への移行](../../relational-databases/backup-restore/migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016.md)に関するページを参照してください。  
  
> [!TIP]  
>  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、Microsoft Azure 仮想マシンで実行されている SQL Server インスタンスに推奨されます。  
  
## <a name="benefits"></a>メリット  
 現在、複数データベースのバックアップを自動化するには、バックアップ方法の開発、カスタム コードの記述、およびバックアップのスケジュール設定が必要です。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を使用すれば、保有期間と保存場所を指定するだけで、バックアップ プランを作成できます。 詳細設定を使用できますが、必須ではありません。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] で行われます。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、データベース レベルまたは SQL Server インスタンス レベルで構成できます。 インスタンス レベルで構成する場合、新しいすべてのデータベースも自動的にバックアップされます。 データベース レベルでの設定を使用して、個々のケースに対するインスタンス レベルの既定値をオーバーライドすることができます。  
  
 また、セキュリティ強化のためにバックアップを暗号化することができ、バックアップのタイミングを制御するためのカスタム スケジュールをセットアップすることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップに Microsoft Azure BLOB ストレージを使用する利点の詳細については、「 [Microsoft Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
##  <a name="Prereqs"></a> 前提条件  
 Microsoft Azure Storage は、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] がバックアップ ファイルを格納するために使用されます。 以下の前提条件が必要です。  
  
|前提条件|[説明]|  
|------------------|-----------------|  
|**Microsoft Azure アカウント**|[購入オプション](https://azure.microsoft.com/pricing/free-trial/) を調べる前に、 [無料評価版](https://azure.microsoft.com/pricing/purchase-options/)で Azure を使用することができます。|  
|**Azure Storage アカウント**|バックアップは、Azure ストレージ アカウントに関連付けられている Azure BLOB ストレージに格納されます。 ストレージ アカウントの詳しい作成手順については、「 [Azure ストレージ アカウントについて](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)」を参照してください。|  
|**BLOB コンテナー**|BLOB はコンテナーで構成されます。 バックアップ ファイルに対してターゲット コンテナーを指定します。 [Azure 管理ポータル](https://manage.windowsazure.com/)でコンテナーを作成することができます。または、 **New-AzureStorageContainer**[Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) コマンドを使用します。|  
|**Shared Access Signature (SAS)**|ターゲット コンテナーへのアクセスは Shared Access Signature (SAS) で制御されます。 SAS の概要については、「[Shared Access Signature、第 1 部:SAS モデル](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)に関するページを参照してください。 SAS トークンは、コードで、または **New-AzureStorageContainerSASToken** PowerShell  コマンドを使用して作成することができます。 このプロセスを簡素化する PowerShell スクリプトについては、「 [Simplifying creation of SQL Credentials with Shared Access Signature ( SAS ) tokens on Azure Storage with PowerShell](https://blogs.msdn.com/b/sqlcat/archive/2015/03/21/simplifying-creation-sql-credentials-with-shared-access-signature-sas-keys-on-azure-storage-containers-with-powershell.aspx)」 (PowerShell を使用する Azure ストレージにおける共有アクセス署名 (SAS) トークンでの SQL 資格情報の作成の簡素化) を参照してください。 **で使用するために SAS トークンを** SQL Credential [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]に格納することができます。|  
|**SQL Server エージェント**|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を機能させるには、SQL Server エージェントを実行する必要があります。 スタートアップ オプションを自動に設定することを検討してください。|  
  
## <a name="components"></a>Components  
 Transact-SQL は、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を操作するためのメイン インターフェイスです。 システム ストアド プロシージャは、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の有効化、構成、および監視に使用します。 システム関数は、既存の構成設定、パラメーター値、およびバックアップ ファイル情報を取得するために使用します。 拡張イベントは、エラーと警告を表示するために使用します。 警告メカニズムを有効にするには、SQL エージェント ジョブと SQL Server のポリシー ベースの管理を使用します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]に関連するオブジェクトとその機能の説明の一覧を次に示します。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成するには、PowerShell コマンドレットも使用できます。 SQL Server Management Studio では、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] によって作成されたバックアップを **[データベースの復元]** タスクを使用して復元することがサポートされています。  
  
|||  
|-|-|  
|システム オブジェクト|[説明]|  
|**MSDB**|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]によって作成されたすべてのバックアップに対するメタデータとバックアップ履歴を格納します。|  
|[managed_backup.sp_backup_config_basic (Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にします。|  
|[managed_backup.sp_backup_config_advanced &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)|暗号化など、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の詳細設定を構成します。|  
|[managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]のカスタム スケジュールを作成します。|  
|[managed_backup.sp_ backup_master_switch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を一時停止し、再開します。|  
|[managed_backup.sp_set_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の監視を有効にし、構成します。 たとえば、拡張イベントの有効化、通知の電子メール設定があります。|  
|[managed_backup.sp_backup_on_demand &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql.md)|ログ チェーンを分断することなく [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を使用できるデータベースのアドホック バックアップを実行します。|  
|[managed_backup.fn_backup_db_config &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql.md)|1 つのデータベース、またはインスタンス上のすべてのデータベースに対する現在の [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の状態と構成値を返します。|  
|[managed_backup.fn_is_master_switch_on &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql.md)|マスターの切り替えの状態を返します。|  
|[managed_backup.sp_get_backup_diagnostics &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql.md)|拡張イベントによってログに記録されるイベントを返します。|  
|[managed_backup.fn_get_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql.md)|警告の監視やメール設定など、バックアップ システムの設定の現在の値を返します。|  
|[managed_backup.fn_available_backups &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql.md)|指定されたデータベース、またはインスタンス内のすべてのデータベースの利用可能なバックアップを取得します。|  
|[managed_backup.fn_get_current_xevent_settings &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql.md)|現在の拡張イベントの設定を返します。|  
|[managed_backup.fn_get_health_status &#40;Transact-SQL&#41;](../../relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql.md)|指定した期間に拡張イベントによってログに記録されたエラーの集計数を返します。|  
  
## <a name="backup-strategy"></a>バックアップ方法  
  
### <a name="backup-scheduling"></a>バックアップのスケジュール設定  
 システム ストアド プロシージャ [managed_backup.sp_backup_config_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)」を参照してください。 カスタム スケジュールを指定しない場合は、スケジュールされたバックアップの種類とそのバックアップの頻度は、データベースのワークロードに基づいて決定されます。 保有期間の設定を使用して、バックアップ ファイルをストレージに保持しておく期間と、保有期間内の特定の時点にデータベースを復旧できるかどうかを決定します。  
  
### <a name="backup-file-naming-conventions"></a>バックアップ ファイルの名前付け規則  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は指定されたコンテナーを使用するため、コンテナーの名前を制御できます。 バックアップ ファイルについて、可用性データベース以外のデータベースには次の規則に従って名前が付けられます。名前は、データベース名の先頭 40 文字、データベース GUID ('-' を除く)、およびタイムスタンプを使用して作成されます。 各セグメントの間には、区切り記号としてアンダースコア文字が挿入されます。 完全バックアップにはファイル拡張子として **.bak** が使用され、ログ バックアップには **.log** が使用されます。 可用性グループ データベースでは、前のファイル名前付け規則に加え、40 文字のデータベース名の後に可用性グループ データベース GUID が追加されます。 可用性グループ データベース GUID 値は、sys.databases の group_database_id の値です。  
  
### <a name="full-database-backup"></a>データベースの完全バックアップ  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] エージェントは、次のいずれかが当てはまる場合にデータベースの完全バックアップをスケジュールします。  
  
-   データベースで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を初めて有効にしたとき、またはインスタンス レベルで既定の設定を使用して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効したとき。  
  
-   前回のデータベースの完全バックアップ以降にログが 1 GB 以上に拡張されている。  
  
-   前回のデータベースの完全バックアップ以降に 1 週間という最大期間が経過している。  
  
-   ログ チェーンが分断されている。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] では、バックアップ ファイルの最初と最後の LSN を比較することで、ログ チェーンが分断されていないかどうかを定期的に確認します。 なんらかの理由でログ チェーンが分断されている場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] はデータベースの完全バックアップをスケジュールします。 ログ チェーンが分断される最も一般的な理由として、Transact-SQL を使用するか SQL Server Management Studio のバックアップ タスクを使用してバックアップ コマンドが実行されていることが考えられます。  その他の一般的なシナリオには、バックアップ ログ ファイルを誤って削除した、バックアップを誤って上書きしたなどがあります。  
  
### <a name="transaction-log-backup"></a>トランザクション ログ バックアップ  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、次のいずれかが当てはまる場合にログ バックアップをスケジュールします。  
  
-   ログ バックアップの履歴が見つからない。 通常、これは [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を初めて有効にしたときに当てはまります。  
  
-   使用されているトランザクション ログ領域が 5 MB 以上になった。  
  
-   前回のログ バックアップの後に 2 時間という最大期間に達している。  
  
-   トランザクション ログのバックアップがデータベースの完全バックアップより遅れている。 目標は、ログ チェーンが完全バックアップより進んだ状態にしておくことです。  
  
## <a name="retention-period-settings"></a>保有期間の設定  
 バックアップを有効にするときに、保有期間を日単位で設定する必要があります。最小値は 1 日で、最大値は 30 日です。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は保有期間の設定に基づいて、指定された期間内の特定の時点に復旧できるかどうかを評価し、保持するバックアップ ファイルと削除するバックアップ ファイルを決定します。 保有期間の設定で指定された期間を特定および照合するために、バックアップの backup_finish_date が使用されます。  
  
## <a name="important-considerations"></a>重要な考慮事項  
 データベースでは、実行されている既存のデータベースの完全バックアップ ジョブがある場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は現在のジョブが完了するのを待ってから、同じデータベースの完全バックアップをもう一度実行します。 同様に、一度に実行できるトランザクション ログ バックアップは 1 つだけです。 ただし、データベースの完全バックアップとトランザクション ログ バックアップは同時に実行できます。 エラーは、拡張イベントとしてログに記録されます。  
  
 同時に 10 個を超えるデータベースの完全バックアップがスケジュールされている場合、拡張イベントのデバッグ チャネルを通じて警告が発生します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、バックアップする必要がある残りのデータベースの優先キューを、すべてのバックアップがスケジュールされ完了するまで管理します。  

> [!NOTE]
> プロキシ サーバーでは、SQL Server マネージド バックアップはサポートされていません。
>
  
##  <a name="support_limits"></a> サポート性  
 次のサポートの制限事項と考慮事項は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に固有のものです。  
  
-   **master**、 **model**、 **msdb** の各システム データベースのバックアップがサポートされます。 **tempdb** のバックアップはサポートされません。 
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の場合、すべての復旧モデル (完全、一括ログ、および単純) がサポートされます。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] エージェントでは、データベースの完全バックアップとログ バックアップのみがサポートされます。 ファイル バックアップの自動化はサポートされません。  
  
-   Microsoft Azure BLOB ストレージ サービスは、唯一サポートされているバックアップ ストレージ オプションです。 ディスクまたはテープへのバックアップはサポートされていません。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ではブロック BLOB へのバックアップ機能を使用します。 ブロック BLOB の最大サイズは 200 GB です。 ストライピングを利用することにより、個々のバックアップの最大サイズを 12 TB まで指定できます。 バックアップ要件がこれを超える場合は、圧縮の使用を検討し、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]をセットアップする前にバックアップ ファイルのサイズをテストします。 テストは、ローカル ディスクにバックアップするか、Transact-SQL の **BACKUP TO URL** ステートメントを使用して手動で Microsoft Azure ストレージにバックアップして行うことができます。 詳細については、「 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」を参照してください。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]は、バックアップ、高可用性、またはディザスター リカバリーをサポートする他のテクノロジで構成されている場合にいくつかの制限がある場合があります。  
  
## <a name="see-also"></a>参照  
- [Microsoft Azure への SQL Server マネージド バックアップを有効にする](../../relational-databases/backup-restore/enable-sql-server-managed-backup-to-microsoft-azure.md)   
- [Microsoft Azure への SQL Server マネージド バックアップの詳細設定オプションの構成](../../relational-databases/backup-restore/configure-advanced-options-for-sql-server-managed-backup-to-microsoft-azure.md)   
- [Microsoft Azure への SQL Server マネージド バックアップを無効にする](../../relational-databases/backup-restore/disable-sql-server-managed-backup-to-microsoft-azure.md)
- [システム データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)
- [SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
  
  
