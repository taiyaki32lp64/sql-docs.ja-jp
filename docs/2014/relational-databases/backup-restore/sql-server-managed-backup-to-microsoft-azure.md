---
title: Azure へのマネージバックアップの SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ab44323dfabd389113351e413751b7a230c176e6
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175754"
---
# <a name="sql-server-managed--backup-to-azure"></a>Azure へのマネージバックアップの SQL Server
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、Azure Blob ストレージサービスへの SQL Server のバックアップを管理および自動化します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]で使用されるバックアップ方法は、データベースの保有期間とトランザクション ワークロードに基づきます。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] では、指定された保有期間の特定の時点への復元がサポートされています。   
[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]は、データベース レベルで有効にすることも、インスタンス レベルで有効にして SQL Server インスタンス上のすべてのデータベースを管理することもできます。 SQL Server は、オンプレミスまたは Azure 仮想マシンなどのホストされた環境で実行できます。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、Azure Virtual Machines で実行されている SQL Server にお勧めします。  
  
## <a name="benefits-of-automating-sql-server-backup-using-includess_smartbackupincludesss-smartbackup-mdmd"></a>[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を使用して SQL Server バックアップを自動化する利点  
  
-   現在、複数データベースのバックアップを自動化するには、バックアップ方法の開発、カスタム コードの記述、およびバックアップのスケジュール設定が必要です。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の使用で必要になるのは、保有期間の設定と格納場所の指定のみです。 スケジュールを [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] すると、バックアップが実行され、維持されます。  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]は、データベース レベルで構成するか、SQL Server インスタンスの既定の設定を使用して構成することができます。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を使用したバックアップの自動化には、次の利点があります。  
  
    -   インスタンス レベルで既定値を設定すると、その後作成されたデータベースにこれらの設定を適用できます。これにより、新しいデータベースがバックアップされずデータが失われるというリスクがなくなります。  
  
    -   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にしてデータベース レベルで保有期間を設定すると、インスタンス レベルで設定した既定の設定をオーバーライドできます。 これにより、特定のデータベースの復旧をより細かく制御できます。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]では、データベースのバックアップの種類や頻度を指定する必要はありません。  保有期間を指定すると、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] によって、Azure Blob ストレージサービスにバックアップが格納されるデータベースのバックアップの種類と頻度が決まります。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] がバックアップ方法の作成に使用する一連の条件の詳細については、このトピックの「[コンポーネントと概念](#Concepts)」を参照してください。  
  
-   暗号化が使用されるように構成すると、バックアップ データに対するセキュリティを強化できます。 詳細については、「[バックアップの暗号化](backup-encryption.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップに Azure Blob storage を使用する利点の詳細については、 [Azure Blob Storage サービスを使用したバックアップと復元](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)に関する SQL Server を参照してください。  
  
## <a name="terms-and-definitions"></a>用語と定義  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 データベースのバックアップを自動化し、保有期間に基づいてバックアップを管理する SQL Server 機能です。  
  
 保有期間  
 保有期間は、指定された期間内の特定の時点にデータベースを復旧するために、ストレージに保持するバックアップファイルを決定するために [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] によって使用されます。  1 ～ 30 日の範囲の値がサポートされます。  
  
 ログ チェーン  
 ログ バックアップの連続的なシーケンスを、ログ チェーンと呼びます。 ログ チェーンは、データベースの完全バックアップから始まります。  
  
##  <a name="Concepts"></a>要件、概念、およびコンポーネント  
  
  
###  <a name="Security"></a> アクセス許可  
 Transact-SQL は、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の構成と監視に使用する主なインターフェイスです。 一般に、構成ストアドプロシージャを実行するには、 **ALTER ANY CREDENTIAL**権限を持つデータベースロールを**db_backupoperator** 、 **sp_delete_backuphistory**ストアドプロシージャに対する `EXECUTE` 権限が必要です。  情報を確認するために使用するストアド プロシージャと関数には、通常、ストアド プロシージャに対する `Execute` 権限と、関数に対する `Select` 権限がそれぞれ必要です。  
  
###  <a name="Prereqs"></a> の前提条件  
 **前提条件:**  
  
 **Azure Storage サービス**は、バックアップファイルを格納するために [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] によって使用されます。    Azure ストレージアカウントを作成するための概念、構造、および要件の詳細については、「 **SQL Server Backup TO URL** 」の「[主要なコンポーネントと概念の概要](sql-server-backup-to-url.md#intorkeyconcepts)」セクションを参照してください。  
  
 **SQL 資格**情報は、Azure ストレージアカウントに対する認証に必要な情報を格納するために使用されます。 SQL 資格情報オブジェクトには、アカウント名とアクセス キー情報が格納されます。 詳細については、「 **SQL Server Backup TO URL** 」トピックの「[主要なコンポーネントと概念の概要](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」セクションを参照してください。 Azure Storage 認証情報を格納するための SQL 資格情報を作成する方法のチュートリアルについては、「[レッスン 2: SQL Server 資格情報を作成](../../tutorials/lesson-2-create-a-sql-server-credential.md)する」を参照してください。  
  
###  <a name="Concepts_Components"></a>概念と主要なコンポーネント  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]は、バックアップ操作を管理する機能です。 メタデータは、 **msdb**データベースに格納され、システムジョブを使用してデータベースとトランザクションログの完全バックアップが書き込まれます。  
  
#### <a name="components"></a>のコンポーネント  
 Transact-SQL は、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を操作するためのメイン インターフェイスです。 システム ストアド プロシージャは、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の有効化、構成、および監視に使用します。 システム関数は、既存の構成設定、パラメーター値、およびバックアップ ファイル情報を取得するために使用します。 拡張イベントは、エラーと警告を表示するために使用します。 警告メカニズムを有効にするには、SQL エージェント ジョブと SQL Server のポリシー ベースの管理を使用します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]に関連するオブジェクトとその機能の説明の一覧を次に示します。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成するには、PowerShell コマンドレットも使用できます。 SQL Server Management Studio では、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] によって作成されたバックアップを **[データベースの復元]** タスクを使用して復元することがサポートされています。  
  
|||  
|-|-|  
|システム オブジェクト|[説明]|  
|**MSDB**|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]によって作成されたすべてのバックアップに対するメタデータとバックアップ履歴を格納します。|  
|[smart_admin set_db_backup &#40;transact-sql&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)|データベースの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を有効にして構成するためのシステム ストアド プロシージャです。|  
|[smart_admin set_instance_backup &#40;transact-sql&#41;](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|SQL Server インスタンスに [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 既定の設定を有効化および構成するためのシステムストアドプロシージャです。|  
|[smart_admin sp_ backup_master_switch &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を一時停止および再開するためのシステム ストアド プロシージャです。|  
|[smart_admin sp_set_parameter &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の監視を有効にして構成するためのシステム ストアド プロシージャです。 たとえば、拡張イベントの有効化、通知の電子メール設定があります。|  
|[smart_admin sp_backup_on_demand &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|ログチェーンを中断せずに [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の使用が有効になっているデータベースのアドホックバックアップを実行するために使用されるシステムストアドプロシージャ。|  
|[smart_admin fn_backup_db_config &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|データベースまたはインスタンス上のすべてのデータベースについて、現在の [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] の状態と構成値を返すシステム関数。|  
|[smart_admin fn_is_master_switch_on &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|マスターの切り替えの状態を返すシステム関数です。|  
|[smart_admin sp_get_backup_diagnostics &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|拡張イベントによってログに記録されたイベントを返すためのシステム ストアド プロシージャです。|  
|[smart_admin fn_get_parameter &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|警告の監視やメール設定など、バックアップ システムの設定の現在の値を返すシステム関数です。|  
|[smart_admin fn_available_backups &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|指定されたデータベース、またはインスタンス内のすべてのデータベースの利用可能なバックアップを取得するためのストアド プロシージャです。|  
|[smart_admin fn_get_current_xevent_settings &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|現在の拡張イベントの設定を返すシステム関数です。|  
|[smart_admin fn_get_health_status &#40;transact-sql&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|指定した期間に拡張イベントによってログに記録されたエラーの集計された数を返すシステム関数です。|  
|[Azure への SQL Server マネージバックアップの監視](sql-server-managed-backup-to-microsoft-azure.md)|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の監視用拡張イベント、エラーおよび警告の電子メール通知、SQL Server のポリシー ベースの管理。|  
  
#### <a name="backup-strategy"></a>バックアップ方法  
 **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]によって使用されるバックアップ方法:**  
  
 スケジュールされたバックアップの種類とそのバックアップの頻度は、データベースのワークロードに基づいて決定されます。 保有期間の設定を使用して、バックアップ ファイルをストレージに保持しておく期間と、保有期間内の特定の時点にデータベースを復旧できるかどうかを決定します。  
  
 **バックアップコンテナーとファイルの名前付け規則:**  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、可用性データベース以外のすべてのデータベースの SQL Server インスタンス名を使用して、Azure ストレージコンテナーに名前を指定します。  可用性データベースについては、可用性グループの GUID を使用して Azure storage コンテナーの名前を指定します。  
  
 可用性データベース以外のデータベースのバックアップファイルには、次の規則を使用して名前が付けられます。名前は、データベース名の最初の40文字、データベース GUID ('-' を除く)、およびタイムスタンプを使用して作成されます。 各セグメントの間には、区切り記号としてアンダースコア文字が挿入されます。 完全バックアップにはファイル拡張子として **.bak** が使用され、ログ バックアップには **.log** が使用されます。 可用性グループ データベースでは、前のファイル名前付け規則に加え、40 文字のデータベース名の後に可用性グループ データベース GUID が追加されます。 可用性グループ データベース GUID 値は、sys.databases の group_database_id の値です。  
  
 **データベースの完全バックアップ:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] エージェントは、次のいずれかに該当する場合にデータベースの完全バックアップをスケジュールします。  
  
-   データベースで [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を初めて有効にしたとき、またはインスタンス レベルで既定の設定を使用して [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を有効したとき。  
  
-   前回のデータベースの完全バックアップ以降にログが 1 GB 以上に拡張されている。  
  
-   前回のデータベースの完全バックアップ以降に 1 週間という最大期間が経過している。  
  
-   ログ チェーンが分断されている。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] では、バックアップ ファイルの最初と最後の LSN を比較することで、ログ チェーンが分断されていないかどうかを定期的に確認します。 なんらかの理由でログ チェーンが分断されている場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] はデータベースの完全バックアップをスケジュールします。 ログ チェーンが分断される最も一般的な理由として、Transact-SQL を使用するか SQL Server Management Studio のバックアップ タスクを使用してバックアップ コマンドが実行されていることが考えられます。  その他の一般的なシナリオには、バックアップ ログ ファイルを誤って削除した、バックアップを誤って上書きしたなどがあります。  
  
 **トランザクションログバックアップ:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 次のいずれかに該当する場合にログバックアップをスケジュールします。  
  
-   ログ バックアップの履歴が見つからない。 通常、これは [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を初めて有効にしたときに当てはまります。  
  
-   使用されているトランザクション ログ領域が 5 MB 以上になった。  
  
-   前回のログ バックアップの後に 2 時間という最大期間に達している。  
  
-   トランザクション ログのバックアップがデータベースの完全バックアップより遅れている。 目標は、ログ チェーンが完全バックアップより進んだ状態にしておくことです。  
  
#### <a name="retention-period-settings"></a>保有期間の設定  
 バックアップを有効にするときに、保有期間を日単位で設定する必要があります。最小値は 1 日で、最大値は 30 日です。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は保有期間の設定に基づいて、指定された期間内の特定の時点に復旧できるかどうかを評価し、保持するバックアップ ファイルと削除するバックアップ ファイルを決定します。 保有期間の設定で指定された期間を特定および照合するために、バックアップの backup_finish_date が使用されます。  
  
#### <a name="important-considerations"></a>重要な考慮事項  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]操作への影響を理解するために重要な注意点がいくつかあります。 これらの注意点を次に示します。  
  
-   データベースでは、実行されている既存のデータベースの完全バックアップ ジョブがある場合、 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は現在のジョブが完了するのを待ってから、同じデータベースの完全バックアップをもう一度実行します。 同様に、一度に実行できるトランザクション ログ バックアップは 1 つだけです。 ただし、データベースの完全バックアップとトランザクション ログ バックアップは同時に実行できます。 エラーは、拡張イベントとしてログに記録されます。  
  
-   同時に 10 個を超えるデータベースの完全バックアップがスケジュールされている場合、拡張イベントのデバッグ チャネルを通じて警告が発生します。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] は、バックアップする必要がある残りのデータベースの優先キューを、すべてのバックアップがスケジュールされ完了するまで管理します。  
  
###  <a name="support_limits"></a>サポートの制限事項  
 次に、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に固有の制限事項をいくつか示します。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] エージェントでは、データベースのバックアップ (データベースの完全バックアップとログ バックアップ) のみがサポートされます。  ファイル バックアップの自動化はサポートされません。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の操作は、現在 Transact-SQL を使用してサポートされています。 監視とトラブルシューティングは、拡張イベントを使用して行うことができます。 PowerShell と SMO のサポートは、SQL Server インスタンスのストレージと保有期間の既定の設定を構成すること、および SQL Server のポリシー ベースの管理ポリシーに基づいてバックアップ状態と全体的な正常性を監視することに制限されています。  
  
-   システム データベースはサポートされていません。  
  
-   サポートされている唯一のバックアップストレージオプションは Azure Blob Storage service です。 ディスクまたはテープへのバックアップはサポートされていません。  
  
-   現時点では、Azure Storage のページ Blob で許容される最大ファイルサイズは 1 TB です。 ファイルが 1 TB を超えると、バックアップが失敗します。 この状況を回避するには、大規模なデータベースでは圧縮を使用し、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を設定する前にバックアップ ファイルのサイズをテストしておくことをお勧めします。 テストするには、ローカルディスクにバックアップするか、`BACKUP TO URL` Transact-sql ステートメントを使用して Azure storage に手動でバックアップします。 詳細については、「 [SQL Server Backup to URL](sql-server-backup-to-url.md)」を参照してください。  
  
-   復旧モデル: 完全復旧モデルまたは一括ログ復旧モデルに設定されたデータベースのみがサポートされています。  単純復旧モデルに設定されたデータベースはサポートされていません。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]は、バックアップ、高可用性、またはディザスター リカバリーをサポートする他のテクノロジで構成されている場合にいくつかの制限がある場合があります。 詳細については、「 [Azure へのマネージバックアップの SQL Server: 相互運用性と共存](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
|||  
|-|-|  
|**タスクの説明**|**トピック**|  
|データベースの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成する、インスタンス レベルで既定の設定を構成する、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]をインスタンス レベルまたはデータベース レベルで無効にする、[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を一時停止して再起動するなどの基本的なタスク。|[Azure へのマネージバックアップの SQL Server-保有期間とストレージの設定](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**チュートリアル:** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]を構成および監視する手順について説明します。|[Azure への SQL Server マネージバックアップの設定](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**チュートリアル:** 可用性グループ内のデータベースの [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] を構成および監視する手順について説明します。|[可用性グループのための Azure への SQL Server マネージバックアップの設定](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]の監視に関連するツール、概念、およびタスク。|[Azure への SQL Server マネージバックアップの監視](sql-server-managed-backup-to-microsoft-azure.md)|  
|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]のトラブルシューティングを行うためのツールと手順。|[Azure への管理されたバックアップ SQL Server のトラブルシューティング](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>参照  
 [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [SQL Server Backup TO URL](sql-server-backup-to-url.md)   
 [Azure へのマネージバックアップの SQL Server: 相互運用性と共存](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [Azure への管理されたバックアップ SQL Server のトラブルシューティング](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
