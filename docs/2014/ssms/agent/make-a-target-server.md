---
title: ターゲット サーバーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.tsxwiz.msx.f1
- sql12.ag.tsxwiz.cover.f1
- sql12.ag.tsxwiz.credentials.f1
- sql12.ag.tsxwiz.complete.f1
helpviewer_keywords:
- Target Server Wizard
- SQL Server Agent jobs, target servers
- target servers [SQL Server], creating
ms.assetid: 13aabe2d-67fe-4c67-8d49-2928dd705b7a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 744ebc5411e626c083676440502489029e888a28
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798185"
---
# <a name="make-a-target-server"></a>ターゲット サーバーの作成
  このトピックでは、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、[!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクト (SMO) を使用して、ターゲット サーバーを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **ターゲット サーバーを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> Security  
 プロキシに関連付けられているステップがある分散ジョブは、ターゲット サーバーのプロキシ アカウントのコンテキストで実行されます。 次の条件を満たしていることを確認してください。満たしていないと、プロキシに関連付けられているジョブ ステップがマスター サーバーから対象サーバーにダウンロードされません。  
  
-   マスターサーバーレジストリサブキー **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<*instance_name*> \ SQL server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) が 1 (true) に設定されています。 既定では、この値は 0 (false) に設定されます。  
  
-   ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前を持つターゲット サーバーにプロキシ アカウントが存在すること。  
  
 マスター サーバーからターゲット サーバーにプロキシ アカウントをダウンロード中に、これらのアカウントを使用するジョブ ステップが失敗した場合は、**msdb** データベースの **sysdownloadlist** テーブルの **error_message** 列を参照して、以下のエラー メッセージの有無を確認します。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、ターゲット サーバーで一致するプロキシが無効です。"  
  
     このエラーを解決するには、 **AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを 1 に設定します。  
  
-   "プロキシ アカウントが見つかりませんでした。"  
  
     このエラーを解決するには、ターゲット サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
####  <a name="Permissions"></a> アクセス許可  
 このプロシージャの実行権限は、既定では `sysadmin` 固定サーバー ロールのメンバーに与えられています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-make-a-target-server"></a>ターゲット サーバーを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして、 **[対象サーバーに設定]** をクリックします。 **ターゲット サーバー設定ウィザード**を使用して、ターゲット サーバーを設定します。  
  
3.  **[マスター サーバーの選択]** ページで、このターゲット サーバーが受け取るジョブの送信元のマスター サーバーを選択します。  
  
     **[サーバーの選択]**  
     マスター サーバーに接続します。  
  
     **[このサーバーの説明]**  
     このターゲット サーバーの説明を入力します。 この説明はターゲット サーバーからマスター サーバーにアップロードされます。  
  
4.  **[マスター サーバー ログインの資格情報]** ページで、必要に応じてターゲット サーバーに新しいログインを作成します。  
  
     **[必要に応じて新しいログインを作成し、MSX へのアクセス権を割り当てる]**  
     指定されたログインが存在しない場合に、新しいログインをターゲット サーバーに作成します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-make-a-target-server"></a>ターゲット サーバーを作成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、**[実行]** をクリックします。 この例では、現在のサーバーを AdventureWorks1 マスター サーバーに追加します。 現在のサーバーの場所は、Building 21 の Room 309 の Rack 5 です。  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
        N'Building 21, Room 309, Rack 5' ;   
    GO;  
    ```  
  
     詳細については、「 [sp_msx_enlist &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)」を参照してください。  
  
##  <a name="PowerShellProcedure"></a>SQL Server 管理オブジェクト (SMO) の使用  
  
## <a name="see-also"></a>「  
 [エンタープライズ全体の管理の自動化](automated-administration-across-an-enterprise.md)  
