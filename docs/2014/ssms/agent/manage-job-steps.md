---
title: ジョブ ステップの管理 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job steps [SQL Server replication]
- job steps [SQL Server Agent]
- jobs [SQL Server Agent], Integration Services package step
- executable programs as job steps
- operating systems [SQL Server], job steps
- Transact-SQL job step
- job steps [Transact-SQL]
- Integration Services packages, job steps
- replication job steps [SQL Server]
- logs [SQL Server], jobs
- SQL Server Agent jobs, job steps
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: 51352afc-a0a4-428b-8985-f9e58bb57c31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 27dfa9f596d63021eb5f22b2e0b25a306e7fa2b5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798222"
---
# <a name="manage-job-steps"></a>ジョブ ステップの管理
  ジョブ ステップは、ジョブがデータベースまたはサーバーで行う処理です。 すべてのジョブには、最低 1 つのジョブ ステップを含める必要があります。 ジョブ ステップには次のような種類があります。  
  
-   実行可能プログラムまたはオペレーティング システムのコマンド。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント。ストアド プロシージャと拡張ストアド プロシージャを含みます。  
  
-   PowerShell スクリプト。  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX スクリプト。  
  
-   レプリケーション タスク。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] タスク。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ。  
  
 各ジョブ ステップは特定のセキュリティ コンテキストで実行されます。 ジョブ ステップがプロキシを指定している場合、このジョブ ステップは指定されたプロキシの資格情報のセキュリティ コンテキストで実行されます。 ジョブ ステップがプロキシを指定していない場合、このジョブ ステップは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントのコンテキストで実行されます。 プロキシを明示的に指定せずにジョブを作成できるのは、sysadmin 固定サーバー ロールのメンバーのみです。  
  
 ジョブ ステップは特定の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザーのコンテキストで実行されるので、ユーザーには、ジョブ ステップの実行に必要なアクセス許可と構成が必要です。 たとえば、ドライブ文字または汎用名前付け規則 (UNC) パスを必要とするようなジョブを作成した場合、タスクのテスト時にはジョブ ステップを作成者の Windows ユーザー アカウントで実行していることがあります。 ところが、このジョブ ステップの Windows ユーザーにも、このジョブ ステップを実行するためのアクセス許可、ドライブ文字構成、指定ドライブへのアクセスが必要になります。 そうでなければ、このジョブ ステップは失敗します。 この問題を回避するには、各ジョブ ステップのプロキシに、ジョブ ステップで実行するタスクに対して必要なアクセス許可が設定されていることを確認してください。 詳細については、「 [SQL Server データベースエンジンと Azure SQL Database の Security Center](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)」を参照してください。  
  
## <a name="job-step-logs"></a>ジョブ ステップのログ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、オペレーティング システム ファイルまたは msdb データベースの sysjobstepslogs テーブルに、一部のジョブ ステップからの出力を書き込むことができます。 両方の出力先に出力を書き込めるジョブ ステップの種類は次のとおりです。  
  
-   実行可能プログラムまたはオペレーティング システムのコマンド。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントのいずれでもサポートされません。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] タスク。  
  
 ジョブ ステップの出力をオペレーティング システム ファイルに書き込めるのは、sysadmin 固定サーバー ロールのメンバーであるユーザーが実行するジョブ ステップのみです。 ジョブ ステップを実行するユーザーが、msdb データベースの SQLAgentUserRole 固定データベース ロール、SQLAgentReaderRole 固定データベース ロール、または SQLAgentOperatorRole 固定データベース ロールのメンバーである場合、ジョブ ステップの出力は sysjobstepslogs テーブルにのみ書き込むことができます。  
  
 ジョブ ステップのログは、ジョブまたはジョブ ステップが削除されると自動的に削除されます。  
  
> [!NOTE]  
>  レプリケーション タスクと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのジョブ ステップのログ記録は、それぞれのサブシステムによって処理されます。 これらのタイプのジョブ ステップについては、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用してジョブ ステップのログ記録を構成することはできません。  
  
## <a name="executable-programs-and-operating-system-commands-as-job-steps"></a>ジョブ ステップとしての実行可能プログラムとオペレーティング システム コマンド  
 実行可能プログラムとオペレーティング システム コマンドは、ジョブ ステップとして使用できます。 これらのファイルの拡張子は、.bat、.cmd、.com、または .exe です。  
  
 実行可能プログラムまたはオペレーティング システム コマンドをジョブ ステップとして使用する場合は、次の項目を指定する必要があります。  
  
-   コマンドが正常に終了した場合に返されるプロセス終了コード。  
  
-   実行するコマンド。 オペレーティング システム コマンドを実行する場合、これはコマンド自体を指します。 外部プログラムの場合は、 **C:\Program Files\Microsoft SQL Server\100\Tools\Binn\sqlcmd.exe -e -q "sp_who"** など、プログラム名とそのプログラムの引数を指します。  
  
    > [!NOTE]  
    >  システム パスまたはジョブ ステップの実行ユーザーのパスで指定されたディレクトリ内に、実行可能ファイルが存在しない場合は、実行可能ファイルの完全パスを指定する必要があります。  
  
## <a name="transact-sql-job-steps"></a>Transact-SQL ジョブ ステップ  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップを作成するには、次の操作を行う必要があります。  
  
-   ジョブを実行するデータベースを特定します。  
  
-   実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを入力します。 このステートメントで、ストアド プロシージャまたは拡張ストアド プロシージャを呼び出すことができます。  
  
 必要に応じて、ジョブ ステップのコマンドとして既存の [!INCLUDE[tsql](../../includes/tsql-md.md)] ファイルを開くことができます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシを使用しません。 このジョブ ステップはジョブ ステップの所有者として実行されるか、ジョブ ステップの所有者が sysadmin 固定サーバー ロールのメンバーの場合には [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントとして実行されます。 sysadmin 固定サーバー ロールのメンバーは、sp_add_jobstep ストアド プロシージャの [!INCLUDE[tsql](../../includes/tsql-md.md)] database_user_name *パラメーターを使用して、別のユーザーのコンテキストで* ジョブ ステップが実行されるように指定することもできます。 詳細については、「 [transact-sql &#40;&#41;の sp_add_jobstep](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップに、複数のバッチを含めることができます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップには埋め込み GO コマンドを含めることができます。  
  
## <a name="powershell-scripting-job-steps"></a>PowerShell スクリプティング ジョブ ステップ  
 PowerShell スクリプト ジョブ ステップを作成するときには、次のいずれかをステップのコマンドとして指定する必要があります。  
  
-   PowerShell スクリプトのテキスト。  
  
-   開く対象の既存の PowerShell スクリプト ファイル。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの PowerShell サブシステムが PowerShell セッションを開き、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell スナップインを読み込みます。ジョブステップコマンドとして使用される PowerShell スクリプトは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダーとコマンドレットを参照できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell スナップインを使用した PowerShell スクリプトの作成の詳細については、「 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)」を参照してください。  
  
## <a name="activex-scripting-job-steps"></a>ActiveX スクリプティング ジョブ ステップ  
  
> [!IMPORTANT]  
>  ActiveX スクリプティング ジョブ ステップは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の将来のバージョンで [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントから削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。  
  
 ActiveX スクリプティング ジョブ ステップを作成するには、次の操作を行う必要があります。  
  
-   ジョブ ステップを記述するスクリプティング言語を特定します。  
  
-   ActiveX スクリプトを記述します。  
  
 ジョブ ステップのコマンドとして既存の ActiveX スクリプト ファイルを開くこともできます。 ActiveX スクリプト コマンドは、Microsoft Visual Basic などを使用して外部でコンパイルし、実行可能プログラムとして実行することもできます。  
  
 ジョブ ステップ コマンドが ActiveX スクリプトの場合は、SQLActiveScriptHost オブジェクトを使用してジョブ ステップ履歴ログに出力するか、COM オブジェクトを作成することができます。 SQLActiveScriptHost は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのホスト システムによってスクリプト名前空間に導入されるグローバル オブジェクトです。 このオブジェクトには 2 つのメソッドがあります (Print と CreateObject)。 次の例は、Visual Basic Scripting Edition (VBScript) での ActiveX スクリプティングの動作を示しています。  
  
```  
' VBScript example for ActiveX Scripting job step  
' Create a Dmo.Server object. The object connects to the  
' server on which the script is running.  
  
Set oServer = CreateObject("SQLDmo.SqlServer")  
oServer.LoginSecure = True  
oServer.Connect "(local)"  
'Disconnect and destroy the server object  
oServer.DisConnect  
Set oServer = nothing
```  
  
## <a name="replication-job-steps"></a>レプリケーション ジョブ ステップ  
 レプリケーションを使用してパブリケーションとサブスクリプションを作成した場合、既定でレプリケーション ジョブが作成されます。 作成されるジョブの種類は、レプリケーションの種類 (スナップショット レプリケーション、トランザクション レプリケーション、またはマージ レプリケーション) と使用するオプションによって決まります。  
  
 レプリケーション ジョブ ステップでは、次のレプリケーション エージェントのいずれかがアクティブになります。  
  
-   スナップショット エージェント (スナップショット ジョブ)  
  
-   ログ リーダー エージェント (LogReader ジョブ)  
  
-   ディストリビューション エージェント (ディストリビューション ジョブ)  
  
-   マージ エージェント (マージ ジョブ)  
  
-   キュー リーダー エージェント (QueueReader ジョブ)  
  
 レプリケーションのセットアップ時には、レプリケーション エージェントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント起動後に連続的に実行するか、要求に応じて実行するか、またはスケジュールに従って実行するかを指定できます。 レプリケーション エージェントの詳細については、「 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)」を参照してください。  
  
## <a name="analysis-services-job-steps"></a>Analysis Services ジョブ ステップ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでは、コマンド ジョブ ステップとクエリ ジョブ ステップという 2 種類の Analysis Services ジョブ ステップがサポートされます。  
  
### <a name="analysis-services-command-job-steps"></a>Analysis Services コマンド ジョブ ステップ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] コマンド ジョブ ステップを作成するには、次の操作を行う必要があります。  
  
-   ジョブ ステップが実行される OLAP サーバーのデータベースを特定します。  
  
-   実行するステートメントを入力します。 ステートメントは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Execute** メソッドの XML である必要があります。 ステートメントには、完全な SOAP エンベロープまたは [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] **Discover** メソッドの XML が含まれていない可能性があります。 SOAP エンベロープおよび [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Discover **メソッドは、** ではサポートされていますが、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップではサポートされていません。  
  
### <a name="analysis-services-query-job-steps"></a>Analysis Services クエリ ジョブ ステップ  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] クエリ ジョブ ステップを作成するには、次の操作を行う必要があります。  
  
-   ジョブ ステップが実行される OLAP サーバーのデータベースを特定します。  
  
-   実行するステートメントを入力します。 このステートメントでは、多次元式 (MDX) クエリを使用する必要があります。  
  
 MDX の詳細については、「 [Mdx &#40;クエリ&#41;の基礎 Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services)」を参照してください。  
  
## <a name="integration-services-packages"></a>Integration Services パッケージ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ ジョブ ステップを作成するには、次の操作を行う必要があります。  
  
-   パッケージのソースを特定します。  
  
-   パッケージの場所を特定します。  
  
-   パッケージに構成ファイルが必要な場合は、構成ファイルを特定します。  
  
-   パッケージにコマンド ファイルが必要な場合は、コマンド ファイルを特定します。  
  
-   パッケージに使用する検証方法を特定します。 たとえば、パッケージに署名や特定のパッケージ ID が必要であることを指定できます。  
  
-   パッケージのデータ ソースを特定します。  
  
-   ログ プロバイダーを特定します。  
  
-   パッケージを実行する前に、変数と値を指定します。  
  
-   実行オプションを特定します。  
  
-   コマンド ライン オプションを追加または変更します。  
  
 SSIS カタログにパッケージを配置し、 **[SSIS カタログ]** をパッケージのソースとして指定した場合、この構成情報の多くがパッケージから自動的に得られることに注意してください。 **[構成]** タブでは、環境、パラメーターの値、接続マネージャーの値、プロパティのオーバーライド設定、およびパッケージが 32 ビット ランタイム環境で実行するかどうかを指定できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを実行するジョブ ステップの作成に関する詳細については、「 [パッケージに対する SQL Server エージェント ジョブ](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**説明**|**トピック**|  
|実行可能プログラムを使用してジョブ ステップを作成する方法について説明します。|[CmdExec ジョブ ステップの作成](create-a-cmdexec-job-step.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのアクセス許可をリセットする方法について説明します。|[SQL Server エージェント ジョブ ステップを作成および管理するユーザーの構成](configure-a-user-to-create-and-manage-sql-server-agent-jobs.md)|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] ジョブ ステップを作成する方法について説明します。|[Transact-SQL ジョブ ステップの作成](create-a-transact-sql-job-step.md)|  
|Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント Transact-SQL ジョブ ステップのオプションを定義する方法について説明します。|[Transact-SQL ジョブ ステップのオプションの定義](define-transact-sql-job-step-options.md)|  
|ActiveX スクリプト ジョブ ステップを作成する方法について説明します。|[ActiveX スクリプト ジョブ ステップの作成](create-an-activex-script-job-step.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Service のコマンドとクエリを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブ ステップを作成し、定義する方法について説明します。|[Analysis Services ジョブ ステップの作成](create-an-analysis-services-job-step.md)|  
|ジョブの実行中にエラーが発生した場合に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行する必要があるアクションについて説明します。|[ジョブ ステップの成功時または失敗時の動作の設定](set-job-step-success-or-failure-flow.md)|  
|[ジョブ ステップのプロパティ] ダイアログ ボックスにジョブ ステップの詳細を表示する方法について説明します。|[ジョブ ステップ情報の表示](view-job-step-information.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブ ステップのログを削除する方法について説明します。|[ジョブ ステップのログの削除](delete-a-job-step-log.md)|  
  
## <a name="see-also"></a>参照  
 [dbo. sysjobstepslogs &#40;transact-sql&#41; ](/sql/relational-databases/system-tables/dbo-sysjobstepslogs-transact-sql)   
 [ジョブの作成](create-jobs.md)   
 [sp_add_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-job-transact-sql)  
