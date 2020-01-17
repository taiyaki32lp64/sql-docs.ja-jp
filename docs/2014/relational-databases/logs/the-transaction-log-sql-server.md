---
title: トランザクション ログ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], about
- databases [SQL Server], transaction logs
- logs [SQL Server], transaction logs
ms.assetid: d7be5ac5-4c8e-4d0a-b114-939eb97dac4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1b4a175ad850ccbb0711a0997c3658cf01497686
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144618"
---
# <a name="the-transaction-log-sql-server"></a>トランザクション ログ (SQL Server)
  すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにはトランザクション ログがあり、データベース内のすべてのトランザクションとそれらのトランザクションによって加えられた変更が記録されます。 トランザクション ログは、いっぱいにならないように、定期的に切り捨てる必要があります。 ただし、いくつかの要因によってログの切り捨てが遅れる可能性があるため、ログのサイズを監視することは重要です。 一部の操作は、トランザクション ログのサイズへの影響を軽減するためにログへの記録を最小限に抑えることができます。  
  
 トランザクション ログはデータベースの重要なコンポーネントの 1 つであり、システム障害が発生すると、データベースを一貫性のある状態にするために求められる場合があります。 結果がどのようになるかを完全に把握できる場合を除き、トランザクション ログを削除または移動しないでください。  
  
> [!NOTE]  
>  データベース復旧時にトランザクション ログの適用を開始する既知の最適なポイントがチェックポイントによって作成されます。 詳細については、「[データベース チェックポイント &#40;SQL Server&#41;](database-checkpoints-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   [利点:トランザクション ログでサポートされる操作](#Benefits)  
  
-   [トランザクション ログの切り捨て](#Truncation)  
  
-   [ログの切り捨てが遅れる要因](#FactorsThatDelayTruncation)  
  
-   [最小ログ記録操作](#MinimallyLogged)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="Benefits"></a> 利点:トランザクション ログによりサポートされる操作  
 トランザクション ログでは、次の操作がサポートされます。  
  
-   個別のトランザクションの復旧  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に未完了だったすべてのトランザクションの復旧  
  
-   復元したデータベース、ファイル、ファイル グループ、またはページの障害時点までのロールフォワード  
  
-   トランザクション レプリケーションのサポート  
  
-   高可用性およびディザスター リカバリー ソリューションのサポート: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]、データベース ミラーリング、およびログ配布  
  
##  <a name="Truncation"></a> トランザクション ログの切り捨て  
 ログの切り捨てによりログ ファイルの領域が解放され、トランザクション ログで再利用できるようになります。 ログの切り捨ては、ログがいっぱいにならないようにするために不可欠です。 ログの切り捨てでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの論理トランザクション ログから非アクティブな仮想ログ ファイルが削除されます。また、論理ログの領域が解放され、物理トランザクション ログで再利用できるようになります。 トランザクション ログが切り捨てられなければ、物理ログ ファイルに割り当てられているディスク上の領域がいっぱいになってしまいます。  
  
 この問題を回避するために、何かの理由でログの切り捨てが遅れている場合を除き、次のイベントの後に切り捨てが自動的に発生します。  
  
-   単純復旧モデルでは、チェックポイント以降。  
  
-   完全復旧モデルまたは一括ログ復旧モデルでは、前回のバックアップ後にチェックポイントが発生した場合、ログ バックアップ (コピーのみのログ バックアップの場合を除く) の後に切り捨てが発生します。  
  
 詳細については、このトピックの「 [ログの切り捨てが遅れる原因となる要因](#FactorsThatDelayTruncation)」を参照してください。  
  
> [!NOTE]  
>  ログの切り捨てを行っても、物理ログ ファイルのサイズは縮小されません。 物理ログ ファイルの物理サイズを削減するには、ログ ファイルを圧縮する必要があります。 物理ログ ファイルのサイズの圧縮の詳細については、「 [トランザクション ログ ファイルのサイズの管理](manage-the-size-of-the-transaction-log-file.md)」を参照してください。  
  
##  <a name="FactorsThatDelayTruncation"></a> ログの切り捨てが遅れる要因  
 ログ レコードが長い間アクティブなままになると、トランザクション ログの切り捨てが遅れて、トランザクション ログがいっぱいになる可能性があります。  
  
> [!IMPORTANT]  
>  トランザクション ログがいっぱいに応答する方法については、「 [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)」を参照してください。  
  
 ログの切り捨ては、さまざまな要因で遅延が発生する場合があります。 ログの切り捨てを妨げている原因は、 **sys.databases** カタログ ビューの **log_reuse_wait** 列と [log_reuse_wait_desc](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列に対するクエリを実行して見つけることができます。 次の表では、これらの列の値について説明します。  
  
|log_reuse_wait の値|log_reuse_wait_desc の値|Description|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|現在 1 つ以上の再利用可能な仮想ログ ファイルがある。|  
|1|CHECKPOINT|最後にログの切り捨てを行ってからチェックポイントが発生していないか、ログの先頭が仮想ログ ファイルを超えて移動していない (すべての復旧モデル)。<br /><br /> これは、ログの切り捨てが遅れる一般的な原因です。 詳細については、「[データベース チェックポイント &#40;SQL Server&#41;](database-checkpoints-sql-server.md)」を参照してください。|  
|2|LOG_BACKUP|トランザクション ログを切り捨てる前にログ バックアップが必要である (完全復旧モデルまたは一括ログ復旧モデルのみ)。<br /><br /> 次のログ バックアップが完了した時点で、ログ領域の一部が再利用可能になります。|  
|3|ACTIVE_BACKUP_OR_RESTORE|データ バックアップまたは復元が実行中である (すべての復旧モデル)。<br /><br /> データ バックアップによってログの切り捨てが妨げられる場合、バックアップ操作を取り消すと、当面の問題には対処できます。|  
|4|ACTIVE_TRANSACTION|トランザクションがアクティブである (すべての復旧モデル)。<br /><br /> 実行時間の長いトランザクションがログ バックアップの先頭に存在する可能性がある。 この場合、領域を解放するには再度ログ バックアップが必要になります。 実行時間の長いトランザクションがログの切り捨てがこのトランザクション ログが一般に切り捨てられます自動チェックポイントのたびに、単純復旧モデルを含む、すべての復旧モデルを防ぐことに注意してください。<br /><br /> トランザクションが遅延している。 *遅延トランザクション* は、一部リソースが確保できないためにロールバックがブロックされている、実質的にはアクティブなトランザクションです。 遅延トランザクションの原因、およびトランザクションの遅延を解決する方法については、「[遅延トランザクション &#40;SQL Server&#41;](../backup-restore/deferred-transactions-sql-server.md)」を参照してください。 <br /><br />実行時間の長いトランザクションも、tempdb のトランザクション ログをいっぱいにする可能性があります。 tempdb は、並べ替えの作業テーブル、ハッシュの作業ファイル、カーソル作業テーブル、行のバージョン管理といった、内部オブジェクトに対するユーザー トランザクションで暗黙的に使用されます。 ユーザー トランザクションには、(SELECT クエリ) のデータの読み取りのみが含まれている場合でも、内部オブジェクトが作成され、ユーザー トランザクションで使用する可能性があります。 その結果 tempdb のトランザクション ログがいっぱいになる可能性があります。|  
|5|DATABASE_MIRRORING|データベース ミラーリングが一時中断されるか、高パフォーマンス モードでは、ミラー データベースがプリンシパル データベースに大幅に遅れる (完全復旧モデルのみ)。<br /><br /> 詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。|  
|6|REPLICATION|トランザクション レプリケーション中、パブリケーションに関連するトランザクションがディストリビューション データベースにまだ配信されていない (完全復旧モデルのみ)。<br /><br /> トランザクション レプリケーションの詳細については、「 [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md)」を参照してください。|  
|7|DATABASE_SNAPSHOT_CREATION|データベース スナップショットが作成されている (すべての復旧モデル)。<br /><br /> これは、通常、短い時間ログの切り捨てが遅れる一般的な原因となります。|  
|8|LOG_SCAN|ログ スキャンが行われている (すべての復旧モデル)。<br /><br /> これは、通常、短い時間ログの切り捨てが遅れる一般的な原因となります。|  
|9|AVAILABILITY_REPLICA|可用性グループのセカンダリ レプリカが、このデータベースのトランザクション ログ レコードを対応するセカンダリ データベースに適用中である (完全復旧モデル)。<br /><br /> 詳細については、次を参照してください。 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)します。|  
|10|-|内部使用のみ|  
|11|-|内部使用のみ|  
|12|-|内部使用のみ|  
|13|OLDEST_PAGE|データベースが間接的なチェックポイントを使用するように構成されている場合、データベース上の最も古いページはチェックポイントの LSN よりも古くなることがある。 この場合、最も古いページのログの切り捨てが遅れる可能性があります (すべての復旧モデル)。<br /><br /> 間接的なチェックポイントの詳細については、「 [Database Checkpoints &#40;SQL Server&#41;](database-checkpoints-sql-server.md)」を参照してください。|  
|14|OTHER_TRANSIENT|この値は現在使用されていません。|  
|16|XTP_CHECKPOINT|データベースにメモリ最適化ファイル グループがある場合は、自動 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] チェックポイントがトリガーされるまで (これはログが 512 MB 増加するたびに発生します)、トランザクション ログは切り捨てられません。<br /><br /> 注:512 MB のサイズになる前に、トランザクション ログを切り捨てるには、対象のデータベースに対して手動で Checkpoint コマンドを起動します。|  
  
##  <a name="MinimallyLogged"></a> 最小ログ記録操作  
 *最小ログ記録* では、トランザクションの復旧に必要な情報だけが記録されます。特定の時点への復旧はサポートしません。 このトピックでは、一括ログ復旧モデルで (バックアップが実行されていない場合は単純復旧モデルで) 最小ログが記録される操作について説明します。  
  
> [!NOTE]  
>  最小ログ記録は、メモリ最適化テーブルではサポートされていません。  
  
> [!NOTE]  
>  完全復旧モデルでは、すべての一括操作が完全にログに記録されます。 ただし、一括操作のためにデータベースを一時的に一括ログ復旧モデルに切り替えることで、一連の一括操作用のログ記録を最小限に抑えることができます。 最小ログ記録は、完全ログ記録より効率的であり、一括トランザクションの実行中に、使用可能なトランザクション ログ領域が大規模な一括操作でいっぱいになる可能性を低減します。 ただし、最小ログ記録が有効なときにデータベースが破損または消失した場合は、データベースを障害発生時点まで復旧できません。  
  
 次に示す操作は、完全復旧モデルで完全にログ記録されますが、単純復旧モデルと一括ログ復旧モデルでは最小限にしかログ記録されません。  
  
-   一括インポート操作 ([bcp](../../tools/bcp-utility.md)、[BULK INSERT](/sql/t-sql/statements/bulk-insert-transact-sql)、[INSERT...SELECT](/sql/t-sql/statements/insert-transact-sql))。 テーブルへの一括インポートの最小ログ記録の詳細については、「 [Prerequisites for Minimal Logging in Bulk Import](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」を参照してください。  
  
    > [!NOTE]  
    >  トランザクション レプリケーションが有効な場合、BULK INSERT 操作は、一括ログ復旧モデルでも完全にログ記録されます。  
  
-   SELECT [INTO](/sql/t-sql/queries/select-into-clause-transact-sql) 操作。  
  
    > [!NOTE]  
    >  トランザクション レプリケーションが有効な場合、SELECT INTO 操作は、一括ログ復旧モデルでも完全にログ記録されます。  
  
-   新規データの挿入時または追加時の、 [UPDATE](/sql/t-sql/queries/update-transact-sql) ステートメントの .WRITE 句を使用した、大きな値のデータ型の部分更新。 既存の値を更新する場合は、最小ログ記録は使用されません。 大きな値のデータ型の詳細については、「[データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)」を参照してください。  
  
-   [WRITETEXT](/sql/t-sql/queries/writetext-transact-sql)と[UPDATETEXT](/sql/t-sql/queries/updatetext-transact-sql)ステートメントを挿入またはに新しいデータを追加するとき、 `text`、 `ntext`、および`image`データ型の列。 既存の値を更新する場合は、最小ログ記録は使用されません。  
  
    > [!NOTE]  
    >  WRITETEXT ステートメントおよび UPDATETEXT ステートメントは非推奨とされます。新しいアプリケーションでは、これらを使用しないようにしてください。  
  
-   データベースが単純復旧モデルまたは一括ログ復旧モデルに設定されている場合、一部のインデックス DDL 操作は、オフラインで実行されても、オンラインで実行されても、最小ログ記録の対象になります。 最小ログ記録が行われるインデックス操作は、次のとおりです。  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql) 操作 (インデックス付きビューを含む)。  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql) REBUILD 操作または DBCC DBREINDEX 操作。  
  
        > [!NOTE]  
        >  DBCC DBREINDEX ステートメントは非推奨とされます。新しいアプリケーションでは、これを使用しないようにしてください。  
  
    -   DROP INDEX による新しいヒープの再構築 (適用可能な場合)。  
  
        > [!NOTE]  
        >  [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql) 操作中のインデックス ページの割り当て解除は、常に完全にログ記録されます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 `Managing the transaction log`  
  
-   [トランザクション ログ ファイルのサイズの管理](manage-the-size-of-the-transaction-log-file.md)  
  
-   [満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
 **トランザクション ログのバックアップ (完全復旧モデル)**  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
 **トランザクション ログの復元 (完全復旧モデル)**  
  
-  [トランザクション ログ バックアップを復元します。](../backup-restore/restore-a-transaction-log-backup-sql-server.md)   
  
## <a name="see-also"></a>参照  
 [トランザクションの持続性の制御](control-transaction-durability.md)   
 [一括インポートで最小ログ記録を行うための前提条件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [SQL Server データベースのバックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [データベース チェックポイント &#40;SQL Server&#41;](database-checkpoints-sql-server.md)   
 [データベースのプロパティの表示または変更](../databases/view-or-change-the-properties-of-a-database.md)   
 [復旧モデル &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)  
  
  
