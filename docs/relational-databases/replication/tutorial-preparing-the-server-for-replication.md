---
title: チュートリアル:レプリケーションの準備
description: このチュートリアルでは、Windows アカウントを作成し、スナップショット フォルダーを準備して、ディストリビューションを構成することで、レプリケーション用のパブリッシャー、ディストリビューター、サブスクライバーを準備する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: quickstart
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 09d68b763d967b6bcea4853f40bfc2ee2694421b
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75320449"
---
# <a name="tutorial-prepare-sql-server-for-replication-publisher-distributor-subscriber"></a>チュートリアル:レプリケーション用の SQL Server の準備 (パブリッシャー、ディストリビューター、サブスクライバー)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
レプリケーション トポロジを構成するには、事前にセキュリティ計画を立てることが重要です。 このチュートリアルでは、レプリケーション トポロジのセキュリティを向上する方法について説明します。 また、データのレプリケーションの最初の手順である配布の構成方法についても説明します。 他のチュートリアルを行う前に、まずこのチュートリアルを実行してください。  
  
> [!NOTE]  
> サーバー間でデータを安全にレプリケートするには、「[レプリケーション セキュリティの推奨事項](../../relational-databases/replication/security/replication-security-best-practices.md)」の推奨事項をすべて実践してください。  
  
## <a name="what-you-will-learn"></a>学習する内容  
このチュートリアルでは、サーバーを準備し、レプリケーションを最小の特権で安全に実行できるようにする方法を説明します。  

このチュートリアルでは、次の内容を学習します。
> [!div class="checklist"]
> * レプリケーション用の Windows アカウントを作成する。
> * スナップショット フォルダーを準備する。
> * ディストリビューションを構成する。

## <a name="prerequisites"></a>前提条件
このチュートリアルは、データベースの基本的な操作は理解しているが、レプリケーション機能についてはあまり詳しくないユーザーを対象としています。 

このチュートリアルを実行するには、SQL Server、SQL Server Management Studio (SSMS)、および AdventureWorks データベースが必要です。  
  
- パブリッシャー サーバー側 (レプリケーション元) に以下をインストールします。  
  
   - SQL Server Express または SQL Server Compact を除く [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の任意のエディション。 除外されているエディションはレプリケーションのパブリッシャーとして使用できません。   
   - [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] サンプル データベース。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。  
  
- サブスクライバー サーバー (レプリケーション先) に、[!INCLUDE[ssEW](../../includes/ssew-md.md)] を除く [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の任意のエディションをインストールします。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] は、トランザクション レプリケーションのサブスクライバーとして使用できません。  
  
- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールします。
- [AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases)をダウンロードします。 SSMS でデータベースを復元する方法の詳細については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)に関するページを参照してください。 
    
>[!NOTE]
> - 3 つ以上離れたバージョンの SQL Server インスタンスでは、レプリケーションはサポートされていません。 詳細については、「[Supported SQL Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)」(レプリケーション トポロジでサポートされている SQL Server のバージョン) を参照してください。
> - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、固定サーバー ロール **sysadmin** のメンバーとしてログインし、パブリッシャーとサブスクライバーに接続する必要があります。 このロールの詳細については、「[サーバー レベルのロール](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles)」を参照してください。  


**このチュートリアルの推定所要時間: 30 分**
  
## <a name="create-windows-accounts-for-replication"></a>レプリケーション用の Windows アカウントの作成
このセクションでは、レプリケーション エージェントを実行するための Windows アカウントを作成します。 また、次のエージェントを実行するための別の Windows アカウントをローカル サーバー上に作成します。  
  
|エージェント|Location|アカウント名|  
|---------|------------|----------------|  
|スナップショット エージェント|Publisher|<*machine_name*>\repl_snapshot|  
|ログ リーダー エージェント (Log Reader Agent)|Publisher|<*machine_name*>\repl_logreader|  
|ディストリビューション エージェント|パブリッシャーおよびサブスクライバー|<*machine_name*>\repl_distribution|  
|[マージ エージェント]|パブリッシャーおよびサブスクライバー|<*machine_name*>\repl_merge|  
  
> [!NOTE]  
> このレプリケーション チュートリアルでは、パブリッシャーとディストリビューターで同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス (NODE1\SQL2016) を共有します。 サブスクライバー インスタンス (NODE2 \ SQL2016) はリモートです。 パブリッシャーとサブスクライバーが同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを共有することもできますが、これは必須条件ではありません。 パブリッシャーとサブスクライバーが同じインスタンスを共有している場合、サブスクライバー側でアカウントの作成に使用される手順は必要ありません。  

### <a name="create-local-windows-accounts-for-replication-agents-at-the-publisher"></a>パブリッシャー側でレプリケーション エージェントを実行するためのローカル Windows アカウントを作成する
  
1. パブリッシャー側で、[コントロール パネル] の **[管理ツール]** から **[コンピューターの管理]** を開きます。  
  
2. **[システム ツール]** の **[ローカル ユーザーとグループ]** を展開します。  
  
3. **[ユーザー]** を右クリックし、 **[新しいユーザー]** を選択します。  
     
4. **[ユーザー名]** ボックスに「**repl_snapshot**」と入力し、パスワードおよびその他の必要な情報を入力し、 **[作成]** を選択して repl_snapshot アカウントを作成します。 

   ![[新しいユーザー] ダイアログ ボックス](media/tutorial-preparing-the-server-for-replication/newuser.png)
  
5. 同様に、repl_logreader、repl_distribution、repl_merge の各アカウントを作成します。  
 
   ![ユーザーのレプリケーションのリスト](media/tutorial-preparing-the-server-for-replication/replusers.png)
  
6. **[閉じる]** を選択します。  
  
### <a name="create-local-windows-accounts-for-replication-agents-at-the-subscriber"></a>サブスクライバー側でレプリケーション エージェントを実行するためのローカル Windows アカウントを作成する  
  
1. サブスクライバー側で、[コントロール パネル] の **[管理ツール]** から **[コンピューターの管理]** を開きます。  
  
2. **[システム ツール]** の **[ローカル ユーザーとグループ]** を展開します。  
  
3. **[ユーザー]** を右クリックし、 **[新しいユーザー]** を選択します。  
  
4. **[ユーザー名]** ボックスに「 **repl_distribution** 」と入力し、パスワードおよびその他の必要な情報を入力し、 **[作成]** を選択して repl_distribution アカウントを作成します。  
  
5. 同様にして、repl_merge アカウントも作成します。  
  
6. **[閉じる]** を選択します。  

詳細については、「[レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)」を参照してください。  

## <a name="prepare-the-snapshot-folder"></a>スナップショット フォルダーの準備
このセクションでは、パブリケーション スナップショットの作成と保存に使用されるスナップショット フォルダーを構成します。 

### <a name="create-a-share-for-the-snapshot-folder-and-assign-permissions"></a>スナップショット フォルダーの共有を作成し、アクセス許可を与える  
  
1. エクスプローラーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ フォルダーを参照します。 既定の場所は、C:\Program Files\Microsoft SQL Server\MSSQL.X\MSSQL\Data です。  
  
2. **repldata**という名前の新しいフォルダーを作成します。  
  
3. フォルダーを右クリックし、 **[プロパティ]** を選択します。  
  
   a. **[repldata のプロパティ]** ダイアログ ボックスの **[共有]** タブで、 **[詳細な共有]** を選択します。  
  
   b. **[詳細な共有]** ダイアログ ボックスで、 **[このフォルダーを共有する]** を選択し、 **[アクセス許可]** を選択します。  

   ![repldata フォルダーを共有する選択](media/tutorial-preparing-the-server-for-replication/repldata.png)

6. **[repldata のアクセス許可]** ダイアログ ボックスで **[追加]** を選択します。 **[ユーザー、コンピューター、サービス アカウントまたはグループの選択]** ボックスに、前に作成したスナップショット エージェント アカウントの名前 (<*パブリッシャー コンピューター名*> **\repl_snapshot**) を入力します。 **[名前の確認]** を選択し、 **[OK]** を選択します。  

   ![共有アクセス許可を追加する選択](media/tutorial-preparing-the-server-for-replication/addshareperms.png)

7. 手順 6 を繰り返して以前に作成したその他の 2 つのアカウント <*パブリッシャー コンピューター名*> **\repl_merge** と <*パブリッシャー コンピューター名*> **\repl_distribution** を追加します。

8. 3 つのアカウントを追加したら、次のアクセス許可を割り当てます。      
   - repl_distribution: **読み取り**  
   - repl_merge: **読み取り**  
   - repl_snapshot: **フル コントロール**    

   ![各アカウントの共有のアクセス許可](media/tutorial-preparing-the-server-for-replication/sharedpermissions.png)

9. 共有のアクセス許可が正しく構成されたら、 **[OK]** を選択して、 **[repldata のアクセス許可]** ダイアログ ボックスを閉じます。 **[OK]** を選択して **[詳細な共有]** ダイアログ ボックスを閉じます。 

10. **[repldata のプロパティ]** ダイアログ ボックスで、 **[セキュリティ]** タブを選択し、 **[編集]** を選択します。  

    ![[セキュリティ] タブの [編集] ボタン](media/tutorial-preparing-the-server-for-replication/editsecurity.png)   

11. **[repldata のアクセス許可]** ダイアログ ボックスで **[追加]** を選択します。 **[ユーザー、コンピューター、サービス アカウントまたはグループの選択]** ボックスに、前に作成したスナップショット エージェント アカウントの名前 (<*パブリッシャー コンピューター名*> **\repl_snapshot**) を入力します。 **[名前の確認]** を選択し、 **[OK]** を選択します。  

    ![セキュリティ アクセス許可を追加する選択](media/tutorial-preparing-the-server-for-replication/addsecuritypermissions.png)

  
12. 前の手順を繰り返して、ディストリビューション エージェント (<*パブリッシャー コンピューター名*> **\repl_distribution**) とマージ エージェント (<*パブリッシャー コンピューター名*> **\repl_merge**) のアクセス許可を追加します。  
    
  
13. 次のアクセス許可が与えられていることを確認します。  
  
    - repl_distribution: **読み取り**
    - repl_merge: **読み取り**
    - repl_snapshot: **フル コントロール**   
 
    ![レプリケーション データに必要なユーザー アクセス許可](media/tutorial-preparing-the-server-for-replication/replpermissions.png) 

14. **[共有]** タブをもう一度選択し、共有の **[ネットワーク パス]** をメモします。 後でスナップショット フォルダーを構成するときにこのパスが必要になります。  

    ![[共有] タブのネットワーク パス](media/tutorial-replicating-data-between-continuously-connected-servers/networkpath.png)

15. **[OK]** を選択して **[repldata のプロパティ]** ダイアログ ボックスを閉じます。 
 
詳細については、「[スナップショット フォルダーのセキュリティ保護](../../relational-databases/replication/security/secure-the-snapshot-folder.md)」を参照してください。  
  

## <a name="configure-distribution"></a>ディストリビューションを構成する
このセクションでは、パブリッシャー側のディストリビューションを構成し、パブリケーション データベースとディストリビューション データベースに対して必要なアクセス許可を設定します。 ディストリビューターを構成済みの場合は、このセクションを開始する前に、パブリッシングとディストリビューションを無効にする必要があります。 特に実稼働環境で既存のレプリケーション トポロジを維持する必要がある場合は、このレッスンを実行しないでください。   
  
パブリッシャー側のリモート ディストリビューターの構成は、このチュートリアルの対象外です。  

### <a name="configure-distribution-at-the-publisher"></a>パブリッシャー側でディストリビューションを構成する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開します。  
  
2. **[レプリケーション]** フォルダーを右クリックし、 **[ディストリビューションの構成]** を選択します。  

   ![ショートカット メニューの [ディストリビューションの構成] コマンド](media/tutorial-preparing-the-server-for-replication/configuredistribution.png)
  
   > [!NOTE]  
   > 実際のサーバー名ではなく **localhost** を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が **localhost** に接続できないことを示す警告が表示されます。 警告ダイアログで **[OK]** を選択します。 **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバー名]** を **localhost** から使用しているサーバーの名前に変更します。 次に、 **[接続]\(Connect\)** を選択します。  
  
   ディストリビューション構成ウィザードが起動します。  
  
3. **[ディストリビューター]** ページで、[< *'サーバー名'* >  **を独自のディストリビューターとする (SQL Server はディストリビューション データベースとログを作成します)]** を選択します。 **[次へ]** を選択します。  

   ![サーバーを独自のディストリビューターとするオプション](media/tutorial-preparing-the-server-for-replication/serverdistributor.png)
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されていない場合は、 **[[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの起動]** ページで、 **[はい、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを自動的に開始するように構成します]** を選択します。 **[次へ]** を選択します。  

     
5. **[スナップショット フォルダー]** ボックスにパス \\\\<*パブリッシャー コンピューター名*> **\repldata** を入力し、 **[次へ]** を選択します。 このパスは、共有のプロパティを構成した後に repldata のプロパティ フォルダーの **[ネットワーク パス]** に以前表示されていたパスと一致する必要があります。 

   ![[repldata のプロパティ] ダイアログ ボックスとディストリビューション構成ウィザードのネットワークパスの比較](media/tutorial-preparing-the-server-for-replication/repldatasnapshot.png)
  
6. ウィザードの残りのページでは、既定値をそのまま使用します。  
    
   ![ウィザードの最後のページ](media/tutorial-preparing-the-server-for-replication/distributionwizarddefaults.png)
  
7. **[完了]** をクリックしてディストリビューションを有効にします。 

ディストリビューターを構成するときに次のエラーが表示される可能性があります。 これは、SQL Server エージェント アカウントの開始に使用されたアカウントが、システムの管理者ではないことを示します。 SQL Server エージェントを手動で開始して、既存のアカウントにこれらのアクセス許可を付与するか、SQL Server エージェントが使用するアカウントを変更する必要があります。 

![SQL Server エージェントを構成する際のエラー メッセージ](media/tutorial-preparing-the-server-for-replication/startingagenterror.png)

SQL Server Management Studio インスタンスが管理者権限で実行されている場合は、SSMS 内から手動で SQL エージェントを起動できます。  
    
![SSMS のエージェントのショートカット メニューで [開始] を選択する](media/tutorial-preparing-the-server-for-replication/ssmsstartagent.png) 

>[!NOTE]
> SQL エージェントが自動的に起動しない場合は、SSMS で SQL Server エージェントを右クリックし、 **[更新]** を選択します。 それでも停止状態である場合、SQL Server 構成マネージャーから手動で起動します。    
  
## <a name="set-database-permissions"></a>データベースのアクセス許可を設定する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[セキュリティ]** を展開して **[ログイン]** を右クリックし、 **[新しいログイン]** をクリックします。  

   ![ショートカット メニューの [新しいログイン] コマンド](media/tutorial-preparing-the-server-for-replication/newlogin.png)
  
2. **[全般]** ページで、 **[検索]** を選択します。 **[選択するオブジェクト名を入力します]** ボックスに「<*パブリッシャー コンピューター名*> **\repl_snapshot**」と入力し、 **[名前の確認]** を選択して、 **[OK]** を選択します。  

   ![オブジェクト名を入力する際の選択](media/tutorial-preparing-the-server-for-replication/addsnapshotlogin.png)
  
3. **[このログインにマップされたユーザー]** の一覧にある **[ユーザー マッピング]** ページで、**ディストリビューション** データベースと [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの両方を選択します。  
  
   [データベース ロールのメンバーシップ] の一覧で、両方のデータベースのログイン用に **db_owner** ロールを選択します。  

   ![データベースとそのロールの選択](media/tutorial-preparing-the-server-for-replication/dbowner.png)
  
4. **[OK]** を選択して、ログインを作成します。  
  
5. その他のローカル アカウント (repl_distribution、repl_logreader、および repl_merge) のログインを作成するために手順 1 ～ 4 を繰り返します。 これらのログインも、**ディストリビューション** データベースと **AdventureWorks** データベースの固定データベース ロール **db_owner** のメンバーとなっているユーザーにマップする必要があります。  

   ![オブジェクト エクスプローラーの 4 つのアカウントすべてが表示された画面](media/tutorial-preparing-the-server-for-replication/usersinssms.png)
   
  
詳細については、次を参照してください。
- [ディストリビューションの構成](../../relational-databases/replication/configure-distribution.md) 
- [レプリケーション エージェントのセキュリティ モデル](../../relational-databases/replication/security/replication-agent-security-model.md)  

## <a name="next-steps"></a>次のステップ
サーバーをレプリケーション用に正常に準備しました。 次の記事では、トランザクション レプリケーションを構成する方法を説明します。 

> [!div class="nextstepaction"]
> [チュートリアル:2 つの常時接続サーバー間のレプリケーション (トランザクション) を構成する](tutorial-replicating-data-between-continuously-connected-servers.md)

  
  
