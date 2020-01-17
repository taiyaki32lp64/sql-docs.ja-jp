---
title: トランザクション ログ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2019
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: cd975ed830f9a0b705e516707d550697fbf34325
ms.sourcegitcommit: 93012fddda7b778be414f31a50c0f81fe42674f4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/26/2019
ms.locfileid: "75493586"
---
# <a name="the-transaction-log-sql-server"></a>トランザクション ログ (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースにはトランザクション ログがあり、データベース内のすべてのトランザクションとそれらのトランザクションによって加えられた変更が記録されます。
  
トランザクション ログは、データベースの重要なコンポーネントです。 システム障害がある場合、データベースを一貫性のある状態に戻すには、そのログが必要になります。 

トランザクション ログのアーキテクチャと内部構造の詳細については、「[SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)」を参照してください。

> [!WARNING] 
> もたらされる影響を完全に理解していない限り、このログを削除または移動しないでください。 

> [!TIP]
> データベース復旧時にトランザクション ログの適用を開始する既知の最適なポイントがチェックポイントによって作成されます。 詳細については、「[Database Checkpoints (SQL Server)](../../relational-databases/logs/database-checkpoints-sql-server.md)」 (データベース チェックポイント (SQL Server)) をご覧ください。  
  
## <a name="operations-supported-by-the-transaction-log"></a>トランザクション ログによりサポートされる操作  
 トランザクション ログでは、次の操作がサポートされます。  
  
-   個別のトランザクションの復旧  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に未完了だったすべてのトランザクションの復旧 
-   復元したデータベース、ファイル、ファイル グループ、またはページの障害時点までのロールフォワード  
-   トランザクション レプリケーションのサポート  
-   高可用性およびディザスター リカバリー ソリューションのサポート: [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]、データベース ミラーリング、およびログ配布

### <a name="individual-transaction-recovery"></a>個別のトランザクションの復旧
アプリケーションで `ROLLBACK` ステートメントが実行されるか、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] でクライアントとの通信の喪失などのエラーが検出された場合、未完了のトランザクションによって加えられた変更をロールバックするために、ログ レコードが使用されます。 

### <a name="recovery-of-all-incomplete-transactions-when-includessnoversionincludesssnoversion-mdmd-is-started"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に未完了だったすべてのトランザクションの復旧
サーバーに障害が起きると、データベースは一部の変更がバッファー キャッシュからデータ ファイルに書き込まれない状態になる場合があり、未完了のトランザクションによる変更がデータ ファイル内に存在している可能性もあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは、起動時に各データベースの復旧を行います。 ログに記録されていて、データ ファイルに書き込まれなかった可能性があるすべての変更は、ロールフォワードされます。 その後、トランザクション ログに記録されている未完了のトランザクションは、データベースの整合性を確保するために、すべてロールバックされます。 詳細については、「[復元と復旧の概要 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)」を参照してください。

### <a name="rolling-a-restored-database-file-filegroup-or-page-forward-to-the-point-of-failure"></a>復元したデータベース、ファイル、ファイル グループ、またはページの障害時点までのロールフォワード
ハードウェアの故障やディスク障害などによりデータベース ファイルが影響を受けた場合、そのデータベースを障害が発生した時点まで復元できます。 まずデータベースの最新の完全バックアップまたは差分バックアップを復元し、次にその後の一連のトランザクション ログ バックアップを障害が発生した時点まで復元します。 

各ログのバックアップを復元するときに、ログに記録されている変更が [!INCLUDE[ssde_md](../../includes/ssde_md.md)] により再適用されて、すべてのトランザクションがロールフォワードされます。 最後のログのバックアップが復元されると、[!INCLUDE[ssde_md](../../includes/ssde_md.md)] により、ログ情報を使用して、その時点で完了していなかったすべてのトランザクションがロールバックされます。 詳細については、「[復元と復旧の概要 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)」を参照してください。

### <a name="supporting-transactional-replication"></a>トランザクション レプリケーションのサポート
ログ リーダー エージェントは、トランザクション レプリケーション用に構成された各データベースのトランザクション ログを監視し、レプリケーションのマークが付けられたトランザクションをトランザクション ログからディストリビューション データベースにコピーします。 詳しくは、「 [トランザクション レプリケーションの動作方法](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms151706(v=sql.105))」をご覧ください。

### <a name="supporting-high-availability-and-disaster-recovery-solutions"></a>高可用性とディザスター リカバリー ソリューションのサポート
スタンバイ サーバー ソリューション、[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]、データベース ミラーリング、およびログ配布は、トランザクション ログに大きく依存しています。 

**[!INCLUDE[ssHADR](../../includes/sshadr-md.md)] シナリオ**では、データベース (プライマリ レプリカ) に対するすべての更新は、別に存在するデータベースの完全なコピー (セカンダリ レプリカ) で直ちに再現されます。 プライマリ レプリカにより各ログ レコードが直ちにセカンダリ レプリカに送信されます。そこでは、受信したログ レコードが可用性グループのデータベースに適用され、継続的にロールフォワードされます。 詳しくは、「 [AlwaysOn フェールオーバー クラスター インスタンス](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」をご覧ください。

**ログ配布シナリオ**では、プライマリ データベースのアクティブなトランザクション ログがプライマリ サーバーから 1 つ以上の配布先に送信されます。 各セカンダリ サーバーでは、受信したログがローカルのセカンダリ データベースに復元されます。 詳しくは、「 [ログ配布について](../../database-engine/log-shipping/about-log-shipping-sql-server.md)」をご覧ください。 

**データベース ミラーリング シナリオ**では、プリンシパル データベースに対するすべての更新が、そのデータベースの完全なコピーである、独立したミラー データベースに直ちに再現されます。 各ログ レコードは、プリンシパル サーバー インスタンスからミラー サーバー インスタンスに直ちに送信されます。ここでは、受信したログ レコードがミラー データベースに適用され、継続的にロールフォワードされます。 詳しくは、「 [データベース ミラーリング](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」をご覧ください。

##  <a name="Characteristics"></a>トランザクション ログの特性
[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のトランザクション ログには、次のような特性があります。 
-  トランザクション ログは、データベース内に別個のファイルまたはファイル セットとして実装されます。 ログ キャッシュはデータ ページ用のバッファー キャッシュとは別に管理され、単純かつ高速の、堅牢なコードとして[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に実装されています。 詳細については、「[トランザクション ログの物理アーキテクチャ](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch)」を参照してください。

-  ログのレコードとページの形式は、データ ページの形式に従うように制約はされません。

-  トランザクション ログは、複数のファイルとして実装できます。 ログの `FILEGROWTH` 値を設定することで、これらのファイルが自動的に拡張されるように定義できます。 これにより、トランザクション ログが領域不足になる可能性が減り、同時に管理のオーバーヘッドも減少します。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41; の File および Filegroup オプション](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)」を参照してください。

-  ログ ファイル内の領域を再利用するメカニズムは高速で、トランザクションのスループットに及ぼす影響も最小限で済みます。

トランザクション ログのアーキテクチャと内部構造の詳細については、「[SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)」を参照してください。

##  <a name="Truncation"></a> トランザクション ログの切り捨て  
ログの切り捨てによりログ ファイルの領域が解放され、トランザクション ログで再利用できるようになります。 トランザクション ログの定期的な切り捨ては、ログがいっぱいにならないようにするために不可欠です。 いくつかの要因によってログの切り捨てが遅れる可能性があるため、ログのサイズを監視することは重要です。 一部の操作は、トランザクション ログのサイズへの影響を軽減するためにログへの記録を最小限に抑えることができます。  
 
ログの切り捨てでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの論理トランザクション ログから非アクティブな[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) が削除されます。これにより、論理ログの領域が解放され、物理トランザクション ログで再利用できるようになります。 トランザクション ログが切り捨てられなければ、物理ログ ファイルに割り当てられているディスク上の領域がいっぱいになってしまいます。  
  
領域が足りなくなるのを回避するために、何かの理由でログの切り捨てが遅れている場合を除き、次のイベントの後に切り捨てが自動的に発生します。  
  
- 単純復旧モデルでは、チェックポイント以降。  
- 完全復旧モデルまたは一括ログ復旧モデルでは、前回のバックアップ後にチェックポイントが発生した場合、ログ バックアップ (コピーのみのログ バックアップの場合を除く) の後に切り捨てが発生します。  
  
 詳細については、このトピックの「[ログの切り捨てが遅れる原因となる要因](#FactorsThatDelayTruncation)」を参照してください。  
  
> [!NOTE]
> ログの切り捨てを行っても、物理ログ ファイルのサイズは縮小されません。 物理ログ ファイルの物理サイズを削減するには、ログ ファイルを圧縮する必要があります。 物理ログ ファイルのサイズの圧縮の詳細については、「 [トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)」を参照してください。  
> ただし、[ログの切り捨てが遅れる原因となる要因](#FactorsThatDelayTruncation)には留意してください。 ログの圧縮後、ストレージ領域が再び必要になると、トランザクション ログが再び増え、その分のパフォーマンスのオーバーヘッドが発生します。
  
##  <a name="FactorsThatDelayTruncation"></a> Factors that can delay log truncation  
 このトピックで前述したように、ログ レコードが長い間アクティブなままになると、トランザクション ログの切り捨てが遅れて、トランザクション ログがいっぱいになります。  
  
> [!IMPORTANT]
> トランザクション ログがいっぱいに応答する方法については、「 [Troubleshoot a Full Transaction Log &#40;SQL Server Error 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)」を参照してください。  
  
 実際に、ログの切り捨てはさまざまな理由で遅延が発生する場合があります。 ログの切り捨てを妨げている原因を、[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) カタログ ビューの **log_reuse_wait** 列と **log_reuse_wait_desc** 列に対するクエリを実行して確認してください。 次の表では、これらの列の値について説明します。  
  
|log_reuse_wait の値|log_reuse_wait_desc の値|[説明]|  
|----------------------------|----------------------------------|-----------------|  
|0|NOTHING|現在 1 つ以上の再利用可能な[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) がある。|  
|1|CHECKPOINT|最後にログの切り捨てを行ってからチェックポイントが発生していないか、ログの先頭が[仮想ログ ファイル (VLF)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) を超えて移動していない。 (すべての復旧モデル)。<br /><br /> これは、ログの切り捨てが遅れる一般的な原因です。 詳細については、「[データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)」を参照してください。|  
|2|LOG_BACKUP|トランザクション ログを切り捨てる前にログ バックアップが必要である (完全復旧モデルまたは一括ログ復旧モデルのみ)。<br /><br /> 次のログ バックアップが完了した時点で、ログ領域の一部が再利用可能になります。|  
|3|ACTIVE_BACKUP_OR_RESTORE|データ バックアップまたは復元が実行中である (すべての復旧モデル)。<br /><br /> データ バックアップによってログの切り捨てが妨げられる場合、バックアップ操作を取り消すと、当面の問題には対処できます。|  
|4|ACTIVE_TRANSACTION|トランザクションがアクティブである (すべての復旧モデル):<br /><br /> 実行時間の長いトランザクションがログ バックアップの先頭に存在する可能性がある。 この場合、領域を解放するには再度ログ バックアップが必要になります。 単純復旧モデルを含むすべての復旧モデルでは、実行時間の長いトランザクションによってログの切り捨てが妨げられます。この場合、通常は自動チェックポイントのたびにトランザクション ログが切り捨てられます。<br /><br /> トランザクションが遅延している。 *遅延トランザクション* は、一部リソースが確保できないためにロールバックがブロックされている、実質的にはアクティブなトランザクションです。 遅延トランザクションの原因、およびトランザクションの遅延を解決する方法については、「[遅延トランザクション &#40;SQL Server&#41;](../../relational-databases/backup-restore/deferred-transactions-sql-server.md)」を参照してください。<br /> <br /> 実行時間の長いトランザクションも、tempdb のトランザクション ログをいっぱいにする可能性があります。 tempdb は、並べ替えの作業テーブル、ハッシュの作業ファイル、カーソル作業テーブル、行のバージョン管理といった、内部オブジェクトに対するユーザー トランザクションで暗黙的に使用されます。 ユーザー トランザクションにデータ読み取り (`SELECT`クエリ) だけが含まれる場合でも、ユーザー トランザクションで内部オブジェクトが作成され使用されることがあります。 その結果 tempdb のトランザクション ログがいっぱいになる可能性があります。|  
|5|DATABASE_MIRRORING|データベース ミラーリングが一時中断されるか、高パフォーマンス モードでは、ミラー データベースがプリンシパル データベースに大幅に遅れる (完全復旧モデルのみ)。<br /><br /> 詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。|  
|6|レプリケーション|トランザクション レプリケーション中、パブリケーションに関連するトランザクションがディストリビューション データベースにまだ配信されていない (完全復旧モデルのみ)。<br /><br /> トランザクション レプリケーションの詳細については、「 [SQL Server Replication](../../relational-databases/replication/sql-server-replication.md)」を参照してください。|  
|7|DATABASE_SNAPSHOT_CREATION|データベース スナップショットが作成されている (すべての復旧モデル)。<br /><br /> これは、通常、短い時間ログの切り捨てが遅れる一般的な原因となります。|  
|8|LOG_SCAN|ログ スキャンが行われている (すべての復旧モデル)。<br /><br /> これは、通常、短い時間ログの切り捨てが遅れる一般的な原因となります。|  
|9|AVAILABILITY_REPLICA|可用性グループのセカンダリ レプリカが、このデータベースのトランザクション ログ レコードを対応するセカンダリ データベースに適用中である (完全復旧モデル)。<br /><br /> 詳細については、「 [Always On 可用性グループの概要 &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)」を参照してください。|  
|10|-|内部使用のみ|  
|11|-|内部使用のみ|  
|12|-|内部使用のみ|  
|13|OLDEST_PAGE|データベースが間接的なチェックポイントを使用するように構成されている場合、データベース上の最も古いページはチェックポイントの[ログ シーケンス番号 (LSN)](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#Logical_Arch) よりも古くなることがある。 この場合、最も古いページのログの切り捨てが遅れる可能性があります (すべての復旧モデル)。<br /><br /> 間接的なチェックポイントの詳細については、「 [Database Checkpoints &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)」を参照してください。|  
|14|OTHER_TRANSIENT|この値は現在使用されていません。|  
|16|XTP_CHECKPOINT|インメモリ OLTP チェックポイントを実行する必要があります。メモリ最適化されたテーブルの場合、前回のチェックポイント以後、トランザクション ログ ファイルが 1.5 GB を超えると (ディスクベースのテーブルとメモリ最適化されたテーブルの両方を含む)、自動チェックポイントが取得されます。<br /> 詳細については、「[メモリ最適化テーブルのチェックポイント操作](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md)」と「インメモリ最適化されたテーブルのログ記録とチェックポイント」 (https://blogs.msdn.microsoft.com/sqlcat/2016/05/20/logging-and-checkpoint-process-for-memory-optimized-tables-2/) を参照してください。
  
##  <a name="MinimallyLogged"></a> 最小ログ記録が可能な操作  
*最小ログ記録* では、トランザクションの復旧に必要な情報だけが記録されます。特定の時点への復旧はサポートしません。 このトピックでは、一括ログ [復旧モデル](../backup-restore/recovery-models-sql-server.md) で (バックアップが実行されていない場合は単純復旧モデルで) 最小ログが記録される操作について説明します。  
  
> [!NOTE]
> 最小ログ記録は、メモリ最適化テーブルではサポートされていません。  
  
> [!NOTE]
> 完全 [復旧モデル](../backup-restore/recovery-models-sql-server.md)では、すべての一括操作が完全にログに記録されます。 ただし、一括操作のためにデータベースを一時的に一括ログ復旧モデルに切り替えることで、一連の一括操作用のログ記録を最小限に抑えることができます。 最小ログ記録は、完全ログ記録より効率的であり、一括トランザクションの実行中に、使用可能なトランザクション ログ領域が大規模な一括操作でいっぱいになる可能性を低減します。 ただし、最小ログ記録が有効なときにデータベースが破損または消失した場合は、データベースを障害発生時点まで復旧できません。  
  
 次に示す操作は、完全復旧モデルで完全にログ記録されますが、単純復旧モデルと一括ログ復旧モデルでは最小限にしかログ記録されません。  
  
-   一括インポート操作 ([bcp](../../tools/bcp-utility.md)、[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)、[INSERT...SELECT](../../t-sql/statements/insert-transact-sql.md))。 テーブルへの一括インポートの最小ログ記録の詳細については、「 [Prerequisites for Minimal Logging in Bulk Import](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」を参照してください。  
  
トランザクション レプリケーションが有効な場合、`BULK INSERT` 操作は、一括ログ復旧モデルでも完全にログ記録されます。  
  
-   [SELECT INTO](../../t-sql/queries/select-into-clause-transact-sql.md) 操作。  
  
トランザクション レプリケーションが有効な場合、`SELECT INTO` 操作は、一括ログ復旧モデルでも完全にログ記録されます。  
  
-   新規データの挿入時または追加時の、[UPDATE](../../t-sql/queries/update-transact-sql.md) ステートメントの `.WRITE` 句を使用した、大きな値のデータ型の部分更新。 既存の値を更新する場合は、最小ログ記録は使用されません。 大きな値のデータ型の詳細については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」を参照してください。  
  
-   [text](../../t-sql/queries/writetext-transact-sql.md) 、 [ntext](../../t-sql/queries/updatetext-transact-sql.md) 、 **image**の各データ型列に新規データを挿入または追加するときの **WRITETEXT**ステートメントおよび **UPDATETEXT** ステートメント。 既存の値を更新する場合は、最小ログ記録は使用されません。  
  
    > [!WARNING]
    > `WRITETEXT` ステートメントおよび `UPDATETEXT` ステートメントの使用は**非推奨となりました**。新しいアプリケーションでは、これらを使用しないようにしてください。  
  
-   データベースが単純復旧モデルまたは一括ログ復旧モデルに設定されている場合、一部のインデックス DDL 操作は、オフラインで実行されても、オンラインで実行されても、最小ログ記録の対象になります。 最小ログ記録が行われるインデックス操作は、次のとおりです。  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md) 操作 (インデックス付きビューを含む)。  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) REBUILD 操作または DBCC DBREINDEX 操作。  
  
        > [!WARNING]
        > `DBCC DBREINDEX` ステートメントは**非推奨となりました**。新しいアプリケーションでは使用しないようにしてください。  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) による新しいヒープの再構築 (適用可能な場合)。 `DROP INDEX` 操作中のインデックス ページの割り当て解除は、**常に**完全にログ記録されます。
  
##  <a name="RelatedTasks"></a> 関連タスク  
**トランザクション ログの管理**  
  
-   [トランザクション ログ ファイルのサイズの管理](../../relational-databases/logs/manage-the-size-of-the-transaction-log-file.md)  
  
-   [満杯になったトランザクション ログのトラブルシューティング &#40;SQL Server エラー 9002&#41;](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
**トランザクション ログのバックアップ (完全復旧モデル)**  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  

-   [データベースが破損したときのトランザクション ログのバックアップ (SQL Server)](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)

**トランザクション ログの復元 (完全復旧モデル)**  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>参照  
[SQL Server トランザクション ログのアーキテクチャと管理ガイド](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)   
[トランザクションの持続性の制御](../../relational-databases/logs/control-transaction-durability.md)   
[一括インポートで最小ログ記録を行うための前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
[SQL Server データベースのバックアップと復元](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)     
[復元と復旧の概要 (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery)      
[データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
[データベースのプロパティの表示または変更](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md)   
[復旧モデル &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)    
[sys.dm_db_log_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)  
[sys.dm_db_log_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)    
  
  
