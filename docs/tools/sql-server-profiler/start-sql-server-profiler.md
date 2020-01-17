---
title: 実行 SQL Server プロファイラー |Microsoft Docs
ms.custom: ''
ms.date: 07/07/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
- Profiler [SQL Server Profiler], running
- SQL Server Profiler, running
- running SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 697905061bb60e91884d8844a103ba1302c5c4ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059619"
---
# <a name="run-sql-server-profiler"></a>SQL Server Profiler の実行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  さまざまなシナリオでのトレース出力の収集をサポートするために、いくつかの異なる方法で [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を実行できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、Windows 10 の **[スタート]** メニューや[!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーの **[ツール]** メニューから起動できるほか、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] から起動することもできます。  
  
最初に [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動し、 **[ファイル]** メニューから **[新しいトレース]** を選択すると、 **[サーバーへの接続]** ダイアログ ボックスが表示されるので、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定できます。  
## <a name="to-start-sql-server-profiler-from-the-windows-10-start-menu"></a>Windows 10 の [スタート] メニューから SQL Server Profiler を起動するには  
-  Windows の **[スタート]** アイコンをクリックするか、windows キーを押して、「SQL Server プロファイラー17」と入力します。 **[SQL Server プロファイラー 17]** タイルが表示されたら、それをクリックします。   

## <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>データベース エンジン チューニング アドバイザーで SQL Server Profiler を起動するには  
-  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーで、 **[ツール]** メニューの **[SQL Server Profiler]** をクリックします。  

## <a name="to-start-sql-server-profiler-in-sql-server-management-studio"></a>SQL Server Management Studio で SQL Server プロファイラーを開始するには  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] の[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]複数の場所から開始できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動すると、その時点の接続コンテキスト、トレース テンプレート、およびフィルター コンテキストが読み込まれます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]は、それぞれのインスタンスで各 SQL Server プロファイラーセッションを開始し、シャットダウン[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]した場合はプロファイラーを実行し続けます。  
### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>[ツール] メニューから SQL Server Profiler を起動するには  
-  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **チューニング アドバイザーの** メニューの **[SQL Server Profiler]** から起動することもできます。  

### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>クエリ エディターから SQL Server Profiler を起動するには  
- クエリ エディター内で右クリックし、 **[SQL Server Profiler でクエリをトレース]** を選択します。  

  > [!NOTE]  
  >  接続コンテキストはエディター接続、トレース テンプレートは TSQL_SPs、適用されているフィルターは SPID = query window SPID です。  
    
### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>利用状況モニターから SQL Server Profiler を起動するには  
- 利用状況モニターで、 **[プロセス]** ウィンドウをクリックし、プロファイルするプロセスを右クリックします。次に、 **[SQL Server Profiler のトレース プロセス]** をクリックします。  

    > [!NOTE]  
    >  プロセスを選択したときに、利用状況モニターが開いていた場合、接続コンテキストはオブジェクト エクスプローラー接続になります。 トレース テンプレートはサーバーの種類に応じた既定値になります。SPID は、選択されたプロセスの SPID と等しくなります。  
    
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
- Windows 認証モードでは、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を実行するユーザー アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続するアクセス許可を持っている必要があります。  
- [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]でトレースを実行するには、ユーザーが ALTER TRACE 権限も持っている必要があります。  

## <a name="next-steps"></a>次の手順  
 [SQL Server プロファイラーの概要](../../tools/sql-server-profiler/sql-server-profiler.md)   
 [SQL Server Management Studio の使用 [SQL Server]](https://msdn.microsoft.com/library/f289e978-14ca-46ef-9e61-e1fe5fd593be)  
