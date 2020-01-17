---
title: マスター サーバーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.msxwiz.complete.f1
- sql12.ag.msxwiz.target.f1
- sql12.ag.msxwiz.login.f1
- sql12.ag.msxwiz.cover.f1
- sql12.ag.msxwiz.operator.f1
helpviewer_keywords:
- master servers [SQL Server], creating
- wizards [SQL Server Management Studio], Master Server Wizard
- SQL Server Agent jobs, master servers
- Master Server Wizard
ms.assetid: 05739a73-1fdf-4d9d-92a6-70f328380322
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca0e79c617db6cc2906ac9225efd92e156699951
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68189133"
---
# <a name="make-a-master-server"></a>マスター サーバーの作成
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してマスター サーバー [!INCLUDE[tsql](../../includes/tsql-md.md)]を作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [Security](#Security)  
  
-   **マスター サーバーを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Security"></a> セキュリティ  
 プロキシに関連付けられているステップがある分散ジョブは、ターゲット サーバーのプロキシ アカウントのコンテキストで実行されます。 次の条件を満たしていることを確認してください。満たしていないと、プロキシに関連付けられているジョブ ステップがマスター サーバーから対象サーバーにダウンロードされません。  
  
-   マスター サーバー レジストリのサブキー **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<*instance_name*> \SQL Server Agent\AllowDownloadedJobsToMatchProxyName** (REG_DWORD) が 1 (true) に設定します。 既定では、この値は 0 (false) に設定されます。  
  
-   ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前を持つターゲット サーバーにプロキシ アカウントが存在すること。  
  
 マスター サーバーからターゲット サーバーにプロキシ アカウントをダウンロード中に、これらのアカウントを使用するジョブ ステップが失敗した場合は、**msdb** データベースの **sysdownloadlist** テーブルの **error_message** 列を参照して、以下のエラー メッセージの有無を確認します。  
  
-   "ジョブ ステップではプロキシ アカウントが必要ですが、ターゲット サーバーで一致するプロキシが無効です。"  
  
     このエラーを解決するには、 **AllowDownloadedJobsToMatchProxyName** レジストリ サブキーを 1 に設定します。  
  
-   "プロキシ アカウントが見つかりませんでした。"  
  
     このエラーを解決するには、ターゲット サーバー上にプロキシ アカウントが存在し、ジョブ ステップを実行するマスター サーバー プロキシ アカウントと同じ名前が付けられているかどうかを確認します。  
  
####  <a name="Permissions"></a> Permissions  
 このプロシージャの実行権限は、既定では `sysadmin` 固定サーバー ロールのメンバーに与えられています。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-make-a-master-server"></a>マスター サーバーを作成するには  
  
1.  **オブジェクト エクスプローラー** で、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチサーバーの管理]** をポイントして、 **[マスター サーバーに設定]** をクリックします。 **マスター サーバー ウィザード** を使用してマスター サーバーを作成し、対象サーバーを追加します。  
  
3.  **[マスター サーバー オペレーター]** ページで、マスター サーバーのオペレーターを設定します。電子メールまたはポケットベルを使用してオペレーターに通知を送信するには、電子メールが送信されるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを設定しておく必要があります。 **net send**を使用してオペレーターに通知を送信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが置かれているサーバーで Messenger サービスが実行されている必要があります。  
  
     **[電子メール アドレス]**  
     オペレーターの電子メール アドレスを設定します。  
  
     **[ポケットベル アドレス]**  
     オペレーターのポケットベル メール アドレスを設定します。  
  
     **[Net Send アドレス]**  
     オペレーターの **net send** アドレスを設定します。  
  
4.  **[対象サーバー]** ページで、マスター サーバーの対象サーバーを選択します。  
  
     **[登録済みサーバー]**  
     Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] に登録されているサーバーで、まだターゲット サーバーになっていないものを一覧表示します。  
  
     **[対象サーバー]**  
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
  
5.  **[マスター サーバー ログインの資格情報]** ページで、必要に応じて対象サーバーの新しいログインを作成してマスター サーバーへの権利を割り当てるかどうかを指定します。  
  
     **[必要に応じて新しいログインを作成し、MSX へのアクセス権を割り当てる]**  
     指定されたログインが存在しない場合に、新しいログインをターゲット サーバーに作成します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-make-a-master-server"></a>マスター サーバーを作成するには  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続します。  
  
2.  [標準] ツール バーの **[新しいクエリ]** をクリックします。  
  
3.  次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。 この例では、現在のサーバーを AdventureWorks1 マスター サーバーに追加します。 現在のサーバーの場所は、Building 21 の Room 309 の Rack 5 です。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_msx_enlist N'AdventureWorks1',   
    N'Building 21, Room 309, Rack 5' ;   
GO;  
```  
  
 詳細については、次を参照してください。 [sp_msx_enlist &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)します。  
  
## <a name="see-also"></a>参照  
 [マルチサーバー環境の作成](create-a-multiserver-environment.md)   
 [エンタープライズ全体の管理の自動化](automated-administration-across-an-enterprise.md)  
  
  
