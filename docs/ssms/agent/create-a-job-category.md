---
title: ジョブ カテゴリの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b1c34e565365113629e64dda7500501816d7a222
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553134"
---
# <a name="create-a-job-category"></a>ジョブ カテゴリの作成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理オブジェクトを使用して、ジョブ カテゴリを作成する方法について説明します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントには、ジョブを割り当てることができる組み込みのジョブ カテゴリが用意されています。また、ジョブ カテゴリを作成してジョブを割り当てることができます。 ジョブ カテゴリを使用してジョブを管理すると、フィルター操作やグループ化を簡単に行うことができます。 たとえば、データベース バックアップに関するすべてのジョブを [データベースのメンテナンス] カテゴリとしてまとめます。 ジョブ カテゴリは、独自に作成することもできます。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
マルチサーバー カテゴリは、マスター サーバー上だけに存在します。 マスター サーバー上で使用できるのは、 **[未カテゴリ化 (マルチサーバー)]** という既定のジョブ カテゴリだけです。 マルチサーバー ジョブがダウンロードされると、ターゲット サーバー上ではそのカテゴリが **[MSX からのジョブ]** に変更されます。  
  
### <a name="Security"></a>セキュリティ  
詳細については、「 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」をご覧ください。  
  
## <a name="SSMS"></a>SQL Server Management Studio の使用  
  
#### <a name="to-create-a-job-category"></a>ジョブ カテゴリを作成するには  
  
1.  **オブジェクト エクスプ ローラー**で、プラス記号をクリックして、ジョブ カテゴリを作成するサーバーを展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  **[ジョブ]** フォルダーを右クリックし、 **[ジョブ カテゴリの管理]** をクリックします。  
  
4.  **&lt;server_name&gt;** __ ダイアログ ボックスで、 **追加**をクリックします。  
  
5.  新しいダイアログ ボックスで、 **[名前]** ボックスに新しいジョブ カテゴリの名前を入力します。  
  
6.  **[すべてのジョブを表示]** チェック ボックスをオンにします。 ジョブに対応するチェック ボックスをオンにして、新しいカテゴリのジョブを 1 つ以上選択します。  
  
7.  **[OK]** をクリックします。  
  
8.  **&lt;server_name&gt;** __ ダイアログ ボックスで、 **最新の情報に更新** をクリックして、新しいジョブ カテゴリをアクティブにします。 すべての設定が適切であることを確認したら、このダイアログ ボックスを閉じます。  
  
これらのダイアログ ボックスの詳細については、「 [[ジョブ カテゴリ] - [ジョブ カテゴリの管理]](../../ssms/agent/job-categories-manage-job-categories.md) 」および「 [ジョブ カテゴリのプロパティ - [新しいジョブ カテゴリ]](../../ssms/agent/job-categories-properties-new-job-category.md)」をご覧ください。  
  
## <a name="TSQL"></a>Transact-SQL の使用  
  
#### <a name="to-create-a-job-category"></a>ジョブ カテゴリを作成するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
詳細については、「 [sp_add_category (Transact-SQL)](https://msdn.microsoft.com/6cca32cd-d941-4378-aed6-a7c90cb7520a)」をご覧ください。  
  
## <a name="SMO"></a>SQL Server 管理オブジェクトの使用  
**ジョブ カテゴリを作成するには**  
  
Visual Basic、Visual C#、PowerShell などのプログラミング言語で **JobCategory** クラスを呼び出します。 コード例については、「 [SQL Server エージェントでの自動管理タスクのスケジュール設定](../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)」を参照してください。  
  
