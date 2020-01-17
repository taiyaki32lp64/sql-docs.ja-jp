---
title: SQL Server の機能のサポート |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c39f03a7-e223-4fd7-bd30-142e28f51654
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 660515f10797e1f11fac22c1baf4ed74e9f67c0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157237"
---
# <a name="supported-sql-server-features"></a>サポートされる SQL Server の機能
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の、メモリ最適化オブジェクトの使用に関してサポートされる機能またはサポートされない機能について説明します。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-supported-for-in-memory-oltp"></a>インメモリ OLTP に対してサポートされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能  
 次に示す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、(メモリ最適化ファイル グループを含む) メモリ最適化オブジェクトを持つデータベースでサポートされます。  
  
 サポートされるデータ型の詳細については、「 [Supported Data Types](supported-data-types-for-in-memory-oltp.md)」を参照してください。  
  
-   メモリ最適化テーブルでサポートされるオプションと操作。 詳細については、「[CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)」を参照してください。  
  
-   ネイティブ コンパイル ストアド プロシージャでサポートされるオプションと操作。 詳細については、「[CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)」を参照してください。  
  
-   解釈された [!INCLUDE[tsql](../../../includes/tsql-md.md)] を使用してメモリ最適化テーブルにアクセスする機能。 解釈された [!INCLUDE[tsql](../../../includes/tsql-md.md)] の対象領域は、ネイティブでコンパイルされていないストアド プロシージャおよび [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用してメモリ最適化されていないテーブルにアクセスする場合と同じです。 詳細については、「[解釈された Transact-SQL を使用したメモリ最適化テーブルへのアクセス](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)」を参照してください。  
  
-   複数バージョン管理とオプティミスティック コンカレンシー。 詳細については、「 [Transaction Isolation Levels](../../database-engine/transaction-isolation-levels.md)」をご覧ください。  
  
-   メモリ最適化データ ファイル グループを含むデータベースのバックアップと復元。 詳細については、「 [Back Up and Restore of SQL Server Databases](../backup-restore/back-up-and-restore-of-sql-server-databases.md)」をご覧ください。  
  
-   サポートを実現するためのカタログ ビュー、動的管理ビュー、および拡張イベント。 詳細については、[インメモリ OLTP 向けのシステム ビュー、ストアド プロシージャ、DMV、待機の種類](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)に関するページを参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクト。 詳細については、「[インメモリ OLTP に対する SQL Server 管理オブジェクトのサポート](sql-server-management-objects-support-for-in-memory-oltp.md)」を参照してください。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 詳細については、「[SQL Server Management Studio によるインメモリ OLTP のサポート](sql-server-management-studio-support-for-in-memory-oltp.md)」を参照してください。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell。 詳細については、「 [SQL Server PowerShell の概要](https://msdn.microsoft.com/library/cc281954\(SQL.105\).aspx)」を参照してください。  
  
-   bcp ユーティリティを使用した一括データのインポートとエクスポート。 詳細については、「[bcp ユーティリティを使用した一括データのインポートとエクスポート &#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)」を参照してください。  
  
-   クラッシュ後の復旧。  
  
-   インメモリ OLTP オブジェクトを格納し、目標復旧時間 (RTO) を削減するための、メモリ最適化データ ファイル グループ内の複数のコンテナー。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トランザクション ログ ブロックは、チェックサムを計算し、検証します。  
  
-   新しい SNAPSHOT テーブル ヒント。 詳細については、「[テーブル ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)」を参照してください。  
  
-   DB COMPAT レベル。  
  
-   部分的包含データベース。 Contained database authentication がサポートされます。 ただし、すべてのインメモリ OLTP オブジェクトは、DMV dm_db_uncontained_entities で "breaking containment" とマークされています。  
  
-   サービス ブローカー (制限付き)。 ネイティブ コンパイル ストアド プロシージャからキューにアクセスできません。 メモリ最適化テーブルにアクセスするトランザクションでリモート データベースのキューにアクセスできません。  
  
-   フェールオーバー クラスタ リング:一部として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] AlwaysOn 製品、AlwaysOn フェールオーバー クラスター インスタンスは、サーバー インスタンス レベルではフェールオーバー クラスターでの冗長性によるローカル高可用性を提供する Windows Server フェールオーバー クラスタ リング (WSFC) 機能を活用して。インスタンス (FCI)。 詳細については、「[Always On フェールオーバー クラスター インスタンス (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md)」を参照してください。  
  
-   AlwaysOn との統合: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、サーバーやデータベースの高可用性を実現するために、AlwaysOn などの複数の方法が用意されています。 詳細については、「[高可用性ソリューション &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)」を参照してください。  
  
-   ログ配布:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ配布プライマリ サーバー インスタンスでプライマリ データベースから別のセカンダリ サーバー インスタンスで 1 つまたは複数のセカンダリ データベースにトランザクション ログ バックアップを自動的に送信することができます。 詳細については、「[ログ配布について &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)」を参照してください。  
  
-   サブスクライバー上でのメモリ最適化されたテーブルに対するトランザクション レプリケーションはサポートされていますが、いくつかの制限があります。 詳細については、「[メモリ最適化テーブル サブスクライバーへのレプリケーション](../replication/replication-to-memory-optimized-table-subscribers.md)」を参照してください。  
  
-   リソース ガバナー:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソース ガバナーは、管理に使用できる機能[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ワークロードとシステム リソースの消費します。 リソース ガバナーを使用すると、受信するアプリケーション要求で使用可能な CPU、物理 IO、およびメモリの量に制限を指定できます。 詳細については、「 [Managing Memory for In-Memory OLTP](../../database-engine/managing-memory-for-in-memory-oltp.md) 」および「 [Resource Governor](../resource-governor/resource-governor.md)」を参照してください。  
  
-   インメモリ OLTP には、メモリ最適化テーブルの (var)char 型の列のサポートされているコード ページと、インデックスおよびネイティブ コンパイル ストアド プロシージャで使用されるサポートされている照合順序に関して制限事項があります。 詳細については、「 [Collations and Code Pages](../../database-engine/collations-and-code-pages.md)」を参照してください。  
  
-   BACPAC のサポート。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-features-not-supported-for-in-memory-oltp"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インメモリ OLTP に対してサポートされない機能  
 次に示す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能は、(メモリ最適化データ ファイル グループを含む) メモリ最適化オブジェクトを持つデータベースでサポートされません。  
  
|サポートされない機能|機能の説明|  
|-------------------------|-------------------------|  
|メモリ最適化テーブルに対するデータ圧縮。|データ圧縮機能を使用することにより、データベース内のデータを圧縮したり、データベースのサイズを小さくすることができます。 詳細については、「 [Data Compression](../data-compression/data-compression.md)」を参照してください。|  
|メモリ最適化テーブルと HASH インデックスのパーティション分割。|パーティション テーブルとパーティション インデックスのデータは、データベース内の複数のファイル グループに分散できるように、複数の単位に分割されます。 詳細については、「 [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md)」を参照してください。|  
|データベースのメモリ最適化データ ファイル グループの透過的なデータ暗号化 (TDE)。|透過的なデータ暗号化 (TDE) では、データとログ ファイルの暗号化と暗号化解除がリアルタイムの I/O で実行されます。 詳細については、「[透過的なデータ暗号化 &#40;TDE&#41;](../security/encryption/transparent-data-encryption.md)」を参照してください。<br /><br /> TDE は、インメモリ OLTP オブジェクトを含むデータベースで有効にすることができます。 TDE が有効な場合、インメモリ OLTP ログ レコードが暗号化されます。 持続性のあるテーブルのチェックポイント ファイルは、データベースで TDE が有効になっている場合でも暗号化されません。|  
|レプリケーション|サブスクライバー上でのメモリ最適化されたテーブルに対するトランザクション レプリケーションを除き、他のレプリケーション構成は、メモリ最適化されたテーブルを参照するテーブルまたはビューと互換性がありません。 Sync_mode を使用してレプリケーションを = 'database snapshot' はメモリ最適化ファイル グループがある場合にサポートされていません。 詳細については、「[メモリ最適化テーブル サブスクライバーへのレプリケーション](../replication/replication-to-memory-optimized-table-subscribers.md)」を参照してください。|  
|複数のアクティブな結果セット (MARS)|複数のアクティブな結果セット (MARS) は、メモリ最適化テーブルではサポートされていません。 また、このエラーは、リンク サーバーの使用を示します。 リンク サーバーは MARS を使用できます。 リンク サーバーは、メモリ最適化テーブルでサポートされていません。 代わりに、メモリ最適化テーブルをホストするサーバーとデータベースに直接接続してください。|  
|ミラーリング|データベース ミラーリングは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの可用性を高めるためのソリューションです。 詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。|  
|ログの再構築|ログの再構築は、MEMORY_OPTIMIZED_DATA ファイル グループのデータベースでは、アタッチと ALTER DATABASE のいずれによるものでもサポートされていません。|  
|Linked Server|詳しくは、「[リンク サーバー &#40;データベース エンジン&#41;](../linked-servers/linked-servers-database-engine.md)」を参照してください。|  
|一括ログ記録|データベースの復旧モデルにかかわらず、持続性のあるメモリ最適化テーブル上のすべての操作は、常に完全にログに記録されます。|  
|最小ログ記録|最小ログ記録は、メモリ最適化テーブルではサポートされていません。 最小ログ記録の詳細については、「[トランザクション ログ &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)」および「[一括インポートで最小ログ記録を行うための前提条件](../import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」を参照してください。|  
|変更の追跡|変更の追跡は、インメモリ OLTP オブジェクトを含むデータベースで有効にすることができます。 ただし、メモリ最適化テーブルの変更は追跡されません。|  
|DDL トリガー|インメモリ OLTP テーブルおよびネイティブ コンパイル ストアド プロシージャでは、データベース レベルおよびサーバー レベルの DDL トリガーはどちらもサポートされません。|  
|変更データ キャプチャ (CDC)|DROP などの特定の操作が妨げられるため、インメモリ OLTP オブジェクトが存在するデータベースでは CDC を有効にしないでください。|  
|データベースの包含|データベースの包含は、ネイティブ コンパイル ストアド プロシージャおよびメモリ最適化テーブルを含むデータベースではサポートされません。 詳細については、「 [Contained Databases](../databases/contained-databases.md)」をご覧ください。|  
|コンテキスト接続|CLR ストアド プロシージャ内からのコンテキスト接続を使用したメモリ最適化テーブルへのアクセスはサポートされません。|  
|カーソル|メモリ最適化テーブルにアクセスするクエリでのキーセットと動的カーソル。 これらのクエリは静的クエリに降格され、読み取り専用になります。|  
|TABLESTAMP|TABLESTAMP はサポートされません。 詳細については、「[FROM &#40;Transact-SQL&#41;](/sql/t-sql/queries/from-transact-sql)」を参照してください。|  
|AUTO_CLOSE|AUTO_CLOSE はサポートされません。 詳細については、「 [Set the AUTO_CLOSE Database Option to OFF](../policy-based-management/set-the-auto-close-database-option-to-off.md)」を参照してください。|  
|データベース スナップショット|データベースのスナップショットはサポートされません。 詳細については、「[データベース スナップショット &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md)」を参照してください。|  
|トランザクション DDL。|トランザクション DDL はインメモリ OLTP ではサポートされません。|  
|イベント通知|イベント通知はサポートされません。 詳細については、「 [Event Notifications](../service-broker/event-notifications.md)」を参照してください。|  
|ファイバー モード|ファイバー モードは、インメモリ OLTP ではサポートされていません。|  
|ポリシー ベースの管理 (PBM)。|PBM の "回避" モードと "ログのみ" モードはサポートされません。 サーバーにこのようなポリシーが存在すると、インメモリ OLTP の DDL が正常に実行されないことがあります。 "要求時" モードと "スケジュールで実行" モードはサポートされます。|  
|DACFX 配置/抽出。|DAC F フレームワークの配置/抽出は、インメモリ OLTP ではサポートされません。|  
  
 一部の例外を除き、複数データベースにまたがるトランザクションはサポートされません。 次の表では、サポートされるケースと、対応する制限について説明します (「 [複数データベースにまたがるクエリ](cross-database-queries.md)」も参照してください。)  
  
|データベース|Allowed|説明|  
|---------------|-------------|-----------------|  
|ユーザー データベース、model、および msdb|いいえ|複数のデータベースにまたがるクエリおよびトランザクションはサポートされません。<br /><br /> メモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャにアクセスするクエリおよびトランザクションは、システム データベースの master (読み取り専用アクセス) と tempdb を除き、他のデータベースにアクセスできません。|  
|Resource データベース、および tempdb|はい|シングル ユーザー データベース以外に resource データベースと tempdb のみを使用する複数のデータベースにまたがるトランザクションに関する制限はありません。|  
|master|読み取り専用|インメモリ OLTP と master データベースを使用する複数のデータベースにまたがるトランザクションは、master データベースへの書き込みが含まれる場合にコミットに失敗します。 master に対して読み取り操作のみを実行し、ユーザー データベースを 1 つだけ使用する複数のデータベースにまたがるトランザクションは許可されます。|  
  
## <a name="see-also"></a>関連項目  
 [SQL Server によるインメモリ OLTP のサポート](sql-server-support-for-in-memory-oltp.md)  
  
  
