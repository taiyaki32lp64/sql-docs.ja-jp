---
title: Oracle データベースからのパブリケーションの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], Oracle databases
- Oracle publishing [SQL Server replication], configuring
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b43b3b2f67554a59388ccd6a50485e4c71d9e1a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908597"
---
# <a name="create-a-publication-from-an-oracle-database"></a>Oracle データベースからのパブリケーションの作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して、Oracle データベースからパブリケーションを作成する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
-   **Oracle データベースからパブリケーションを作成するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   パブリケーションを作成する前に、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターに Oracle ソフトウェアをインストールし、Oracle データベースを構成する必要があります。 詳細については、「[Configure an Oracle Publisher (Oracle パブリッシャーの構成)](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)」を参照してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 パブリケーションの新規作成ウィザードを使用して、Oracle データベースからスナップショット パブリケーションまたはトランザクション パブリケーションを作成します。  
  
 Oracle データベースからパブリケーションを最初に作成するときは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターで Oracle パブリッシャーを識別する必要があります (以降同じデータベースからパブリケーションを作成するときは、この作業は不要です)。 Oracle パブリッシャーの識別は、パブリケーションの新規作成ウィザードまたは **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスで行うことができます。このトピックでは、 **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスについて説明します。  
  
#### <a name="to-identify-the-oracle-publisher-at-the-sql-server-distributor"></a>SQL Server ディストリビューターで Oracle パブリッシャーを識別するには  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]で、Oracle パブリッシャーがディストリビューターとして使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを右クリックし、 **[ディストリビューターのプロパティ]** をクリックします。  
  
3.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[パブリッシャー]** ページで、 **[追加]** をクリックし、 **[Oracle パブリッシャーの追加]** をクリックします。  
  
4.  **[サーバーへの接続]** ダイアログ ボックスで、 **[オプション]** ボタンをクリックします。  
  
5.  **[ログイン]** タブで、次の操作を実行します。  
  
    1.  Oracle データベースのインスタンス名を入力するか、または **[サーバー インスタンス]** コンボ ボックスで **[参照]** を選択します。  
  
    2.  **[Oracle 標準認証]** (推奨) または **[Windows 認証]** を選択してください。  
  
         **[Windows 認証]** を選択する場合は、Windows 資格情報を使用した接続を許可するように Oracle サーバーが構成されている必要があります (詳細については、Oracle のマニュアルを参照してください)。また、レプリケーション管理ユーザー スキーマに指定した [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows アカウントと同じアカウントを使用して現在ログインしている必要があります。  
  
    3.  **[Oracle 標準認証]** を選択する場合は、構成時に Oracle パブリッシャーで作成したレプリケーション管理ユーザー スキーマのログインおよびパスワードを入力します。  
  
6.  **[接続プロパティ]** タブで、パブリッシャーの種類として **[ゲートウェイ]** または **[完全]** を選択します。  
  
     **[完全]** オプションを選択した場合は、Oracle パブリッシング用にサポートされる完全な機能セットがスナップショットおよびトランザクション パブリケーションに提供されます。 **[ゲートウェイ]** オプションを選択した場合は、レプリケーションがシステム間のゲートウェイとして動作する場合のパフォーマンスを向上させるために、特定のデザインが最適化されます。 複数のトランザクション パブリケーションに同じテーブルをパブリッシュする場合は、 **[ゲートウェイ]** オプションは使用できません。 **[ゲートウェイ]** オプションを選択した場合、1 つのテーブルは、最大で 1 つのトランザクション パブリケーションおよび任意の数のスナップショット パブリケーションに含めることができます。  
  
7.  **[接続]** をクリックします。これにより、Oracle パブリッシャーへの接続が作成され、レプリケーション用に構成されます。 **[サーバーへの接続]** ダイアログ ボックスが閉じ、 **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスに戻ります。  
  
    > [!NOTE]  
    >  ネットワーク構成に問題がある場合は、この時点でエラーが返されます。 Oracle データベースへの接続中に問題が発生した場合は、「 [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)」の「SQL Server ディストリビューターが Oracle データベース インスタンスに接続できない」を参照してください。  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

#### <a name="to-create-a-publication-from-an-oracle-database"></a>Oracle データベースからパブリケーションを作成するには  
  
1.  Oracle パブリッシャーがディストリビューターとして使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開します。  
  
3.  **[ローカル パブリケーション]** フォルダーを右クリックし、 **[新しい Oracle パブリケーション]** をクリックします。  
  
4.  パブリケーションの新規作成ウィザードの **[Oracle パブリッシャー]** ページで、Oracle パブリッシャーを選択します。 Oracle パブリッシャーが表示されていない場合は、 **[Oracle パブリッシャーの追加]** をクリックし、前の手順から操作を行います。  
  
5.  **[パブリケーションの種類]** ページで、 **[スナップショット パブリケーション]** または **[トランザクション パブリケーション]** を選択します。  
  
6.  **[アーティクル]** ページで、パブリッシュするデータベース オブジェクトを選択します。  
  
     必要に応じて、テーブルを展開してから 1 つ以上の列のチェック ボックスをオフにし、テーブルの列をフィルター選択します。 **[アーティクルのプロパティ]** をクリックしてアーティクルのプロパティを表示および変更し、必要に応じて代替データ型マッピングを指定します。 データ型マッピングの詳細については、「[Specify Data Type Mappings for an Oracle Publisher](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)」(Oracle パブリッシャーのデータ型マッピング) を参照してください。  
  
7.  **[テーブル行のフィルター選択]** ページで、必要に応じてフィルターを適用し、1 つ以上のテーブルからデータのサブセットをパブリッシュします。  
  
8.  サブスクリプション データベースですべてのオブジェクトを作成し、必要なデータをすべて追加している場合に限り、 **[スナップショット エージェント]** ページで **[スナップショットをすぐに作成する]** をオフにします。  
  
9. **[エージェント セキュリティ]** ページで、スナップショット エージェントの資格情報 (すべてのパブリケーション用) およびログ リーダー エージェントの資格情報 (トランザクション パブリケーション用) を指定します。 エージェントが実行され、指定した [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows アカウントのコンテキストを使用して [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ディストリビューターへの接続が確立されます。 レプリケーション管理ユーザー スキーマとして指定したアカウントのコンテキストを使用して、エージェントから Oracle データベースへの接続が確立されます。 詳細については、「[Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)」(Oracle パブリッシャーの構成) をご覧ください。  
  
     各エージェントで必要な権限の詳細については、「 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 」および「 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)」を参照してください。  
  
10. **[ウィザードのアクション]** ページで、必要に応じてパブリケーションのスクリプトを作成できます。 詳細については、「 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)」をご参照ください。  
  
11. **[ウィザードの完了]** ページで、パブリケーションの名前を指定します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 Oracle データベースをパブリッシャーとして構成した後で、システム ストアド プロシージャを使用して、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] パブリッシャーから行う場合と同じ方法でトランザクション パブリケーションまたはスナップショット パブリケーションを作成できます。  
  
#### <a name="to-create-an-oracle-publication"></a>Oracle パブリケーションを作成するには  
  
1.  Oracle データベースをパブリッシャーとして構成します。 詳細については、「[Configure an Oracle Publisher](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)」(Oracle パブリッシャーの構成) をご覧ください。  
  
2.  リモート ディストリビューターが存在しない場合は、リモート ディストリビューターを構成します。 詳細については、「 [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md)」をご参照ください。  
  
3.  Oracle パブリッシャーが使用するリモート ディストリビューターで、[sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md) を実行します。 **\@publisher** に Oracle データベース インスタンスの TNS (Transparent Network Substrate) 名を、 **\@publisher_type** に **ORACLE** または **ORACLE GATEWAY** の値を指定します。 `Specify` 次のいずれかの方法で、Oracle パブリッシャーからリモート [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ディストリビューターに接続するときに使用されるセキュリティ モードを指定します。  
  
    -   既定の Oracle 標準認証を使用するには、 **\@security_mode** に **0** を、 **\@login** に Oracle パブリッシャーで構成時に作成したレプリケーション管理ユーザー スキーマを、 **\@password** にパスワードを指定します。  
  
        > [!IMPORTANT]  
        >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する場合は、不正アクセスを防ぐために、そのファイルをセキュリティで保護する必要があります。  
  
    -   Windows 認証を使用するには、 **\@security_mode** に **1** を指定します。  
  
        > [!NOTE]  
        >  Windows 認証を使用する場合は、Windows 資格情報を使用した接続を許可するように Oracle サーバーが構成されている必要があります (詳細については、Oracle のマニュアルを参照してください)。また、レプリケーション管理ユーザー スキーマに指定した Microsoft Windows アカウントと同じアカウントを使用して現在ログインしている必要があります。  
  
4.  パブリケーション データベースのログ リーダー エージェント ジョブを作成します。  
  
    -   パブリッシュされたデータベースにログ リーダー エージェント ジョブが存在するかどうか不明である場合は、ディストリビューション データベースの Oracle パブリッシャーによって使用されるディストリビューターで [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) を実行します。 **\@publisher** に Oracle パブリッシャーの名前を指定します。 結果セットが空の場合、ログ リーダー エージェント ジョブを作成する必要があります。  
  
    -   パブリケーション データベース用のログ リーダー エージェント ジョブが既に存在する場合、手順 5. に進みます。  
  
    -   Oracle パブリッシャーのディストリビューション データベースによって使用されるディストリビューターで、[sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md) を実行します。 **\@job_login** と **\@job_password** に、エージェントを実行するときに使用する Windows 資格情報を指定します。  
  
        > [!NOTE]  
        >  **\@job_login** パラメーターは、手順 3 で指定したログインと一致する必要があります。 パブリッシャーのセキュリティ情報を指定しないでください。 ログ リーダー エージェントは、手順 3. で指定されたセキュリティ情報を使用してパブリッシャーに接続します。  
  
5.  ディストリビューター側のディストリビューション データベースに対して、パブリケーションを作成する [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) を実行します。 詳細については、「 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)」をご覧ください。  
  
6.  ディストリビューター側のディストリビューション データベースに対して、パブリケーションを作成する [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) を実行します。 手順 4 で使用したパブリケーション名を **\@publication** に指定し、スナップショット エージェントを実行するときに使用される Windows 資格情報を **\@job_name** と **\@password** に指定します。 パブリッシャーへの接続時に Oracle 標準認証を使用するには、 **\@publisher_security_mode** に **0** を指定し、 **\@publisher_login** と **\@publisher_password** に Oracle ログイン情報を指定する必要があります。 これにより、パブリケーション用のスナップショット エージェント ジョブが作成されます。  
  
## <a name="see-also"></a>参照  
 [Configure an Oracle Publisher (Oracle パブリッシャーの構成)](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Oracle パブリッシャー用のトランザクション セット ジョブの構成 &#40;レプリケーション Transact-SQL プログラミング&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Oracle パブリッシングの概要](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  
