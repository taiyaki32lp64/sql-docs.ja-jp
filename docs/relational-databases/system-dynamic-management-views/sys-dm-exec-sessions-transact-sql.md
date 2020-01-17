---
title: dm_exec_sessions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_sessions_TSQL
- sys.dm_exec_sessions
- dm_exec_sessions
- sys.dm_exec_sessions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_sessions dynamic management view
ms.assetid: 2b7e8e0c-eea0-431e-819f-8ccd12ec8cfa
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9b5cdba7e82c0432cda81a6e1526e2e039e5676e
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983147"
---
# <a name="sysdm_exec_sessions-transact-sql"></a>sys.dm_exec_sessions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での認証済みセッションごとに 1 行を返します。 sys.dm_exec_sessions は、すべてのアクティブなユーザー接続と内部タスクに関する情報を示すサーバー スコープのビューです。 この情報には、クライアント バージョン、クライアント プログラム名、クライアントのログイン日時、ログイン ユーザー、現在のセッション設定などが含まれます。 sys.dm_exec_sessions を使用して、最初に、現在のシステムの負荷を表示して目的のセッションを特定します。その後、他の動的管理ビューまたは動的管理関数を使用して、そのセッションの詳細を参照します。  
  
 Dm_exec_connections、sys. dm_exec_sessions、および dm_exec_requests の動的管理ビューは、システムテーブルにマップさ[れます。](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)  
  
> **注:** [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] または [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]から呼び出すには、「 **sys. dm_pdw_nodes_exec_sessions**」という名前を使用します。  
  
|列名|データ型|説明とバージョン固有の情報|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|アクティブな各プライマリ接続に関連付けられたセッションを識別します。 NULL 値は許可されません。|  
|login_time|**datetime**|セッションが確立された時刻。 NULL 値は許可されません。|  
|host_name|**nvarchar(128)**|セッション固有のクライアント ワークステーションの名前。 内部セッションの場合、この値は NULL になります。 NULL 値が許可されます。<br /><br /> **セキュリティに関する注意:** クライアントアプリケーションはワークステーション名を提供し、不正確なデータを提供できます。 HOST_NAME はセキュリティ機能としては期待しないでください。|  
|program_name|**nvarchar(128)**|セッションを開始したクライアント プログラムの名前。 内部セッションの場合、この値は NULL になります。 NULL 値が許可されます。|  
|host_process_id|**int**|セッションを開始したクライアント プログラムのプロセス ID。 内部セッションの場合、この値は NULL になります。 NULL 値が許可されます。|  
|client_version|**int**|クライアントでサーバーへの接続に使用されるインターフェイスの TDS プロトコル バージョン。 内部セッションの場合、この値は NULL になります。 NULL 値が許可されます。|  
|client_interface_name|**nvarchar(32)**|クライアントがサーバーとの通信に使用しているライブラリまたはドライバーの名前。 内部セッションの場合、この値は NULL になります。 NULL 値が許可されます。|  
|security_id|**varbinary(85)**|ログインに関連付けられた、Microsoft Windows のセキュリティ ID。 NULL 値は許可されません。|  
|login_name|**nvarchar(128)**|現在セッションを実行している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン名。 セッションを作成した元のログイン名については、original_login_name を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証されたログイン名または Windows 認証済みのドメインユーザー名を指定できます。 NULL 値は許可されません。|  
|nt_domain|**nvarchar(128)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> セッションで Windows 認証または信頼された接続を使用している場合のクライアントの Windows ドメイン。 内部セッションまたはドメイン以外のユーザーの場合、この値は NULL になります。 NULL 値が許可されます。|  
|nt_user_name|**nvarchar(128)**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> セッションで Windows 認証または信頼された接続を使用している場合のクライアントの Windows ユーザー名。 内部セッションまたはドメイン以外のユーザーの場合、この値は NULL になります。 NULL 値が許可されます。|  
|ステータス|**nvarchar(30)**|セッションの状態。 有効値は次のとおりです。<br /><br /> **実行中**-現在1つ以上の要求を実行しています<br /><br /> **休止**中-現在要求を実行していません<br /><br /> **休止**セッションは接続プールによってリセットされ、現在はログイン前状態になっています。<br /><br /> **Preconnect** -Session は Resource Governor 分類子にあります。<br /><br /> NULL 値は許可されません。|  
|context_info|**varbinary (128)**|セッションの CONTEXT_INFO 値。 コンテキスト情報は、 [set CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md)ステートメントを使用してユーザーによって設定されます。 NULL 値が許可されます。|  
|cpu_time|**int**|セッションで使用された CPU 時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|memory_usage|**int**|セッションで使用されたメモリの 8 KB ページの数。 NULL 値は許可されません。|  
|total_scheduled_time|**int**|セッション (セッション内にある要求) の実行予定時間の合計 (ミリ秒単位)。 NULL 値は許可されません。|  
|total_elapsed_time|**int**|セッションが確立されてから経過した時間 (ミリ秒単位)。 NULL 値は許可されません。|  
|endpoint_id|**int**|セッションに関連付けられたエンドポイント ID。 NULL 値は許可されません。|  
|last_request_start_time|**datetime**|セッションで要求が最後に開始された時刻。 現在実行されている要求も対象となります。 NULL 値は許可されません。|  
|last_request_end_time|**datetime**|セッションで要求が最後に完了した時刻。 NULL 値が許可されます。|  
|reads|**bigint**|セッション中に、セッションの要求によって実行された読み取りの数。 NULL 値は許可されません。|  
|writes|**bigint**|セッション中に、セッションの要求によって実行された書き込みの数。 NULL 値は許可されません。|  
|logical_reads|**bigint**|このセッションで実行された論理読み取りの数。 NULL 値は許可されません。|  
|is_user_process|**bit**|セッションがシステム セッションの場合は 0。 それ以外の場合は 1 です。 NULL 値は許可されません。|  
|text_size|**int**|セッションの TEXTSIZE 設定。 NULL 値は許可されません。|  
|language|**nvarchar(128)**|セッションの LANGUAGE 設定。 NULL 値が許可されます。|  
|date_format|**nvarchar(3)**|セッションの DATEFORMAT 設定。 NULL 値が許可されます。|  
|date_first|**smallint**|セッションの DATEFIRST 設定。 NULL 値は許可されません。|  
|quoted_identifier|**bit**|セッションの QUOTED_IDENTIFIER 設定。 NULL 値は許可されません。|  
|arithabort|**bit**|セッションの ARITHABORT 設定。 NULL 値は許可されません。|  
|ansi_null_dflt_on|**bit**|セッションの ANSI_NULL_DFLT_ON 設定。 NULL 値は許可されません。|  
|ansi_defaults|**bit**|セッションの ANSI_DEFAULTS 設定。 NULL 値は許可されません。|  
|ansi_warnings|**bit**|セッションの ANSI_WARNINGS 設定。 NULL 値は許可されません。|  
|ansi_padding|**bit**|セッションの ANSI_PADDING 設定。 NULL 値は許可されません。|  
|ansi_nulls|**bit**|セッションの ANSI_NULLS 設定。 NULL 値は許可されません。|  
|concat_null_yields_null|**bit**|セッションの CONCAT_NULL_YIELDS_NULL 設定。 NULL 値は許可されません。|  
|transaction_isolation_level|**smallint**|セッションのトランザクション分離レベル。<br /><br /> 0 = Unspecified<br /><br /> 1 = ReadUncomitted<br /><br /> 2 = ReadCommitted<br /><br /> 3 = Repeatable<br /><br /> 4 = Serializable<br /><br /> 5 = Snapshot<br /><br /> NULL 値は許可されません。|  
|lock_timeout|**int**|セッションの LOCK_TIMEOUT 設定。 値の単位はミリ秒です。 NULL 値は許可されません。|  
|deadlock_priority|**int**|セッションの DEADLOCK_PRIORITY 設定。 NULL 値は許可されません。|  
|row_count|**bigint**|セッションでこの時点までに返された行の数。 NULL 値は許可されません。|  
|prev_error|**int**|セッションで最後に返されたエラーの ID。 NULL 値は許可されません。|  
|original_security_id|**varbinary(85)**|original_login_name に関連付けられている [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows セキュリティ ID。 NULL 値は許可されません。|  
|original_login_name|**nvarchar(128)**|クライアントがこのセッションの作成に使用した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン名。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証済みのログイン名、Windows 認証済みのドメイン ユーザー名、または包含データベースのユーザーになります。 最初の接続後、セッションでは暗黙的または明示的にコンテキストが切り替えられている可能性があります。 たとえば、 [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)が使用されているとします。 NULL 値は許可されません。|  
|last_successful_logon|**datetime**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> 現在のセッションが開始する前に、original_login_name のログオンが最後に成功した時間。|  
|last_unsuccessful_logon|**datetime**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> 現在のセッションが開始する前に、original_login_name のログオン試行が最後に失敗した時間。|  
|unsuccessful_logons|**bigint**|**適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。<br /><br /> last_successful_logon と login_time の間に、original_login_name のログオン試行が失敗した回数。|  
|group_id|**int**|このセッションが属しているワークロード グループの ID。 NULL 値は許可されません。|  
|database_id|**smallint**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> 各セッションの現在のデータベースの ID。|  
|authenticating_database_id|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> プリンシパルを認証するデータベースの ID。 ログインの場合、値は 0 になります。 包含データベース ユーザーの場合、値は包含データベースのデータベース ID になります。|  
|open_transaction_count|**int**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。<br /><br /> セッションごとに開いているトランザクションの数。|  
|pdw_node_id|**int**|**適用対象**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> このディストリビューションが配置されているノードの識別子。|  
|page_server_reads|**bigint**|**適用対象**: Azure SQL Database ハイパースケール<br /><br /> このセッション中に、このセッションの要求によって実行されたページサーバーの読み取り回数。 NULL 値は許可されません。|  
  
## <a name="permissions"></a>アクセス許可  
すべてのユーザーが独自のセッション情報を見ることができます。  
**[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]:** サーバー上のすべてのセッションを表示するには、[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] に対する `VIEW SERVER STATE` 権限が必要です。  
**[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]:** 現在のデータベースへのすべての接続を表示するには、`VIEW DATABASE STATE` が必要です。 `master` データベースで `VIEW DATABASE STATE` を許可することはできません。 
  
  
## <a name="remarks"></a>Remarks  
 [ **Common criteria 準拠を有効に**する] サーバー構成オプションを有効にすると、次の列にログオンの統計情報が表示されます。  
  
-   last_successful_logon  
  
-   last_unsuccessful_logon  
  
-   unsuccessful_logons  
  
 このオプションが有効でない場合、これらの列は NULL 値を返します。 このサーバー構成オプションを設定する方法の詳細については、「 [common criteria コンプライアンスが有効になっているサーバー構成オプション](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)」を参照してください。  
 
 
 Azure SQL Database の管理者接続には、認証されたセッションごとに1行が表示されます。 Resultset に表示される "sa" セッションは、セッションのユーザークォータには影響しません。 管理者以外の接続では、データベースユーザーセッションに関連する情報のみが表示されます。
 
  
## <a name="relationship-cardinalities"></a>リレーションシップの基数  
  
|From|変換先|基準/APPLY|[リレーションシップ]|  
|----------|--------|---------------|------------------|  
|sys.dm_exec_sessions|[sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)|session_id|一対ゼロまたは一対多|  
|sys.dm_exec_sessions|[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)|session_id|一対ゼロまたは一対多|  
|sys.dm_exec_sessions|[sys.dm_tran_session_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)|session_id|一対ゼロまたは一対多|  
|sys.dm_exec_sessions|[dm_exec_cursors](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cursors-transact-sql.md)(session_id &#124; 0)|session_id CROSS APPLY<br /><br /> OUTER APPLY|一対ゼロまたは一対多|  
|sys.dm_exec_sessions|[sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)|session_id|一対一|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-finding-users-that-are-connected-to-the-server"></a>A. サーバーに接続しているユーザーを検索する  
 次の例では、サーバーに接続しているユーザーを検索し、各ユーザーのセッション数を返します。  
  
```sql  
SELECT login_name ,COUNT(session_id) AS session_count   
FROM sys.dm_exec_sessions   
GROUP BY login_name;  
```  
  
### <a name="b-finding-long-running-cursors"></a>b. 長時間実行されているカーソルを検索する  
 次の例では、特定の期間よりも長く開いているカーソル、カーソルの作成者、およびカーソルが配置されているセッションを検索します。  
  
```sql  
USE master;  
GO  
SELECT creation_time ,cursor_id   
    ,name ,c.session_id ,login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s   
   ON c.session_id = s.session_id   
WHERE DATEDIFF(mi, c.creation_time, GETDATE()) > 5;  
```  
  
### <a name="c-finding-idle-sessions-that-have-open-transactions"></a>C. トランザクションが開いているアイドル状態のセッションを検索する  
 次の例では、トランザクションが開いているアイドル状態のセッションを検索します。 アイドル状態のセッションとは、現在要求が実行されていないセッションです。  
  
```sql  
SELECT s.*   
FROM sys.dm_exec_sessions AS s  
WHERE EXISTS   
    (  
    SELECT *   
    FROM sys.dm_tran_session_transactions AS t  
    WHERE t.session_id = s.session_id  
    )  
    AND NOT EXISTS   
    (  
    SELECT *   
    FROM sys.dm_exec_requests AS r  
    WHERE r.session_id = s.session_id  
    );  
```  
  
### <a name="d-finding-information-about-a-queries-own-connection"></a>D. クエリ専用接続についての情報を検索する  
 クエリ専用接続についての情報を収集する典型的なクエリ。  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  



