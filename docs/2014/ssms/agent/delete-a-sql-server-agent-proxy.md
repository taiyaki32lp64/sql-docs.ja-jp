---
title: SQL Server エージェントのプロキシの削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9222253c884fdf3cfa52d283f250580a02a9f7ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62523758"
---
# <a name="delete-a-sql-server-agent-proxy"></a>SQL Server エージェントのプロキシの削除
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)]エージェント プロキシ アカウントを削除する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **SQL Server エージェント プロキシ アカウントを削除する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのプロキシ アカウントを削除する場合は、そのプロキシがアクティブなジョブ ステップを参照していないことを確認してください。 プロキシを参照しているジョブ ステップを確認するには、プロキシを右クリックし、 **プロパティ**をクリックします。 _proxy_name_**プロキシ アカウントのプロパティ** ダイアログ ボックスで、 **参照** ページをクリックします。 プロキシを削除すると、そのプロキシを使用するすべてのジョブ ステップを再割り当てするためのオプションが **[オブジェクトの削除]** ダイアログ ボックスに表示されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシは、資格情報を使用して Windows ユーザー アカウントに関する情報を格納します。 資格情報で指定されているユーザーには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターで "バッチ ジョブとしてログオン" するためのアクセス許可が必要です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、ジョブ ステップを実行するごとに、プロキシからサブシステムへのアクセス許可を確認し、アクセスを確立します。 プロキシにサブシステムへのアクセス許可がない場合、ジョブ ステップは失敗します。 プロキシにアクセス許可がある場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントはプロキシで指定されているユーザーの権限を借用してジョブ ステップを実行します。  
  
-   ユーザーのログインにプロキシへのアクセス許可がある場合、またはプロキシへのアクセス許可のあるロールにユーザーが属している場合、このユーザーはジョブ ステップでプロキシを使用できます。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 プロキシ アカウントを作成、変更、または削除できるのは、 **sysadmin** 固定サーバー ロールのメンバーだけです。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>SQL Server エージェント プロキシ アカウントを削除するには  
  
1.  **オブジェクト エクスプローラー**で、削除するプロキシ アカウントを含むサーバーをプラス記号をクリックして展開します。  
  
2.  プラス記号をクリックして **[SQL Server エージェント]** を展開します。  
  
3.  プラス記号をクリックして **[プロキシ]** フォルダーを展開します。  
  
4.  削除するプロキシ アカウントを含むサブシステムをプラス記号をクリックして展開します (例: **[ActiveX スクリプト]** )。  
  
5.  削除するプロキシ アカウントを右クリックし、 **[削除]** をクリックします。  
  
6.  **[オブジェクトの削除]** ダイアログ ボックスで、削除するプロキシ アカウントが選択されていることを確認します。 現在のプロキシ アカウントを参照するジョブ ステップを別のアカウントに再割り当てするには、 **[再割り当て]** チェック ボックスをオンにします。  
  
7.  **[OK]** をクリックします。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>SQL Server エージェント プロキシ アカウントを削除するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。  
  
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
  
 詳細については、次を参照してください。 [sp_delete_proxy &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql)します。  
  
  
