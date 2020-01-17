---
title: パブリケーションの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
- adding articles
- articles [SQL Server replication], adding
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: dc432ca82662d098b970b2dbeab6a43243e2ead6
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846631"
---
# <a name="create-a-publication"></a>パブリケーションの作成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、パブリケーションを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **パブリケーションを作成してアーティクルを定義するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   パブリケーション名およびアーティクル名には、% , \* , [ , ] , | , : , " , ? を使用できません。 , ' , \ , / , < , >. データベースのオブジェクトにこれらの文字が含まれ、これらをレプリケートする場合は、 **[アーティクルのプロパティ - \<Article>]** ダイアログ ボックスで、オブジェクト名と異なるアーティクル名を指定する必要があります。このダイアログ ボックスは、ウィザードの **[アーティクル]** ページより利用可能です。  
  
###  <a name="Security"></a> セキュリティ  
 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&#xA0;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../../includes/msconame-md.md)] を使用します。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードにより、パブリケーションを作成し、アーティクルを定義します。 パブリケーションを作成したら、 **[パブリケーションのプロパティ - \<Publication>]** ダイアログ ボックスでパブリケーションのプロパティを表示および変更します。 Oracle データベースからパブリケーションを作成する方法については、「[Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)」(Oracle データベースからパブリケーションを作成する) をご覧ください。  
  
#### <a name="to-create-a-publication-and-define-articles"></a>パブリケーションを作成し、アーティクルを定義するには  
  
1.  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを右クリックします。  
  
3.  **[新しいパブリケーション]** をクリックします。  
  
4.  パブリケーションの新規作成ウィザードのページに従い、以下の操作を実行します。  
  
    -   サーバーでディストリビューションが構成されていない場合は、ディストリビューターを指定します。 ディストリビューションの構成の詳細については、「[Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md)」(パブリッシュとディストリビューションの構成) をご覧ください。  
  
         **[ディストリビューター]** ページで、パブリッシャー サーバーが独自のディストリビューター (ローカル ディストリビューター) として機能するように指定した場合、このサーバーはディストリビューターとして構成されていないため、パブリケーションの新規作成ウィザードでサーバーを構成します。 **[スナップショット フォルダー]** ページで、ディストリビューターの既定のスナップショット フォルダーを指定します。 スナップショット フォルダーは、共有として指定したディレクトリです。このフォルダーの読み取りと書き込みをするエージェントには、このフォルダーへのアクセスを可能にする十分な権限が必要です。 フォルダーの適切なセキュリティ保護の詳細については、「[Secure the Snapshot Folder](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
         別のサーバーがディストリビューターとして機能するように指定する場合は、パブリッシャーからディストリビューターへの接続のため、 **[管理パスワード]** ページでパスワードを入力する必要があります。 このパスワードは、リモート ディストリビューターでパブリッシャーを有効にしたときに指定したパスワードと一致する必要があります。  
  
         詳しくは、「 [Configure Distribution](../../../relational-databases/replication/configure-distribution.md)」を参照してください。  
  
    -   パブリケーション データベースを選択します。  
  
    -   パブリケーションの種類を選択します。 詳細については、「[Types of Replication](../../../relational-databases/replication/types-of-replication.md)」(レプリケーションの種類) をご覧ください。  
  
    -   パブリッシュするデータおよびデータベース オブジェクトを指定します。必要に応じて、テーブル アーティクルから列をフィルター選択し、アーティクルのプロパティを設定します。  
  
    -   必要に応じて、テーブル アーティクルから行をフィルター選択します。 詳細については、「[パブリッシュされたデータのフィルター選択](../../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
    -   スナップショット エージェントのスケジュールを設定します。  
  
    -   以下のレプリケーション エージェントの実行および接続に使用される資格情報を指定します。  
  
         \-すべてのパブリケーション用のスナップショット エージェント。  
  
         \-すべてのトランザクション パブリケーション用のログ リーダー エージェント。  
  
         \-更新サブスクリプションを許可するトランザクション パブリケーションのキュー リーダー エージェント。  
  
         詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 」および「 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)」を参照してください。  
  
    -   必要に応じて、パブリケーションのスクリプトを作成します。 詳しくは、「 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)」をご覧ください。  
  
    -   パブリケーションの名前を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 パブリケーションは、レプリケーションのストアド プロシージャを使用してプログラムから作成できます。 どのストアド プロシージャを使用するかは、作成するパブリケーションの種類によって異なります。  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションを作成するには  
  
1.  パブリッシャーのパブリケーション データベースで [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) を実行し、スナップショット レプリケーションまたはトランザクション レプリケーションを使用して現在のデータベースのパブリケーションを有効にします。  
  
2.  トランザクション パブリケーションの場合は、パブリケーション データベースのログ リーダー エージェント ジョブが存在するかどうかを確認します。 スナップショット パブリケーションの場合、この手順は不要です。  
  
    -   パブリケーション データベースのログ リーダー エージェント ジョブが存在する場合は、手順 3. に進みます。  
  
    -   パブリッシュされたデータベース用のログ リーダー エージェント ジョブが存在するかどうかわからない場合は、パブリッシャー側のパブリケーション データベースに対して [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) を実行します。  
  
    -   結果セットが空の場合は、ログ リーダー エージェント ジョブを作成します。 パブリッシャーで、[sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) を実行します。 エージェントの実行に使用される [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 資格情報を **\@job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 手順 3. に進みます。  
  
3.  パブリッシャーで、[sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) を実行します。 **\@publication** にパブリケーション名を指定し、 **\@repl_freq** パラメーターに **snapshot** (スナップショット パブリケーションの場合) または **continuous** (トランザクション パブリケーションの場合) を指定します。 必要に応じて、その他のパブリケーション オプションを指定してください。 これにより、パブリケーションが定義されます。  
  
    > [!NOTE]  
    >  パブリケーション名に、次の文字を含めることはできません。  
    >   
    >  % * [ ] | : " ? \ / < >  
  
4.  パブリッシャーで [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 3 で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@snapshot_job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
5.  パブリケーションにアーティクルを追加します。 詳しくは、「 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
6.  スナップショット エージェント ジョブを起動して、このパブリケーションの初期スナップショットを生成します。 詳しくは、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
#### <a name="to-create-a-merge-publication"></a>マージ パブリケーションを作成するには  
  
1.  パブリッシャーで [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) を実行し、マージ レプリケーションを使用して現在のデータベースのパブリケーションを有効にします。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、[sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) を実行します。 **\@publication** にパブリケーションの名前を指定し、必要に応じて他のパブリケーション オプションを指定します。 これにより、パブリケーションが定義されます。  
  
    > [!NOTE]  
    >  パブリケーション名に、次の文字を含めることはできません。  
    >   
    >  % * [ ] | : " ? \ / < >  
  
3.  パブリッシャーで [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 2 で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@snapshot_job_name** と **\@password** に指定します。 エージェントがパブリッシャーに接続する際に SQL Server 認証を使用する場合、さらに **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
4.  パブリケーションにアーティクルを追加します。 詳しくは、「 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」をご覧ください。  
  
5.  スナップショット エージェント ジョブを起動して、このパブリケーションの初期スナップショットを生成します。 詳しくは、「 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」をご覧ください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、トランザクション パブリケーションを作成します。 スナップショット エージェント ジョブおよびログ リーダー エージェント ジョブの作成に必要な Windows 資格情報は、スクリプト変数を使用して渡しています。  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 この例では、マージ パブリケーションを作成します。 スナップショット エージェント ジョブの作成に必要な Windows 資格情報は、スクリプト変数を使用して渡しています。  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーション管理オブジェクト (RMO) を使用することで、プログラムによってパブリケーションを作成できます。 パブリケーションの作成に使用する RMO クラスは、作成するパブリケーションの種類によって異なります。  
  
#### <a name="to-create-a-snapshot-or-transactional-publication"></a>スナップショット パブリケーションまたはトランザクション パブリケーションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  パブリケーション データベースに <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> クラスのインスタンスを作成し、<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> インスタンスを設定し、<xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> が **false** を返す場合、データベースが存在するかどうか確認してください。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> プロパティが **false** の場合、**true** に設定します。  
  
4.  トランザクション パブリケーションの場合は、<xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> プロパティの値を確認します。 このプロパティが **true**の場合、このデータベースに対するログ リーダー エージェント ジョブが既に存在しています。 このプロパティが **false**の場合、次の操作を実行してください。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドを設定して、ログ リーダー エージェントを実行するときに使用される [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows アカウントの資格情報を指定します。  
  
        > [!NOTE]  
        >  パブリケーションが **sysadmin** 固定サーバー ロールのメンバーにより作成される場合、<xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> の設定は不要です。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) SQL Server 認証を使用してパブリッシャーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> ) フィールドを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> メソッドを呼び出して、データベースに対するログ リーダー エージェント ジョブを作成します。  
  
5.  <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成し、このオブジェクトに次のプロパティを設定します。  
  
    -   手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   パブリッシュするデータベースの名前を <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>に指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> にパブリケーションの名前を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationType> または <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> の <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドに、スナップショット エージェントの実行に使用する Windows アカウントの資格情報を指定します。 このアカウントは、Windows 認証を使用している場合に、スナップショット エージェントがローカル ディストリビューターへの接続や任意のリモート接続を行うときにも使用されます。  
  
        > [!NOTE]  
        >  パブリケーションが <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 固定サーバー ロールのメンバーにより作成される場合、 **P:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity** の設定は不要です。 この場合、エージェントは SQL Server エージェントのアカウントを借用します。 詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) SQL Server 認証を使用してパブリッシャーに接続する場合、 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> の <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> (または <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> ) フィールドを設定します。  
  
    -   (省略可) 包括的論理和演算子 (Visual C# では **|** 、Visual Basic では **Or**) および排他的論理和演算子 (Visual C# では **^** 、Visual Basic では **Xor**) を使用して、 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティに <xref:Microsoft.SqlServer.Replication.PublicationAttributes> の値を設定します。  
  
    -   (省略可) パブリッシャーが SQL Server パブリッシャーでない場合、パブリッシャーの名前を <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> に指定します。  
  
6.  <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> メソッドを呼び出して、パブリケーションを作成します。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>を含むすべてのプロパティに指定された値がディストリビューターにプレーンテキストとして送信されます。 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> メソッドを呼び出す前に、パブリッシャーとリモート ディストリビューター間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
7.  <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> メソッドを呼び出して、パブリケーションに対するスナップショット エージェント ジョブを作成します。  
  
#### <a name="to-create-a-merge-publication"></a>マージ パブリケーションを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  パブリケーション データベースに <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> クラスのインスタンスを作成し、<xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> インスタンスを設定し、<xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> が **false** を返す場合、データベースが存在するかどうか確認してください。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> プロパティが **false** の場合、これを **true** に設定し、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> を呼び出します。  
  
4.  <xref:Microsoft.SqlServer.Replication.MergePublication> クラスのインスタンスを作成し、このオブジェクトに次のプロパティを設定します。  
  
    -   手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に指定します。  
  
    -   パブリッシュするデータベースの名前を <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>に指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>にパブリケーションの名前を指定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> フィールドに、スナップショット エージェントの実行に使用する Windows アカウントの資格情報を指定します。 このアカウントは、Windows 認証を使用している場合に、スナップショット エージェントがローカル ディストリビューターへの接続や任意のリモート接続を行うときにも使用されます。  
  
        > [!NOTE]  
        >  パブリケーションが <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 固定サーバー ロールのメンバーにより作成される場合、 **P:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity** の設定は不要です。 詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)」を参照してください。  
  
    -   (省略可) 包括的論理和演算子 (Visual C# では **|** 、Visual Basic では **Or** ) および排他的論理和演算子 (Visual C# では **^** 、Visual Basic では **Xor** ) を使用して、 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> プロパティに <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> プロパティの値を確認します。  
  
5.  <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> メソッドを呼び出して、パブリケーションを作成します。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>を含むすべてのプロパティに指定された値がディストリビューターにプレーンテキストとして送信されます。 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> メソッドを呼び出す前に、パブリッシャーとリモート ディストリビューター間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
6.  <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> メソッドを呼び出して、パブリケーションに対するスナップショット エージェント ジョブを作成します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、AdventureWorks データベースでトランザクション パブリッシュを有効にして、ログ リーダー エージェント ジョブを定義し、AdvWorksProductTran パブリケーションを作成します。 このパブリケーションには、アーティクルを定義する必要があります。 ログ リーダー エージェント ジョブとスナップショット エージェント ジョブの作成に必要な Windows アカウントの資格情報は、実行時に渡されます。 RMO を使用してスナップショット アーティクルとトランザクション アーティクルを定義する方法については、「 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」を参照してください。  
  
 [!code-cs[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 次の例では、AdventureWorks データベースでマージ パブリッシュを有効にし、AdvWorksSalesOrdersMerge パブリケーションを作成します。 このパブリケーションには、アーティクルを定義する必要があります。 スナップショット エージェント ジョブの作成に必要な Windows アカウントの資格情報は、実行時に渡されます。 RMO を使用してマージ アーティクルを定義する方法については、「 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)」を参照してください。  
  
 [!code-cs[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## <a name="see-also"></a>参照  
 [sqlcmd でのスクリプト変数の使用](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Replication Management Objects Concepts](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)   
 [パブリケーション プロパティの表示および変更](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [[ディストリビューションの構成]](../../../relational-databases/replication/configure-distribution.md)   
 [ディストリビューターのセキュリティ保護](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [パブリッシャーのセキュリティ保護](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  
