---
title: "Windows アプリケーション ログへのジョブ状態の書き込み | Microsoft Docs"
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
- status information [SQL Server], jobs
- SQL Server Agent jobs, status
- writing job status to log
- jobs [SQL Server Agent], status
- logs [SQL Server], jobs
ms.assetid: 3b813702-8f61-40ec-bf3b-ce9deb7e68be
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a23a522ebf0c1d506cc55ef5923a583a19b64434
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="write-the-job-status-to-the-windows-application-log"></a>Windows アプリケーション ログへのジョブ状態の書き込み
このトピックでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]、[!INCLUDE[tsql](../../includes/tsql_md.md)]、または SQL Server 管理オブジェクトを使用して、[!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] でジョブの状態を Windows アプリケーションのイベント ログに書き込むように [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] エージェントを構成する方法について説明します。  
  
ジョブ応答により、データベース管理者はジョブの完了日時や実行頻度を確認できます。 以下に、一般的なジョブ応答を示します。  
  
-   電子メール、ポケットベル、または **net send** メッセージによってオペレーターに通知します。 オペレーターが事後の作業を実行する必要がある場合に、これらのジョブ応答のいずれかを使用します。 たとえば、バックアップ ジョブが正常に終了した場合、オペレーターは、バックアップ テープを取り出して、安全な場所に保管するように通知を受ける必要があります。  
  
-   Windows アプリケーション ログにイベント メッセージを書き込みます。 この応答は、失敗したジョブに対してのみ使用できます。  
  
-   ジョブを自動的に削除します。 このジョブを再実行する必要がないことが明らかな場合に、このジョブ応答を使用します。  
  
**このトピックの内容**  
  
-   **作業を開始する準備:**  
  
    [Security](#Security)  
  
-   **ジョブの状態を Windows アプリケーション ログに書き込む方法:**  
  
    [SQL Server Management Studio](#SSMS)  
  
    [SQL Server 管理オブジェクト](#SMO)  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>Security  
詳細については、「 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-write-job-status-to-the-windows-application-log"></a>ジョブの状態を Windows アプリケーション ログに書き込むには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]**を展開し、 **[ジョブ]**を展開します。次に、編集するジョブを右クリックし、 **[プロパティ]**をクリックします。  
  
3.  **[通知]** ページをクリックします。  
  
4.  **[Windows アプリケーション イベント ログに書き込む]**チェック ボックスをオンにし、次のいずれかを選択します。  
  
    -   ジョブが正常終了したときにジョブの状態をログに記録する場合は、**[ジョブ成功時]**をクリックします。  
  
    -   ジョブが正常終了したときにジョブの状態をログに記録する場合は、**[ジョブ失敗時]**をクリックします。  
  
    -   ジョブが正常終了したときにジョブの状態をログに記録する場合は、**[ジョブ完了時]** をクリックします。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**ジョブの状態を Windows アプリケーション ログに書き込むには**  
  
Visual Basic、Visual C#、PowerShell などのプログラミング言語で **Job** クラスの **EventLogLevel** プロパティを呼び出します。  
  
次のコード例では、ジョブの実行の終了時に、オペレーティング システムのイベント ログ エントリを生成するようにジョブを設定します。  
  
**PowerShell**  
  
```  
$srv = new-object Microsoft.SqlServer.Management.Smo.Server("(local)")  
$jb = new-object Microsoft.SqlServer.Management.Smo.Agent.Job($srv.JobServer, "Test Job")  
$jb.EventLogLevel = [Microsoft.SqlServer.Management.Smo.Agent.CompletionAction]::Always  
```  
  
