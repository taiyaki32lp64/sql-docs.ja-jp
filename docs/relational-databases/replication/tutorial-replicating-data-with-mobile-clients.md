---
title: チュートリアル:マージ レプリケーションの構成
description: このチュートリアルでは、SQL Server とモバイル クライアントの間のマージ レプリケーションを構成する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 04/03/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: quickstart
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 84a07ef89bc42538a5043a46ed3bcd23bc588caf
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321856"
---
# <a name="tutorial-configure-replication-between-a-server-and-mobile-clients-merge"></a>チュートリアル:サーバーとモバイル クライアントの間のレプリケーション (マージ) を構成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
マージ レプリケーションは、中央のサーバーと、常時接続でないモバイル クライアントの間でデータを移動する際の問題を解決する有効なソリューションです。 レプリケーション ウィザードを使用すると、マージ レプリケーション トポロジを簡単に設定し、管理できます。 

このチュートリアルでは、モバイル クライアント用のレプリケーション トポロジを設定する方法を学習します。 マージ レプリケーションの詳細については、[マージ レプリケーションの概要](https://docs.microsoft.com/sql/relational-databases/replication/merge/merge-replication)に関するページを参照してください
  
## <a name="what-you-will-learn"></a>学習する内容  
このチュートリアルでは、マージ レプリケーションを使用して中央のデータベースから 1 名以上のモバイル ユーザーにデータをパブリッシュし、各ユーザーが独自にフィルター選択されたデータ サブセットを取得するようにする方法を説明します。 

このチュートリアルでは、次の内容を学習します。
> [!div class="checklist"]
> * マージ レプリケーションのパブリッシャーを構成する。
> * マージ パブリケーションのモバイル サブスクライバーを追加する。
> * マージ パブリケーションにサブスクリプションを同期する。
  
## <a name="prerequisites"></a>前提条件  
このチュートリアルは、データベースの基本的な操作は理解しているが、レプリケーション機能についてはあまり詳しくないユーザーを対象としています。 このチュートリアルを行うには、[チュートリアル: レプリケーション用の SQL Server の準備](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)に関するページを完了しておく必要があります。  
  
このチュートリアルを実行するには、SQL Server、SQL Server Management Studio (SSMS)、および AdventureWorks データベースが必要です。 
  
- パブリッシャー サーバー側 (レプリケーション元) に以下をインストールします。  
  
   - SQL Server Express または SQL Server Compact を除く、SQL Server の任意のエディション。 レプリケーションのパブリッシャーとして使用できないため除きます。   
   - [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベース。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。  
  
- サブスクライバー サーバー (レプリケーション先) に、SQL Server Express と SQL Server Compact を除く SQL Server の任意のエディションをインストールします。 このチュートリアルで作成するパブリケーションでは、SQL Server Express と SQL Server Compact のどちらもサポートされていません。 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) をインストールします。
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads) をインストールします。
- [AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases)をダウンロードします。 SSMS でデータベースを復元する方法の詳細については、[データベースの復元](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)に関するページを参照してください。  
 
  
>[!NOTE]
> - 3 つ以上離れたバージョンの SQL Server インスタンスでは、レプリケーションはサポートされていません。 詳細については、「[Supported SQL Versions in Replication Topology](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/)」(レプリケーション トポロジでサポートされている SQL Server のバージョン) を参照してください。
> - [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、固定サーバー ロール **sysadmin** のメンバーとしてログインし、パブリッシャーとサブスクライバーに接続する必要があります。 このロールの詳細については、「[サーバー レベルのロール](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles)」を参照してください。  
  
  
**このチュートリアルの推定所要時間: 60 分**  
  
## <a name="configure-a-publisher-for-merge-replication"></a>マージ レプリケーションのパブリッシャーの構成
このセクションでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してマージ パブリケーションを作成し、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースの **Employee** テーブル、**SalesOrderHeader** テーブル、および **SalesOrderDetail** テーブルのサブセットをパブリッシュします。 ここでは、パラメーター化された行フィルターを使ってこれらのテーブルをフィルター処理し、サブスクリプションごとに一意のデータ部分が含まれるようにします。 また、マージ エージェントにより使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインをパブリケーション アクセス リスト (PAL) に追加します。  
  
### <a name="create-merge-publication-and-define-articles"></a>マージ パブリケーションを作成してアーティクルを定義する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開します。  
  
2. オブジェクト エクスプローラーで [SQL Server エージェント] を右クリックして **[開始]** を選択し、SQL Server エージェントを起動します。 この方法でエージェントが起動しない場合は、SQL Server 構成マネージャーから手動で起動する必要があります。  
3. **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** を右クリックして、 **[新しいパブリケーション]** を選択します。 パブリケーションの新規作成ウィザードが開始します。  

   ![パブリケーションの新規作成ウィザードを開始するための選択](media/tutorial-replicating-data-between-continuously-connected-servers/newpublication.png)
  
3. **[パブリケーション データベース]** ページで [[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]] を選択し、 **[次へ]** を選択します。 

      
4. **[パブリケーションの種類]** ページで、 **[マージ パブリケーション]** を選択し、 **[次へ]** を選択します。  
   
5. **[サブスクライバーの種類]** ページで、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降のみが選択されていることを確認し、 **[次へ]** を選択します。 

    ![[パブリケーションの種類] ページと [サブスクライバーの種類] ページ](media/tutorial-replicating-data-with-mobile-clients/mergerpl.png)
  
   
6. **[アーティクル]** ページで、 **[テーブル]** ノードを展開します。 次の 3 つのテーブルを選択します。**Employee**、**SalesOrderHeader**、および **SalesOrderDetail**。 **[次へ]** を選択します。  

   ![[アーティクル] ページでのテーブルの選択](media/tutorial-replicating-data-with-mobile-clients/mergearticles.png)

   >[!NOTE]
   > **Employee** テーブルには、**hierarchyid** データ型を持つ列 (**OrganizationNode**) が含まれています。 このデータ型は、SQL 2017 でのレプリケーションに対してのみサポートされています。 
   >
   > SQL Server 2017 より前のビルドを使用している場合は、双方向のレプリケーションでこの列を使用するとデータ損失の可能性があることを通知するメッセージが画面の下部に表示されます。 このチュートリアルでは、このメッセージは無視してかまいません。 ただし、このデータ型は、サポートされているビルドを使用している場合を除き、実稼働環境でレプリケートしないでください。
   > 
   > **hierarchyid** データ型のレプリケーションに関する詳細は、「[レプリケートされたテーブルでの hierarchyid 列の使用](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)」を参照してください。
    
  
7. **[テーブル行のフィルター選択]** ページで、 **[追加]** 、 **[フィルターの追加]** の順に選択します。  
  
8. **[フィルターの追加]** ダイアログ ボックスの **[フィルターを適用するテーブルを選択します。]** で、 **[Employee (HumanResources)]** を選択します。 **[LoginID]** 列を選択し、右矢印を選択して、この列をフィルター選択クエリの WHERE 句に追加します。さらに、WHERE 句を次のように修正します。  
  
   ```sql 
    WHERE [LoginID] = HOST_NAME()  
   ```  
  
   **[このテーブルの 1 行を 1 つのサブスクリプションのみに移動する]** を選択して、 **[OK]** を選択します。  
 
   ![フィルターを追加するための選択](media/tutorial-replicating-data-with-mobile-clients/mergeaddfilter.png)

    
  
10. **[テーブル行のフィルター選択]** ページで、 **[Employee (Human Resources)]** 、 **[追加]** の順に選択し、 **[選択したフィルターを拡張するために結合を追加する]** を選択します。  
  
    a. **[結合の追加]** ダイアログ ボックスで、 **[結合テーブル]** の下の **[Sales.SalesOrderHeader]** を選択します。 **[JOIN ステートメントを手動で作成する]** を選択し、次のように JOIN ステートメントを完成させます。  
  
    ```sql  
    ON [Employee].[BusinessEntityID] =  [SalesOrderHeader].[SalesPersonID] 
    ```  
  
    b. **[結合オプションを指定します]** で、 **[一意キー]** を選択して **[OK]** を選択します。

    ![フィルターに結合を追加するための選択](media/tutorial-replicating-data-with-mobile-clients/mergeaddjoin.png)

  
13. **[テーブル行のフィルター選択]** ページで、 **[SalesOrderHeader]** 、 **[追加]** の順に選択し、 **[選択したフィルターを拡張するために結合を追加する]** を選択します。  
  
    a. **[結合の追加]** ダイアログ ボックスで、 **[結合テーブル]** の下の **[Sales.SalesOrderDetail]** をクリックします。    
    b. **[ビルダーを使用してステートメントを作成する]** を選択します。  
    c. **[プレビュー]** ボックスで、JOIN ステートメントが次のようになっていることを確認します。  
  
    ```sql  
    ON [SalesOrderHeader].[SalesOrderID] = [SalesOrderDetail].[SalesOrderID] 
    ```  
  
    d. **[結合オプションを指定します]** で、 **[一意キー]** を選択して **[OK]** を選択します。 **[次へ]** を選択します。 

    ![販売注文の別の結合を追加するための選択](media/tutorial-replicating-data-with-mobile-clients/joinsalestables.png)
  
21. **[スナップショットをすぐに作成する]** を選択し、 **[以下のスケジュールでスナップショット エージェントを実行する]** をオフにして、 **[次へ]** を選択します。  

    ![スナップショットをすぐに作成するための選択](media/tutorial-replicating-data-with-mobile-clients/snapshotagent.png)
  
22. **[エージェント セキュリティ]** ページで、 **[セキュリティの設定]** を選択します。 **[プロセス アカウント]** ボックスに「<*パブリッシャー コンピューター名*> **\repl_snapshot**」と入力し、このアカウントのパスワードを入力して **[OK]** をクリックします。 **[次へ]** を選択します。  

    ![スナップショット エージェントのセキュリティ設定の選択](media/tutorial-replicating-data-with-mobile-clients/snapshotagentsecurity.png)
  
23. **[ウィザードの完了]** ページで、 **[パブリケーション名]** ボックスに「**AdvWorksSalesOrdersMerge**」と入力し、 **[完了]** を選択します。  

    ![パブリケーション名が表示された [ウィザードの完了] ページ](media/tutorial-replicating-data-with-mobile-clients/namemergerepl.png)
  
24. パブリケーションが作成されたら、 **[閉じる]** を選択します。 **オブジェクト エクスプローラー**で **[レプリケーション]** ノードの下の **[ローカル パブリケーション]** を右クリックして **[更新]** を選択し、新しいマージ レプリケーションを表示します。  
  
### <a name="view-the-status-of-snapshot-generation"></a>スナップショット生成の状態を表示する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksSalesOrdersMerge]** を右クリックして、 **[スナップショット エージェントの状態の表示]** を選択します。  

   ![スナップショット エージェントの状態表示の選択](media/tutorial-replicating-data-with-mobile-clients/viewsnapshotagentstatus.png)
  
3. パブリケーションのスナップショット エージェントの現在の状態が表示されます。 スナップショット ジョブが正常に終了していることを確認してから次のレッスンに進みます。  
  
### <a name="add-the-merge-agent-login-to-the-pal"></a>マージ エージェントのログインを PAL に追加する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksSalesOrdersMerge]** パブリケーションを右クリックして、 **[プロパティ]** を選択します。  
  
   a. **[パブリケーション アクセス リスト]** ページを選択して、 **[追加]** を選択します。 
  
   b. **[パブリケーション アクセスの追加]** ダイアログ ボックスで、<*パブリッシャー コンピューター名*> **\repl_merge** を選択して **[OK]** を選択します。 もう一度 **[OK]** を選択します。 

   ![マージ エージェントのログインを追加するための選択](media/tutorial-replicating-data-with-mobile-clients/mergepal.png) 

  
詳細については、次を参照してください。  
- [パブリッシュされたデータのフィルター選択](../../relational-databases/replication/publish/filter-published-data.md) 
- [パラメーター化された行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
- [アーティクルの定義](../../relational-databases/replication/publish/define-an-article.md)  
  
  
## <a name="create-a-subscription-to-the-merge-publication"></a>マージ パブリケーションへのサブスクリプションを作成する
このセクションでは、前の手順で作成したマージ パブリケーションにサブスクリプションを追加します。 このチュートリアルでは、リモート サブスクライバー (NODE2\SQL2016) を使用します。 次に、サブスクリプション データベースにアクセス許可を設定し、新しいサブスクリプション用のフィルター選択データのスナップショットを手動で作成します。   
  
### <a name="add-a-subscriber-for-merge-publication"></a>マージ パブリケーションのサブスクライバーを追加する
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でサブスクライバーに接続して、サーバー ノードを展開します。 **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを右クリックして、 **[新しいサブスクリプション]** を選択します。 サブスクリプションの新規作成ウィザードが起動します。

   ![サブスクリプションの新規作成ウィザードを起動する選択](media/tutorial-replicating-data-with-mobile-clients/newsub.png)
  
2. **[パブリケーション]** ページで、 **[パブリッシャー]** ボックスの一覧の **[SQL Server パブリッシャーの検索]** を選択します。  
  
   **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバー名]** ボックスにパブリッシャー インスタンスの名前を入力し、 **[接続]** を選択します。 

   ![パブリッシャーを追加するための選択](media/tutorial-replicating-data-with-mobile-clients/publication.png)
  
4. **[AdvWorksSalesOrdersMerge]** を選択し、 **[次へ]** を選択します。  
  
5. **[マージ エージェントの場所]** ページで、 **[サブスクライバーで各エージェントを実行する]** を選択して、 **[次へ]** を選択します。  

   ![[サブスクライバーで各エージェントを実行する] オプション](media/tutorial-replicating-data-with-mobile-clients/pullsub.png)
  
6. **[サブスクライバー]** ページで、サブスクライバー サーバーのインスタンス名を選択します。 **[サブスクリプション データベース]** の一覧から **[新しいデータベース]** を選択します。  
  
   **[新しいデータベース]** ダイアログ ボックスで、 **[データベース名]** ボックスに「**SalesOrdersReplica**」と入力します。 **[OK]** を選択し、 **[次へ]** を選択します。 

   ![サブスクライバーにデータベースを追加するための選択](media/tutorial-replicating-data-with-mobile-clients/addsubdb.png)
  
8. **[マージ エージェントのセキュリティ]** ページで、省略記号 **[...]** ボタンを選択します。 **[プロセス アカウント]** ボックスに「<*サブスクライバー コンピューター名*> **\repl_merge**」と入力し、このアカウントのパスワードを入力します。 **[OK]** 、 **[次へ]** 、 **[次へ]** の順に選択します。  

   ![マージ エージェント セキュリティの選択](media/tutorial-replicating-data-with-mobile-clients/mergeagentsecurity.png)

9. **[同期スケジュール]** ページで、 **[エージェント スケジュール]** を **[要求時にのみ実行する]** に設定します。 **[次へ]** を選択します。  

   ![エージェントの [要求時にのみ実行する] の選択](media/tutorial-replicating-data-with-mobile-clients/mergesyncschedule.png)
  
9. **[サブスクリプションの初期化]** ページで、 **[次の場合に初期化]** ボックスの一覧から **[初回同期時]** を選択します。 **[次へ]** を選択して **[サブスクリプションの種類]** ページに進み、適切なサブスクリプションの種類を選択します。 このチュートリアルでは **[クライアント]** を使用します。 サブスクリプションの種類を選択した後、 **[次へ]** を再び選択します。 

   ![最初の同期でサブスクリプションを初期化するための選択](media/tutorial-replicating-data-with-mobile-clients/firstsync.png)

10. **[HOST_NAME 値]** ページで、 **[HOST_NAME 値]** ボックスに値「**adventure-works\pamela0**」と入力します。 **[完了]** を選択します。  

    ![[HOST_NAME 値] ページ](media/tutorial-replicating-data-with-mobile-clients/hostname.png)
  
11. **[完了]** をもう一度選択します。 サブスクリプションが作成されたら、 **[閉じる]** を選択します。  

### <a name="set-server-permissions-at-the-subscriber"></a>サブスクライバー側でサーバー アクセス許可を設定する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でサブスクライバーに接続します。 **[セキュリティ]** を展開して **[ログイン]** を右クリックし、 **[新しいログイン]** をクリックします。  
  
   **[全般]** ページで、 **[検索]** を選択し、 **[オブジェクト名を入力してください]** ボックスに「<*サブスクライバーのコンピューター名*> **\repl_merge**」と入力します。 **[名前の確認]** を選択し、 **[OK]** を選択します。 
    
   ![ログインを設定するための選択](media/tutorial-replicating-data-with-mobile-clients/sublogin.png)
  
1. **[ユーザー マッピング]** ページで、 **[SalesOrdersReplica]** データベースを選択し、 **[db_owner]** ロールを選択します。 **[セキュリティ保護可能なリソース]** ページで、 **[トレースの変更]** に **[明示的]** アクセス許可を付与します。 **[OK]** を選択します。

   ![[ユーザー マッピング] ページと [セキュリティ保護可能なリソース] ページ](media/tutorial-replicating-data-with-mobile-clients/setdbo.png)
  
### <a name="create-the-filtered-data-snapshot-for-the-subscription"></a>サブスクリプション用のフィルター選択データのスナップショットを作成する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2. **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksSalesOrdersMerge]** パブリケーションを右クリックして、 **[プロパティ]** を選択します。  
   
   a. **[データ パーティション]** ページを選択して、 **[追加]** を選択します。   
   b. **[データ パーティションの追加]** ダイアログ ボックスで、 **[HOST_NAME 値]** ボックスに「**adventure-works\pamela0**」と入力し、 **[OK]** を選択します。  
   c. 新しく追加したパーティションを選択して、 **[今すぐ選択したスナップショットを生成する]** を選択し、 **[OK]** を選択します。 

   ![パーティションを追加するための選択](media/tutorial-replicating-data-with-mobile-clients/partition.png)
  
  
詳細については、次を参照してください。  
- [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
- [プル サブスクリプションの作成](../../relational-databases/replication/create-a-pull-subscription.md)  
- [パラメーター化されたフィルターを使用したマージ パブリケーションのスナップショット](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)  

## <a name="synchronize-the-subscription-to-the-merge-publication"></a>マージ パブリケーションにサブスクリプションを同期する

このセクションでは、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してマージ エージェントを起動して、サブスクリプションを初期化します。 この手順を使用して、パブリッシャーと同期することもできます。   
  
### <a name="start-synchronization-and-initialize-the-subscription"></a>同期を開始しサブスクリプションを初期化する  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でサブスクライバーに接続します。  
2. SQL Server エージェントが実行されていることを確認します。 実行されていない場合は、オブジェクト エクスプローラーで [SQL Server エージェント] を右クリックして **[開始]** を選択します。 この手順でエージェントの起動に失敗する場合は、SQL Server 構成マネージャーを使用して手動で起動する必要があります。 
  
2. **[レプリケーション]** ノードを展開します。 **[ローカル サブスクリプション]** フォルダーで、**SalesOrdersReplica** データベースのサブスクリプションを右クリックし、 **[同期の状態の表示]** を選択します。  
  
   **[開始]** を選択して、サブスクリプションを初期化します。 

   ![[開始] ボタンとの同期ステータス](media/tutorial-replicating-data-with-mobile-clients/mergesyncstatus.png)
    
  
  
## <a name="next-steps"></a>次のステップ  
マージ レプリケーション用にパブリッシャーとサブスクライバーの両方を正しく構成しました。 次のこともできます。

1. パブリッシャーまたはサブスクライバーで **SalesOrderHeader** または **SalesOrderDetail** テーブルのデータを挿入、更新、削除します。
2. ネットワーク接続が使用可能な場合はこの手順を繰り返してパブリッシャーとサブスクライバー間でデータを同期します。
3. 他のサーバーにある **SalesOrderHeader** または **SalesOrderDetail** テーブルをクエリし、レプリケートされた変更を表示します。  
  
詳細については、次を参照してください。   
- [スナップショットを使用したサブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
- [データの同期](../../relational-databases/replication/synchronize-data.md)  
- [プル サブスクリプションの同期](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
  
  
  
