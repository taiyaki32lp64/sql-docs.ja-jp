---
title: パブリッシングおよびディストリビューションの無効化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- disabling publishing
- publishing [SQL Server replication], disabling
- distribution disabling [SQL Server replication]
- removing replication
- replication [SQL Server], removing
- disabling replication
- disabling distribution
ms.assetid: 6d4a1474-4d13-4826-8be2-80050fafa8a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 682f015215218f362f0ca57557b9d6afb6edee08
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882371"
---
# <a name="disable-publishing-and-distribution"></a>パブリッシングおよびディストリビューションの無効化
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、パブリッシングとディストリビューションを無効にする方法について説明します。  
  
 次の操作を実行できます。  
  
-   ディストリビューターですべてのディストリビューション データベースを削除します。  
  
-   ディストリビューターを使用するすべてのパブリッシャーを無効にし、それらのパブリッシャーのすべてのパブリケーションを削除します。  
  
-   パブリケーションへのすべてのサブスクリプションを削除します。 パブリケーション データベースおよびサブスクリプション データベースのデータは削除されませんが、パブリケーション データベースとの同期リレーションシップは失われます。 サブスクライバーにあるデータを削除するには、手動で削除する必要があります。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
-   **パブリッシングおよびディストリビューションを無効にするために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> の前提条件  
  
-   パブリッシングおよびディストリビューションを無効にするには、すべてのディストリビューション データベースおよびパブリケーション データベースをオンラインにする必要があります。 ディストリビューション データベースまたはパブリケーション データベースに対して、 *データベース スナップショット* が存在する場合、これらを削除してからパブリッシングおよびディストリビューションを無効にする必要があります。 データベース スナップショットは、データベースの読み取り専用のオフライン コピーで、レプリケーション スナップショットとは関連がありません。 詳細については、「[データベース スナップショット &#40;SQL Server&#41;](../databases/database-snapshots-sql-server.md)」を参照してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリッシングとディストリビューションの無効化ウィザードを使用して、パブリッシングおよびディストリビューションを無効化します。  
  
#### <a name="to-disable-publishing-and-distribution"></a>パブリッシングおよびディストリビューションを無効化するには  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で無効化するパブリッシャーまたはディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを右クリックし、 **[パブリッシングとディストリビューションの無効化]** をクリックします。  
  
3.  パブリッシングとディストリビューションの無効ウィザードの手順に従って操作します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 パブリッシングおよびディストリビューションは、レプリケーションのストアド プロシージャを使用してプログラムから無効にできます。  
  
#### <a name="to-disable-publishing-and-distribution"></a>パブリッシングおよびディストリビューションを無効化するには  
  
1.  レプリケーション関連のすべてのジョブを停止します。 ジョブ名の一覧については、「 [レプリケーション エージェントのセキュリティ モデル](security/replication-agent-security-model.md)」の「SQL Server エージェントのエージェント セキュリティ」セクションを参照してください。  
  
2.  各サブスクライバーのサブスクリプション データベースに対して [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) を実行して、レプリケーション オブジェクトをデータベースから削除します。 このストアド プロシージャでは、ディストリビューターのレプリケーション ジョブは削除されません。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) を実行して、レプリケーション オブジェクトをデータベースから削除します。  
  
4.  パブリッシャーがリモート ディストリビューターを使用している場合は、 [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql)を実行します。  
  
5.  ディストリビューターで [sp_dropdistpublisher](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql)を実行します。 このストアド プロシージャは、ディストリビューターに登録されている各パブリッシャーについて一度ずつ実行する必要があります。  
  
6.  ディストリビューターで [sp_dropdistributiondb](/sql/relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql) を実行して、ディストリビューション データベースを削除します。 このストアド プロシージャは、ディストリビューターの各ディストリビューション データベースについて実行する必要があります。 これにより、ディストリビューション データベースに関連付けられているキュー リーダー エージェント ジョブがすべて削除されます。  
  
7.  ディストリビューターで [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql) を実行して、サーバーからディストリビューターの指定を削除します。  
  
    > [!NOTE]  
    >  [sp_dropdistpublisher](/sql/relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql) および [sp_dropdistributor](/sql/relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql)の実行前にレプリケーションのパブリッシング オブジェクトおよびディストリビューション オブジェクトがすべて削除されていなかった場合は、これらのプロシージャからエラーが返されます。 パブリッシャーまたはディストリビューターの削除時に、レプリケーション関連のオブジェクトをすべて削除するには、 **\@no_checks**パラメーターを**1**に設定する必要があります。 パブリッシャーまたはディストリビューターがオフラインであるか、またはディストリビューターに到達できない場合は、 **\@ignore_distributor**パラメーターを**1**に設定して削除することができます。ただし、パブリッシュおよび配布オブジェクトが残されている場合は、手動で削除する必要があります。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例は、サブスクリプション データベースからレプリケーション オブジェクトを削除するスクリプトです。  
  
 [!code-sql[HowTo#sp_removedbreplication](../../snippets/tsql/SQL15/replication/howto/tsql/dropdistpub.sql#sp_removedbreplication)]  
  
 次の例は、パブリッシャーおよびディストリビューターとして機能しているサーバー上のパブリッシングおよびディストリビューションを無効にし、ディストリビューション データベースを削除するスクリプトです。  
  
 [!code-sql[HowTo#sp_DropDistPub](../../snippets/tsql/SQL15/replication/howto/tsql/dropdistpub.sql#sp_dropdistpub)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
  
#### <a name="to-disable-publishing-and-distribution"></a>パブリッシングおよびディストリビューションを無効化するには  
  
1.  ディストリビューターを利用するパブリケーションへのサブスクリプションをすべて削除します。 詳細については、「 [Delete a Pull Subscription](delete-a-pull-subscription.md) 」および「 [Delete a Push Subscription](delete-a-push-subscription.md)」を参照してください。  
  
2.  パブリッシャーとディストリビューターが同じサーバーにある場合、ディストリビューターを利用するパブリケーションをすべて削除し、すべてのデータベースに対するパブリッシングを無効にします。 詳しくは、「 [Delete a Publication](publish/delete-a-publication.md)」をご覧ください。  
  
3.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
4.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> プロパティを指定し、手順 3. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
5.  (省略可) <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得し、パブリッシャーが存在することを確認します。 このメソッドが `false` を返した場合、手順 4. で設定したパブリッシャーの名前が誤っていたか、このディストリビューターではこのパブリッシャーが使用されていません。  
  
6.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Remove%2A> メソッドを呼び出します。 パブリッシャーとディストリビューターが別々のサーバーにあり、パブリッシャーにパブリケーションが存在しないことを最初に確認せずにディストリビューターでパブリッシャーをアンインストールする必要がある場合は、 *force*に `true` の値を渡します。  
  
7.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。 手順 3 の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
8.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.UninstallDistributor%2A> メソッドを呼び出します。 すべてのローカルパブリケーションデータベースが無効になっていること、およびディストリビューションデータベースがアンインストールされていることを最初に確認せずに、ディストリビューターのすべてのレプリケーションオブジェクトを*削除するに*は、`true` の値を渡します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、ディストリビューターのパブリッシャーの登録を削除し、ディストリビューション データベースを削除して、ディストリビューターをアンインストールします。  
  
 [!code-csharp[HowTo#rmo_DropDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropdistpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropdistpub)]  
  
 次の例では、最初にローカル パブリケーション データベースを無効にしたりディストリビューション データベースを削除せずに、ディストリビューターをアンインストールします。  
  
 [!code-csharp[HowTo#rmo_DropDistPubForce](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropdistpubforce)]  
  
 [!code-vb[HowTo#rmo_vb_DropDistPubForce](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropdistpubforce)]  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理オブジェクトの概念](concepts/replication-management-objects-concepts.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)  
  
  
