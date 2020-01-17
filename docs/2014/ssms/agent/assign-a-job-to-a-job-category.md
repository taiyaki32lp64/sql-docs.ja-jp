---
title: ジョブ カテゴリへのジョブの割り当て | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], assigning
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- SQL Server Agent jobs, assigning
- assigning job to category
ms.assetid: a9ea65a2-1d73-4582-a335-63adeb450cb6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ab7695b6a80772ddcd01996e783fffd806447c59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62473203"
---
# <a name="assign-a-job-to-a-job-category"></a>ジョブ カテゴリへのジョブの割り当て
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクトを使用して、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブをジョブ カテゴリに割り当てる方法について説明します。  
  
 ジョブ カテゴリを使用してジョブを管理すると、フィルター操作やグループ化を簡単に行うことができます。 たとえば、データベース バックアップに関するすべてのジョブを [データベースのメンテナンス] カテゴリとしてまとめます。 ジョブは、ビルトイン ジョブ カテゴリに割り当てたり、ユーザー定義ジョブ カテゴリを作成し、そこに割り当てたりすることができます。  
  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>ジョブ カテゴリにジョブを割り当てるには  
  
1.  **オブジェクト エクスプ ローラー**で、プラス記号をクリックして、ジョブ カテゴリにジョブを割り当てるサーバーを展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[ジョブ]** フォルダーを展開します。  
  
4.  編集するジョブを右クリックし、 **[プロパティ]** を選択します。  
  
5.  [ **ジョブのプロパティ -** _job_name_ ] ダイアログ ボックスの **[カテゴリ]** 一覧で、ジョブに割り当てるジョブ カテゴリを選択します。  
  
6.  **[OK]** をクリックします。  
  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-assign-a-job-to-a-job-category"></a>ジョブ カテゴリにジョブを割り当てるには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_update_job &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql)します。  
  
  
  
##  <a name="SMO"></a> SQL Server 管理オブジェクトの使用  
 **ジョブ カテゴリにジョブを割り当てるには**  
  
 使用して、 `JobCategory` Visual Basic、Visual c#、PowerShell など、選択したプログラミング言語を使用してクラス。  
  
  
  
  
