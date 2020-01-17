---
title: 分散再生の要件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 6fffee7d-891f-4d9d-b2c3-dd19855a1c2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0e7a87ad14dbe1b12abb4ca4fe0af6b0a439c57b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149781"
---
# <a name="distributed-replay-requirements"></a>Distributed Replay Requirements
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生機能を使用する前に、このトピックで説明する製品の要件を検討してください。  
  
## <a name="input-trace-requirements"></a>入力トレースの要件  
 トレース データを正常に再生するには、バージョンと形式の要件を満たし、必要なイベントと列が含まれている必要があります。  
  
### <a name="input-trace-versions"></a>入力トレースのバージョン  
 分散再生は、次のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で収集される入力トレース データをサポートします。  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
### <a name="input-trace-formats"></a>入力トレースの形式  
 次のいずれかの形式の入力トレース データを使用できます。  
  
-   `.trc` 拡張子を持つ 1 つのトレース ファイル。  
  
-   ファイル ロールオーバー名前付け規則に準拠したロールオーバー トレース ファイルのセット。例: `<TraceFile>.trc`、`<TraceFile>_1.trc`、`<TraceFile>_2.trc`、`<TraceFile>_3.trc`、... `<TraceFile>_n.trc`。  
  
### <a name="input-trace-events-and-columns"></a>入力トレースのイベントと列  
 入力トレース データには、分散再生で再生される特定のイベントと列を含める必要があります。 **内の** TSQL_Replay [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] テンプレートには、すべての必要なイベントおよび列と、追加情報が含まれています。 このテンプレートの詳細については、「 [再生を実行するための必要条件](../sql-server-profiler/replay-requirements.md)」を参照してください。  
  
> [!WARNING]  
>  **TSQL_Replay** テンプレートを使用して入力トレース データをキャプチャしない場合、または入力トレースの要件が満たされない場合、予期しない再生結果となる場合があります。  
  
 また、次のイベントが含まれる場合に限り、カスタム トレース テンプレートを作成し、それを使用して分散再生でイベントを再生することもできます。  
  
-   Audit Login  
  
-   Audit Logout  
  
-   ExistingConnection  
  
-   RPC Output Parameter  
  
-   RPC:Completed  
  
-   RPC:Starting  
  
-   SQL:BatchCompleted  
  
-   SQL:BatchStarting  
  
 サーバー側カーソルを再生している場合は、次のイベントも必要です。  
  
-   CursorClose  
  
-   CursorExecute  
  
-   CursorOpen  
  
-   CursorPrepare  
  
-   CursorUnprepare  
  
 サーバー側の準備された SQL ステートメントを再生している場合は、次のイベントも必要です。  
  
-   Exec Prepared SQL  
  
-   Prepare SQL  
  
 すべての入力トレース データに、次の列を含める必要があります。  
  
-   Event Class  
  
-   EventSequence  
  
-   TextData  
  
-   Application Name  
  
-   LoginName  
  
-   DatabaseName  
  
-   データベース ID  
  
-   HostName  
  
-   Binary Data  
  
-   SPID  
  
-   Start Time  
  
-   EndTime  
  
-   IsSystem  
  
## <a name="supported-input-trace-and-target-server-combinations"></a>サポートされている入力トレースとターゲット サーバーの組み合わせ  
 次の表に、サポートされているトレース データのバージョンと、データを再生可能なサポートされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンを示します。  
  
|入力トレース データのバージョン|ターゲット サーバー インスタンスでサポートされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョン|  
|---------------------------------|------------------------------------------------------------------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
  
## <a name="operating-system-requirements"></a>必要なオペレーティング システム  
 管理ツールおよびコントローラーとクライアント サービスを実行するためにサポートされるオペレーティング システムは、使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと同じです。 サポートされるオペレーティング システムに関する詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスは、「 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)します。  
  
 分散再生機能は、x86 ベースおよび x64 ベースの両方のオペレーティング システムでサポートされています。 x64 ベース オペレーティング システムでは、Windows on Windows (WOW) モードのみがサポートされます。  
  
## <a name="installation-limitations"></a>インストールの制限  
 コンピューター 1 台につき、分散再生機能がインストールされている 1 つのインスタンスのみを持つことができます。 次の表に、1 つの分散再生環境における各機能のインストール数の上限を示します。  
  
|分散再生機能|再生環境ごとのインストール数の上限|  
|--------------------------------|--------------------------------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生コントローラー サービス|1|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分散再生クライアント サービス|16 (物理コンピューターまたは仮想コンピューター)|  
|管理ツール|無制限|  
  
> [!NOTE]  
>  1 台のコンピューターにインストールできる管理ツールのインスタンスは 1 つだけですが、管理ツールの複数のインスタンスを開始できます。 複数の管理ツールから発行されたコマンドは、受信された順に解決されます。  
  
## <a name="data-access-provider"></a>データ アクセス プロバイダー  
 分散再生は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC データ アクセス プロバイダーのみをサポートします。  
  
## <a name="target-server-preparation-requirements"></a>ターゲット サーバーの準備要件  
 ターゲット サーバーはテスト環境に配置することをお勧めします。 最初に記録されたものと異なる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対してトレース データを再生するには、ターゲット サーバーが次の条件を満たす必要があります。  
  
-   トレース データに含まれるすべてのログインとユーザーが、ターゲット サーバー上の同一のデータベースに存在すること。  
  
-   ターゲット サーバー上のすべてのログインとユーザーに、元のサーバー上で与えられているものと同じ権限が与えられていること。  
  
-   ターゲット コンピューター上のデータベース ID が、ソース コンピューター上のデータベース ID と同じであること。 ただし、これらが同じでない場合、トレース内に **DatabaseName** が存在すれば、それに基づいて一致させることができます。  
  
-   トレース データに含まれている各ログインの既定データベースが、ターゲット サーバー上で、ログインの対象データベースにそれぞれ設定されていること。 たとえば、再生されるトレース データが、 **の元のインスタンス上のデータベース**Fred_Db **に対する、ログイン** Fred [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の利用状況を含むとします。 この場合、ターゲット サーバー上では、ログイン **Fred** の既定データベースが、**Fred_Db** に一致するデータベースに設定されていなければなりません (データベース名が異なる場合も同様)。 ログインの既定データベースを設定するには、 `sp_defaultdb` システム ストアド プロシージャを使用します。  
  
 失われたログインや不正なログインに関連付けられたイベントを再生すると、再生エラーとなります。ただし、再生の処理は継続されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [分散再生のセキュリティ](distributed-replay-security.md)   
 [分散再生のインストール](install-distributed-replay-overview.md)  
  
  
