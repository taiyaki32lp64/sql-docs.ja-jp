---
title: レプリケーションのセキュリティ設定の表示および変更 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying replication security settings
- replication [SQL Server], security
- security [SQL Server replication], viewing settings
- viewing replication security settings
- security [SQL Server replication], modifying settings
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 923d137b4b884300b2fb31cbacf2ee7dff1a6621
ms.sourcegitcommit: 655a7217bdf516ce3337691574880619f16de70f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2019
ms.locfileid: "73912802"
---
# <a name="view-and-modify-replication-security-settings"></a>レプリケーションのセキュリティ設定の表示および変更
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、レプリケーションのセキュリティ設定を表示および変更する方法について説明します。 たとえば、ログ リーダー エージェントからパブリッシャーへの接続を SQL Server 認証から Windows 統合認証に変更したい場合や、Windows アカウントのパスワードを変更したときにエージェント ジョブの実行に使用する資格情報を変更したい場合があります。 各エージェントで必要な権限の詳細については、「 [Replication Agent Security Model](replication-agent-security-model.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **レプリケーションのセキュリティ設定を表示および変更するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
-   **フォロー アップ:**  [レプリケーションのセキュリティ設定を変更した後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   使用するストアド プロシージャは、エージェントの種類およびサーバー接続の種類によって異なります。  
  
-   使用する RMO のクラスとプロパティは、エージェントの種類およびサーバー接続の種類によって異なります。  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティ上の理由から、レプリケーション ストアド プロシージャによって返される結果セットでは、パスワードの実際の値はマスクされます。  
  
####  <a name="Permissions"></a> アクセス許可  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 次のダイアログ ボックスでセキュリティ設定を表示および変更します。  
  
1.  **[レプリケーション パスワードの更新]** ダイアログ ボックス。このダイアログ ボックスは、 **の** [レプリケーション] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]フォルダーから利用できます。 レプリケーション トポロジのサーバーで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アカウントまたは Windows アカウントのパスワードを変更する場合は、そのアカウントを使用する各エージェントのパスワードを更新するよりも、このダイアログ ボックスを使用してください。 複数のサーバー上のエージェントが同じアカウントを使用している場合は、それぞれのサーバーに接続してパスワードを変更する必要があります。 パスワードは、レプリケーションで使用されるすべての場所で更新されます。 パスワードは、リンク サーバーなど、その他の場所では更新されません。  
  
2.  **[パブリケーションのプロパティ -** Publication>] **ダイアログ ボックスの \<[エージェント セキュリティ]** ページ。 このダイアログ ボックスへのアクセス方法の詳細については、「[パブリケーション プロパティの表示および変更](../publish/view-and-modify-publication-properties.md)」を参照してください。  
  
3.  **[サブスクリプションのプロパティ - \<Subscription>]** ダイアログ ボックス。 このダイアログ ボックスへのアクセスの詳細については、「 [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) 」および「 [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md)」を参照してください。  
  
4.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスと **[ディストリビューション データベースのプロパティ - \<Database>]** ダイアログ ボックス。 これらのダイアログ ボックスへのアクセスの詳細については、「 [View and Modify Distributor and Publisher Properties](../view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
5.  **[パブリッシャーのプロパティ - \<Publisher>]** ダイアログ ボックス。 このダイアログ ボックスへのアクセスの詳細については、「 [View and Modify Distributor and Publisher Properties](../view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
#### <a name="to-change-the-password-for-an-account-used-by-one-or-more-agents"></a>1 つ以上のエージェントによって使用されるアカウントのパスワードを変更するには  
  
1.  アカウントが SQL Server アカウントの場合、このダイアログ ボックスによって SQL Server アカウントのパスワードも変更されます。 アカウントが Windows アカウントの場合は、最初に Windows でパスワードを変更します。 詳細については、Windows のマニュアルを参照してください。  
  
    > [!NOTE]  
    >  レプリケーション パスワードを変更したら、そのパスワードを使用する各エージェントを停止して再起動し、エージェントに対して変更を反映させる必要があります。  
  
2.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]でサーバーに接続して、サーバー ノードを展開します。  
  
3.  **[レプリケーション]** フォルダーを右クリックし、 **[レプリケーション パスワードの更新]** をクリックします。  
  
4.  **[レプリケーション パスワードの更新]** ダイアログ ボックスで、アカウントと新しいパスワードを指定します。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>スナップショット エージェントのセキュリティ設定を変更するには  
  
1.  **[パブリケーションのプロパティ -** Publication>] **ダイアログ ボックスの \<[エージェント セキュリティ]** ページで、 **[スナップショット エージェント]** テキスト ボックスの横にある **[セキュリティ設定]** ボタンをクリックします。  
  
2.  **[スナップショット エージェントのセキュリティ]** ダイアログ ボックスで、エージェントを実行するアカウントを指定します。  
  
    -   **[プロセス アカウント]** テキスト ボックスに新しい Windows アカウントを入力します。  
  
    -   **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに、新しい複雑なパスワードを入力します。  
  
3.  エージェントがディストリビューターからパブリッシャーに接続するときのコンテキストを指定します。 **[次の SQL Server ログインを使用する]** を選択する場合は、ログインも指定する必要があります。  
  
    -   **[ログイン]** テキスト ボックスにログインを入力します。  
  
    -   **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに、新しい複雑なパスワードを入力します。  
  
    > [!NOTE]  
    >  パブリッシャーが Oracle パブリッシャーの場合は、接続のコンテキストを **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスで指定します。 コンテキストを変更する手順については、以下を参照してください。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>ログ リーダー エージェントのセキュリティ設定を変更するには  
  
1.  **[パブリケーションのプロパティ -** Publication>] **ダイアログ ボックスの \<[エージェント セキュリティ]** ページで、 **[ログ リーダー エージェント]** テキスト ボックスの横にある **[セキュリティ設定]** ボタンをクリックします。  
  
2.  **[ログ リーダー エージェントのセキュリティ]** ダイアログ ボックスで、エージェントを実行するアカウントを指定します。  
  
    -   **[プロセス アカウント]** テキスト ボックスに新しい Windows アカウントを入力します。  
  
    -   **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに、新しい複雑なパスワードを入力します。  
  
3.  エージェントがディストリビューターからパブリッシャーに接続するときのコンテキストを指定します。 **[次の SQL Server ログインを使用する]** を選択する場合は、ログインも指定する必要があります。  
  
    -   **[ログイン]** テキスト ボックスにログインを入力します。  
  
    -   **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに、新しい複雑なパスワードを入力します。  
  
    > [!NOTE]  
    >  パブリッシャーが Oracle パブリッシャーの場合は、接続のコンテキストを **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスで指定します。 次の手順を使用して、コンテキストを変更します。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  ログ リーダー エージェントは、パブリッシュされているデータベースごとに 1 つ存在します。 1 つのパブリケーションでエージェントのセキュリティ設定を変更すると、パブリケーション データベースのすべてのパブリケーションの設定に影響が及びます。  
  
#### <a name="to-change-the-context-under-which-the-snapshot-agent-and-log-reader-agent-for-an-oracle-publication-make-connections-to-the-publisher"></a>Oracle パブリケーションのスナップショット エージェントおよびログ リーダー エージェントがパブリッシャーに接続するときのコンテキストを変更するには  
  
1.  **[ディストリビューターのプロパティ -** Distributor>] **ダイアログ ボックスの \<[パブリッシャー]** ページで、パブリッシャーの横にあるプロパティ ボタン ( **...** ) をクリックします。  
  
2.  **[パブリッシャーへのエージェント接続]** セクションで、構成したレプリケーション管理ユーザー スキーマによって使用されるログインとパスワードを指定します。 詳細については、「[Configure an Oracle Publisher (Oracle パブリッシャーの構成)](../non-sql/configure-an-oracle-publisher.md)」をご覧ください。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>プッシュ サブスクリプションに対するディストリビューション エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャーの **[サブスクリプションのプロパティ - \<Subscription>]** ダイアログ ボックスでは、次の変更を加えることができます。  
  
    -   ディストリビューション エージェントを実行してディストリビューターへ接続するアカウントを変更するには、 **[エージェント プロセス アカウント]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスで、アカウントとパスワードを指定します。  
  
    -   ディストリビューション エージェントがサブスクライバーに接続するときのコンテキストを変更するには、 **[サブスクライバー接続]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[接続情報の入力]** ダイアログ ボックスでコンテキストを指定します。  
  
         キュー更新サブスクリプションを使用する場合、ここで指定したコンテキストは、サブスクライバーに接続するためにキュー リーダー エージェントでも使用されます。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>プル サブスクリプションに対するディストリビューション エージェントのセキュリティ設定を変更するには  
  
1.  サブスクライバーの **[サブスクリプションのプロパティ - \<Subscription>]** ダイアログ ボックスでは、次の変更を加えることができます。  
  
    -   ディストリビューション エージェントを実行してサブスクライバーへ接続するアカウントを変更するには、 **[エージェント プロセス アカウント]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[ディストリビューション エージェント セキュリティ]** ダイアログ ボックスで、アカウントとパスワードを指定します。  
  
         キュー更新サブスクリプションを使用する場合、ここで指定したコンテキストは、サブスクライバーに接続するためにキュー リーダー エージェントでも使用されます。  
  
    -   ディストリビューション エージェントがディストリビューターに接続するときのコンテキストを変更するには、 **[ディストリビューター接続]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[接続情報の入力]** ダイアログ ボックスでコンテキストを指定します。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>プッシュ サブスクリプションに対するマージ エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャーの **[サブスクリプションのプロパティ - \<Subscription>]** ダイアログ ボックスでは、次の変更を加えることができます。  
  
    -   マージ エージェントを実行してパブリッシャーおよびディストリビューターへ接続するアカウントを変更するには、 **[エージェント プロセス アカウント]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[マージ エージェント セキュリティ]** ダイアログ ボックスで、アカウントとパスワードを指定します。  
  
    -   マージ エージェントがサブスクライバーに接続するときのコンテキストを変更するには、 **[サブスクライバー接続]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[接続情報の入力]** ダイアログ ボックスでコンテキストを指定します。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>プル サブスクリプションに対するマージ エージェントのセキュリティ設定を変更するには  
  
1.  サブスクライバーの **[サブスクリプションのプロパティ - \<Subscription>]** ダイアログ ボックスでは、次の変更を加えることができます。  
  
    -   マージ エージェントを実行してサブスクライバーへ接続するアカウントを変更するには、 **[エージェント プロセス アカウント]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[マージ エージェント セキュリティ]** ダイアログ ボックスで、アカウントとパスワードを指定します。  
  
    -   マージ エージェントがパブリッシャーおよびディストリビューターに接続するときのコンテキストを変更するには、 **[パブリッシャー接続]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。 **[接続情報の入力]** ダイアログ ボックスでコンテキストを指定します。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-change-the-account-under-which-the-queue-reader-agent-runs"></a>キュー リーダー エージェントを実行するアカウントを変更するには  
  
1.  **[ディストリビューターのプロパティ -** Distributor>] **ダイアログ ボックスの \<[全般]** ページで、ディストリビューション データベースの横にあるプロパティ ボタン ( **[...]** ) をクリックします。  
  
2.  **[ディストリビューション データベースのプロパティ - \<Database>]** ダイアログ ボックスで、 **[エージェント プロセス アカウント]** テキスト ボックスの横にある **[セキュリティ設定]** ボタンをクリックします。  
  
3.  **[キュー リーダー エージェントのセキュリティ]** ダイアログ ボックスで、エージェントを実行してディストリビューターへ接続するアカウントを指定します。  
  
    -   **[プロセス アカウント]** テキスト ボックスに新しい Windows アカウントを入力します。  
  
    -   **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに、新しい複雑なパスワードを入力します。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  ディストリビューション データベースには、それぞれ 1 つのキュー リーダー エージェントがあります。 エージェントのセキュリティ設定を変更すると、このディストリビューション データベースを使用するすべてのパブリッシャーのすべてのパブリケーションの設定に影響が及びます。  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-publisher"></a>キュー リーダー エージェントがパブリッシャーに接続するときのコンテキストを変更するには  
  
1.  **[ディストリビューターのプロパティ -** Distributor>] **ダイアログ ボックスの \<[パブリッシャー]** ページで、パブリッシャーの横にあるプロパティ ボタン ( **...** ) をクリックします。  
  
2.  **[パブリッシャーへのエージェント接続]** セクションで、 **[エージェント接続モード]** オプションの **[エージェント プロセス アカウントを借用する]** または **[SQL Server 認証]** の値を指定します。 **[SQL Server 認証]** を指定する場合は、 **[ログイン]** および **[パスワード]** の値も入力します。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  ディストリビューション データベースには、それぞれ 1 つのキュー リーダー エージェントがあります。 エージェントのセキュリティ設定を変更すると、このディストリビューション データベースを使用するすべてのパブリッシャーのすべてのパブリケーションの設定に影響が及びます。  
  
#### <a name="to-change-the-context-under-which-the-queue-reader-agent-makes-connections-to-the-subscriber"></a>キュー リーダー エージェントがサブスクライバーに接続するときのコンテキストを変更するには  
  
-   キュー リーダー エージェントは、ディストリビューション エージェントと同じ接続コンテキストをサブスクリプションに使用します。 詳細については、ディストリビューション エージェントに関する上記の手順を参照してください。  
  
#### <a name="to-change-security-settings-for-an-immediate-updating-pull-subscription"></a>即時更新プル サブスクリプションのセキュリティ設定を変更するには  
  
1.  サブスクライバーの **[サブスクリプションのプロパティ - \<Subscription>]** ダイアログ ボックスで、 **[パブリッシャー接続]** 行をクリックしてから、その行のプロパティ ボタン ( **[...]** ) をクリックします。  
  
2.  **[接続情報の入力]** ダイアログ ボックスで、次のオプションのいずれかを選択します。  
  
    -   **[リンク サーバーまたはリモート サーバーからのログインを使用します]** 。 [sp_addserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql)、[sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、または他の方法を使用してサブスクライバ―とパブリッシャーの間にリモート サーバーまたはリンクされたサーバーを定義した場合は、このオプションを選択します。  
  
    -   **[次のログインとパスワードによる SQL Server 認証を使用する]** 。 サブスクライバーとパブリッシャーの間でリモート サーバーまたはリンク サーバーを定義していない場合は、このオプションを選択します。 レプリケーションによってリンク サーバーが作成されます。 指定するアカウントは、パブリッシャーに既に存在している必要があります。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  この手順により、サブスクライバーで変更が行われたときに、レプリケーション トリガーがサブスクライバーからパブリッシャーに接続するために使用する方法が変更されます。 ディストリビューション エージェントに関連付けられている設定を即時更新サブスクリプション用に変更することもできます。 詳細については、このトピックで既に説明した手順を参照してください。  
>   
>  この手順は、プル サブスクリプションにのみ当てはまります。 プッシュ サブスクリプションには、ストアド プロシージャ [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) を使用します。  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>パブリッシャーからディストリビューターへの管理接続に使用されているパスワードを変更するには  
  
1.  **[ディストリビューターのプロパティ -** Distributor>] **ダイアログ ボックスの \<[パブリッシャー]** ページで、 **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに複雑なパスワードを入力します。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  **[パブリッシャーのプロパティ -** Publisher>] **ダイアログ ボックスの \<[全般]** ページで、 **[パスワード]** テキスト ボックスと **[パスワードの確認入力]** テキスト ボックスに複雑なパスワードを入力します。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
> [!IMPORTANT]  
>  可能な限り、次のすべての手順で、実行時にセキュリティ資格情報を入力するように求めるメッセージをユーザーに表示します。 スクリプト ファイルに資格情報を格納する場合は、不正アクセスを防ぐために、そのファイルをセキュリティで保護する必要があります。  
  
#### <a name="to-change-all-instances-of-a-stored-password-at-a-replication-server"></a>レプリケーション サーバーに格納されたパスワードのインスタンスをすべて変更するには  
  
1.  レプリケーション トポロジ内のサーバーの master データベースで、 [sp_changereplicationserverpasswords](/sql/relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql)を実行します。 **\@ログイン**用にパスワードが変更されている [!INCLUDE[msCoName](../../../includes/msconame-md.md)] の Windows アカウントまたは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインを指定します。また、アカウントまたはログインの新しいパスワードを **\@パスワード**として指定します。 これにより、トポロジ内の他のサーバーに接続すると、サーバーのすべてのエージェントで使用されるパスワードの各インスタンスが変更されます。  
  
    > [!NOTE]  
    >  トポロジ内の特定のサーバー (ディストリビューターやサブスクライバーなど) への接続のログインとパスワードのみを変更するには、このサーバーの名前を **\@server**に指定します。  
  
2.  パスワードの更新が必要なレプリケーション トポロジ内の各サーバーで手順 1. を繰り返します。  
  
    > [!NOTE]  
    >  レプリケーション パスワードを変更したら、そのパスワードを使用する各エージェントを停止して再起動し、エージェントに対して変更を反映させる必要があります。  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent"></a>スナップショット エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャーで、 **\@パブリケーション**を指定して[sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql)を実行します。 これにより、スナップショット エージェントの現在のセキュリティ設定が返されます。  
  
2.  パブリッシャーで[sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql)を実行し、 **\@パブリケーション**と、次の1つまたは複数のセキュリティ設定を変更します。  
  
    -   エージェントを実行する Windows アカウント、またはこのアカウントのパスワードだけを変更するには、 **\@job_login**を指定し、 **job_password\@** します。  
  
    -   パブリッシャーに接続するときに使用するセキュリティモードを変更するには、 **\@publisher_security_mode**に**1**または**0**を指定します。  
  
    -   パブリッシャーへの接続時に使用されるセキュリティモードを**1**から**0**に変更する場合、またはこの接続に使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインを変更する場合は、 **\@publisher_login**を指定し、 **publisher_password を\@** します。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-change-security-settings-for-the-log-reader-agent"></a>ログ リーダー エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャーで、 **\@パブリッシャー**を指定して[sp_helplogreader_agent](/sql/relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql)を実行します。 これにより、ログ リーダー エージェントの現在のセキュリティ設定が返されます。  
  
2.  パブリッシャーで[sp_changelogreader_agent](/sql/relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql)を実行し、 **\@パブリケーション**と、次の1つまたは複数のセキュリティ設定を変更します。  
  
    -   エージェントを実行する Windows アカウント、またはこのアカウントのパスワードだけを変更するには、 **\@job_login**を指定し、 **job_password\@** します。  
  
    -   パブリッシャーに接続するときに使用するセキュリティモードを変更するには、 **\@publisher_security_mode**に**1**または**0**を指定します。  
  
    -   パブリッシャーへの接続時に使用されるセキュリティモードを**1**から**0**に変更する場合、またはこの接続に使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ログインを変更する場合は、 **\@publisher_login**を指定し、 **publisher_password を\@** します。  
  
    > [!NOTE]  
    >  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription"></a>プッシュ サブスクリプションに対するディストリビューション エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャー側のパブリケーションデータベースに対して[sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)を実行し、 **\@パブリケーション**と **\@サブスクライバー**を指定します。 これにより、ディストリビューターで実行されるディストリビューション エージェントのセキュリティ設定を含むサブスクリプションのプロパティが返されます。  
  
2.  パブリッシャー側のパブリケーションデータベースで、 **\@パブリケーション**、 **\@サブスクライバー**、 **\@subscriber_db**、 **\@アーティクル**の場合は**all** 、\@**プロパティ**の場合はセキュリティプロパティの名前、 **\@値**にはプロパティの新しい値を指定して、 [sp_changesubscription](/sql/relational-databases/system-stored-procedures/sp-changesubscription-transact-sql)を実行します。  
  
3.  次のセキュリティ プロパティから変更するものに対してそれぞれ手順 2. を繰り返します。  
  
    -   エージェントを実行する Windows アカウント、またはこのアカウントのパスワードだけを変更するには、 **\@プロパティ**に**distrib_job_password**の値を指定し **\@値**に新しいパスワードを指定します。 アカウント自体を変更する場合は、 **\@プロパティ**に**distrib_job_login**の値を指定し **\@値**に新しい Windows アカウントを指定して、手順 2. を繰り返します。  
  
    -   サブスクライバーへの接続時に使用されるセキュリティモードを変更するには、 **\@プロパティ**に**subscriber_security_mode**を、 **\@値**に**1** (Windows 統合認証) または**0** (SQL Server 認証) の値を指定します。  
  
    -   サブスクライバーのセキュリティモードを SQL Server 認証に変更する場合、または SQL Server 認証のログイン情報を変更する場合は、 **\@プロパティ**に**subscriber_password**の値を指定し、 **\@値**に新しいパスワードを指定します。 手順 2. を繰り返し、 **\@プロパティ**に**subscriber_login**の値を指定し **\@値**に新しいログインを指定します。  
  
    > [!NOTE]  
    >  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 **distrib_job_login** および **distrib_job_password**を含むすべてのプロパティに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription"></a>プル サブスクリプションに対するディストリビューション エージェントのセキュリティ設定を変更するには  
  
1.  サブスクライバーで、 **\@パブリケーション**を指定して[sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql)を実行します。 これにより、サブスクライバーで実行されるディストリビューション エージェントのセキュリティ設定を含むサブスクリプションのプロパティが返されます。  
  
2.  サブスクライバー側のサブスクリプションデータベースで[sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)を実行します。 **\@パブリッシャー**、 **\@publisher_db**、 **\@パブリケーション**、\@**プロパティ**のセキュリティプロパティの名前、 **\@value**のプロパティの新しい値を指定します。  
  
3.  次のセキュリティ プロパティから変更するものに対してそれぞれ手順 2. を繰り返します。  
  
    -   エージェントを実行する Windows アカウント、またはこのアカウントのパスワードだけを変更するには、 **\@プロパティ**に**distrib_job_password**の値を指定し **\@値**に新しいパスワードを指定します。 アカウント自体を変更する場合は、 **\@プロパティ**に**distrib_job_login**の値を指定し **\@値**に新しい Windows アカウントを指定して、手順 2. を繰り返します。  
  
    -   ディストリビューターへの接続時に使用されるセキュリティモードを変更するには、 **\@プロパティ**に**distributor_security_mode**を、 **\@値**に**1** (Windows 統合認証) または**0** (SQL Server 認証) の値を指定します。  
  
    -   ディストリビューターのセキュリティモードを SQL Server 認証に変更する場合、または SQL Server 認証のログイン情報を変更する場合は、 **\@プロパティ**に**distributor_password**を指定し **\@値**に新しいパスワードを指定します。 手順 2. を繰り返し、 **\@プロパティ**に**distributor_login**の値を指定し **\@値**に新しいログインを指定します。  
  
    > [!NOTE]  
    >  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription"></a>プッシュ サブスクリプションに対するマージ エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャー側のパブリケーションデータベースに対して[sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql)を実行し、 **\@パブリケーション**、 **\@サブスクライバー**、 **\@subscriber_db**を指定します。 これにより、ディストリビューターで実行されるマージ エージェントのセキュリティ設定を含むサブスクリプションのプロパティが返されます。  
  
2.  パブリッシャー側のパブリケーションデータベースで、 **\@パブリケーション**、 **\@サブスクライバー**、 **\@subscriber_db**、 **\@プロパティ**のセキュリティプロパティの名前、および **\@value**のプロパティの新しい値を指定して、 [sp_changemergesubscription](/sql/relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql)を実行します。  
  
3.  次のセキュリティ プロパティから変更するものに対してそれぞれ手順 2. を繰り返します。  
  
    -   エージェントを実行する Windows アカウント、またはこのアカウントのパスワードだけを変更するには、 **\@プロパティ**に**merge_job_password**の値を指定し **\@値**に新しいパスワードを指定します。 アカウント自体を変更する場合は、 **\@プロパティ**に**merge_job_login**の値を指定し **\@値**に新しい Windows アカウントを指定して、手順 2. を繰り返します。  
  
    -   サブスクライバーへの接続時に使用されるセキュリティモードを変更するには、 **\@プロパティ**に**subscriber_security_mode**を、 **\@値**に**1** (Windows 統合認証) または**0** (SQL Server 認証) の値を指定します。  
  
    -   サブスクライバーのセキュリティモードを SQL Server 認証に変更する場合、または SQL Server 認証のログイン情報を変更する場合は、 **\@プロパティ**に**subscriber_password**の値を指定し、 **\@値**に新しいパスワードを指定します。 手順 2. を繰り返し、 **\@プロパティ**に**subscriber_login**の値を指定し **\@値**に新しいログインを指定します。  
  
    -   パブリッシャーに接続するときに使用するセキュリティモードを変更するには、 **\@プロパティ**に**publisher_security_mode**を、 **\@値**に**1** (Windows 統合認証) または**0** (SQL Server 認証) の値を指定します。  
  
    -   パブリッシャーのセキュリティモードを SQL Server 認証に変更する場合、または SQL Server 認証のログイン情報を変更する場合は、 **\@プロパティ**に**publisher_password**の値を指定し、 **\@値**に新しいパスワードを指定します。 手順 2. を繰り返し、 **\@プロパティ**に**publisher_login**の値を指定し **\@値**に新しいログインを指定します。  
  
    > [!NOTE]  
    >  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用してパブリッシャーを構成する場合、 **merge_job_login** および **merge_job_password**を含むすべてのプロパティに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription"></a>プル サブスクリプションに対するマージ エージェントのセキュリティ設定を変更するには  
  
1.  サブスクライバーで、 **\@パブリケーション**を指定して[sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql)を実行します。 これにより、サブスクライバーで実行されるマージ エージェントのセキュリティ設定を含むサブスクリプションのプロパティが返されます。  
  
2.  サブスクライバー側のサブスクリプションデータベースで[sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)を実行します。 **\@パブリッシャー**、 **\@publisher_db**、 **\@パブリケーション**、\@**プロパティ**のセキュリティプロパティの名前、 **\@value**のプロパティの新しい値を指定します。  
  
3.  次のセキュリティ プロパティから変更するものに対してそれぞれ手順 2. を繰り返します。  
  
    -   エージェントを実行する Windows アカウント、またはこのアカウントのパスワードだけを変更するには、 **\@プロパティ**に**merge_job_password**の値を指定し **\@値**に新しいパスワードを指定します。 アカウント自体を変更する場合は、 **\@プロパティ**に**merge_job_login**の値を指定し **\@値**に新しい Windows アカウントを指定して、手順 2. を繰り返します。  
  
    -   ディストリビューターへの接続時に使用されるセキュリティモードを変更するには、 **\@プロパティ**に**distributor_security_mode**を、 **\@値**に**1** (Windows 統合認証) または**0** (SQL Server 認証) の値を指定します。  
  
    -   ディストリビューターのセキュリティモードを SQL Server 認証に変更する場合、または SQL Server 認証のログイン情報を変更する場合は、 **\@プロパティ**に**distributor_password**を指定し **\@値**に新しいパスワードを指定します。 手順 2. を繰り返し、 **\@プロパティ**に**distributor_login**の値を指定し **\@値**に新しいログインを指定します。  
  
    -   パブリッシャーに接続するときに使用するセキュリティモードを変更するには、 **\@プロパティ**に**publisher_security_mode**を、 **\@値**に**1** (Windows 統合認証) または**0** (SQL Server 認証) の値を指定します。  
  
    -   パブリッシャーのセキュリティモードを SQL Server 認証に変更する場合、または SQL Server 認証のログイン情報を変更する場合は、 **\@プロパティ**に**publisher_password**を指定し **\@値**に新しいパスワードを指定します。 手順 2. を繰り返し、 **\@プロパティ**に**publisher_login**の値を指定し **\@値**に新しいログインを指定します。  
  
    > [!NOTE]  
    >  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
#### <a name="to-change-security-settings-for-the-snapshot-agent-to-generate-a-filtered-snapshot-for-a-subscriber"></a>サブスクライバーのフィルター選択されたスナップショットを生成する、スナップショット エージェントのセキュリティ設定を変更するには  
  
1.  パブリッシャーで、 **\@パブリケーション**を指定して[sp_helpdynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql)を実行します。 結果セットで、変更するサブスクライバーのパーティションの **job_name** の値を確認します。  
  
2.  パブリッシャーで、 [sp_changedynamicsnapshot_job](/sql/relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql)を実行します。 **\@の発行**、手順 1. で取得した **\@dynamic_snapshot_jobname**の値、および **\@job_password**に対してエージェントを実行する Windows アカウントのログインとパスワードの新しいパスワードを**指定します**。\@\@  
  
    > [!IMPORTANT]  
    >  リモート ディストリビューターを使用するパブリッシャーを構成する場合は、 *job_login* および *job_password*を含むすべてのパラメーターに指定された値がディストリビューターにプレーン テキストとして送信されます。 このストアド プロシージャを実行する前に、パブリッシャーとリモート ディストリビューターの間の接続を暗号化する必要があります。 詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
#### <a name="to-change-security-settings-for-the-queue-reader-agent"></a>キュー リーダー エージェントのセキュリティ設定を変更するには  
  
1.  ディストリビューターで、 [sp_helpqreader_agent](/sql/relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql)を実行します。 これにより、キュー リーダー エージェントの実行時に使用される現在の Windows アカウントが返されます。  
  
    -   ディストリビューターで[sp_changeqreader_agent](/sql/relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql)を実行し、 **\@job_login**および **\@job_passwsord**の Windows アカウント設定を指定します。  
  
    > [!NOTE]  
    >  エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。 ディストリビューション データベースには、それぞれ 1 つのキュー リーダー エージェントがあります。 エージェントのセキュリティ設定を変更すると、このディストリビューション データベースを使用するすべてのパブリッシャーのすべてのパブリケーションの設定に影響が及びます。  
  
2.  キュー リーダー エージェントは、サブスクリプションのディストリビューション エージェントと同じ接続コンテキストを使用して、サブスクライバーへの接続を作成します。  
  
#### <a name="to-change-security-mode-used-by-an-immediate-updating-subscriber-when-connecting-to-the-publisher"></a>パブリッシャーへの接続時に即時更新サブスクライバーで使用するセキュリティ モードを変更するには  
  
1.  サブスクライバー側のサブスクリプション データベースに対して、 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)を実行します。 **\@パブリッシャー**、 **\@パブリケーション**、 **\@publisher_db**のパブリケーションデータベースの名前、 **\@** security_mode に次のいずれかの値を指定します。  
  
    -   **0** - パブリッシャーで更新を作成する場合に SQL Server  認証を使用します。 このオプションを選択するには、 **\@ログイン**と **\@パスワード**に対して、パブリッシャーで有効なログインを指定する必要があります。  
  
    -   **1** - パブリッシャーへの接続時にサブスクライバーで変更するユーザーのセキュリティ コンテキストを使用します。 このセキュリティ モードに関連する制限の詳細については、 [sp_link_publication](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql) のトピックを参照してください。  
  
    -   **2** - [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql) を使って作成された既存のユーザー定義リンク サーバー ログインを使用します。  
  
#### <a name="to-change-the-password-for-a-remote-distributor"></a>リモート ディストリビューターのパスワードを変更するには  
  
1.  ディストリビューター側のディストリビューションデータベースで[sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql)を実行し、 **\@パスワード**のこのログインの新しいパスワードを指定します。  
  
    > [!IMPORTANT]  
    >  **distributor_admin** のパスワードを直接変更しないでください。  
  
2.  このリモートディストリビューターを使用するすべてのパブリッシャーで[sp_changedistributor_password](/sql/relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql)を実行し、 **\@パスワード**の手順 1. のパスワードを指定します。  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
  
> [!IMPORTANT]  
>  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、 [Windows .NET&nbsp;Framework に用意されている](https://go.microsoft.com/fwlink/?LinkId=34733) 暗号化サービス [!INCLUDE[msCoName](../../../includes/msconame-md.md)] を使用します。  
  
#### <a name="to-change-all-instances-of-a-password-stored-on-a-replication-server"></a>レプリケーション サーバーに格納されているパスワードのインスタンスをすべて変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、レプリケーション サーバーに対する接続を作成します。  
  
2.  手順 1. で作成した接続を使用して、 <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> メソッドを呼び出します。 次のパラメーターを指定します。  
  
    -   *security_mode* - <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> 値。パスワードのすべてのインスタンスを変更するために使用する認証の種類を指定します。  
  
    -   *login* - パスワードのすべてのインスタンスを変更するために使用するログイン。  
  
    -   *password* - 新しいパスワード値。  
  
        > [!IMPORTANT]  
        >  可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 資格情報を保存する必要がある場合は、Windows .NET Framework に用意されている [暗号化サービス](https://go.microsoft.com/fwlink/?LinkId=34733) を使用します。  
  
        > [!NOTE]  
        >  固定サーバー ロール `sysadmin` のメンバー以外、このメソッドを呼び出すことはできません。  
  
4.  パスワードを更新する必要のある、レプリケーション トポロジ内のすべてのサーバーについて、手順 1. から手順 3. を繰り返します。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-push-subscription-to-a-transactional-publication"></a>ディストリビューション エージェントのセキュリティ設定をプッシュ サブスクリプション用からトランザクション パブリケーション用に変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成します。  
  
3.  サブスクリプションの <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> の各プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに対し、手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.TransSubscription>のインスタンスに対し、次のいずれかまたは複数のセキュリティ プロパティを設定します。  
  
    -   エージェントの実行に使用する Windows アカウントの資格情報を変更するには、 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>フィールドを設定します。  
  
    -   エージェントがサブスクライバーとの接続に使用する認証の種類に Windows 統合認証を指定するには、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> プロパティの <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> フィールドを `true` に設定します。  
  
    -   エージェントがサブスクライバーに接続するときに使用する認証の種類として SQL Server 認証を指定するには、<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> プロパティの <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> フィールドを `false`に設定し、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> および <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> のフィールドに対してサブスクライバーのログイン資格情報を指定します。  
  
        > [!NOTE]  
        >  ディストリビューターに対するエージェント接続は、常に、 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>によって指定された Windows 資格情報を使用して確立されます。 このアカウントは、Windows 認証を使ってリモート接続を確立する際にも使用されます。  
  
6.  (省略可) `true` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 `false` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
#### <a name="to-change-security-settings-for-the-distribution-agent-for-a-pull-subscription-to-a-transactional-publication"></a>ディストリビューション エージェントのセキュリティ設定をプル サブスクリプション用からトランザクション パブリケーション用に変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成します。  
  
3.  サブスクリプションの <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> の各プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに対し、手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.TransPullSubscription>のインスタンスに対し、次のいずれかまたは複数のセキュリティ プロパティを設定します。  
  
    -   エージェントの実行に使用する Windows アカウントの資格情報を変更するには、 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>フィールドを設定します。  
  
    -   エージェントがディストリビューターとの接続に使用する認証の種類に Windows 統合認証を指定するには、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> プロパティの <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> フィールドを `true` に設定します。  
  
    -   エージェントがディストリビューターに接続するときに使用する認証の種類として SQL Server 認証を指定するには、<xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> プロパティの <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> フィールドを `false`に設定し、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> フィールドと <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドに対してディストリビューターのログイン資格情報を指定します。  
  
        > [!NOTE]  
        >  サブスクライバーに対するエージェント接続は、常に、 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>によって指定された Windows 資格情報を使用して確立されます。 このアカウントは、Windows 認証を使ってリモート接続を確立する際にも使用されます。  
  
6.  (省略可) `true` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 `false` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-pull-subscription-to-a-merge-publication"></a>マージ エージェントのセキュリティ設定をプル サブスクリプション用からマージ パブリケーション用に変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成します。  
  
3.  サブスクリプションの <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> の各プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに対し、手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.MergePullSubscription>のインスタンスに対し、次のいずれかまたは複数のセキュリティ プロパティを設定します。  
  
    -   エージェントの実行に使用する Windows アカウントの資格情報を変更するには、 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>フィールドを設定します。  
  
    -   エージェントがディストリビューターとの接続に使用する認証の種類に Windows 統合認証を指定するには、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> プロパティの <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> フィールドを `true` に設定します。  
  
    -   エージェントがディストリビューターに接続するときに使用する認証の種類として SQL Server 認証を指定するには、<xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> プロパティの <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> フィールドを `false`に設定し、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> フィールドと <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドに対してディストリビューターのログイン資格情報を指定します。  
  
    -   エージェントがパブリッシャーとの接続に使用する認証の種類に Windows 統合認証を指定するには、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> プロパティの <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> フィールドを `true` に設定します。  
  
    -   エージェントがパブリッシャーに接続するときに使用する認証の種類として SQL Server 認証を指定するには、<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> プロパティの <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> フィールドを `false`に設定し、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> フィールドと <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> フィールドに対して、パブリッシャーのログイン資格情報を指定します。  
  
        > [!NOTE]  
        >  サブスクライバーに対するエージェント接続は、常に、 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>によって指定された Windows 資格情報を使用して確立されます。 このアカウントは、Windows 認証を使ってリモート接続を確立する際にも使用されます。  
  
6.  (省略可) `true` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 `false` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
#### <a name="to-change-security-settings-for-the-merge-agent-for-a-push-subscription-to-a-merge-publication"></a>マージ エージェントのセキュリティ設定をプッシュ サブスクリプション用からマージ パブリケーション用に変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成します。  
  
3.  サブスクリプションの <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> の各プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに対し、手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 3. で指定したサブスクリプションのプロパティが正しく定義されていないか、サブスクリプションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.MergeSubscription>のインスタンスに対し、次のいずれかまたは複数のセキュリティ プロパティを設定します。  
  
    -   エージェントの実行に使用する Windows アカウントの資格情報を変更するには、 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> の <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> フィールドおよび <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>フィールドを設定します。  
  
    -   エージェントがサブスクライバーとの接続に使用する認証の種類に Windows 統合認証を指定するには、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> プロパティの <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> フィールドを `true` に設定します。  
  
    -   エージェントがサブスクライバーに接続するときに使用する認証の種類として SQL Server 認証を指定するには、<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> プロパティの <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> フィールドを `false`に設定し、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> および <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> のフィールドに対してサブスクライバーのログイン資格情報を指定します。  
  
    -   エージェントがパブリッシャーとの接続に使用する認証の種類に Windows 統合認証を指定するには、<xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> プロパティの <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> フィールドを `true` に設定します。  
  
    -   エージェントがパブリッシャーに接続するときに使用する認証の種類として SQL Server 認証を指定するには、<xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> プロパティの <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> フィールドを `false`に設定し、<xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> フィールドと <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> フィールドに対して、パブリッシャーのログイン資格情報を指定します。  
  
        > [!NOTE]  
        >  ディストリビューターに対するエージェント接続は、常に、 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>によって指定された Windows 資格情報を使用して確立されます。 このアカウントは、Windows 認証を使ってリモート接続を確立する際にも使用されます。  
  
6.  (省略可) `true` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> を指定した場合、<xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> メソッドを呼び出してサーバーに変更をコミットします。 `false` に <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (既定値) を指定した場合、変更は直ちにサーバーに送られます。  
  
#### <a name="to-change-the-login-information-used-by-an-immediate-updating-subscriber-when-it-connects-to-the-transactional-publisher"></a>即時更新サブスクライバーがトランザクション パブリッシャーへの接続時に使用するログイン情報を変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、サブスクライバーへの接続を作成します。  
  
2.  サブスクリプション データベースの <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> クラスのインスタンスを作成します。 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> を指定し、 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> に手順 1. の <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>を指定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドから `false` が返された場合、手順 2. で指定したデータベースのプロパティが正しく定義されていないか、サブスクリプション データベースが存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> メソッドに次のパラメーターを指定して呼び出します。  
  
    -   *Publisher* - パブリッシャーの名前。  
  
    -   *PublisherDB* - パブリケーション データベースの名前。  
  
    -   *Publication* - 即時更新サブスクライバーでサブスクライブしているパブリケーションの名前。  
  
    -   *Distributor* - ディストリビューターの名前。  
  
    -   *PublisherSecurity* - A <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> オブジェクト。即時更新サブスクライバーがパブリッシャーに接続するときのセキュリティ モードと、その接続に必要なログイン資格情報を指定します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、指定されたログイン値をチェックし、該当する Windows ログイン、または、サーバー上のレプリケーションによって格納された SQL Server ログインを対象にすべてのパスワードを変更します。  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> フォロー アップ: レプリケーションのセキュリティ設定を変更した後  
 エージェントのログインまたはパスワードを変更した後、変更を有効にするには、エージェントを停止して再起動する必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理オブジェクトの概念](../concepts/replication-management-objects-concepts.md)   
 [レプリケーション スクリプトのアップグレード &#40;レプリケーション Transact-SQL プログラミング&#41;](../administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [レプリケーションのログインとパスワードの管理](identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [レプリケーション エージェントのセキュリティ モデル](replication-agent-security-model.md)   
 [レプリケーション セキュリティの推奨事項](replication-security-best-practices.md)   
 [SQL Server レプリケーションセキュリティ](view-and-modify-replication-security-settings.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
