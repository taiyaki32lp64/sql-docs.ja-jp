---
title: SQL Server プロファイラー | を使用したデッドロックの分析Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- process nodes [SQL Server Profiler]
- Profiler [SQL Server Profiler], deadlocks
- deadlocks [SQL Server], identifying cause
- resource nodes [SQL Server Profiler]
- graphs [SQL Server Profiler]
- SQL Server Profiler, deadlocks
- events [SQL Server], deadlocks
- edges [SQL Server Profiler]
ms.assetid: 72d6718f-501b-4ea6-b344-c0e653f19561
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ab8914abdaa2056a71fdd4d0e1a277c89e200dc7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105627"
---
# <a name="analyze-deadlocks-with-sql-server-profiler"></a>SQL Server Profiler を使用したデッドロックの分析
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を使用して、デッドロックの原因を特定します。 デッドロックは、SQL Server 内のリソースの集合に対して複数のスレッド間またはプロセス間で相互に依存関係があるときに発生します。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用すると、分析用にデッドロック イベントを記録、再生、および表示するトレースを作成できます。  
  
 デッドロック イベントをトレースするには、 **Deadlock Graph** イベント クラスをトレースに追加します。 このイベント クラスにより、デッドロックに関連するプロセスとオブジェクトに関する XML データが、トレースの **TextData** データ列に設定されます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] では、この XML ドキュメントをデッドロック XML (.xdl) ファイルに抽出して、後で SQL Server Management Studio で表示できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] Deadlock Graph **イベントを、すべての** Deadlock Graph **イベントが含まれた 1 つのファイルに抽出するか、または個別のファイルに抽出するように** を構成できます。 この抽出は、次の方法のいずれかを使用して実行できます。  
  
-   トレースの構成時に、 **[イベント抽出の設定]** タブを使用する。このタブは、 **[イベントの選択]** タブで **Deadlock Graph** イベントを選択していないと表示されないので注意してください。  
  
-   **[ファイル]** メニューの **[SQL Server イベントの抽出]** オプションを使用する。  
  
-   特定のイベントを右クリックし、 **[イベント データの抽出]** をクリックすることにより、個々のイベントを抽出して保存することもできます。  
  
## <a name="deadlock-graphs"></a>Deadlock Graph  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] と [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、Deadlock Wait-for Graph を使用してデッドロックが説明されます。 Deadlock Wait-for Graph には、プロセス ノード、リソース ノード、およびプロセスとリソース間の関係を表すエッジが含まれています。 次の表では、Deadlock Wait-for Graph の構成要素を定義します。  
  
 プロセス ノード  
 INSERT、UPDATE、DELETE などのタスクを実行するスレッド。  
  
 リソース ノード  
 テーブル、インデックス、行などのデータベース オブジェクト。  
  
 エッジ  
 プロセスとリソース間の関係。 **request** エッジは、プロセスがリソースを待機したときに発生します。 **owner** エッジは、リソースがプロセスを待機したときに発生します。 ロック モードは、エッジの記述に含まれます。 たとえば、" **モード: X**" などです。  
  
## <a name="deadlock-process-node"></a>デッドロック プロセス ノード  
 Deadlock Wait-for Graph には、プロセス ノードにプロセスに関する情報が含まれています。 次の表で、プロセスの構成要素について説明します。  
  
|コンポーネント|定義|  
|---------------|----------------|  
|[サーバー プロセス ID]|サーバー プロセス ID (SPID)。ロックを所有しているプロセスのサーバー割り当て ID です。|  
|[サーバー バッチ ID]|サーバー バッチ ID (SBID)。|  
|[実行コンテキスト ID]|実行コンテキスト ID (ECID)。 特定の SPID に関連付けられている特定のスレッドの実行コンテキスト ID です。<br /><br /> ECID = {0, 1, 2, 3, *...n*}。0 は常にメイン スレッドまたは親スレッドを表し、{1, 2, 3, ... *n*} は、サブスレッドを表します。|  
|[デッドロックの優先度]|プロセスのデッドロックの優先度。 詳細については、「[SET DEADLOCK_PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/set-deadlock-priority-transact-sql.md)」を参照してください。|  
|[使用されたログ]|プロセスで使用されたログ領域の量。|  
|[所有者 ID]|トランザクションを使用しており、現在ロックを待機しているプロセスのトランザクション ID。|  
|[トランザクション記述子]|トランザクションの状態を記述するトランザクション記述子へのポインター。|  
|[入力バッファー]|現在のプロセスの入力バッファー。イベントの種類と実行中のステートメントを定義します。 有効な値は次のとおりです。<br /><br /> **言語**<br /><br /> **RPC**<br /><br /> **なし**|  
|Statement|ステートメントの種類。 有効な値は次のとおりです。<br /><br /> **NOP**<br /><br /> **SELECT**<br /><br /> **UPDATE**<br /><br /> **INSERT**<br /><br /> **DELETE**<br /><br /> **Unknown**|  
  
## <a name="deadlock-resource-node"></a>デッドロック リソース ノード  
 デッドロックにおいて、2 つのプロセスが、他のプロセスで使用されているリソースをそれぞれ待機しています。 Deadlock Graph では、これらのリソースがリソース ノードとして表示されます。  
  
  
