---
title: SQL Server エージェントのプロキシの削除 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 60b852490958b67e0d3fd2411cf0d90ffeaadaa4
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553013"
---
# <a name="delete-a-sql-server-agent-proxy"></a>Delete a SQL Server Agent Proxy
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)]エージェント プロキシ アカウントを削除する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Restrictions"></a>制限事項と制約事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのプロキシ アカウントを削除する場合は、そのプロキシがアクティブなジョブ ステップを参照していないことを確認してください。 プロキシを参照しているジョブ ステップを確認するには、プロキシを右クリックし、 **[プロパティ]** をクリックします。[_proxy\_name_ **プロキシ アカウントのプロパティ]** ダイアログ ボックスで、 **[参照]** ページをクリックします。 プロキシを削除すると、そのプロキシを使用するすべてのジョブ ステップを再割り当てするためのオプションが **[オブジェクトの削除]** ダイアログ ボックスに表示されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシは、資格情報を使用して Windows ユーザー アカウントに関する情報を格納します。 資格情報で指定されているユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターで "バッチ ジョブとしてログオン" するためのアクセス許可が必要です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、ジョブ ステップを実行するごとに、プロキシからサブシステムへのアクセス許可を確認し、アクセスを確立します。 プロキシにサブシステムへのアクセス許可がない場合、ジョブ ステップは失敗します。 プロキシにアクセス許可がある場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはプロキシで指定されているユーザーの権限を借用してジョブ ステップを実行します。  
  
-   ユーザーのログインにプロキシへのアクセス許可がある場合、またはプロキシへのアクセス許可のあるロールにユーザーが属している場合、このユーザーはジョブ ステップでプロキシを使用できます。  
  
### <a name="Security"></a>セキュリティ  
  
#### <a name="Permissions"></a>アクセス許可  
プロキシ アカウントを作成、変更、または削除できるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>SQL Server エージェント プロキシ アカウントを削除するには  
  
1.  **オブジェクト エクスプローラー**で、削除するプロキシ アカウントを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[プロキシ]** フォルダーを展開します。  
  
4.  削除するプロキシ アカウントを含むサブシステムをプラス記号をクリックして展開します (例: **[ActiveX スクリプト]** )。  
  
5.  削除するプロキシ アカウントを右クリックし、 **[削除]** をクリックします。  
  
6.  **[オブジェクトの削除]** ダイアログ ボックスで、削除するプロキシ アカウントが選択されていることを確認します。 現在のプロキシ アカウントを参照するジョブ ステップを別のアカウントに再割り当てするには、 **[再割り当て]** チェック ボックスをオンにします。  
  
7.  **[OK]** をクリックします。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>SQL Server エージェント プロキシ アカウントを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde_md.md)]のインスタンスに接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
詳しくは、「 [sp_delete_proxy (Transact-SQL)](https://msdn.microsoft.com/44a1db13-b7f2-4dab-a1b5-b8dafb41737c)」をご覧ください。  
  
