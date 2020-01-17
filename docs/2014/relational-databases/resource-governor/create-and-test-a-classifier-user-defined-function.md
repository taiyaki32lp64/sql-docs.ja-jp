---
title: ユーザー定義の分類子関数の作成とテスト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function create
- classifier function [SQL Server], test
- classifier function [SQL Server], create
- Resource Governor, classifier function test
ms.assetid: 7866b3c9-385b-40c6-aca5-32d3337032be
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5118ebcb3da31b97859ca0b2b38e3ad552604990
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68212004"
---
# <a name="create-and-test-a-classifier-user-defined-function"></a>ユーザー定義の分類子関数の作成とテスト
  このトピックでは、ユーザー定義 (UDF) の分類子関数を作成してテストする方法について説明します。 この手順では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディターで [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ステートメントを実行します。  
  
 次の手順で紹介する例のように、ユーザー定義の分類子関数の作成はかなり複雑になる場合があります。  
  
 ここで使用する例の内容は次のとおりです。  
  
-   指定された時間範囲内の実稼働プロセスに対し、リソース プール (pProductionProcessing) とワークロード グループ (gProductionProcessing) を作成します。  
  
-   実稼働プロセスの要件を満たしていない接続を処理するために、リソース プール (pOffHoursProcessing) とワークロード グループ (gOffHoursProcessing) を作成します。  
  
-   ログイン時間に対して評価可能な開始時間と終了時間を保持するためのテーブル (TblClassificationTimeTable) を master に作成します。 リソース ガバナーが分類子関数にスキーマ バインドを使用するため、このテーブルは master に作成する必要があります。  
  
    > [!NOTE]  
    >  サイズが大きく、頻繁に更新されるテーブルは、master に格納しないようにしてください。  
  
 分類子関数を使用するとログイン時間が長くなります。 関数が複雑すぎると、ログインがタイムアウトになったり、接続速度が低下したりすることがあります。  
  
### <a name="to-create-the-classifier-user-defined-function"></a>ユーザー定義の分類子関数を作成するには  
  
1.  新しいリソース プールとワークロード グループを作成して構成します。 各ワークロード グループを適切なリソース プールに割り当てます。  
  
    ```  
    --- Create a resource pool for production processing  
    --- and set limits.  
    USE master  
    GO  
    CREATE RESOURCE POOL pProductionProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 100,  
         MIN_CPU_PERCENT = 50  
    )  
    GO  
    --- Create a workload group for production processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gProductionProcessing  
    WITH  
    (  
         IMPORTANCE = MEDIUM  
    )  
    --- Assign the workload group to the production processing  
    --- resource pool.  
    USING pProductionProcessing  
    GO  
    --- Create a resource pool for off-hours processing  
    --- and set limits.  
  
    CREATE RESOURCE POOL pOffHoursProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 50,  
         MIN_CPU_PERCENT = 0  
    )  
    GO  
    --- Create a workload group for off-hours processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gOffHoursProcessing  
    WITH  
    (  
         IMPORTANCE = LOW  
    )  
    --- Assign the workload group to the off-hours processing  
    --- resource pool.  
    USING pOffHoursProcessing  
    GO  
    ```  
  
2.  メモリ内の構成を更新します。  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
3.  テーブルを作成し、実稼働プロセスの時間範囲の開始時間と終了時間を定義します。  
  
    ```  
    USE master  
    GO  
    CREATE TABLE tblClassificationTimeTable  
    (  
         strGroupName     sysname          not null,  
         tStartTime       time              not null,  
         tEndTime         time              not null  
    )  
    GO  
    --- Add time values that the classifier will use to  
    --- determine the workload group for a session.  
    INSERT into tblClassificationTimeTable VALUES('gProductionProcessing', '6:35 AM', '6:15 PM')  
    go  
    ```  
  
4.  時刻関数および参照テーブル内の時間に対して評価可能な値を使用する分類子関数を作成します。 分類子関数における参照テーブルの使用については、このトピックの「分類子関数に参照テーブルを使用する際のベスト プラクティス」を参照してください。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 日付と時刻のデータ型および関数の拡張セットが導入されました。 詳細については、「[日付と時刻のデータ型および関数&#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)」を参照してください。  
  
    ```  
    CREATE FUNCTION fnTimeClassifier()  
    RETURNS sysname  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
         DECLARE @strGroup sysname  
         DECLARE @loginTime time  
         SET @loginTime = CONVERT(time,GETDATE())  
         SELECT TOP 1 @strGroup = strGroupName  
              FROM dbo.tblClassificationTimeTable  
              WHERE tStartTime <= @loginTime and tEndTime >= @loginTime  
         IF(@strGroup is not null)  
         BEGIN  
              RETURN @strGroup  
         END  
    --- Use the default workload group if there is no match  
    --- on the lookup.  
         RETURN N'gOffHoursProcessing'  
    END  
    GO  
    ```  
  
5.  分類子関数を登録し、メモリ内の構成を更新します。  
  
    ```  
    ALTER RESOURCE GOVERNOR with (CLASSIFIER_FUNCTION = dbo.fnTimeClassifier)  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
    ```  
  
### <a name="to-verify-the-resource-pools-workload-groups-and-the-classifier-user-defined-function"></a>リソース プール、ワークロード グループ、およびユーザー定義の分類子関数を確認するには  
  
1.  次のクエリを使用して、リソース プールとワークロード グループの構成を取得します。  
  
    ```  
    USE master  
    SELECT * FROM sys.resource_governor_resource_pools  
    SELECT * FROM sys.resource_governor_workload_groups  
    GO  
    ```  
  
2.  次のクエリを使用して、分類子関数が存在し、有効になっていることを確認します。  
  
    ```  
    --- Get the classifier function Id and state (enabled).  
    SELECT * FROM sys.resource_governor_configuration  
    GO  
    --- Get the classifer function name and the name of the schema  
    --- that it is bound to.  
    SELECT   
          object_schema_name(classifier_function_id) AS [schema_name],  
          object_name(classifier_function_id) AS [function_name]  
    FROM sys.dm_resource_governor_configuration  
  
    ```  
  
3.  次のクエリを使用して、リソース プールとワークロード グループの現在のランタイム データを取得します。  
  
    ```  
    SELECT * FROM sys.dm_resource_governor_resource_pools  
    SELECT * FROM sys.dm_resource_governor_workload_groups  
    GO  
    ```  
  
4.  次のクエリを使用して、各グループにあるセッションを確認します。  
  
    ```  
    SELECT s.group_id, CAST(g.name as nvarchar(20)), s.session_id, s.login_time, CAST(s.host_name as nvarchar(20)), CAST(s.program_name AS nvarchar(20))  
              FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
              ON g.group_id = s.group_id  
    ORDER BY g.name  
    GO  
    ```  
  
5.  次のクエリを使用して、各グループにある要求を確認します。  
  
    ```  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
                ON g.group_id = r.group_id  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
6.  次のクエリを使用して、分類子関数で実行されている要求を確認します。  
  
    ```  
    SELECT s.group_id, g.name, s.session_id, s.login_time, s.host_name, s.program_name   
               FROM sys.dm_exec_sessions s  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = s.group_id  
                     AND 'preconnect' = s.status  
    ORDER BY g.name  
    GO  
  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, r.command, r.sql_handle, t.text   
               FROM sys.dm_exec_requests r  
         INNER JOIN sys.dm_resource_governor_workload_groups g  
               ON g.group_id = r.group_id  
                     AND 'preconnect' = r.status  
         CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name  
    GO  
    ```  
  
### <a name="best-practices-for-using-lookup-tables-in-a-classifier-function"></a>分類子関数に参照テーブルを使用する際のベスト プラクティス  
  
1.  どうしても必要である場合を除き、参照テーブルは使用しないでください。 使用する必要がある場合は、関数そのものに参照テーブルをハードコーディングすることができます。ただし、そのためには、分類子関数に伴う複雑さや動的な変化とのバランスを考慮する必要があります。  
  
2.  参照テーブルに対して実行される I/O を制限します。  
  
    1.  TOP 1 を使用して、返される行数を 1 行に絞り込みます。  
  
    2.  テーブルの行数を最小限にします。  
  
    3.  テーブルのすべての行が単一のページまたは少数のページに収まるようにします。  
  
    4.  Index Seek 操作を使用して検出された行に、シーク列ができるだけ多く使用されていることを確認します。  
  
    5.  複数のテーブルを結合によって使用することを検討している場合は、単一のテーブルに非正規化します。  
  
3.  参照テーブルでのブロックを回避します。  
  
    1.  `NOLOCK` ヒントを使用してブロックを回避するか、 `SET LOCK_TIMEOUT` (最大値は 1000 ミリ秒) を関数に使用します。  
  
    2.  テーブルは、master データベース内に存在している必要があります (クライアント コンピューターの接続試行時に復旧が保証されるデータベースは、master データベースだけです)。  
  
    3.  テーブル名は必ずスキーマ付きで完全修飾します。 master データベースであることがわかっているため、データベース名は不要です。  
  
    4.  テーブルにトリガーがないようにします。  
  
    5.  テーブルの内容を更新する場合は、ライターがリーダーをブロックすることのないように、必ずスナップショット分離レベル トランザクションを使用します。 この点は `NOLOCK` ヒントを使用して回避することもできます。  
  
    6.  テーブルの内容を変更する場合、可能であれば、分類子関数を無効にします。  
  
        > [!WARNING]  
        >  以上のベスト プラクティスに従うことを強くお勧めします。 ベスト プラクティスに従うことのできない事情がある場合は、問題の発生を事前に防ぐためにも、Microsoft サポートにお問い合わせいただくことをお勧めします。  
  
## <a name="see-also"></a>関連項目  
 [リソース ガバナー](resource-governor.md)   
 [リソース ガバナーの有効化](enable-resource-governor.md)   
 [リソース ガバナー リソース プール](resource-governor-resource-pool.md)   
 [リソース ガバナー ワークロード グループ](resource-governor-workload-group.md)   
 [テンプレートを使用してリソース ガバナーを構成する](configure-resource-governor-using-a-template.md)   
 [リソース ガバナー プロパティの表示](view-resource-governor-properties.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-workload-group-transact-sql)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
