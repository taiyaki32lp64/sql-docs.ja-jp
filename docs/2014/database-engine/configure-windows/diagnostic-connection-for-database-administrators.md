---
title: データベース管理者用の診断接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 5e8022dd9a7bd4f301ca55f60614e1b13369b804
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62810423"
---
# <a name="diagnostic-connection-for-database-administrators"></a>データベース管理者用の診断接続
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、サーバーへの標準の接続が確立できないときに、管理者向けの特殊な診断接続が用意されています。 診断接続を使用することにより、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が標準の接続要求に応答していない場合でも、管理者は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアクセスして診断クエリを実行し、問題のトラブルシューティングを行うことができるようになります。  
  
 この DAC (専用管理者接続) では、暗号化やその他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のセキュリティ機能がサポートされます。 DAC で実行できるのは、ユーザー コンテキストを別の管理者ユーザーに変更する操作のみです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は DAC の正常な接続を試みますが、極端な状況においては失敗する場合もあります。  
  
||  
|-|  
|**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)、 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。|  
  
## <a name="connecting-with-dac"></a>DAC による接続  
 また、既定では、サーバーで実行されているクライアントからしか接続できません。 [remote admin connections オプション](remote-admin-connections-server-configuration-option.md)を指定した sp_configure ストアド プロシージャを使用して構成しない限り、ネットワーク接続は許可されません。  
  
 DAC を使用して接続できるのは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin ロールのメンバーのみです。  
  
 DAC は、 **sqlcmd** コマンド プロンプト ユーティリティで特殊な管理者スイッチ ( **-A**) を指定することによって使用できます。 **sqlcmd** を使用する方法については、「[sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)」を参照してください。 プレフィックスとして接続することもできます`admin:`形式でインスタンス名に**sqlcmd-sadmin:** _< instance_name >。_ DAC を開始することも、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]に接続してクエリ エディター `admin:` \< *instance_name*>。  
  
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
  
-   DAC では、使用できるリソースが制限されます。 リソースを集中的に消費するクエリ ( 大きなテーブルでの複雑な結合など) や、ブロックされる可能性があるクエリの実行には DAC を使用しないでください。 これは、DAC によって既存のサーバーの問題が悪化するのを防ぐためです。 ブロックする可能性があるクエリを実行しなければならない場合、ブロッキングが発生する状況を回避するには、可能な限りそのクエリをスナップショット ベースの分離レベルで実行します。この分離レベルで実行できない場合は、トランザクションの分離レベルを READ UNCOMMITTED に設定するか、LOCK_TIMEOUT の値を 2,000 ミリ秒などの短い値に設定します。または、両方の設定を行います。 これにより、DAC セッションがブロックされるのを防ぐことができます。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の状態によっては、ラッチで DAC セッションがブロックされることがあります。 Ctrl&lt;/localizedText&gt; キーを押しながら &lt;localizedText&gt;C&lt;/localizedText&gt; キーを押すことによって、DAC セッションを終了できることもありますが、必ず終了されるわけではありません。 このような場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の再起動が唯一の選択肢になります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、DAC による接続とトラブルシューティングを確実に行うために、限定されたリソースを確保して DAC で実行されるコマンドを処理します。 通常、次に示す単純な診断関数とトラブルシューティング関数を実行する場合には、この限定されたリソースだけで十分です。  
  
 理論上は、DAC で並列に実行する必要のない [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントはすべて実行できますが、次の診断コマンドとトラブルシューティング コマンド以外は使用しないことを強くお勧めします。  
  
-   ロックの状態を確認するための sys.dm_tran_locks、キャッシュの使用状況を確認するための sys.dm_os_memory_cache_counters、アクティブなセッションや要求を確認するための sys.dm_exec_requests と sys.dm_exec_sessions など、基本的な診断を行うためのクエリの動的管理ビュー。 リソースを集中的に消費する動的管理ビュー (たとえば、sys.dm_tran_version_store ではバージョン ストアの完全なスキャンが実行され、集中的に I/O が行われる可能性があります) や複雑な結合を使用する動的管理ビューは使用しないようにしてください。 パフォーマンスへの影響に関する詳細については、特定の [動的管理ビュー](../../relational-databases/views/views.md)のリファレンスを参照してください。  
  
-   カタログ ビューのクエリ。  
  
-   DBCC FREEPROCCACHE、DBCC FREESYSTEMCACHE、DBCC DROPCLEANBUFFERS、DBCC SQLPERF などの基本的な DBCC コマンド。`,` **DBCC** CHECKDB、DBCC DBREINDEX、DBCC SHRINKDATABASE などのリソースを集中的に消費するコマンドは実行しないでください。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] KILL *\<spid>* コマンド。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の状態によっては、KILL コマンドは必ずしも成功しません。この場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を再起動するしか方法がありません。 次に一般的なガイドラインをいくつか示します。  
  
    -   `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`というクエリを実行し、SPID が実際に強制終了されたかどうかを確認します。 行が返されなかった場合は、セッションが強制終了されたことを示します。  
  
    -   セッションが依然として確立されている場合は、クエリ `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`を実行して、このセッションに割り当てられたタスクがあるかどうかを確認します。 タスクが存在する場合は、セッションが現在強制終了中である可能性が高くなります。 この処理には非常に長い時間がかかるため、成功しない場合があることに注意してください。  
  
    -   このセッションに関連付けられている sys.dm_os_tasks にタスクが存在しないが、KILL コマンドの実行後に sys.dm_exec_sessions に依然としてセッションが存在する場合は、使用できるワーカーがないことを示します。 現在実行中のタスク ( `sessions_id <> NULL`を指定して sys.dm_os_tasks ビューに一覧されるタスク) のいずれかを選択し、そのタスクに関連付けられているセッションを強制終了して、ワーカーを解放します。 1 つのセッションを強制終了するだけでは不十分で、複数のセッションを強制終了する必要が生じる場合があります。  
  
## <a name="dac-port"></a>DAC ポート  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、TCP ポート 1434 (使用可能な場合) または [!INCLUDE[ssDE](../../includes/ssde-md.md)] の起動時に動的に割り当てられる TCP ポートで DAC をリッスンします。 エラー ログには、DAC がリッスンしているポート番号が含まれています。 既定では、DAC リスナーはローカル ポートでの接続のみを受け入れます。 リモート管理接続をアクティブにするサンプル コードについては、「 [remote admin connections サーバー構成オプション](remote-admin-connections-server-configuration-option.md)」を参照してください。  
  
 リモート管理接続を構成すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動しなくても DAC リスナーが有効になり、クライアントからリモートで DAC に接続できるようになります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答しない場合でも、DAC リスナーを有効にしてリモート接続を受け入れることができます。これを行うには、まず DAC をローカルに使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続してから、sp_configure ストアド プロシージャを実行してリモート接続からの接続を受け入れます。  
  
 クラスター構成では、DAC は既定でオフになります。 ユーザーは、sp_configure の remote admin connection オプションを実行すると、DAC リスナーを有効にしてリモート接続にアクセスできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答せず、DAC リスナーが有効になっていない場合は、DAC で接続するために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動する必要が生じる場合があります。 この理由から、クラスター システムでは remote admin connections 構成オプションを有効にすることをお勧めします。  
  
 DAC ポートは、起動中に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって動的に割り当てられます。 既定のインスタンスに接続する場合、DAC では SQL Server Browser サービスへの SSRP ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol) 要求が使用されません。 まず、TCP ポート 1434 経由で接続が試行されます。 接続が失敗した場合、ポートを取得するために SSRP 呼び出しが実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が SSRP 要求をリッスンしていない場合は、接続要求によってエラーが返されます。 DAC がリッスンしているポート番号を確認するには、エラー ログを参照します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリモート管理接続を受け入れるように構成されている場合、次のように DAC を明示的なポート番号で開始する必要があります。  
  
 **sqlcmd-Stcp:** _\<server>,\<port>_  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログには DAC のポート番号が一覧されます。既定のポート番号は 1434 です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がローカルの DAC 接続のみを受け入れるように構成されている場合は、次のコマンドを実行し、ループバック アダプターを使用して接続します。  
  
 **sqlcmd-S127.0.0.1**,`1434`  
  
## <a name="example"></a>例  
 この例では、管理者がサーバー `URAN123` が応答していないことに気付き、その問題を診断します。 これを行うには、次のように、ユーザーが `sqlcmd` コマンド プロンプト ユーティリティをアクティブにし、DAC であることを示す `URAN123` を指定して、サーバー `-A` に接続します。  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 これで、管理者はクエリを実行して問題を診断し、場合によっては応答していないセッションを終了させることができます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
## <a name="related-content"></a>関連コンテンツ  
 [sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)  
  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
 [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)  
  
 [sp_lock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql)  
  
 [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkalloc-transact-sql)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [DBCC OPENTRAN &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-opentran-transact-sql)  
  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-inputbuffer-transact-sql)  
  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
 [トランザクション関連の動的管理ビューおよび関数  &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql)  
  
 [トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
