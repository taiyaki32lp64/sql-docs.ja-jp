---
title: チュートリアル:トランザクション レプリケーションの構成
description: このチュートリアルでは、常時接続の 2 つの SQL Server 間でトランザクション レプリケーションを構成する方法を説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- replication [SQL Server], tutorials
- wizards [SQL Server replication]
ms.assetid: 7b18a04a-2c3d-4efe-a0bc-c3f92be72fd0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 603846718e4e21c7af8ee81d94210d12242c35c7
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321929"
---
# <a name="tutorial-configure-replication-between-two-fully-connected-servers-transactional"></a>チュートリアル:2 つの常時接続サーバー間のレプリケーション (トランザクション) を構成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
トランザクション レプリケーションは、常時接続サーバー間でデータを移動する際の問題を解決する有効なソリューションです。 レプリケーション ウィザードを使用すると、レプリケーション トポロジを簡単に設定し、管理できます。 

このチュートリアルでは、常時接続サーバー間にトランザクション レプリケーション トポロジを設定する方法を学習します。 トランザクション レプリケーションのしくみについては、[トランザクション レプリケーションの概要](https://docs.microsoft.com/sql/relational-databases/replication/transactional/transactional-replication)に関するページを参照してください。 
  
## <a name="what-you-will-learn"></a>学習する内容  
このチュートリアルでは、トランザクション レプリケーションによって 1 つのデータベースから別のデータベースにデータをパブリッシュする方法について説明します。  

このチュートリアルでは、次の内容を学習します。
> [!div class="checklist"]
> * トランザクション レプリケーションを使用してパブリッシャーを作成する。
> * トランザクション パブリッシャーのサブスクライバーを作成する。
> * サブスクリプションを検証し、待機時間を計測する。
  
  
## <a name="prerequisites"></a>前提条件  
このチュートリアルは、データベースの基本的な操作は理解しているが、レプリケーション機能についてはあまり詳しくないユーザーを対象としています。 このチュートリアルを行うには、[チュートリアル: レプリケーション用の SQL Server の準備](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)に関するページを完了しておく必要があります。  
  
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
  
  
**このチュートリアルの推定所要時間: 60 分**  
  
## <a name="configure-the-publisher-for-transactional-replication"></a>トランザクション レプリケーションのパブリッシャーを構成する
このセクションでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してトランザクション パブリケーションを作成し、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースの **Product** テーブルからフィルター選択したサブセットをパブリッシュします。 また、ディストリビューション エージェントにより使用される SQL Server ログインをパブリケーション アクセス リスト (PAL) に追加します。


### <a name="create-a-publication-and-define-articles"></a>パブリケーションを作成し、アーティクルを定義する
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開します。  
  
2. **[SQL Server エージェント]** を右クリックし、 **[開始]** を選択します。 パブリケーションを作成する前に、SQL Server エージェントが実行されている必要があります。 この手順でエージェントが起動しない場合は、SQL Server 構成マネージャーから手動で起動する必要があります。 
3. **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを右クリックして、 **[新しいパブリケーション]** を選択します。 この手順で、パブリケーションの新規作成ウィザードが開始されます。  

   ![パブリケーションの新規作成ウィザードを開始するための選択](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
  
3. **[パブリケーション データベース]** ページで [[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]] を選択し、 **[次へ]** を選択します。  
  
4. **[パブリケーションの種類]** ページで **[トランザクション パブリケーション]** を選択し、 **[次へ]** を選択します。  

   ![パブリケーションの種類が選択された [パブリケーションの種類] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/tranrepl.png)
  
5. **[アーティクル]** ページで、 **[テーブル]** ノードを展開し、 **[Product]** チェック ボックスをオンにします。 次に、 **[Product]** を展開し、 **[ListPrice]** と **[StandardCost]** の横のチェック ボックスをオフにします。 **[次へ]** を選択します。  

   ![パブリッシュするアーティクルが選択された [アーティクル] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/replarticles.png)
  
6. **[テーブル行のフィルター選択]** ページで、 **[追加]** を選択します。   
  
7. **[フィルターの追加]** ダイアログ ボックスで **[SafetyStockLevel]** 列を選択します。 右矢印を選択して、フィルター選択クエリの Filter ステートメントの WHERE 句にこの列を追加します。 次に、WHERE 句の修飾子に次のように手動で入力します。  
  
   ```sql  
   WHERE [SafetyStockLevel] < 500  
   ```
  
   ![[テーブル行のフィルター選択] と [フィルターの追加] ダイアログ ボックス](media/tutorial-replicating-data-between-continuously-connected-servers/filter.png)
  
8. **[OK]** を選択し、 **[次へ]** を選択します。  
  
9. **[スナップショットをすぐに作成し、サブスクリプションを初期化できるようにそのスナップショットを保持する]** チェック ボックスをオンにして、 **[次へ]** を選択します。  

   ![チェック ボックスがオンの [スナップショット エージェント] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/snapshot.png)
  
10. **[エージェント セキュリティ]** ページで、 **[スナップショット エージェントのセキュリティ設定を使用する]** チェック ボックスをオフにします。   
  
    スナップショット エージェントの **[セキュリティ設定]** を選択します。 **[プロセス アカウント]** ボックスに「<*パブリッシャー コンピューター名*> **\repl_snapshot**」と入力し、このアカウントのパスワードを入力して **[OK]** をクリックします。  

    ![[エージェント セキュリティ] ページと [スナップショット エージェントのセキュリティ] ダイアログ ボックス](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagentsecurity.png)
  
12. 同様に、ログ リーダー エージェントのプロセス アカウントとして <*パブリッシャー コンピューター名*> **\repl_logreader** を設定します。 **[OK]** をクリックします。  

    ![[ログ リーダー エージェントのセキュリティ] ダイアログ ボックスと [エージェント セキュリティ] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/logreaderagentsecurity.png)   

  
13. **[ウィザードの完了]** ページで、 **[パブリケーション名]** ボックスに「**AdvWorksProductTrans**」と入力し、 **[完了]** を選択します。  

    ![パブリケーション名が表示された [ウィザードの完了] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/advworksproducttrans.png)
  
14. パブリケーションが作成されたら、 **[閉じる]** を選択してウィザードを閉じます。 

パブリケーションを作成しようとしたときに、SQL Server エージェントが実行されていないと、次のエラーが発生する可能性があります。 このエラーは、パブリケーションは正常に作成されたが、スナップショット エージェントが起動できなかったことを示しています。 これが発生した場合は、SQL Server エージェントを起動してから、手動でスナップショット エージェントを起動する必要があります。 次のセクションで手順について説明します。 

![スナップショット エージェントが起動に失敗したという警告](media/tutorial-replicating-data-between-continuously-connected-servers/snapshotagenterror.png)
    
  
### <a name="view-the-status-of-snapshot-generation"></a>スナップショット生成の状態を表示する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksProductTrans]** を右クリックして、 **[スナップショット エージェントの状態の表示]** を選択します。  
   ![スナップショット エージェントの状態を表示することができるショートカット メニューのコマンド](media/tutorial-replicating-data-between-continuously-connected-servers/viewsnapshot.png)
  
3. パブリケーションのスナップショット エージェントの現在の状態が表示されます。 スナップショット ジョブが正常に終了していることを確認してから次のセクションに進みます。
          
パブリケーションを作成したときに、SQL Server エージェントが実行されていないと、パブリケーションのスナップショット エージェントの状態を確認したときに、スナップショット エージェントの '実行履歴がない' と表示されます。 その場合は、 **[開始]** を選択して、スナップショット エージェントを起動します。 

![[開始] ボタンと、スナップショット エージェントが実行されたことを示す状態の変更メッセージ](media/tutorial-replicating-data-between-continuously-connected-servers/startsnapshotagent.png)
     
ここでエラーが発生する場合は、[スナップショット エージェント エラーのトラブルシューティング](troubleshoot-tran-repl-errors.md#find-errors-with-the-snapshot-agent)に関するページを参照してください。


  
### <a name="add-the-distribution-agent-login-to-the-pal"></a>ディストリビューション エージェントのログインを PAL に追加する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksProductTrans]** パブリケーションを右クリックして、 **[プロパティ]** を選択します。  **[パブリケーションのプロパティ]** ダイアログ ボックスが表示されます。    
  
   a. **[パブリケーション アクセス リスト]** ページを選択して、 **[追加]** を選択します。  
   b. **[パブリケーション アクセスの追加]** ダイアログ ボックスで、<*パブリッシャー コンピューター名*> **\repl_distribution** を選択して **[OK]** を選択します。
   
   ![パブリケーション アクセス リストにログインを追加する選択](media/tutorial-replicating-data-between-continuously-connected-servers/tranreplproperties.png)

詳細については、「[レプリケーションのプログラミング概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)」を参照してください。  
  

## <a name="create-a-subscription-to-the-transactional-publication"></a>トランザクション パブリケーションへのサブスクリプションの作成
このセクションでは、前の手順で作成したパブリケーションにサブスクライバーを追加します。 このチュートリアルでは、リモート サブスクライバー (NODE2\SQL2016) を使用しますが、ローカルでパブリッシャーにサブスクリプションを追加することもできます。 

### <a name="create-the-subscription"></a>サブスクリプションを作成する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksProductTrans]** パブリケーションを右クリックして、 **[新しいサブスクリプション]** を選択します。 サブスクリプションの新規作成ウィザードが起動します。 
 
   ![サブスクリプションの新規作成ウィザードを起動する選択](media/tutorial-replicating-data-between-continuously-connected-servers/newsub.png)     
  
3. **[パブリケーション]** ページで **[AdvWorksProductTrans]** を選択し、 **[次へ]** を選択します。  

   ![パブリケーションが選択された [パブリケーション] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/selectpub.png)
  
4. **[ディストリビューション エージェントの場所]** ページで、 **[ディストリビューターですべてのエージェントを実行する]** を選択し、 **[次へ]** を選択します。  プル サブスクリプションとプッシュ サブスクリプションの詳細については、「[パブリケーションのサブスクライブ](https://docs.microsoft.com/sql/relational-databases/replication/subscribe-to-publications)」を参照してください。

   ![ディストリビューターですべてのエージェントを実行するオプションが選択された [ディストリビューション エージェントの場所] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/runagentsatdist.png)
  
5. **[サブスクライバー]** ページでサブスクライバー インスタンスの名前が表示されない場合は、 **[サブスクライバーの追加]** を選択し、ドロップダウン リストから **[SQL Server サブスクライバーの追加]** を選択します。 この手順で、 **[サーバーへの接続]** ダイアログ ボックスが開きます。 サブスクライバー インスタンス名を入力し、 **[接続]** を選択します。  
    
   サブスクライバーが追加されたら、そのサブスクライバーのインスタンス名の横にあるチェック ボックスをオンにします。 次に、 **[サブスクリプション データベース]** の下で **[新しいデータベース]** を選択します。   

   ![サブスクライバー サーバーの追加が選択された [サブスクライバー] ページ](media/tutorial-replicating-data-between-continuously-connected-servers/addsub.png)

7. **[新規データベース]** ダイアログ ボックスが表示されます。 **[データベース名]** ボックスに「**ProductReplica**」と入力し、 **[OK]** 、 **[次へ]** の順に選択します。 
  
   ![サブスクリプション データベースの名前を入力する](media/tutorial-replicating-data-between-continuously-connected-servers/productreplica.png)
  
8. **[ディストリビューション エージェント セキュリティ]** ページで、省略記号 ( **...** ) ボタンを選択します。 **[プロセス アカウント]** ボックスに「<*パブリッシャー コンピューター名*> **\repl_distribution**」を入力し、次に、このアカウントのパスワードを入力して、 **[OK]** 、 **[次へ]** の順に選択します。

   ![[ディストリビューション エージェント セキュリティ] ダイアログ ボックスのディストリビューション アカウント情報](media/tutorial-replicating-data-between-continuously-connected-servers/adddistaccount.png)
  
9. 以降のページでは既定値をそのまま採用し、 **[完了]** を選択してウィザードを終了します。  
  
### <a name="set-database-permissions-at-the-subscriber"></a>サブスクライバー側のデータベース権限を設定する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でサブスクライバーに接続します。 **[セキュリティ]** を展開して **[ログイン]** を右クリックし、 **[新しいログイン]** をクリックします。     
  
   a. **[全般]** ページの **[ログイン名]** の下で **[検索]** を選択し、<*サブスクライバー コンピューター名*> **\repl_distribution** のログインを追加します。

   b. **[ユーザー マッピング]** ページで、**ProductReplica** データベースにログイン **db_owner** メンバーシップを付与します。 

   ![サブスクライバーのログインを構成する選択](media/tutorial-replicating-data-between-continuously-connected-servers/loginforsub.png)

2. **[OK]** を選択して、 **[新しいログイン]** ダイアログ ボックスを閉じます。 

  
### <a name="view-the-synchronization-status-of-the-subscription"></a>サブスクリプションの同期状態を表示する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続します。 サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーで、**AdvWorksProductTrans** パブリケーションを展開し、**ProductReplica** データベースのサブスクリプションを右クリックして、 **[同期の状態の表示]** を選択します。 サブスクリプションの現在の同期状態が表示されます。

   ![[同期の状態の表示] ダイアログ ボックスを開く選択](media/tutorial-replicating-data-between-continuously-connected-servers/viewsyncstatus.png)
3. **[AdvWorksProductTrans]** の下にサブスクリプションが表示されない場合は、F5 キーを押して一覧を更新します。  
  
詳細については、次を参照してください。  
- [スナップショットを使用したサブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)  
- [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  

## <a name="measure-replication-latency"></a>レプリケーションの待機時間を計測する
このセクションでは、トレーサー トークンを使って、変更内容がサブスクライバーにレプリケートされているかどうかを確認し、待機時間を決定します。 待機時間は、パブリッシャー側で行われた変更がサブスクライバーに表示されるのにかかる時間です。
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続します。 サーバー ノードを展開して **[レプリケーション]** フォルダーを右クリックし、 **[レプリケーション モニターの起動]** を選択します。

   ![ショートカット メニューの [レプリケーション モニターの起動] コマンド](media/tutorial-replicating-data-between-continuously-connected-servers/launchreplmonitor.png)

2. 左ペインでパブリッシャー グループを展開し、パブリッシャー インスタンスを展開して、 **[AdvWorksProductTrans]** パブリケーションを選択します。  
  
   a. **[トレーサー トークン]** タブを選択します。  
   b. **[トレーサーの挿入]** を選択します。    
   c. 次の列にトレーサー トークンの経過時間を表示します。 **[Publisher to Distributor]\(パブリッシャーからディストリビューターまで\)** 、 **[Distributor to Subscriber]\(ディストリビューターからサブスクライバーまで\)** 、 **[合計待機時間]** 。 **[保留中]** と表示された場合は、トークンが特定のポイントに到達していないことを示します。

   ![トレーサー トークンの情報](media/tutorial-replicating-data-between-continuously-connected-servers/tracertoken.png)


詳細については、次を参照してください。 
- [トランザクション レプリケーションの待機時間の計測および接続の検証](../../relational-databases/replication/monitor/measure-latency-and-validate-connections-for-transactional-replication.md)
- [トランザクション レプリケーション エージェントでエラーを見つける](troubleshoot-tran-repl-errors.md)


## <a name="next-steps"></a>次のステップ
トランザクション レプリケーション用にパブリッシャーとサブスクライバーの両方を正しく構成しました。 これで、パブリッシャーで **Product** テーブルに対してデータを挿入、更新、または削除することができます。 その後、サブスクライバーで **Product** テーブルに対してクエリを実行して、レプリケートされた変更を表示することができます。 

次の記事では、マージ レプリケーションを構成する方法について説明します。  

> [!div class="nextstepaction"]
> [チュートリアル:サーバーとモバイル クライアントの間のレプリケーション (マージ) を構成する](tutorial-replicating-data-with-mobile-clients.md)
