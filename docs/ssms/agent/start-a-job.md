---
title: "ジョブの開始 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], starting
- SQL Server Agent jobs, starting
- starting jobs
ms.assetid: cec9f7f7-d0a7-4239-9dc5-a69c011ebaa0
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c5ef8705a19038363c537f288a0da910e13d18ee
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="start-a-job"></a>Start a Job
このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)]、または SQL Server 管理オブジェクトを使用して、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント ジョブの実行を開始する方法について説明します。  
  
ジョブとは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェントで実行される特定の一連の処理のことです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェント ジョブは、1 つのローカル サーバーで実行することも、複数のリモート サーバーで実行することもできます。  
  
-   **作業を開始する準備:**  
  
    [Security](#Security)  
  
-   **ジョブを開始する方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [Transact-SQL](#TSQL)  
  
    [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>Security  
詳細については、「 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-start-a-job"></a>ジョブを開始するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開し、 **[ジョブ]**を展開します。 ジョブの開始方法に応じて、次のいずれかを行います。  
  
    -   単一のサーバーまたは対象サーバー上で作業を行っている場合、またはマスター サーバー上でローカル サーバー ジョブを実行している場合、開始するジョブを右クリックして、 **[ジョブの開始]**をクリックします。  
  
    -   複数のジョブを開始するには、 **[ジョブの利用状況モニター]**を右クリックし、 **[ジョブの利用状況の表示]**をクリックします。 ジョブの利用状況モニターでは、複数のジョブを選択し、選択内容を右クリックして、 **[ジョブの開始]**をクリックできます。  
  
    -   マスター サーバー上で作業を行っていて、すべての対象サーバーで同時にジョブを実行する場合、開始するジョブを右クリックし、 **[ジョブの開始]**をクリックします。次に、 **[すべての対象サーバーで開始]**をクリックします。  
  
    -   マスター サーバー上で作業を行っていて、ジョブの対象サーバーを指定する場合、開始するジョブを右クリックし、 **[ジョブの開始]**をクリックします。次に、 **[特定の対象サーバーで開始]**をクリックします。 **[ダウンロード命令の通知]** ダイアログ ボックスの **[特定の対象サーバー]** チェック ボックスをオンにし、このジョブが実行される各対象サーバーを選択します。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-start-a-job"></a>ジョブを開始するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]**をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]**をクリックします。  
  
    ```  
    -- starts a job named Weekly Sales Data Backup.    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_start_job N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
詳細については、「 [sp_start_job (Transact-SQL)](http://msdn.microsoft.com/en-us/8a91df6a-eb84-4512-9a17-4a6e32a9538a)」を参照してください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**ジョブを開始するには**  
  
Visual Basic、Visual C#、PowerShell などの選択したプログラミング言語を使用して **Job** クラスの **Start** メソッドを呼び出します。 詳細については、「 [SQL Server 管理オブジェクト (SMO) プログラミング ガイド](http://msdn.microsoft.com/library/ms162169.aspx)」を参照してください。  
  
