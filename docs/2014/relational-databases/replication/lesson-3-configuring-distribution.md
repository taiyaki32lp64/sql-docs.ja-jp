---
title: 'レッスン 3: ディストリビューションの構成 |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: f248984a-0b59-4c2f-a56d-31f8dafe72b5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 8d873d3664c88963b17550734b488e6872a9cc84
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721101"
---
# <a name="lesson-3-configuring-distribution"></a>レッスン 3: ディストリビューションの構成
  このレッスンでは、パブリッシャー側のディストリビューションを構成し、パブリケーション データベースとディストリビューション データベースに対して必要な権限を設定します。 ディストリビューターを構成済みの場合は、このレッスンを開始する前に、パブリッシングとディストリビューションを無効にする必要があります。 既存のレプリケーション トポロジを維持する必要がある場合は、このレッスンを実行しないでください。  
  
 パブリッシャー側のリモート ディストリビューターの構成は、このチュートリアルの対象外です。  
  
### <a name="configuring-distribution-at-the-publisher"></a>パブリッシャー側のディストリビューションを構成するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを右クリックし、 **[ディストリビューションの構成]** をクリックします。  
  
    > [!NOTE]  
    >  実際のサーバー名ではなく [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] localhost **を使用して** に接続すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が **'localhost'** サーバーに接続できないことを示す警告とメッセージが表示されます。 警告ダイアログで **[OK]** をクリックします。 **[サーバーへの接続]** ダイアログで、 **[サーバー名]** を **localhost** から使用しているサーバーの名前に変更します。 **[接続]** をクリックします。  
  
     ディストリビューション構成ウィザードが起動します。  
  
3.  **ディストリビューター**  ページで、 **'** _\<ServerName >_ **' 独自のディストリビューターとして機能します。SQL Server はディストリビューション データベースとログは作成**、 をクリックし、**次**します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されていない場合は、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**エージェントの起動** ] ページで **[はい]** を選択し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが自動的に起動するように構成します。 **[次へ]** をクリックします。  
  
5.  **[スナップショット フォルダー]** ボックスに、「 **\\\\** \<_コンピューター名>_ **\repldata**」と入力します (\<*コンピューター名>* はパブリッシャーの名前)。その後、 **[次へ]** をクリックします。  
  
6.  ウィザードの残りのページでは、既定値をそのまま使用します。  
  
7.  **[完了]** をクリックしてディストリビューションを有効にします。  
  
### <a name="setting-database-permissions-at-the-publisher"></a>パブリッシャー側のデータベース権限を設定するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[セキュリティ]** を展開して **[ログイン]** を右クリックし、 **[新しいログイン]** をクリックします。  
  
2.  **[全般]** ページで、 **[検索]** をクリックして **[選択するオブジェクト名を入力してください]** ボックスに「\<_コンピューター名>_ **\repl_snapshot**」と入力します (\<*コンピューター名>* はローカルのパブリッシャー サーバーの名前)。その後、 **[名前の確認]** をクリックし、 **[OK]** をクリックします。  
  
3.  **[このログインにマップされたユーザー]** の一覧にある **[ユーザー マッピング]** ページで、 **ディストリビューション** データベースと [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの両方を選択します。  
  
     **データベース ロールのメンバーシップ**ボックスの一覧、`db_owner`両方のデータベース ログインのロール。  
  
4.  **[OK]** をクリックすると、ログインが作成されます。  
  
5.  手順 1. ～ 4. を繰り返して、ローカルの repl_logreader アカウントのログインを作成します。 このログインは、ユーザーのメンバーであるにもマップする必要があります、`db_owner`固定データベース ロール、**配布**と**AdventureWorks**データベース。  
  
6.  手順 1. ～ 4. を繰り返して、ローカルの repl_distribution アカウントのログインを作成します。 このログインは、のメンバーであるユーザーにマップする必要があります、`db_owner`固定データベース ロール、**配布**データベース。  
  
7.  手順 1. ～ 4. を繰り返して、ローカルの repl_merge アカウントのログインを作成します。 このログインは、 **ディストリビューション** データベースと **AdventureWorks** データベースのユーザーにマップする必要があります。  
  
## <a name="see-also"></a>参照  
 [[ディストリビューションの構成]](configure-distribution.md)   
 [レプリケーション エージェントのセキュリティ モデル](security/replication-agent-security-model.md)  
  
  
