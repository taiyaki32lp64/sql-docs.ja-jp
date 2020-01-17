---
title: ジョブの利用状況の表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- viewing job activity
- jobs [SQL Server Agent], viewing
- SQL Server Agent jobs, viewing
- displaying job activity
ms.assetid: 5c284e5e-7775-435d-ac49-f3f12a27ddc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3fc6099fa9f523b351489ce4301596aeb90c1509
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211304"
---
# <a name="view-job-activity"></a>[ジョブの利用状況の表示]
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)]エージェント ジョブの実行状態を表示する方法を説明します。  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが開始されるときに、新しいセッションが作成され、すべての既存の定義済みジョブが **sysjobactivity** データベースの **sysjobactivity** テーブルに設定されます。 このテーブルには、現在のジョブの利用状況と状態が記録されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブの利用状況モニターを使用すると、ジョブの現在状態を表示できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが予期せず終了した場合は、 **sysjobactivity** テーブルを参照して、サービスが終了したときにどのジョブが実行されていたかを確認できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **ジョブの利用状況を表示する方法:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
## <a name="before-you-begin"></a>はじめに  
  
###  <a name="Security"></a> セキュリティ  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  
  
##  <a name="SSMS"></a> SQL Server Management Studio の使用  
  
#### <a name="to-view-job-activity"></a>ジョブの利用状況を表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を展開します。  
  
3.  **[ジョブの利用状況モニター]** を右クリックし、 **[ジョブの利用状況の表示]** をクリックします。  
  
4.  このサーバーに対して定義された各ジョブに関する詳細が、 **[ジョブの利用状況モニター]** に表示されます。  
  
5.  ジョブの開始、ジョブの停止、ジョブの有効化や無効化、ジョブの利用状況モニターに表示されている状態の最新の情報への更新、ジョブの削除、ジョブの履歴やプロパティの表示などの操作を行うには、ジョブを右クリックします。  複数のジョブの開始、停止、有効化や無効化、または最新の情報への更新には、ジョブの利用状況モニターで複数の行を選択し、選択項目を右クリックします。  
  
6.  ジョブの利用状況モニターを更新するには、 **[更新]** をクリックします。 表示される行を少なくするには、 **[フィルター]** をクリックし、フィルターのパラメーターを入力します。  
  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-view-job-activity"></a>ジョブの利用状況を表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- lists activity for all jobs that the current user has permission to view.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_jobactivity ;  
    GO  
    ```  
  
 詳細については、次を参照してください。 [sp_help_jobactivity &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-jobactivity-transact-sql)します。  
  
  
