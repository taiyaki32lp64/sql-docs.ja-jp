---
title: トラブルシューティング ツール:SQL Server トランザクション レプリケーション エラーを検出する | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 7c9924d2062b3c4fa41c8731df17b49fe9a86b07
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907287"
---
# <a name="troubleshooter-find-errors-with-sql-server-transactional-replication"></a>トラブルシューティング ツール:トラブルシューティング ツール: SQL Server トランザクション レプリケーション エラーを検出する 
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

トランザクション レプリケーションがどのように動作するのかを基本的に理解していないと、レプリケーション エラーのトラブルシューティングはフラストレーションを感じることがあります。 パブリケーション作成の最初のステップは、スナップショット エージェントでスナップショットを作成し、スナップショット フォルダーにそれを保存することです。 次に、ディストリビューション エージェントがサブスクライバーにスナップショットを適用します。 

このプロセスでは、パブリケーションが作成されて、"*同期*" 状態にされます。 同期は次の 3 つのフェーズで動作します。
1. レプリケートされるオブジェクトでトランザクションが発生し、トランザクション ログで "レプリケーション用" とマークされます。 
2. ログ リーダー エージェントがトランザクション ログをスキャンし、"レプリケーション用" とマークされたトランザクションを探します。 これらのトランザクションはディストリビューション データベースに保存されます。 
3. ディストリビューション エージェントは、リーダー スレッドを使用してディストリビューション データベースをスキャンします。 次に、ライター スレッドを使用することにより、このエージェントはサブスクライバーに接続して、変更をサブスクライバーに適用します。

このプロセスのどのステップにおいてもエラーが発生する可能性があります。 これらのエラーを見つけることは、同期に関する問題のトラブルシューティングの最も困難な側面です。 レプリケーション モニターを使うとこのプロセスが簡単になります。 

>[!NOTE]
> - このトラブルシューティング ガイドの目的は、トラブルシューティングの手法を説明することです。 特定のエラーを解決することではなく、レプリケーションでのエラーの発見に関する一般的なガイダンスを提供することを目的として作成されています。 具体的な例がいくつか示されていますが、それらの解決方法は環境によって異なる場合があります。 
> - このガイドで例として提供されているエラーは、[トランザクション レプリケーションの構成](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)に関するチュートリアルが基になっています。



## <a name="troubleshooting-methodology"></a>トラブルシューティングの手法 

### <a name="questions-to-ask"></a>質問すること
1. 同期プロセスのどこでレプリケーションが失敗するか。
2. どのエージェントでエラーが発生するか。
1. レプリケーションが最後に正常に動作したのはいつか。 その後で何か変更したか。  

### <a name="steps-to-take"></a>実行手順
1. レプリケーション モニターを使用して、レプリケーションでエラーが発生した箇所 (どのエージェント) をあきらかにします。
   - **パブリッシャーからディストリビューターまで**セクションでエラーが発生している場合は、ログ リーダー エージェントに関する問題です。 
   - **ディストリビューターからサブスクライバーまで**セクションでエラーが発生している場合は、ディストリビューション エージェントに関する問題です。  
2. ジョブの利用状況モニターでそのエージェントのジョブ履歴を調べて、エラーの詳細を明らかにします。 ジョブ履歴では十分な詳細がわからない場合は、その特定のエージェントで[詳細ログを有効にする](#enable-verbose-logging-on-any-agent)ことができます。
3. エラーの解決方法の決定を試みます。


## <a name="find-errors-with-the-snapshot-agent"></a>スナップショット エージェントでエラーを見つける
スナップショット エージェントは、スナップショットを生成し、それを指定されたスナップショット フォルダーに書き込みます。 

1. スナップショット エージェントの状態を表示します。

    A. オブジェクト エクスプローラーで、 **[レプリケーション]** の下の **[ローカル パブリケーション]** ノードを展開します。

    B. **AdvWorksProductTrans** パブリケーションを右クリックして、 **[スナップショット エージェントの状態の表示]** をクリックします。 

    ![ショートカット メニューの [スナップショット エージェントの状態の表示] コマンド](media/troubleshooting-tran-repl-errors/view-snapshot-agent-status.png)

1. スナップショット エージェントの状態でエラーが報告された場合は、スナップショット エージェントのジョブ履歴で詳細を確認することができます。

    A. オブジェクト エクスプローラーで **[SQL Server エージェント]** を展開し、[ジョブの利用状況モニター] を開きます。 

    B. **[カテゴリ]** で並べ替えて、カテゴリ **REPL-Snapshot** でスナップショット エージェントを識別します。

    c. そのスナップショット エージェントを右クリックして、 **[履歴の表示]** を選択します。 

   ![スナップショット エージェントの履歴を開くための選択](media/troubleshooting-tran-repl-errors/snapshot-agent-history.png)
    
1. スナップショット エージェントの履歴で、関連するログ エントリを選択します。 これは、通常、エラーが報告されているエントリの 1 または 2 行 "*前*" にあります。 (赤い x 印がエラーを示します。)ログの下のボックスでメッセージ テキストを確認します。 

    ![アクセス拒否のスナップショット エージェント エラー](media/troubleshooting-tran-repl-errors/snapshot-access-denied.png)

        The replication agent had encountered an exception.
        Exception Message: Access to path '\\node1\repldata.....' is denied.

スナップショット フォルダーに Windows のアクセス許可が正しく構成されていない場合は、スナップショット エージェントに "アクセスが拒否されました" エラーが表示されます。 スナップショットが格納されているフォルダーへのアクセス許可を確認し、スナップショット エージェントの実行に使用しているアカウントに共有にアクセスするためのアクセス許可があることを確認する必要があります。  

## <a name="find-errors-with-the-log-reader-agent"></a>ログ リーダー エージェントでエラーを見つける
ログ リーダー エージェントは、パブリッシャー データベースに接続して、"レプリケーション用" とマークされているすべてのトランザクションのトランザクション ログをスキャンします。 そして、それらのトランザクションをディストリビューション データベースに追加します。 

1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続します。 サーバー ノードを展開して **[レプリケーション]** フォルダーを右クリックし、 **[レプリケーション モニターの起動]** を選択します。  

    ![ショートカット メニューの [レプリケーション モニターの起動] コマンド](media/troubleshooting-tran-repl-errors/launch-repl-monitor.png)
  
    レプリケーション モニターが開きます。![レプリケーション モニター](media/troubleshooting-tran-repl-errors/repl-monitor.png) 
   
2. 赤い X 印は、パブリケーションが同期していないことを示します。 左側で **[マイ パブリッシャー]** を展開し、関連するパブリッシャー サーバーを展開します。  
  
3.  左側で **AdvWorksProductTrans** パブリケーションを選択し、いずれかのタブで赤い X 印を探して、どこに問題があるかを特定します。 この場合、赤い X 印は **[エージェント]** タブにあるので、エージェントの 1 つでエラーが発生しています。 

    ![[エージェント] タブの赤い X 印](media/troubleshooting-tran-repl-errors/agent-error.png)

4. **[エージェント]** タブを選択し、どのエージェントでエラーが発生しているかを特定します。 

    ![失敗しているログ リーダー エージェントの赤い X 印](media/troubleshooting-tran-repl-errors/log-reader-agent-failure.png)


5. この表示では、スナップショット エージェントとログ リーダー エージェントの 2 つのエージェントが示されています。 エラーが発生しているものに赤い X 印が付いています。この例ではログ リーダー エージェントです。 

    エラーが報告されている行をダブルクリックして、ログ リーダー エージェントのエージェント履歴を開きます。 この履歴では、エラーに関する詳細情報が提供されます。 
    
    ![ログ リーダー エージェントのエラーの詳細](media/troubleshooting-tran-repl-errors/log-reader-error.png)

       Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
       The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
       Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
       Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        

6. エラーは、通常、パブリッシャー データベースの所有者が正しく設定されていないときに発生します。 これは、データベースが復元されるときに発生することがあります。 これを確認するには、次のようにします。

    A. オブジェクト エクスプローラーで **[データベース]** を展開します。

    B. **AdventureWorks2012** を右クリックして、 **[プロパティ]** をクリックします。 

    c. **[ファイル]** ページの下に所有者が存在することを確認します。 このボックスが空白の場合は、これが問題の原因と考えられます。 

   ![データベースのプロパティの [ファイル] ページで [所有者] ボックスが空白になっている](media/troubleshooting-tran-repl-errors/db-properties.png)

7. **[ファイル]** ページで所有者が空白の場合は、AdventureWorks2012 データベースのコンテキストで **[新しいクエリ]** ウィンドウを開きます。 次の T-SQL コードを実行します。

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXEC sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. ログ リーダー エージェントの再起動が必要な場合があります。

    A. オブジェクト エクスプローラーで **[SQL Server エージェント]** ノードを展開し、ジョブの利用状況モニターを開きます。

    B. **[カテゴリ]** で並べ替え、**REPL-LogReader** カテゴリによってログ リーダー エージェントを識別します。 

    c. **ログ リーダー エージェント** ジョブを右クリックし、 **[Start Job at Step]\(ステップでジョブを開始\)** を選択します。 

    ![ログ リーダー エージェントを再起動するための選択](media/troubleshooting-tran-repl-errors/start-job-at-step.png)

9. レプリケーション モニターをもう一度開いて、パブリケーションが現在同期されていることを確認します。 まだ開いていない場合は、オブジェクト エクスプローラーで **[レプリケーション]** を右クリックして見つけることができます。 
10. **AdvWorksProductTrans** パブリケーション、 **[エージェント]** タブの順に選択し、ログ リーダー エージェントをダブルクリックして、エージェントの履歴を開きます。 これで、ログ リーダー エージェントが実行中で、コマンドをレプリケートしているか、"レプリケートされたトランザクションが存在しない" のいずれかが示されるはずです。

    ![レプリケートされたトランザクションがなくて実行しているログ リーダー エージェント](media/troubleshooting-tran-repl-errors/log-reader-running.png)

## <a name="find-errors-with-the-distribution-agent"></a>ディストリビューション エージェントでエラーを見つける
ディストリビューション エージェントは、ディストリビューション データベースでデータを見つけて、それをサブスクライバーに適用します。 

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリッシャーに接続します。 サーバー ノードを展開して **[レプリケーション]** フォルダーを右クリックし、 **[レプリケーション モニターの起動]** を選択します。  
2. **[レプリケーション モニター]** で、 **[AdvWorksProductTrans]** パブリケーションを選択し、 **[すべてのサブスクリプション]** タブを選択します。サブスクリプションを右クリックし、 **[詳細表示]** を選択します。

    ![ショートカット メニューの [詳細表示] コマンド](media/troubleshooting-tran-repl-errors/view-details.png)

2. **[ディストリビューターからサブスクライバーまで]** 履歴ダイアログ ボックスが開き、エージェントで発生しているエラーの内容を明確にします。 

     ![ディストリビューション エージェントのエラーの詳細](media/troubleshooting-tran-repl-errors/dist-history-error.png)
    
        Error messages:
        Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.

3. このエラーは、ディストリビューション エージェントが再試行していることを示します。 詳細情報を探すには、ディストリビューション エージェントのジョブ履歴を確認します。 

    A. オブジェクト エクスプローラーで **[SQL Server エージェント]** を展開し、 **[ジョブの利用状況モニター]** を開きます。 
    
    B. **[カテゴリ]** でジョブを並べ替えます。 

    c. カテゴリ **REPL-Distribution** でディストリビューション エージェントを識別します。 エージェントを右クリックして、 **[履歴の表示]** を選択します。

    ![ディストリビューション エージェントの履歴表示の選択](media/troubleshooting-tran-repl-errors/view-dist-agent-history.png)

5. いずれかのエラー エントリを選択し、ウィンドウの下部にエラー テキストを表示します。  

    ![ディストリビューション エージェントのパスワードが間違っていることを示すエラー テキスト](media/troubleshooting-tran-repl-errors/dist-pw-wrong.png)
    
        Message:
        Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)

6. このエラーは、ディストリビューション エージェントで使用されたパスワードが正しくないことを示しています。 これを解決するには次のようにします。

    A. オブジェクト エクスプローラーで **[レプリケーション]** のノードを展開します。
    
    B. サブスクリプションを右クリックして、 **[プロパティ]** をクリックします。
    
    c. **[エージェント プロセス アカウント]** の横にある省略記号 [...] を選択して、パスワードを変更します。

    ![ディストリビューション エージェントのパスワードを変更するための選択](media/troubleshooting-tran-repl-errors/dist-agent-pw-change.png)

7. オブジェクト エクスプローラーで **[レプリケーション]** を右クリックして、レプリケーション モニターをもう一度確認します。 **[すべてのサブスクリプション]** の下の赤い X 印は、ディストリビューション エージェントでまだエラーが発生していることを示します。 

    **[レプリケーション モニター]** でサブスクリプションを右クリックして **[詳細表示]** を選択し、 **[ディストリビューターからサブスクライバーまで]** の履歴を開きます。 ここでは、異なるエラーが表示されるようになります。 

    ![ディストリビューション エージェントが接続できないことを示すエラー](media/troubleshooting-tran-repl-errors/dist-agent-cant-connect.png)
           
        Connecting to Subscriber 'NODE2\SQL2016'        
        Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
        Number:  18456
        Message: Login failed for user 'NODE2\repl_distribution'.

8. このエラーは、ユーザー **NODE2\repl_distribution** のログインが失敗したため、ディストリビューション エージェントがサブスクライバーに接続できなかったことを示しています。 さらに詳しく調べるには、サブスクライバーに接続して、オブジェクト エクスプローラーで **[管理]** ノードの下の*現在の* SQL Server エラー ログを開きます。 

    ![サブスクライバーのログイン失敗を示すエラー](media/troubleshooting-tran-repl-errors/login-failed.png)
    
    このエラーが表示される場合は、ログインがサブスクライバー上にありません。 このエラーを解決するには、[レプリケーションのためのアクセス許可](../../relational-databases/replication/security/security-role-requirements-for-replication.md)に関するページをご覧ください。

9. ログイン エラーが解決された後、もう一度レプリケーション モニターを確認してください。 すべての問題が解決されると、 **[パブリケーション名]** の横に緑色の矢印が表示され、 **[すべてのサブスクリプション]** の下の状態が **[実行中]** になります。 

    サブスクリプションを右クリックして **[ディストリビューターからサブスクライバーまで]** 履歴をもう一度開き、成功したことを確認します。 ディストリビューション エージェントを初めて実行する場合は、スナップショットがサブスクライバーに一括コピーされます。 

     ![[実行] 状態と一括コピーに関するメッセージが表示されているディストリビューション エージェント](media/troubleshooting-tran-repl-errors/dist-agent-success.png)   


## <a name="enable-verbose-logging-on-any-agent"></a>エージェントで詳細ログを有効にする
詳細ログを使用して、レプリケーション トポロジ内のエージェントで発生したエラーに関する詳細な情報を見ることができます。 手順はどのエージェントでも同じです。 ジョブの利用状況モニターで正しいエージェントを選択していることだけを確認してください。 

   >[!NOTE]   
   > プル サブスクリプションかプッシュ サブスクリプションかに応じて、エージェントはパブリッシャーまたはサブスクライバーのどちらにあってもかまいません。 見ているサーバー上に探しているエージェントが見つからない場合は、他のサーバーを確認してください。  

1. 詳細ログを保存するかどうかを決めて、フォルダーが存在することを確認します。 この例では c:\temp を使います。 
2. オブジェクト エクスプローラーで **[SQL Server エージェント]** ノードを展開し、ジョブの利用状況モニターを開きます。 

    ![ジョブの利用状況モニターのショートカット メニューの [ジョブの利用状況の表示] コマンド](media/troubleshooting-tran-repl-errors/job-activity-monitor.png)    

1. **[カテゴリ]** で並べ替えて、関心のあるエージェントを見つけます。 この例では、ログ リーダー エージェントを使います。 関心のあるエージェントを右クリックして、 **[プロパティ]** をクリックします。

    ![エージェントのプロパティを開くための選択](media/troubleshooting-tran-repl-errors/log-agent-properties.png)

1. **[ステップ]** ページを選択し、 **[エージェントを実行します]** ステップを強調表示にします。 **[編集]** を選択します。 

    ![[エージェントを実行します] ステップを編集するための選択](media/troubleshooting-tran-repl-errors/edit-steps.png)

1. **[コマンド]** ボックスで新しい行を開始し、次のテキストを入力して、 **[OK]** を選択します。 

       -Output C:\Temp\OUTPUTFILE.txt -Outputverboselevel 3
    
    必要に応じて、場所と詳細レベルを変更できます。

    ![ジョブ ステップのプロパティの詳細出力](media/troubleshooting-tran-repl-errors/verbose.png)

   > [!NOTE]
   > 詳細出力パラメーターを追加するとき、次のような問題があると、エージェントが失敗したり、出力ファイルが作成されない可能性があります。
   > - 書式設定に問題があり、ダッシュがハイフンになっています。 
   > - ディスク上に場所が存在しません。または、エージェントを実行しているアカウントに、指定した場所に書き込むアクセス許可がありません。 
   > - 最後のパラメーターと `-Output` パラメーターの間にスペースがありません。 
   > - エージェントにより、サポートされる詳細さのレベルが異なります。 詳細ログを有効にしてもエージェントが起動しない場合は、指定した詳細レベルを 1 つ下げて再試行してください。 

1. エージェントを右クリックして **[Stop Job at Step]\(ステップでジョブを停止\)** を選択し、ログ リーダー エージェントを再起動します。 ツール バーの **[更新]** アイコンを選択して更新します。 エージェントを右クリックして、 **[Start Job at Step]\(ステップでジョブを開始\)** を選択します。
2. ディスクで出力を確認します。 

    ![出力テキスト ファイル](media/troubleshooting-tran-repl-errors/output.png)

    
1. 詳細ログを無効にするには、前と同じ手順に従い、前に追加した `-Output` 行全体を削除します。 

詳細については、[レプリケーション エージェントの詳細ログを有効にする方法](https://support.microsoft.com/help/312292/how-to-enable-replication-agents-for-logging-to-output-files-in-sql-se)に関するページをご覧ください。 


## <a name="see-also"></a>参照
<br>[トランザクション レプリケーションの概要](../../relational-databases/replication/transactional/transactional-replication.md)
<br>[レプリケーションのチュートリアル](../../relational-databases/replication/replication-tutorials.md)
<br>[ReplTalk ブログ](https://blogs.msdn.microsoft.com/repltalk)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

