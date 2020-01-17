---
title: データベース管理者用の診断接続 | Microsoft Docs
ms.custom: ''
ms.date: 02/27/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a961dc8923d07b9a3036c38d9e0ae05a6b6a6010
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983038"
---
# <a name="diagnostic-connection-for-database-administrators"></a>データベース管理者用の診断接続
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md.md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サーバーへの標準の接続が確立できないときに、管理者向けの特殊な診断接続が用意されています。 診断接続を使用することにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が標準の接続要求に応答していない場合でも、管理者は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアクセスして診断クエリを実行し、問題のトラブルシューティングを行うことができるようになります。  
  
 この DAC (専用管理者接続) では、暗号化やその他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のセキュリティ機能がサポートされます。 DAC で実行できるのは、ユーザー コンテキストを別の管理者ユーザーに変更する操作のみです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は DAC の正常な接続を試みますが、極端な状況においては失敗する場合もあります。  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降)、[!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
## <a name="connecting-with-dac"></a>DAC による接続  
 また、既定では、サーバーで実行されているクライアントからしか接続できません。 [remote admin connections オプション](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)を指定した sp_configure ストアド プロシージャを使用して構成しない限り、ネットワーク接続は許可されません。  
  
 DAC を使用して接続できるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin ロールのメンバーのみです。  
  
 DAC は、 **sqlcmd** コマンド プロンプト ユーティリティで特殊な管理者スイッチ ( **-A**) を指定することによって使用できます。 **sqlcmd** を使用する方法については、「[sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)」を参照してください。 また、**sqlcmd -S admin:<*instance_name*>** という形式で、インスタンス名に **admin:** というプレフィックスを指定して接続することもできます。 また、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] クエリ エディターから **admin:\<*instance_name*>** に接続して DAC を開始することもできます。  
  
## <a name="restrictions"></a>制限  
 DAC の唯一の目的は、ごくまれな状況でサーバーの問題を診断することであるので、この接続には次のようないくつかの制限があります。  
  
-   接続に使用できるリソースを確保するために、DAC は 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスにつき 1 つしか許可されません。 DAC 接続が既にアクティブな場合は、DAC を使用して接続する新たな要求は、エラー 17810 で拒否されます。  
  
-   リソースに限りがあるので、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] はトレース フラグ 7806 を使用して開始されない限り、DAC ポートでリッスンしません。  
  
-   DAC では、まずログインに関連付けられた既定のデータベースへの接続が試行されます。 既定のデータベースに正常に接続されたら、master データベースに接続できます。 既定のデータベースがオフライン状態であるか、または別の原因で使用できない場合、接続の際にエラー 4060 が返されます。 ただし、master データベースへ接続するために、次のコマンドを使用する代わりに既定のデータベースをオーバーライドすると成功します。  
  
     **sqlcmd -A -d master**  
  
     DAC を使用するときは、master データベースに接続することをお勧めします。これは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが起動すると master を使用できることが保証されているためです。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、DAC で複数のクエリやコマンドを並列実行することは禁止されています。 たとえば、DAC で次のいずれかのステートメントを実行すると、エラー 3637 が生成されます。  
  
    -   RESTORE  
  
    -   BACKUP  
  
-   DAC では、使用できるリソースが制限されます。 リソースを集中的に消費するクエリ ( 大きなテーブルでの複雑な結合など) や、ブロックされる可能性があるクエリの実行には DAC を使用しないでください。 これは、DAC によって既存のサーバーの問題が悪化するのを防ぐためです。 ブロックする可能性があるクエリを実行しなければならない場合、ブロッキングが発生する状況を回避するには、可能な限りそのクエリをスナップショット ベースの分離レベルで実行します。この分離レベルで実行できない場合は、トランザクションの分離レベルを READ UNCOMMITTED に設定するか、LOCK_TIMEOUT の値を 2,000 ミリ秒などの短い値に設定します。または、両方の設定を行います。 これにより、DAC セッションがブロックされるのを防ぐことができます。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の状態によっては、ラッチで DAC セッションがブロックされることがあります。 Ctrl キーを押しながら C キーを押して DAC セッションを終了できることがありますが、終了できないこともあります。 このような場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の再起動が唯一の選択肢になります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、DAC による接続とトラブルシューティングを確実に行うために、限定されたリソースを確保して DAC で実行されるコマンドを処理します。 通常、次に示す単純な診断関数とトラブルシューティング関数を実行する場合には、この限定されたリソースだけで十分です。  
  
 理論上は、DAC で並列に実行する必要のない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントはすべて実行できますが、次の診断コマンドとトラブルシューティング コマンド以外は使用しないことを強くお勧めします。  
  
-   基本的な診断を行うための動的管理ビューのクエリ。たとえば、ロックの状態を確認する [sys.dm_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)、キャッシュの正常性を確認する [sys.dm_os_memory_cache_counters](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-counters-transact-sql.md)、アクティブなセッションと要求を確認する [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) と [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) などです。 リソースを集中的に消費する動的管理ビュー (たとえば、[sys.dm_tran_version_store](../../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql.md) ではバージョン ストアの完全なスキャンが実行され、集中的に I/O が行われる可能性があります) や複雑な結合を使用する動的管理ビューは使用しないようにしてください。 パフォーマンスへの影響に関する詳細については、特定の [動的管理ビュー](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)のリファレンスを参照してください。  
  
-   カタログ ビューのクエリ。  
  
-   [DBCC FREEPROCCACHE](../..//t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)、[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)、[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)、[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md) などの基本的な DBCC コマンド。 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)、[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)、[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md) などのリソースを集中的に消費するコマンドは実行しないでください。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] KILL *\<spid>* コマンド。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の状態によっては、KILL コマンドは必ずしも成功しません。この場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動するしか方法がありません。 次に一般的なガイドラインをいくつか示します。  
  
    -   `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`というクエリを実行し、SPID が実際に強制終了されたかどうかを確認します。 行が返されなかった場合は、セッションが強制終了されたことを示します。  
  
    -   セッションが依然として確立されている場合は、クエリ `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`を実行して、このセッションに割り当てられたタスクがあるかどうかを確認します。 タスクが存在する場合は、セッションが現在強制終了中である可能性が高くなります。 この処理には非常に長い時間がかかるため、成功しない場合があることに注意してください。  
  
    -   このセッションに関連付けられている sys.dm_os_tasks にタスクが存在しないが、KILL コマンドの実行後に sys.dm_exec_sessions に依然としてセッションが存在する場合は、使用できるワーカーがないことを示します。 現在実行中のタスク ( `sessions_id <> NULL`を指定して sys.dm_os_tasks ビューに一覧されるタスク) のいずれかを選択し、そのタスクに関連付けられているセッションを強制終了して、ワーカーを解放します。 1 つのセッションを強制終了するだけでは不十分で、複数のセッションを強制終了する必要が生じる場合があります。  
  
## <a name="dac-port"></a>DAC ポート  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、TCP ポート 1434 (使用可能な場合) または [!INCLUDE[ssDE](../../includes/ssde-md.md)] の起動時に動的に割り当てられる TCP ポートで DAC をリッスンします。 [エラー ログ](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)には、DAC がリッスンしているポート番号が含まれています。 既定では、DAC リスナーはローカル ポートでの接続のみを受け入れます。 リモート管理接続をアクティブにするサンプル コードについては、「 [remote admin connections サーバー構成オプション](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)」を参照してください。  
  
 リモート管理接続を構成すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動しなくても DAC リスナーが有効になり、クライアントからリモートで DAC に接続できるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答しない場合でも、DAC リスナーを有効にしてリモート接続を受け入れることができます。これを行うには、まず DAC をローカルに使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続してから、sp_configure ストアド プロシージャを実行してリモート接続からの接続を受け入れます。  
  
 クラスター構成では、DAC は既定でオフになります。 ユーザーは、sp_configure の remote admin connection オプションを実行すると、DAC リスナーを有効にしてリモート接続にアクセスできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答せず、DAC リスナーが有効になっていない場合は、DAC で接続するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要が生じる場合があります。 この理由から、クラスター システムでは remote admin connections 構成オプションを有効にすることをお勧めします。  
  
 DAC ポートは、起動中に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって動的に割り当てられます。 既定のインスタンスに接続する場合、DAC では SQL Server Browser サービスへの SSRP ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol) 要求が使用されません。 まず、TCP ポート 1434 経由で接続が試行されます。 接続が失敗した場合、ポートを取得するために SSRP 呼び出しが実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が SSRP 要求をリッスンしていない場合は、接続要求によってエラーが返されます。 DAC がリッスンしているポート番号を確認するには、エラー ログを参照します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリモート管理接続を受け入れるように構成されている場合、次のように DAC を明示的なポート番号で開始する必要があります。  
  
 **sqlcmd -S tcp:** _\<server>,\<port>_  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログには DAC のポート番号が一覧されます。既定のポート番号は 1434 です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がローカルの DAC 接続のみを受け入れるように構成されている場合は、次のコマンドを実行し、ループバック アダプターを使用して接続します。  
  
 **sqlcmd -S 127.0.0.1,1434**  
  
> [!TIP]  
>  DAC を使用して [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] に接続するときに、-d オプションを使用して接続文字列でデータベース名も指定する必要があります。  
  
## <a name="example"></a>例  
 この例では、管理者がサーバー `URAN123` が応答していないことに気付き、その問題を診断します。 これを行うには、次のように、ユーザーが `sqlcmd` コマンド プロンプト ユーティリティをアクティブにし、DAC であることを示す `URAN123` を指定して、サーバー `-A` に接続します。  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 これで、管理者はクエリを実行して問題を診断し、場合によっては応答していないセッションを終了させることができます。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] の接続に関する類似の例では、-d パラメーターが含まれる次のコマンドを使用してデータベースを指定します。  
  
 `sqlcmd -S serverName.database.windows.net,1434 -U sa -P <xxx> -d AdventureWorks`  
  
## <a name="related-content"></a>関連コンテンツ  
 [sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)  
 [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md)  
 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
 [DBCC OPENTRAN &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
 [トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
  
  

