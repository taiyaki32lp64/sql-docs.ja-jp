---
title: マスター サーバーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.msxwiz.operator.f1
- sql13.ag.msxwiz.login.f1
- sql13.ag.msxwiz.target.f1
- sql13.ag.msxwiz.complete.f1
- sql13.ag.msxwiz.cover.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 79f02ab705f6bf340403739ed01d46e8ab11b024
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69552878"
---
# <a name="make-a-master-server"></a>Make a Master Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) では現在、すべてではありませんがほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、「[Azure SQL Database Managed Instance と SQL Server の T-SQL の相違点](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)」を参照してください。

このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してマスター サーバー [!INCLUDE[tsql](../../includes/tsql-md.md)]を作成する方法について説明します。  
  
## <a name="BeforeYouBegin"></a>はじめに  
  
### <a name="Security"></a>セキュリティ  
プロキシに関連付けられているステップがある分散ジョブは、ターゲット サーバーのプロキシ アカウントのコンテキストで実行されます。 次の条件を満たしていることを確認してください。満たしていないと、プロキシに関連付けられているジョブ ステップがマスター サーバーから対象サーバーにダウンロードされません。  
  
-   マスター サーバー レジストリのサブキー **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<&#42;instance_name&#42;>\SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) が 1 (true) に設定されていること。 既定では、この値は 0 (false) に設定されます。  
  
-   ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前を持つターゲット サーバーにプロキシ アカウントが存在すること。  
  
マスター サーバーからターゲット サーバーにプロキシ アカウントをダウンロード中に、これらのアカウントを使用するジョブ ステップが失敗した場合は、**msdb** データベースの **sysdownloadlist** テーブルの **error_message** 列を参照して、以下のエラー メッセージの有無を確認します。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、ターゲット サーバーで一致するプロキシが無効です。"  
  
    このエラーを解決するには、 **AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを 1 に設定します。  
  
-   "プロキシ アカウントが見つかりませんでした。"  
  
    このエラーを解決するには、ターゲット サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
#### <a name="Permissions"></a>アクセス許可  
このプロシージャの実行権限は、既定では **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-make-a-master-server"></a>マスター サーバーを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチサーバーの管理]** をポイントして、 **[マスター サーバーに設定]** をクリックします。 **マスター サーバー ウィザード** を使用してマスター サーバーを作成し、ターゲット サーバーを追加します。  
  
3.  **[マスター サーバー オペレーター]** ページで、マスター サーバーのオペレーターを設定します。電子メールまたはポケットベルを使用してオペレーターに通知を送信するには、電子メールが送信されるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを設定しておく必要があります。 **net send**を使用してオペレーターに通知を送信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが置かれているサーバーで Messenger サービスが実行されている必要があります。  
  
    **[電子メール アドレス]**  
    オペレーターの電子メール アドレスを設定します。  
  
    **[ポケットベル アドレス]**  
    オペレーターのポケットベル メール アドレスを設定します。  
  
    **[Net Send アドレス]**  
    オペレーターの **net send** アドレスを設定します。  
  
4.  **[ターゲット サーバー]** ページで、マスター サーバーのターゲット サーバーを選択します。  
  
    **[登録済みサーバー]**  
    Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に登録されているサーバーで、まだターゲット サーバーになっていないものを一覧表示します。  
  
    **[ターゲット サーバー]**  
    ターゲット サーバーであるサーバーを一覧表示します。  
  
    **>**  
    選択したサーバーをターゲット サーバーの一覧に移動します。  
  
    **>>**  
    すべてのサーバーをターゲット サーバーの一覧に移動します。  
  
    **<**  
    選択したサーバーをターゲット サーバーの一覧から削除します。  
  
    **<<**  
    すべてのサーバーをターゲット サーバーの一覧から削除します。  
  
    **[接続の追加]**  
    サーバーを登録せずにターゲット サーバーの一覧に追加します。  
  
    **[接続]**  
    選択したサーバーの接続プロパティを変更します。  
  
5.  **[マスター サーバー ログインの資格情報]** ページで、必要に応じてターゲット サーバーの新しいログインを作成してマスター サーバーへの権利を割り当てるかどうかを指定します。  
  
    **[必要に応じて新しいログインを作成し、MSX へのアクセス権を割り当てる]**  
    指定されたログインが存在しない場合に、新しいログインをターゲット サーバーに作成します。  
  
## <a name="TsqlProcedure"></a>Transact-SQL の使用  
  
#### <a name="to-make-a-master-server"></a>マスター サーバーを作成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde_md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、現在のサーバーを AdventureWorks1 マスター サーバーに追加します。 現在のサーバーの場所は、Building 21 の Room 309 の Rack 5 です。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
詳細については、「 [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)」を参照してください。  
  
## <a name="see-also"></a>参照  
[マルチサーバー環境の作成](../../ssms/agent/create-a-multiserver-environment.md)  
[エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
