---
title: データ変更の追跡
ms.custom: seo-dt-2019
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], compared to change tracking
- change data capture vs. change tracking
- change data capture [SQL Server], data type behaviors
- Sync Services for ADO.NET
- change tracking [SQL Server], Sync Services for ADO.NET
- change tracking [SQL Server]
- change data capture [SQL Server], security
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7a34be46-15b4-4b6b-8497-cfd8f9f14234
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 94f5ccf6d7983a25bb8cafe084dbca103f966255
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095426"
---
# <a name="track-data-changes-sql-server"></a>データ変更の追跡 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベースのデータに対する変更を追跡する [変更データ キャプチャ](#Capture) および [変更の追跡](#Tracking)という 2 つの機能が用意されています。 これらの機能では、データベース内のユーザー テーブルに対して行われた DML の変更 (挿入操作、更新操作、および削除操作) をアプリケーションで特定できます。 変更データ キャプチャと変更の追跡は、同じデータベースに対して有効にすることができます。特別な配慮は必要ありません。 変更データ キャプチャと変更の追跡をサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションについては、「 [SQL Server 2016 の各エディションでサポートされる機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。 変更の追跡は [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]でサポートされています。 変更データ キャプチャは、SQL Server および Azure SQL Database Managed Instance でのみサポートされています。
  
## <a name="benefits-of-using-change-data-capture-or-change-tracking"></a>変更データ キャプチャまたは変更の追跡を使用する利点  
 データベースで変更されたデータをクエリする機能は、一部のアプリケーションの効率を高めるための重要な要件です。 一般に、データ変更を確認するには、アプリケーション開発者がトリガー、timestamp 列、および追加のテーブルを組み合わせて使用することで、カスタムの追跡方法をアプリケーションに実装する必要があります。 通常、このようなアプリケーションを作成するには実装に非常に手間がかかり、スキーマの更新も必要になり、多くの場合、パフォーマンスのオーバーヘッドが増加します。  
  
 カスタム ソリューションを開発する代わりに、アプリケーションで変更データ キャプチャまたは変更の追跡を使用してデータベースでの変更を追跡すると、次のような利点があります。  
  
-   開発時間が短縮されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で使用可能な機能により、カスタム ソリューションを開発する必要はありません。  
  
-   スキーマの変更が不要 削除された行を追跡するため、または変更追跡情報を格納するため (列をユーザー テーブルに追加できない場合) に列の追加、トリガーの追加、またはサイド テーブルの作成を行う必要がありません。  
  
-   組み込みのクリーンアップ メカニズムがあります。 変更の追跡のクリーンアップは、バックグラウンドで自動的に実行されます。 サイド テーブルに格納されるデータのカスタム クリーンアップは必要ありません。  
  
-   変更情報を取得するための関数が用意されています。  
  
-   DML 操作のオーバーヘッドが低減します。 同期変更追跡では、オーバーヘッドが常に若干発生します。 しかし、変更の追跡を使用すると、オーバーヘッドを最小限に抑えることができます。 多くの場合、オーバーヘッドは、代わりのソリューション (特にトリガーを使用する必要があるソリューション) を使用する場合よりも少なくなります。  
  
-   コミットされたトランザクションに基づいた変更の追跡 変更の順序は、トランザクションのコミット時間に基づきます。 このため、実行時間の長いトランザクションや重複するトランザクションが存在する場合でも、信頼性が高い結果を取得できます。 **timestamp** 値を使用するカスタム ソリューションは、このようなシナリオに対処するように特別に設計する必要があります。  
  
-   構成および管理に使用できる標準的なツールがあります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 標準の DDL ステートメント、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、カタログ ビュー、およびセキュリティ権限を利用できます。  
  
## <a name="feature-differences-between-change-data-capture-and-change-tracking"></a>変更データ キャプチャと変更の追跡の機能の違い  
 次の表に、変更データ キャプチャと変更の追跡の機能の違いを示します。 変更データ キャプチャの追跡メカニズムでは、非同期キャプチャによりトランザクション ログから変更がキャプチャされ、DML 操作後に変更を利用できます。 変更の追跡の追跡メカニズムでは、同期追跡により DML 操作に即して変更が追跡され、すぐに変更情報を利用できます。  
  
|機能|変更データ キャプチャ|変更の追跡|  
|-------------|-------------------------|---------------------|  
|**追跡される変更**|||  
|DML の変更|はい|はい|  
|**追跡される情報**|||  
|履歴データ|はい|いいえ|  
|列が変更されたかどうか|はい|はい|  
|DML 型|はい|はい|  
  
##  <a name="Capture"></a> Change Data Capture  
 変更データ キャプチャでは、DML の変更が行われたという事実と変更された実際のデータの両方がキャプチャされ、ユーザー テーブルの変更情報の履歴が提供されます。 変更は、非同期プロセスを使用してトランザクション ログを読み取ることによってキャプチャされます。これは、システムへの影響が少ない方法です。  
  
 次の図に示すように、ユーザー テーブルに対して行われた変更は、対応する変更テーブルにキャプチャされます。 これらの変更テーブルには、時間の経過に伴う変更の履歴が表示されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の[変更データ キャプチャ](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)関数を使用して、変更データを簡単かつ体系的に利用できます。  
  
 ![変更データ キャプチャの概念図](../../relational-databases/track-changes/media/cdcart1.gif "変更データ キャプチャの概念図")  
  
### <a name="security-model"></a>セキュリティ モデル  
 ここでは、変更データ キャプチャのセキュリティ モデルについて説明します。  
  
 **構成と管理**  
 データベースで変更データ キャプチャを有効または無効にするには、[sys.sp_cdc_enable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) または [sys.sp_cdc_disable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) の呼び出し元が固定サーバー ロール **sysadmin** のメンバーである必要があります。 テーブル レベルで変更データ キャプチャを有効または無効にするには、[sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md) および [sys.sp_cdc_disable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md) の呼び出し元が sysadmin ロールのメンバーか **database db_owner** データベース ロールのメンバーである必要があります。  
  
 変更データ キャプチャ ジョブの管理をサポートするストアド プロシージャを使用できるのは、サーバー **sysadmin** ロールのメンバー、および **database db_owner** ロールのメンバーに制限されます。  
  
 **変更の列挙とメタデータ クエリ**  
 キャプチャ インスタンスに関連付けられた変更データにアクセスするには、関連付けられたソース テーブルのすべてのキャプチャ対象列に対する選択アクセスがユーザーに許可されている必要があります。 また、キャプチャ インスタンスの作成時にゲーティング ロールが指定されている場合、呼び出し元は、指定されたゲーティング ロールのメンバーである必要もあります。 メタデータにアクセスするためのその他の一般的な変更データ キャプチャ関数には、public ロールですべてのデータベース ユーザーがアクセスできます。ただし、通常は、返されるメタデータへのアクセスも、基になるソース テーブルに対する選択アクセス、および定義されたすべてのゲーティング ロールのメンバーシップに基づいて制限されます。  
  
 **変更データ キャプチャが有効になっているソース テーブルに対する DDL 操作**  
 テーブルで変更データ キャプチャが有効になっているときにテーブルに DDL 操作を適用できるのは、固定サーバー ロール **sysadmin**のメンバー、 **database role db_owner**のメンバー、または **database role db_ddladmin**のメンバーのみです。 テーブルに対する DDL 操作の実行が明示的に許可されているユーザーがこれらの操作を実行しようとすると、エラー 22914 が返されます。  
  
### <a name="data-type-considerations-for-change-data-capture"></a>変更データ キャプチャのデータ型に関する考慮事項  
 基本的な列の種類はすべて変更データ キャプチャでサポートされています。 次の表では、さまざまな列の型の動作と制限について説明します。  
  
|列の種類|変更テーブルで変更をキャプチャする|制限事項|  
|--------------------|---------------------------------------|-----------------|  
|スパース列|はい|columnset を使用する場合は変更のキャプチャをサポートしません。|  
|計算列|いいえ|計算列に対する変更は追跡されません。 列は適切な種類の変更テーブルに表示されますが、値は NULL になります。|  
|XML|はい|個々の XML 要素に対する変更は追跡されません。|  
|timestamp|はい|変更テーブル内のデータ型はバイナリに変換されます。|  
|BLOB データ型|はい|BLOB 列の前の画像は、列自体が変更された場合にのみ保存されます。|  
  
### <a name="change-data-capture-and-other-sql-server-features"></a>変更データ キャプチャとその他の SQL Server 機能  
 ここでは、次の機能と変更データ キャプチャとの連携について説明します。  
  
-   データベース ミラーリング  
  
-   トランザクション レプリケーション  
  
-   データベースの復元またはアタッチ  
  
#### <a name="database-mirroring"></a>データベース ミラーリング  
 変更データ キャプチャが有効になっているデータベースをミラー化できます。 ミラーでキャプチャとクリーンアップが自動的に行われるようにするには、次の手順を実行します。  
  
1.  ミラーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていることを確認します。  
  
2.  プリンシパルがミラーにフェールオーバーした後、ミラーでキャプチャ ジョブとクリーンアップ ジョブを作成します。 ジョブを作成するには、ストアド プロシージャ [sys.sp_cdc_add_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql.md) を使用します。  

 データベース ミラーリングの詳細については、「[データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)」を参照してください。  
  
#### <a name="transactional-replication"></a>トランザクション レプリケーション  
 変更データ キャプチャとトランザクション レプリケーションは、同じデータベースで共存できます。ただし、両方の機能が有効になっている場合、変更テーブルが異なる方法で作成されます。 変更データ キャプチャとトランザクション レプリケーションでは、トランザクション ログから変更を読み取る際に、常に同じプロシージャ ( [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)) が使用されます。 変更データ キャプチャのみが有効になっている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブによって **sp_replcmds**が呼び出されます。 同じデータベースで両方の機能が有効になっている場合は、ログ リーダー エージェントによって **sp_replcmds**が呼び出されます。 このエージェントは、変更テーブルとディストリビューション データベース テーブルの両方を作成します。 詳細については、「 [Replication Log Reader Agent](../../relational-databases/replication/agents/replication-log-reader-agent.md)」を参照してください。  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで変更データ キャプチャが有効になっており、2 つのテーブルでキャプチャが有効になっているシナリオについて考えてみます。 変更テーブルを作成するために、キャプチャ ジョブによって **sp_replcmds**が呼び出されます。 データベースでトランザクション レプリケーションが有効になり、パブリケーションが作成されます。 次に、ログ リーダー エージェントがデータベースに対して作成され、キャプチャ ジョブが削除されます。 ログ リーダー エージェントは、変更テーブルにコミットされた最後のログ シーケンス番号からログのスキャンを続行します。 これにより、変更テーブル内のデータの一貫性が確保されます。 このデータベースでトランザクション レプリケーションが無効になっている場合、ログ リーダー エージェントが削除され、キャプチャ ジョブが再作成されます。  
  
> [!NOTE]  
>  変更データ キャプチャとトランザクション レプリケーションの両方でログ リーダー エージェントを使用している場合、レプリケートされた変更が最初にディストリビューション データベースに書き込まれます。 次に、キャプチャされた変更が変更テーブルに書き込まれます。 両方の操作は同時にコミットされます。 ディストリビューション データベースへの書き込みの際に遅延が生じた場合、変更テーブルに変更が表示される前に、それに対応する遅延が発生します。  
  
#### <a name="restoring-or-attaching-a-database-enabled-for-change-data-capture"></a>変更データ キャプチャが有効になっているデータベースの復元またはアタッチ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベースが復元またはアタッチされた後に変更データ キャプチャを有効のままにするかどうかを、次のロジックに従って判断します。  
  
-   データベースを同じサーバーに同じデータベース名で復元した場合、変更データ キャプチャは有効のままです。  
  
-   データベースを別のサーバーに復元した場合、既定では変更データ キャプチャが無効になり、関連するメタデータがすべて削除されます。  
  
     変更データ キャプチャを保持するには、データベースを復元する際に **KEEP_CDC** オプションを使用します。 このオプションの詳細については、「 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。  
  
-   データベースをデタッチしてから、同じサーバーまたは別のサーバーにアタッチした場合、変更データ キャプチャは有効のままです。  
  
-   **KEEP_CDC** オプションを使用してデータベースを Standard または Enterprise 以外のエディションにアタッチまたは復元しようとすると、操作がブロックされます。これは変更データ キャプチャを使用するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard または Enterprise Edition が必要であるためです。 エラー メッセージ 932 が表示されます。  
  
     `SQL Server cannot load database '%.*ls' because change data capture is enabled. The currently installed edition of SQL Server does not support change data capture. Either disable change data capture in the database by using a supported edition of SQL Server, or upgrade the instance to one that supports change data capture.`  
  
 [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) を使用すると、復元またはアタッチされたデータベースから変更データ キャプチャを削除できます。  
  
##  <a name="Tracking"></a> Change Tracking  
 変更の追跡では、テーブル内の行が変更されたという事実がキャプチャされますが、変更されたデータはキャプチャされません。 この機能を使用すると、変更された行をアプリケーションで特定し、最新の行データについてはユーザー テーブルから直接取得することができます。 したがって、変更の追跡で確認できる履歴の情報は変更データ キャプチャと比較すると限定されますが、 変更データがキャプチャされないため、履歴情報が必要ではないアプリケーションではストレージ オーバーヘッドがはるかに少なくて済みます。 変更は、同期追跡メカニズムを使用して追跡されます。 これは、DML 操作のオーバーヘッドを最小限に抑えるように設計されています。  
  
 次の図は、変更の追跡を使用すると効果的な同期のシナリオを示しています。 このシナリオのアプリケーションでは、テーブルの前回の同期後に変更されたすべてのテーブル行の現在の行データのみが必要です。 同期メカニズムを使用して変更が追跡されるため、アプリケーションで双方向同期を実行して、発生する可能性がある競合を確実に検出できます。  
  
 ![変更の追跡の概念図](../../relational-databases/track-changes/media/cdcart2.gif "変更の追跡の概念図")  
  
### <a name="change-tracking-and-sync-services-for-adonet"></a>変更の追跡と Sync Services for ADO.NET  
 [!INCLUDE[sql_sync_long](../../includes/sql-sync-long-md.md)] データベース間の同期が可能になり、直感的で柔軟性の高い API を使用して、オフラインおよびコラボレーションのシナリオを対象とするアプリケーションを構築できます。 [!INCLUDE[sql_sync_long](../../includes/sql-sync-long-md.md)] 変更を同期する API が用意されていますが、この API ではサーバーまたはピア データベース内の変更は実際には追跡されません。 カスタム変更追跡システムを作成できますが、一般に複雑さやパフォーマンスのオーバーヘッドが大幅に増加します。 サーバーまたはピア データベースの変更を追跡するには、構成が簡単でパフォーマンスの高い追跡を実現できる [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の変更の追跡を使用することをお勧めします。  
  
 変更の追跡と [!INCLUDE[sql_sync_long](../../includes/sql-sync-long-md.md)]の詳細については、以下のリンクを参照してください。  
  
-   [変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
     変更の追跡について説明します。変更の追跡のしくみについて概要を示し、変更の追跡が [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のその他の機能とどのように連携するかを説明します。  
  
-   [Microsoft Sync Framework デベロッパー センター](https://go.microsoft.com/fwlink/?LinkId=108054)  
  
     [!INCLUDE[ssSyncFrameLong](../../includes/sssyncframelong-md.md)] および [!INCLUDE[sql_sync_short](../../includes/sql-sync-short-md.md)]に関する完全なドキュメントが用意されています。 [!INCLUDE[sql_sync_short](../../includes/sql-sync-short-md.md)] のドキュメントのトピック「How to:Use SQL Server Change Tracking」(方法: SQL Server 変更の追跡を使用する) には、詳細な情報とコードの例が掲載されています。  
  
## <a name="related-tasks-required"></a>関連タスク (必須)  
  
|||  
|-|-|  
|**タスク**|**トピック**|  
|変更データ キャプチャの概要を示します。|[変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)|  
|データベースまたはテーブルに対して変更データ キャプチャを有効または無効にする方法について説明します。|[変更データ キャプチャの有効化と無効化 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)|  
|変更データ キャプチャを管理および監視する方法について説明します。|[変更データ キャプチャの管理と監視 &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)|  
|変更データ キャプチャのコンシューマーが使用できる変更データを操作する方法について説明します。 LSN の下限と上限の検証、クエリ関数、およびクエリ関数のシナリオについて説明します。|[変更データの処理 &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)|  
|変更の追跡の概要を示します。|[変更の追跡について &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)|  
|データベースまたはテーブルに対して変更の追跡を有効または無効にする方法について説明します。|[変更の追跡の有効化と無効化 &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md)|  
|変更の追跡を管理する方法、セキュリティを構成する方法、および変更の追跡を使用する場合のストレージとパフォーマンスへの影響を判断する方法について説明します。|[変更の追跡の管理 &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)|  
|変更の追跡を使用するアプリケーションが、追跡した変更を取得し、その変更を別のデータ ストアに適用して、ソース データベースを更新する方法について説明します。 また、フェールオーバーが発生してデータベースをバックアップから復元する必要がある場合に、変更の追跡が果たす役割についても説明します。|[変更の追跡のしくみ &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md)|  
  
## <a name="see-also"></a>参照  
 [変更データ キャプチャの関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [変更追跡関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [変更データ キャプチャ ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)   
 [変更データ キャプチャのテーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/change-data-capture-tables-transact-sql.md)   
 [変更データ キャプチャに関連した動的管理ビュー &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)  
  
  

