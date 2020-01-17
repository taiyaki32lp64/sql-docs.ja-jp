---
title: ジョブ カテゴリ情報の一覧の表示 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dae8f1d98fb1758e9a9802883def1574bda68a78
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798212"
---
# <a name="list-job-category-information"></a>ジョブ カテゴリ情報の一覧の表示
  [!INCLUDE[tsql](../../includes/tsql-md.md)] または SQL Server 管理オブジェクトを使用して [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にジョブカテゴリ情報を一覧表示する方法。  

  
##  <a name="Security"></a> Security  
 詳細については、「 [SQL Server エージェントのセキュリティの実装](implement-sql-server-agent-security.md)」をご覧ください。  

  
##  <a name="TSQL"></a> Transact-SQL の使用  
  
#### <a name="to-list-job-category-information"></a>ジョブ カテゴリ情報の一覧を表示するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、**[実行]** をクリックします。  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 詳細については、「 [sp_help_category &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql)」を参照してください。  
  
  
##  <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
 **ジョブ カテゴリ情報の一覧を表示するには**  
  
 Visual Basic、Visual C#、PowerShell などのプログラミング言語で `JobCategory` クラスを使用します。 詳細については[、 &#40;「&#41; SQL Server 管理オブジェクト SMO プログラミングガイド](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)」を参照してください。  
