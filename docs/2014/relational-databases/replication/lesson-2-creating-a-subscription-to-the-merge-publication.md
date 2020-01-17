---
title: レッスン 2:マージ パブリケーションに対するサブスクリプションを作成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 06722baa-9065-443e-b1d5-99036cf89074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 495fb831490a35043b500caea2c835bfd80b6a8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721032"
---
# <a name="lesson-2-creating-a-subscription-to-the-merge-publication"></a>レッスン 2:マージ パブリケーションへのサブスクリプションの作成
  このレッスンでは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を使用してサブスクリプションを作成します。 次に、サブスクリプション データベースに権限を設定し、新しいサブスクリプション用のフィルター選択データのスナップショットを手動で作成します。 このレッスンでは、前のレッスンを完了している必要があります[レッスン 1。マージ レプリケーションを使用してデータのパブリッシュ](lesson-1-publishing-data-using-merge-replication.md)します。  
  
### <a name="to-create-the-subscription"></a>サブスクリプションを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続し、サーバー ノード、 **[レプリケーション]** フォルダーの順に展開して、 **[ローカル サブスクリプション]** フォルダーを右クリックし、 **[新しいサブスクリプション]** をクリックします。  
  
     サブスクリプションの新規作成ウィザードが起動します。  
  
2.  **[パブリケーション]** ページで、 **[パブリッシャー]** ボックスの一覧の **[SQL Server パブリッシャーの検索]** をクリックします。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバー名]** ボックスにパブリッシャー インスタンスの名前を入力し、 **[接続]** をクリックします。  
  
4.  **[AdvWorksSalesOrdersMerge]** をクリックし、 **[次へ]** をクリックします。  
  
5.  [マージ エージェントの場所] ページで、 **[サブスクライバーで各エージェントを実行する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  [サブスクライバー] ページで、サブスクライバー サーバーのインスタンス名を選択します。**サブスクリプション データベース**を選択します **\<新しいデータベース >** 一覧から。  
  
7.  **[新しいデータベース]** ダイアログ ボックスで、 **[データベース名]** ボックスに「 **SalesOrdersReplica** 」と入力し、 **[OK]** をクリックして **[次へ]** をクリックします。  
  
8.  マージ エージェント セキュリティ ページで、省略記号をクリックします ( **.。** ) ボタンを入力\< _Machine_Name >_ **\repl_merge**で、**プロセス アカウント**ボックスに、このアカウントのパスワードを入力、 をクリックして**OK**、 をクリックして**次**、順にクリックします**次へ**もう一度します。  
  
9. [サブスクリプションの初期化] ページで、 **[次の場合に初期化]** ボックスの一覧から **[初回同期時]** を選択し、 **[次へ]** をクリックし、 **[次へ]** もう一度です。  
  
10. HOST_NAME 値 ページの値を入力します。`adventure-works\pamela0`で、 **HOST_NAME 値**ボックスをクリック**完了**します。  
  
11. もう一度 **[完了]** をクリックし、サブスクリプションが作成されたら **[閉じる]** をクリックします。  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>サブスクライバー側のデータベース権限を設定するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサブスクライバーに接続し、 **[データベース]** 、 **[SalesOrdersReplica]** 、 **[セキュリティ]** の順に展開して、 **[ユーザー]** を右クリックし、 **[新しいユーザー]** を選択します。  
  
2.  **全般**ページで、入力\< _Machine_Name >_ **\repl_merge**で、**ユーザー名**ボックスで、省略記号ボタン (をクリックして **...** ) ボタンをクリックして**参照**を選択します\< _Machine_Name >_ **\repl_merge**、 をクリックして**OK**、 をクリックして**名前の確認**、 をクリックし、 **OK**します。  
  
3.  **[データベース ロールのメンバーシップ]** で **[db_owner]** を選択し、 **[OK]** をクリックしてユーザーを作成します。  
  
### <a name="to-create-the-filtered-data-snapshot-for-the-subscription"></a>サブスクリプション用のフィルター選択データのスナップショットを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続して、サーバー ノードを展開し、 **[レプリケーション]** フォルダーを展開します。  
  
2.  **[ローカル パブリケーション]** フォルダーを展開し、 **[AdvWorksSalesOrdersMerge]** パブリケーションを右クリックして、 **[プロパティ]** をクリックします。  
  
     **[パブリケーションのプロパティ]** ダイアログ ボックスが表示されます。  
  
3.  **[データ パーティション]** ページを選択して、 **[追加]** をクリックします。  
  
4.  **データ パーティションの追加**ダイアログ ボックスに「`adventure-works\pamela0`で、 **HOST_NAME 値**ボックスをクリック**OK**。  
  
5.  新しく追加したパーティションを選択して、 **[今すぐ選択したスナップショットを生成する]** をクリックし、 **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 ここでは、マージ パブリケーションへのサブスクリプションを作成し、新しいサブスクリプションのデータ パーティション用のフィルター選択スナップショットを生成して、サブスクリプション初期化時に使用できるようにしました。 次は、サブスクリプション データベースのマージ エージェントに権限を付与します。さらに、マージ エージェントを実行して、同期の開始とサブスクリプションの初期化を行います。 「[レッスン 3:マージ パブリケーションに対するサブスクリプションの同期](lesson-3-synchronizing-the-subscription-to-the-merge-publication.md)します。  
  
## <a name="see-also"></a>参照  
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [パラメーター化されたフィルターを使用したマージ パブリケーションのスナップショット](snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  
