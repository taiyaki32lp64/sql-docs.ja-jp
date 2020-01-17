---
title: レッスン 1:トランザクション レプリケーションを使用してデータのパブリッシュ |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8267f70049d0ef37c0ce80bc594dff25d53f15fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721094"
---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>レッスン 1:トランザクション レプリケーションを使用してデータのパブリッシュ
  このレッスンでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してトランザクション パブリケーションを作成し、 **サンプル データベースの** Product [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] テーブルからフィルター選択したサブセットをパブリッシュします。 また、ディストリビューション エージェントにより使用される SQL Server ログインをパブリケーション アクセス リスト (PAL) に追加します。 このチュートリアルを行うには、前のチュートリアル「 [レプリケーションに備えたサーバーの準備](tutorial-preparing-the-server-for-replication.md)」を完了している必要があります。  
  
### <a name="to-create-a-publication-and-define-articles"></a>パブリケーションを作成し、アーティクルを定義するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを右クリックして、 **[新しいパブリケーション]** をクリックします。  
  
     パブリケーションの新規作成ウィザードが起動します。  
  
3.  [パブリケーション データベース] ページで [ [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]] を選択し、 **[次へ]** をクリックします。  
  
4.  [パブリケーションの種類] ページで **[トランザクション パブリケーション]** を選択し、 **[次へ]** をクリックします。  
  
5.  [アーティクル] ページで、 **[テーブル]** ノードを展開して **[Product]** チェック ボックスをオンにします。次に、 **[Product]** を展開して、 **[ListPrice]** チェック ボックスと **[StandardCost]** チェック ボックスをオフにします。 **[次へ]** をクリックします。  
  
6.  [テーブル行のフィルター選択] ページで、 **[追加]** をクリックします。  
  
7.  **[フィルターの追加]** ダイアログ ボックスで **[SafetyStockLevel]** 列をクリックし、右矢印をクリックして、フィルター選択クエリの Filter ステートメントの WHERE 句にこの列を追加します。さらに、WHERE 句を次のように変更します。  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  **[OK]** をクリックし、 **[次へ]** をクリックします。  
  
9. **[スナップショットをすぐに作成し、サブスクリプションを初期化できるようにそのスナップショットを保持する]** チェック ボックスをオンにして、 **[次へ]** をクリックします。  
  
10. [エージェント セキュリティ] ページで、 **[スナップショット エージェントのセキュリティ設定を使用する]** チェック ボックスをオフにします。  
  
11. スナップショット エージェントの **[セキュリティ設定]** をクリックして、 **[プロセス アカウント]** ボックスに「\<_コンピューター名>_ **\repl_snapshot**」と入力し、このアカウントのパスワードを入力して **[OK]** をクリックします。  
  
12. 同様に、ログ リーダー エージェントのプロセス アカウントとして repl_logreader を設定し、 **[完了]** をクリックします。  
  
13. [ウィザードの完了] ページで、 **[パブリケーション名]** ボックスに「 **AdvWorksProductTrans** 」と入力し、 **[完了]** をクリックします。  
  
14. パブリケーションが作成されたら、 **[閉じる]** をクリックしてウィザードを閉じます。  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>スナップショット生成の状態を表示するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2.  **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksProductTrans]** を右クリックして、 **[スナップショット エージェントの状態の表示]** をクリックします。  
  
3.  パブリケーションのスナップショット エージェントの現在の状態が表示されるので、 スナップショット ジョブが正常に終了していることを確認してから次のレッスンに進みます。  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>ディストリビューション エージェントのログインを PAL に追加するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2.  **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksProductTrans]** パブリケーションを右クリックして、 **[プロパティ]** をクリックします。  
  
     **[パブリケーションのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[パブリケーション アクセス リスト]** ページを選択して、 **[追加]** をクリックします。  
  
4.  **[パブリケーション アクセスの追加]** ダイアログ ボックスで、 _<コンピューター名>_ **\repl_distribution** を選択して **[OK]** をクリックし、 **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 ここでは、トランザクション パブリケーションを作成しました。 次は、このパブリケーションをサブスクライブします。 「[レッスン 2:トランザクション パブリケーションに対するサブスクリプションを作成する](lesson-2-creating-a-subscription-to-the-transactional-publication.md)します。  
  
## <a name="see-also"></a>関連項目  
 [パブリッシュされたデータのフィルター処理](publish/filter-published-data.md)   
 [Define an Article](publish/define-an-article.md)   
 [スナップショットの作成および適用](create-and-apply-the-snapshot.md)  
  
  
