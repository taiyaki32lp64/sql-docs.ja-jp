---
title: サンプル:サーバー イベント用 WMI プロバイダーを使用して SQL Server エージェント警告の作成 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SQL Server Agent [WMI]
- WMI Provider for Server Events, samples
- sample applications [WMI]
ms.assetid: d44811c7-cd46-4017-b284-c863ca088e8f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a793c6ee6e1f6e168ca2a957b84b1ba4a1d2a453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68195833"
---
# <a name="sample-creating-a-sql-server-agent-alert-by-using-the-wmi-provider-for-server-events"></a>サンプル:WMI Provider for Server Events の使用による SQL Server エージェント警告の作成
  WMI イベント プロバイダーの標準的な使い方の 1 つは、特定のイベントに応答する SQL Server エージェントを作成することです。 次のサンプルでは、後で分析するために、テーブルに XML デッドロック グラフ イベントを保存する簡単な警告を提供しています。 SQL Server エージェントは、WQL 要求の送信、WMI イベントの受信、およびイベントに応答したジョブの実行を行います。 通知メッセージの処理に関連する Service Broker オブジェクトはいくつかありますが、WMI イベント プロバイダーはこれらのオブジェクトの作成および管理の詳細を処理します。  
  
## <a name="example"></a>例  
 まず、デッドロック グラフ イベントを格納するために、`AdventureWorks` データベースにテーブルが作成されます。 テーブルには、2 つの列が含まれています。`AlertTime`列は、警告が実行時間を保持し、`DeadlockGraph`列は、デッドロック グラフを含む XML ドキュメントを保持します。  
  
 次に警告が作成されます。 スクリプトは、まず、警告が実行するジョブを作成し、ジョブ ステップをジョブに追加し、そのジョブを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスに指定します。 次に、スクリプトは警告を作成します。  
  
 ジョブ ステップを取得、 **TextData**プロパティの WMI イベントのインスタンスとその値を挿入、 **DeadlockGraph**の列、 **DeadlockEvents**テーブル。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、暗黙に文字列を XML 形式に変換することに注意してください。 このジョブ ステップでは [!INCLUDE[tsql](../../includes/tsql-md.md)] サブシステムを使用するので、プロシキは指定されません。  
  
 警告は、デッドロック グラフ トレース イベントのログが記録されるたびに、ジョブを実行します。 WMI 警告の場合、SQL Server エージェントは、指定された名前空間および WQL ステートメントを使用して通知クエリを作成します。 この警告の場合、SQL Server エージェントは、ローカル コンピューター上の既定のインスタンスを監視します。 WQL ステートメントは、既定のインスタンス内の任意の `DEADLOCK_GRAPH` イベントを要求します。 警告が監視するインスタンスを変更するには、警告する `MSSQLSERVER` 内の `@wmi_namespace` のインスタンス名を置き換えます。  
  
> [!NOTE]  
>  WMI のイベントを受信する SQL Server エージェントの[!INCLUDE[ssSB](../../includes/sssb-md.md)]で有効にする必要があります**msdb**と[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]します。  
  
```  
USE AdventureWorks ;  
GO  
  
IF OBJECT_ID('DeadlockEvents', 'U') IS NOT NULL  
BEGIN  
    DROP TABLE DeadlockEvents ;  
END ;  
GO  
  
CREATE TABLE DeadlockEvents  
    (AlertTime DATETIME, DeadlockGraph XML) ;  
GO  
-- Add a job for the alert to run.  
  
EXEC  msdb.dbo.sp_add_job @job_name=N'Capture Deadlock Graph',   
    @enabled=1,   
    @description=N'Job for responding to DEADLOCK_GRAPH events' ;  
GO  
  
-- Add a jobstep that inserts the current time and the deadlock graph into  
-- the DeadlockEvents table.  
  
EXEC msdb.dbo.sp_add_jobstep  
    @job_name = N'Capture Deadlock Graph',  
    @step_name=N'Insert graph into LogEvents',  
    @step_id=1,   
    @on_success_action=1,   
    @on_fail_action=2,   
    @subsystem=N'TSQL',   
    @command= N'INSERT INTO DeadlockEvents  
                (AlertTime, DeadlockGraph)  
                VALUES (getdate(), N''$(ESCAPE_SQUOTE(WMI(TextData)))'')',  
    @database_name=N'AdventureWorks' ;  
GO  
  
-- Set the job server for the job to the current instance of SQL Server.  
  
EXEC msdb.dbo.sp_add_jobserver @job_name = N'Capture Deadlock Graph' ;  
GO  
  
-- Add an alert that responds to all DEADLOCK_GRAPH events for  
-- the default instance. To monitor deadlocks for a different instance,  
-- change MSSQLSERVER to the name of the instance.  
  
EXEC msdb.dbo.sp_add_alert @name=N'Respond to DEADLOCK_GRAPH',   
@wmi_namespace=N'\\.\root\Microsoft\SqlServer\ServerEvents\MSSQLSERVER',   
    @wmi_query=N'SELECT * FROM DEADLOCK_GRAPH',   
    @job_name='Capture Deadlock Graph' ;  
GO  
```  
  
## <a name="testing-the-sample"></a>サンプルのテスト  
 ジョブの実行を確認するには、デッドロックを発生させます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、2 つ開きます**SQL クエリ**タブし、両方のクエリを同じインスタンスに接続します。 次のスクリプトを 2 つのクエリ タブのうちの 1 つで実行します。 このスクリプトは、1 つの結果セットを作成して終了します。  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 2 番目のクエリ タブで、次のスクリプトを実行します。このスクリプトは、1 つの結果セットを生成し、ブロック、に対するロックの取得を待機している`Production.Product`します。  
  
```  
USE AdventureWorks ;  
GO  
  
BEGIN TRANSACTION ;  
GO  
  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
  
SELECT TOP(1) Name FROM Production.Product WITH (XLOCK) ;  
GO  
```  
  
 最初のクエリ タブで、次のスクリプトを実行します。このスクリプト ブロックは、に対するロックの取得を待機している`Production.Location`します。 すぐにタイムアウトになった後、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、このスクリプトとサンプル内のスクリプトのどちらかをデッドロックの対象として選択し、トランザクションを終了します。  
  
```  
SELECT TOP(1) Name FROM Production.Location WITH (XLOCK) ;  
GO  
```  
  
 デッドロックが発生した後、SQL Server エージェントが警告を有効化してジョブを実行するまで、しばらく待ちます。 次のスクリプトを実行して、`DeadlockEvents` テーブルの内容を調べます。  
  
```  
SELECT * FROM DeadlockEvents ;  
GO  
```  
  
 `DeadlockGraph` 列には、デッドロック グラフ イベントのすべてのプロパティを示した XML ドキュメントが格納されているはずです。  
  
## <a name="see-also"></a>関連項目  
 [WMI Provider for Server Events の概念](wmi-provider-for-server-events-concepts.md)  
  
  
