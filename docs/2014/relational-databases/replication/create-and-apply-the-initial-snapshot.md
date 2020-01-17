---
title: 初期スナップショットの作成および適用 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], creating
- snapshot replication [SQL Server], initial snapshots
ms.assetid: 742727a1-5189-44ec-b3ae-6fd7aa1f5347
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a69d4805a21cfbd83bd9a8d79b5150460d4977be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721684"
---
# <a name="create-and-apply-the-initial-snapshot"></a>初期スナップショットの作成および適用
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、初期スナップショットを作成および適用する方法について説明します。 パラメーター化されたフィルターを使用するマージ パブリケーションでは、2 つの部分から成るスナップショットが必要です。 詳しくは、「 [パラメーター化されたフィルターを使用したパブリケーションのスナップショットの作成](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **初期スナップショットを作成および適用するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されている場合、パブリケーションの新規作成ウィザードでパブリケーションが作成された直後に、スナップショット エージェントによってスナップショットが生成されます。 既定では、スナップショットはディストリビューション エージェント (スナップショット レプリケーションおよびトランザクション レプリケーションの場合) またはマージ エージェント (マージ サブスクリプションの場合) によって、すべてのサブスクリプションに対して適用されます。 スナップショットは、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] およびレプリケーション モニターを使用して生成することもできます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
#### <a name="to-create-a-snapshot-in-management-studio"></a>Management Studio でスナップショットを作成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  スナップショットを作成するパブリケーションを右クリックして、 **[スナップショット エージェントの状態の表示]** をクリックします。  
  
4.  **[スナップショット エージェントの状態の表示 - \<Publication>]** ダイアログ ボックスで **[開始]** をクリックします。  
  
 スナップショット エージェントによるスナップショットの生成が完了すると、"[100%] 17 個のアーティクルのスナップショットが生成されました。" などのメッセージが表示されます。  
  
#### <a name="to-create-a-snapshot-in-replication-monitor"></a>レプリケーション モニターでスナップショットを作成するには  
  
1.  レプリケーション モニターの左ペインでパブリッシャー グループを展開し、パブリッシャーを展開します。  
  
2.  スナップショットを生成するパブリケーションを右クリックして、 **[スナップショットの生成]** をクリックします。  
  
3.  スナップショット エージェントの状態を表示するには、 **[エージェント]** タブをクリックします。詳細情報については、グリッドでスナップショット エージェントを右クリックし、 **[詳細表示]** をクリックしてください。  
  
#### <a name="to-apply-a-snapshot"></a>スナップショットを適用するには  
  
1.  生成したスナップショットは、ディストリビューション エージェントまたはマージ エージェントによるサブスクリプションの同期によって適用されます。  
  
    -   エージェントを連続して実行するように設定している場合 (トランザクション レプリケーションの既定の動作)、スナップショットは生成後に自動的に適用されます。  
  
    -   スケジュールに基づいてエージェントを実行するように設定している場合、スナップショットは、スケジュールによる次回のエージェント実行時に適用されます。  
  
    -   要求時にエージェントを実行するように設定している場合、スナップショットは、次回のエージェント実行時に適用されます。  
  
     サブスクリプションの同期の詳細については、「 [Synchronize a Push Subscription](synchronize-a-push-subscription.md) 」および「 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)ダイアログ ボックスを使用します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 初期スナップショットは、スナップショット エージェント ジョブを作成、実行するか、スナップショット エージェントの実行可能ファイルをバッチ ファイルから実行することによってプログラムから作成できます。 生成された初期スナップショットは、サブスクリプションの初回同期時にサブスクライバーに転送されて適用されます。 スナップショット エージェントをコマンド プロンプトまたはバッチ ファイルから実行する場合、既存のスナップショットが無効になるたびにエージェントを再実行する必要があります。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する必要がある場合は、不正アクセスを防ぐために、ファイルを保護します。  
  
#### <a name="to-create-and-run-a-snapshot-agent-job-to-generate-the-initial-snapshot"></a>スナップショット エージェント ジョブを作成、実行して初期スナップショットを生成するには  
  
1.  スナップショット パブリケーション、トランザクション パブリケーション、またはマージ パブリケーションを作成します。 詳細については、「 [Create a Publication](publish/create-a-publication.md)」を参照してください。  
  
2.  [sp_addpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql) を実行します。 このとき、 **@publication** パラメーターを指定したうえで、次のパラメーターを指定します。  
  
    -   **ディストリビューターで実行するスナップショット エージェントが使用するための Windows 認証の資格情報を @job_login に指定します。**  
  
    -   **Windows 資格情報に対応するパスワードを @job_password** に指定します。  
  
    -   (省略可) エージェントからパブリッシャーへの接続に SQL Server 認証を使用する場合は、 **@publisher_security_mode** の値に **@publisher_security_mode** を指定します。 この場合は、さらに、 **@publisher_login** 」および「 **@publisher_password** 」をご覧ください。  
  
    -   (省略可) スナップショット エージェント ジョブの同期スケジュールを指定します。 詳しくは、「 [Specify Synchronization Schedules](specify-synchronization-schedules.md)」をご覧ください。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
3.  パブリケーションにアーティクルを追加します。 詳しくは、「 [アーティクルを定義](publish/define-an-article.md)」をご覧ください。  
  
4.  パブリケーション データベースのパブリッシャーで [sp_startpublication_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql) を実行し、手順 1 の **@publication** の値を指定します。  
  
#### <a name="to-run-the-snapshot-agent-to-generate-the-initial-snapshot"></a>スナップショット エージェントを実行して初期スナップショットを生成するには  
  
1.  スナップショット パブリケーション、トランザクション パブリケーション、またはマージ パブリケーションを作成します。 詳細については、「 [Create a Publication](publish/create-a-publication.md)」を参照してください。  
  
2.  パブリケーションにアーティクルを追加します。 詳しくは、「 [アーティクルを定義](publish/define-an-article.md)」をご覧ください。  
  
3.  コマンド プロンプトまたはバッチ ファイルから、次のコマンド ライン引数を指定して [snapshot.exe](agents/replication-snapshot-agent.md) を実行し、 **レプリケーション マージ エージェント**を起動します。  
  
    -   **-Publication**  
  
    -   **-Publisher**  
  
    -   **-Distributor**  
  
    -   **-PublisherDB**  
  
    -   **-ReplicationType**  
  
     SQL Server 認証を使用する場合は、次の引数も指定する必要があります。  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-DistributorSecurityMode** =  **@publisher_security_mode**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-PublisherSecurityMode** =  **@publisher_security_mode**  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トランザクション パブリケーションを作成し、 **sqlcmd** スクリプト変数を使用して、新しいパブリケーション用にスナップショット エージェント ジョブを追加します。 ジョブを開始するコードも含まれています。  
  
 [!code-sql[HowTo#sp_trangenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpubinitialsnapshot.sql#sp_trangenerate_snapshot)]  
  
 次の例では、マージ パブリケーションを作成し、 **sqlcmd** 変数を使用して、そのパブリケーション用のスナップショット エージェント ジョブを追加します。 ジョブを開始するコードも含まれています。  
  
 [!code-sql[HowTo#sp_mergegenerate_snapshot](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubinitialsnapshot.sql#sp_mergegenerate_snapshot)]  
  
 次のコマンド ライン引数は、スナップショット エージェントを起動して、マージ パブリケーション用のスナップショットを生成します。  
  
> [!NOTE]  
>  読みやすくするために、改行が追加されています。 バッチ ファイルの場合、コマンドは 1 行で入力する必要があります。  
  
 [!code-sql[HowTo#startmergesnapshot_10](../../snippets/tsql/SQL15/replication/howto/tsql/createmergesnapshot_10.bat)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 スナップショット エージェントは、パブリッシャーが作成された後でスナップショットを生成します。 レプリケーション管理オブジェクト (RMO) およびレプリケーション エージェント機能への直接的なマネージド コード アクセスを使用して、これらのスナップショットをプログラムで生成できます。 使用するオブジェクトは、レプリケーションの種類によって異なります。 スナップショット エージェントを同期的に開始する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> オブジェクトを使用し、非同期的に開始する場合はエージェント ジョブを使用します。 初期スナップショットの生成後、サブスクリプションを最初に同期するときに、初期スナップショットをサブスクライバーに転送して適用することができます。 既存のスナップショットに最新の有効なデータが含まれていない場合は、エージェントを再実行する必要があります。 詳細については、「[Maintain Publications](publish/maintain-publications.md)」(パブリケーションの管理) を参照してください。  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&#xA0;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../includes/msconame-md.md)] を使用します。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>スナップショット エージェント ジョブを非同期的に開始して、スナップショット パブリケーションまたはトランザクション パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを読み込みます。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> の値が `false` の場合は、<xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> を呼び出して、このパブリケーション用のスナップショット エージェント ジョブを作成します。  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> メソッドを呼び出して、このパブリケーションのスナップショットを生成するエージェント ジョブを開始します。  
  
6.  (省略可) <xref:Microsoft.SqlServer.Replication.TransPublication.SnapshotAvailable%2A> の値が `true` である場合は、スナップショットをサブスクライバーに使用できます。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-snapshot-or-transactional-publication-by-running-the-snapshot-agent-synchronous"></a>スナップショット エージェント ジョブを同期的に実行して、スナップショット パブリケーションまたはトランザクション パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> クラスのインスタンスを作成し、次の必須プロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - パブリッシャーの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - パブリケーション データベースの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - パブリケーションの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - ディストリビューターの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - パブリッシャーへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。パブリッシャーへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - ディストリビューターへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。ディストリビューターへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Transactional> に <xref:Microsoft.SqlServer.Replication.ReplicationType.Snapshot> または <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> メソッドを呼び出します。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-starting-the-snapshot-agent-job-asynchronous"></a>スナップショット エージェント ジョブを非同期的に開始して、マージ パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成します。 パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトの残りのプロパティを読み込みます。 このメソッドが `false` を返す場合、手順 2. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.Publication.SnapshotAgentExists%2A> の値が `false` の場合は、<xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> を呼び出して、このパブリケーション用のスナップショット エージェント ジョブを作成します。  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.StartSnapshotGenerationAgentJob%2A> メソッドを呼び出して、このパブリケーションのスナップショットを生成するエージェント ジョブを開始します。  
  
6.  (省略可) <xref:Microsoft.SqlServer.Replication.MergePublication.SnapshotAvailable%2A> の値が `true` である場合は、スナップショットをサブスクライバーに使用できます。  
  
#### <a name="to-generate-the-initial-snapshot-for-a-merge-publication-by-running-the-snapshot-agent-synchronous"></a>スナップショット エージェントを同期的に実行して、マージ パブリケーションの初期スナップショットを生成するには  
  
1.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent> クラスのインスタンスを作成し、次の必須プロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publisher%2A> - パブリッシャーの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherDatabase%2A> - パブリケーション データベースの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Publication%2A> - パブリケーションの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.Distributor%2A> - ディストリビューターの名前  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherSecurityMode%2A> - パブリッシャーへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。パブリッシャーへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.PublisherPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
    -   <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorSecurityMode%2A> - ディストリビューターへの接続時に Windows 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SecurityMode.Integrated> を指定します。ディストリビューターへの接続時に <xref:Microsoft.SqlServer.Replication.SecurityMode.Standard> 認証を使用する場合は <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorLogin%2A> を指定し、 <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.DistributorPassword%2A> および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に値を指定します。 推奨されるのは、Windows 認証です。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationType.Merge> に <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.ReplicationType%2A>を設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.SnapshotGenerationAgent.GenerateSnapshot%2A> メソッドを呼び出します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、スナップショット エージェントを同期的に実行して、トランザクション パブリケーションの初期スナップショットを生成します。  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot)]  
  
 次の例では、エージェント ジョブを非同期的に開始して、トランザクション パブリケーションの初期スナップショットを生成します。  
  
 [!code-csharp[HowTo#rmo_GenerateSnapshot_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_generatesnapshot_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_GenerateSnapshot_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_generatesnapshot_withjob)]  
  
## <a name="see-also"></a>関連項目  
 [Create a Publication](publish/create-a-publication.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [ssSDSFull](create-a-push-subscription.md)   
 [Specify Synchronization Schedules](specify-synchronization-schedules.md)   
 [スナップショットの作成および適用](create-and-apply-the-snapshot.md)   
 [Initialize a Subscription with a Snapshot (スナップショットを使用したサブスクリプションの初期化)](initialize-a-subscription-with-a-snapshot.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [sqlcmd でのスクリプト変数の使用](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
