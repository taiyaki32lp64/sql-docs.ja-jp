---
title: max worker threads サーバー構成オプションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5d4aae8a264bd77d51c3365183ee510043ae814b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787594"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>max worker threads サーバー構成オプションの構成
  このトピックでは、 **または** を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] max worker threads [!INCLUDE[tsql](../../includes/tsql-md.md)]サーバー構成オプションを構成する方法について説明します。 **max worker threads** オプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで利用できるワーカー スレッド数を構成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、オペレーティング システムのネイティブ スレッド サービスを使用しているため、1 つ以上のスレッドが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で同時にサポートされている各ネットワークをサポートし、他のスレッドがデータベース チェックポイントを処理し、スレッド プールがすべてのユーザーを処理します。 **max worker threads** の既定値は 0 です。 この場合、ワーカー スレッドの数が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって起動時に自動で構成されます。 既定の設定は、ほとんどのシステムで最適な設定です。 ただし、システム構成によっては、 **max worker threads** を特定の値に設定するとパフォーマンスが向上することがあります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **以下を使用して max worker threads オプションを構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **補足情報:** [max worker threads オプションを構成した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   実際のクエリ要求数が **max worker threads**に設定した値を下回る場合、1 つのスレッドで 1 つのクエリ要求が処理されます。 一方、実際のクエリ要求数が **max worker threads**に設定した値を超える場合は、ワーカー スレッド プールが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって作成され、次に使用可能なワーカー スレッドで要求を処理できるようになります。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   このオプションは詳細設定オプションであるため、熟練したデータベース管理者または認定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術者だけが変更するようにしてください。  
  
-   スレッド プールは、多数のクライアントがサーバーに接続されている場合のパフォーマンスの最適化に役立ちます。 通常、クエリ要求ごとに個別のオペレーティング システム スレッドが作成されます。 ただし、サーバーへの接続が数百にもなる場合、クエリ要求ごとに 1 つのスレッドを使用すると大量のシステム リソースが消費されることがあります。 **max worker threads** オプションを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってワーカー スレッド プールが作成され多数のクエリ要求を処理できるようになります。その結果、パフォーマンスが向上します。  
  
-   次の表に、CPU および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各バージョンのさまざまな組み合わせに対して、自動的に構成されるワーカー スレッドの最大数を示します。  
  
    |CPU の数|32 ビット コンピューター|64 ビット コンピューター|  
    |--------------------|----------------------|----------------------|  
    |\<= 4 個のプロセッサ|256|512|  
    |8 個のプロセッサ|288|576|  
    |16 個のプロセッサ|352|704|  
    |32 個のプロセッサ|480|960|  
    |64 個のプロセッサ|736|1472|  
    |128 個のプロセッサ|4224|4480|  
    |256 個のプロセッサ|8320|8576|  
  
    > [!NOTE]  
    >  64 個を超える CPU を使用する場合の推奨事項については、「[64 個を超える CPU を搭載したコンピューター上で SQL Server を実行する場合のベスト プラクティス](https://technet.microsoft.com/library/ee210547\(SQL.105\).aspx)」を参照してください。  
  
    > [!WARNING]  
    >  32 ビット コンピューター上で動作する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの場合、ワーカー スレッドの最大数として 1024 をお勧めします。  
  
-   クエリの実行が長時間にわたり、すべてのスレッドがアクティブになっている場合、いずれかのワーカー スレッドが処理を完了し使用できるようになるまで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が応答していないように見えることがあります。 これは欠陥ではありませんが、望ましくない場合があります。 プロセスが応答せず新しいクエリを処理できない場合は、専用管理者接続 (DAC) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続し、プロセスを終了します。 このような状態を回避するには、ワーカー スレッド数を増やします。  
  
 **max worker threads** サーバー構成オプションでは、可用性グループ、Service Broker、ロック マネージャーなど、すべてのシステム タスクに必要なスレッドは考慮されません。  構成されたスレッドの数を超えている場合は、次のクエリによって、追加のスレッドを生成したシステム タスクに関する情報が取得されます。  
  
```  
SELECT  
s.session_id,  
r.command,  
r.status,  
r.wait_type,  
r.scheduler_id,  
w.worker_address,  
w.is_preemptive,  
w.state,  
t.task_state,  
t.session_id,  
t.exec_context_id,  
t.request_id  
FROM sys.dm_exec_sessions AS s  
INNERJOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
WHERE s.is_user_process = 0;  
  
```  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 パラメーターなしで、または最初のパラメーターだけを指定して **sp_configure** を実行する権限は、既定ですべてのユーザーに付与されます。 両方のパラメーターを指定して **sp_configure** を実行し構成オプションを変更したり RECONFIGURE ステートメントを実行したりするには、ALTER SETTINGS サーバーレベル権限がユーザーに付与されている必要があります。 ALTER SETTINGS 権限は、 **sysadmin** 固定サーバー ロールと **serveradmin** 固定サーバー ロールでは暗黙のうちに付与されています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>max worker threads オプションを構成するには  
  
1.  オブジェクト エクスプローラーで、サーバーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[プロセッサ]** ノードをクリックします。  
  
3.  **[ワーカー スレッド最大数]** ボックスに、128 ～ 32767 の値を入力するか、または選択します。  
  
     **[ワーカー スレッド最大数]** オプションを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで利用できるワーカー スレッド数を設定できます。 ほとんどのシステムの場合、 **[ワーカー スレッド最大数]** の既定値を使用するのが最適です。 ただし、システム構成によっては、 **max worker threads** の値を小さくするとパフォーマンスが向上することがあります。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>max worker threads オプションを構成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) を使用して、 `max worker threads` オプションを `900`に設定する方法を示します。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 詳細については、「 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)」を参照してください。  
  
##  <a name="FollowUp"></a>補足情報: max worker threads オプションを構成した後  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] を再起動しなくても、変更は直ちに有効になります。  
  
## <a name="see-also"></a>関連項目  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [データベース管理者用の診断接続](diagnostic-connection-for-database-administrators.md)  
  
  
