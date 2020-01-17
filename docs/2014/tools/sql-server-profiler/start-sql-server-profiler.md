---
title: SQL Server Profiler の起動 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], starting
- SQL Server Profiler, starting
- starting SQL Server Profiler
ms.assetid: 22e57ffa-63b0-4de3-b92e-df297dda1226
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a3219168a070a9c264d4fb5457f9e5844734844a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68186111"
---
# <a name="start-sql-server-profiler"></a>SQL Server Profiler の起動
  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、さまざまなシナリオでのトレース出力の収集をサポートするために、いくつかの異なる方法で起動することができます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、 **[スタート]** メニューや **チューニング アドバイザーの** [ツール] [!INCLUDE[ssDE](../../includes/ssde-md.md)] メニューから起動できるほか、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から起動することもできます。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動し、 **[ファイル]** メニューの **[新しいトレース]** をクリックすると、 **[サーバーへの接続]** ダイアログ ボックスが表示されるので、接続先の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定できます。  
  
### <a name="to-start-sql-server-profiler-from-the-start-menu"></a>[スタート] メニューから SQL Server Profiler を起動するには  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]、 **[パフォーマンス ツール]** の順にポイントして、 **[SQL Server Profiler]** をクリックします。  
  
### <a name="to-start-sql-server-profiler-in-database-engine-tuning-advisor"></a>データベース エンジン チューニング アドバイザーで SQL Server Profiler を起動するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)] チューニング アドバイザーで、 **[ツール]** メニューの **[SQL Server Profiler]** をクリックします。  
  
## <a name="starting-sql-server-profiler-in-management-studio"></a>Management Studio での SQL Server Profiler の起動  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、それぞれのインスタンスで各プロファイラー セッションを開始します。このセッションは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]をシャットダウンしても実行が続きます。  
  
 以降の各手順に示すように、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]の複数の場所から起動できます。 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を起動すると、その時点の接続コンテキスト、トレース テンプレート、およびフィルター コンテキストが読み込まれます。  
  
#### <a name="to-start-sql-server-profiler-from-the-tools-menu"></a>[ツール] メニューから SQL Server Profiler を起動するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **チューニング アドバイザーの** メニューの **[SQL Server Profiler]** から起動することもできます。  
  
#### <a name="to-start-sql-server-profiler-from-the-query-editor"></a>クエリ エディターから SQL Server Profiler を起動するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のメニュー バーの **[新しいクエリ]** をクリックします。  
  
2.  クエリ エディター内で右クリックし、 **[SQL Server Profiler でクエリをトレース]** を選択します。  
  
    > [!NOTE]  
    >  接続コンテキストはエディター接続、トレース テンプレートは TSQL_SPs、適用されているフィルターは SPID = query window SPID です。  
  
#### <a name="to-start-sql-server-profiler-from-activity-monitor"></a>利用状況モニターから SQL Server Profiler を起動するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを右クリックし、 **[利用状況モニター]** をクリックします。  
  
2.  **プロセス** ペインをクリックし、プロファイルするプロセスを右クリックして **[SQL Server Profiler のトレース プロセス]** をクリックします。  
  
    > [!NOTE]  
    >  プロセスを選択したときに、利用状況モニターが開いていた場合、接続コンテキストはオブジェクト エクスプローラー接続になります。 トレース テンプレートはサーバーの種類に応じた既定値になります。SPID は、選択されたプロセスの SPID と等しくなります。  
  
## <a name="net-framework-security"></a>.NET Framework セキュリティ  
 Windows 認証モードでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] を実行するユーザー アカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続する権限を持っている必要があります。  
  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]でトレースを実行するには、ユーザーが ALTER TRACE 権限も持っている必要があります。  
  
## <a name="see-also"></a>関連項目  
 [[SQL Server Profiler]](sql-server-profiler.md)   
 [SQL Server Management Studio の使用 [SQL Server]](../../database-engine/use-sql-server-management-studio.md)  
  
  
