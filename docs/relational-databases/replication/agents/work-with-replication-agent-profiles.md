---
title: レプリケーション エージェント プロファイルを操作する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- agents [SQL Server replication], profiles
- profiles [SQL Server], replication agents
ms.assetid: 9c290a88-4e9f-4a7e-aab5-4442137a9918
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 93ee480a595178627f65613b502c10e44dffc8e3
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907805"
---
# <a name="work-with-replication-agent-profiles"></a>レプリケーション エージェント プロファイルを操作する
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、レプリケーション エージェント プロファイルを操作する方法について説明します。 各レプリケーション エージェントの動作は、エージェント プロファイルで設定できる一連のパラメーターによって制御されます。 各エージェントには既定のプロファイルがあり、その一部には事前に定義された追加のプロファイルがあります。1 つのエージェントに対しては、1 つのプロファイルのみがアクティブになります。  
  
 **このトピックの内容**  
  
-   **レプリケーション エージェント プロファイルを操作するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
    -   [エージェント プロファイル] ダイアログ ボックスへのアクセス  
  
    -   エージェントのプロファイルの指定  
  
    -   プロファイルの作成  
  
    -   プロファイルの変更  
  
    -   プロファイルの削除  
  
     [Transact-SQL](#TsqlProcedure)  
  
    -   プロファイルの作成  
  
    -   プロファイルの変更  
  
    -   プロファイルの削除  
  
    -   同期時のエージェント プロファイルの使用  
  
    -   Transact-SQL の例  
  
     [レプリケーション管理オブジェクト (Replication Management Objects)](#RMOProcedure)  
  
    -   プロファイルの作成  
  
    -   プロファイルの変更  
  
    -   プロファイルの削除  
  
-   **補足情報:** [エージェント パラメーターを変更した後](#FollowUp)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
###  <a name="Access_SSMS"></a> SQL Server Management Studio から [エージェント プロファイル] ダイアログ ボックスにアクセスするには  
  
1.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[全般]** ページで、 **[プロファイルの既定値]** をクリックします。  

#### <a name="to-access-the-agent-profiles-dialog-box-from-replication-monitor"></a>レプリケーション モニターから [エージェント プロファイル] ダイアログ ボックスにアクセスするには  
  
-   すべてのエージェントに対するダイアログ ボックスを開くには、パブリッシャーを右クリックし、 **[エージェント プロファイル]** をクリックします。  
  
-   単一のエージェントに対するダイアログ ボックスを開くには  
  
    1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
    2.  ディストリビューション エージェントとマージ エージェントのプロファイルの場合は、 **[すべてのサブスクリプション]** タブでサブスクリプションを右クリックし、 **[エージェント プロファイル]** をクリックします。 その他のエージェントの場合は、 **[エージェント]** タブでエージェントを右クリックし、 **[エージェント プロファイル]** をクリックします。  
  
###  <a name="Specify_SSMS"></a> エージェントのプロファイルを指定するには  
  
1.  **[エージェント プロファイル]** ダイアログ ボックスにエージェントのプロファイルが複数表示されている場合は、エージェントを 1 つ選択します。  
  
2.  **[エージェント プロファイル]** グリッドの **[新規の既定]** 列でプロファイルを選択します。 既定では、プロファイルは、新しいパブリケーションとサブスクリプションに対するエージェントにのみ適用されます。  
  
3.  既存のパブリケーションまたはサブスクリプションに対して選択された種類のすべてのエージェントがこのプロファイルを使用するように指定するには、 **[既存のエージェントの変更]** をクリックします。  
  
###  <a name="Modify_SSMS"></a> プロファイルに関連付けられたパラメーターを表示および編集するには  
  
1.  **[エージェント プロファイル]** ダイアログ ボックスにエージェントのプロファイルが複数表示されている場合は、エージェントを 1 つ選択します。  
  
2.  プロファイルの横にあるプロパティ ボタン **[...]** をクリックします。  
  
3.  **[\<ProfileName> プロファイル プロパティ]** ダイアログ ボックスにパラメーターと値が表示されます。  
  
    -   ユーザー定義プロファイルのパラメーターは編集できます。事前に定義されているシステム プロファイルのパラメーターは編集できません。  
  
    -   1 つのエージェントに対するすべてのパラメーターを表示するには、 **[このプロファイルに使用されているパラメーターのみ表示する]** チェック ボックスをオフにします。 エージェント パラメーターの詳細については、このトピックの末尾のリンクを参照してください。  
  
4.  **[閉じる]** をクリックします。  
  
###  <a name="Create_SSMS"></a> ユーザー定義プロファイルを作成するには  
  
1.  **[エージェント プロファイル]** ダイアログ ボックスにエージェントのプロファイルが複数表示されている場合は、エージェントを 1 つ選択します。  
  
2.  **[新規作成]** をクリックします。  
  
3.  **[新しいエージェント プロファイル]** 初期化ダイアログ ボックスで、新しいプロファイルの基となる既存のプロファイルを選択します。  
  
4.  **[新しいエージェント プロファイル]** ダイアログ ボックスで、 **[名前]** と **[説明]** ボックスに値を入力します。  
  
5.  パラメーターを変更してプロファイルを調整します。 1 つのエージェントに対するすべてのパラメーターを表示するには、 **[このプロファイルに使用されているパラメーターのみ表示する]** チェック ボックスをオフにします。 エージェント パラメーターの詳細については、このトピックの末尾のリンクを参照してください。  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
###  <a name="Delete_SSMS"></a> ユーザー定義プロファイルを削除するには  
  
1.  **[エージェント プロファイル]** ダイアログ ボックスにエージェントのプロファイルが複数表示されている場合は、エージェントを 1 つ選択します。  
  
2.  1 つのプロファイルが 1 つ以上のエージェントに関連付けられている場合は、これらのエージェントに対するプロファイルを変更します。  
  
    1.  **[エージェント プロファイル]** グリッドで別のプロファイルを選択します。  
  
    2.  **[既存のエージェントの変更]** をクリックします。  
  
        > [!NOTE]  
        >  これによって、削除したいプロファイルを使用しているエージェントだけではなく、既存のパブリケーションまたはサブスクリプションに対して選択された種類のすべてのエージェントに対するプロファイルが変更されます。  
  
3.  削除するプロファイルを選択し、 **[削除]** をクリックします。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
###  <a name="Create_tsql"></a> 新しいエージェント プロファイルを作成するには  
  
1.  ディストリビューターで、[sp_add_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md) を実行します。 **\@name** を指定し、 **\@profile_type** に **1** を、 **\@agent_type** に次のいずれかの値を指定します。  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     このプロファイルがこの種類のレプリケーション エージェントの新しい既定のプロファイルになる場合、 **\@default** に **1** を指定します。 新しいプロファイルの ID は、 **\@profile_id** 出力パラメーターにより返されます。 これにより、特定の種類のエージェントの既定のプロファイルに基づいたプロファイル パラメーターのセットを備えた、新しいプロファイルが作成されます。  
  
2.  新しいプロファイルを作成したら、既定のパラメーターを追加、削除、変更してプロファイルをカスタマイズします。  
  
###  <a name="Modify_tsql"></a> 既存のエージェント プロファイルを変更するには  
  
1.  ディストリビューターで、[sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md) を実行します。 次のいずれかの値を **\@agent_type** に指定します。  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     これにより、指定された種類のエージェントのプロファイルがすべて返されます。 変更するプロファイルの結果セットで **profile_id** の値を確認します。  
  
2.  ディストリビューターで、[sp_help_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md) を実行します。 手順 1 で確認したプロファイル ID を **\@profile_id** に指定します。 これにより、プロファイルのすべてのパラメーターが返されます。 変更するパラメーター、またはプロファイルから削除するパラメーターの名前を確認します。  
  
3.  プロファイル内のパラメーターの値を変更するには、[sp_change_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-change-agent-parameter-transact-sql.md) を実行します。 手順 1 で確認したプロファイル ID を **\@profile_id** に指定し、変更するパラメーターの名前を **\@parameter_name** に、パラメーターの新しい値を **\@parameter_value** に指定します。  
  
    > [!NOTE]  
    >  既存のエージェント プロファイルを変更して、エージェントの既定のプロファイルにすることはできません。 代わりに、前の手順に示すように、新しいプロファイルを既定のプロファイルとして作成する必要があります。  
  
4.  プロファイルからパラメーターを削除するには、[sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md) を実行します。 手順 1 で確認したプロファイル ID を **\@profile_id** に指定し、削除するパラメーターの名前を **\@parameter_name** に指定します。  
  
5.  プロファイルに新しいパラメーターを追加するには、次の手順を実行する必要があります。  
  
    -   ディストリビューターで [MSagentparameterlist &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/msagentparameterlist-transact-sql.md) テーブルに対してクエリを実行して、各種類のエージェントに設定できるプロファイル パラメーターを確認します。  
  
    -   ディストリビューターで、[sp_add_agent_parameter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md) を実行します。 手順 1 で確認したプロファイル ID を **\@profile_id** に指定し、追加する有効なパラメーターの名前を **\@parameter_name** に、パラメーターの値を **\@parameter_value** に指定します。  
  
###  <a name="Delete_tsql"></a> エージェント プロファイルを削除するには  
  
1.  ディストリビューターで、[sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md) を実行します。 次のいずれかの値を **\@agent_type** に指定します。  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     これにより、指定された種類のエージェントのプロファイルがすべて返されます。 削除するプロファイルの結果セットで **profile_id** の値を確認します。  
  
2.  ディストリビューターで、[sp_drop_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md) を実行します。 手順 1 で確認したプロファイル ID を **\@profile_id** に指定します。  
  
###  <a name="Synch_tsql"></a> 同期の際にエージェント プロファイルを使用するには  
  
1.  ディストリビューターで、[sp_help_agent_profile &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md) を実行します。 次のいずれかの値を **\@agent_type** に指定します。  
  
    -   **\@profile_type** - [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
    -   **2** - [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
    -   **3** - [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)  
  
    -   **4** - [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)  
  
    -   **9** - [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
     これにより、指定された種類のエージェントのプロファイルがすべて返されます。 使用するプロファイルの結果セットで **profile_name** の値を確認します。  
  
2.  エージェントがエージェント ジョブから起動される場合、エージェントを起動するジョブ ステップを編集して、手順 1. で得た **profile_name** の値を **-ProfileName** コマンド ライン パラメーターの後に指定します。 詳細については、「[View and Modify Replication Agent Command Prompt Parameters &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)」(レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;) を参照してください。  
  
3.  コマンド プロンプトからエージェントを起動する場合、手順 1. で得た **profile_name** の値を **-ProfileName** コマンド ライン パラメーターの後に指定します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、 **custom_merge**という名前のマージ エージェント用のカスタム プロファイルを作成して、 **-UploadReadChangesPerBatch** パラメーターの値を変更し、 **-ExchangeType** パラメーターを新しく追加して、作成されたプロファイルに関する情報を返します。  
  
 [!code-sql[HowTo#sp_addagentprofileparam](../../../relational-databases/replication/codesnippet/tsql/work-with-replication-ag_1.sql)]  
  
##  <a name="RMOProcedure"></a> RMO の使用  
  
###  <a name="Create_RMO"></a> 新しいエージェント プロファイルを作成するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスのインスタンスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.AgentProfile> クラスのインスタンスを作成します。  
  
3.  オブジェクトの次のプロパティを設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> - プロファイルの名前。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AgentType%2A> - プロファイルを作成するレプリケーション エージェントの種類を指定する <xref:Microsoft.SqlServer.Replication.AgentType> 値。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 手順 1. で作成した <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 。  
  
    -   (省略可) <xref:Microsoft.SqlServer.Replication.AgentProfile.Description%2A> - プロファイルの説明。  
  
    -   (省略可) <xref:Microsoft.SqlServer.Replication.AgentProfile.Default%2A> - この **T:Microsoft.SqlServer.Replication.AgentType** の新しいエージェント ジョブすべてが、既定でこのプロファイルを使用する場合、このプロパティを <xref:Microsoft.SqlServer.Replication.AgentType> に設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.AgentProfile.Create%2A> メソッドを呼び出し、サーバーにプロファイルを作成します。  
  
5.  サーバーにプロファイルが作成されたら、レプリケーション エージェントのパラメーター値を追加、削除、変更することで、プロファイルをカスタマイズできます。  
  
6.  既存のレプリケーション エージェント ジョブにプロファイルを割り当てるには、 <xref:Microsoft.SqlServer.Replication.AgentProfile.AssignToAgent%2A> メソッドを呼び出します。 ディストリビューション データベースの名前を *distributionDBName* に渡し、ジョブの ID を *agentID*に渡します。  
  
###  <a name="Modify_RMO"></a> 既存のエージェント プロファイルを変更するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスのインスタンスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> クラスのインスタンスを作成します。 手順 1. で作成した <xref:Microsoft.SqlServer.Management.Common.ServerConnection> オブジェクトを渡します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが **false**を返す場合、ディストリビューターが存在するかどうかを確認してください。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumAgentProfiles%2A> メソッドを呼び出します。 特定の種類のレプリケーション エージェントのプロファイルが返されるように、 <xref:Microsoft.SqlServer.Replication.AgentType> 値を渡します。  
  
5.  返された <xref:Microsoft.SqlServer.Replication.AgentProfile> から目的の <xref:System.Collections.ArrayList>オブジェクトを取得します。オブジェクトの <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> プロパティはプロファイル名と同じです。  
  
6.  <xref:Microsoft.SqlServer.Replication.AgentProfile> の次のメソッドの 1 つを呼び出して、プロファイルを変更します。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.AddParameter%2A> - サポートされるパラメーターをプロファイルに追加します。ここで、 *name* はレプリケーション エージェント パラメーターの名前、 *value* は指定する値です。 指定されたエージェントの種類でサポートされるエージェント パラメーターをすべて列挙するには、 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> メソッドを呼び出します。 このメソッドは、サポートされるすべてのパラメーターを表す <xref:System.Collections.ArrayList> オブジェクトの <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> を返します。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.RemoveParameter%2A> - プロファイルから既存のパラメーターを削除します。ここで、 *name* はレプリケーション エージェント パラメーターの名前です。 プロファイルに定義されている現在のエージェント パラメーターをすべて列挙するには、 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> メソッドを呼び出します。 このメソッドは、このプロファイルの既存のパラメーターを表す <xref:System.Collections.ArrayList> オブジェクトの <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> を返します。  
  
    -   <xref:Microsoft.SqlServer.Replication.AgentProfile.ChangeParameter%2A> - プロファイルの既存のパラメーターの設定を変更します。ここで、 *name* はエージェント パラメーターの名前、 *newValue* はパラメーターの変更後の値です。 プロファイルに定義されている現在のエージェント パラメーターをすべて列挙するには、 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameters%2A> メソッドを呼び出します。 このメソッドは、このプロファイルの既存のパラメーターを表す <xref:System.Collections.ArrayList> オブジェクトの <xref:Microsoft.SqlServer.Replication.AgentProfileParameter> を返します。 サポートされるエージェント パラメーターの設定をすべて列挙するには、 <xref:Microsoft.SqlServer.Replication.AgentProfile.EnumParameterInfo%2A> メソッドを呼び出します。 このメソッドは、すべてのパラメーターでサポートされる値を表す <xref:System.Collections.ArrayList> オブジェクトの <xref:Microsoft.SqlServer.Replication.AgentProfileParameterInfo> を返します。  
  
###  <a name="Delete_RMO"></a> エージェント プロファイルを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスのインスタンスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.AgentProfile> クラスのインスタンスを作成します。 プロファイルの名前を <xref:Microsoft.SqlServer.Replication.AgentProfile.Name%2A> に設定し、手順 1. の <xref:Microsoft.SqlServer.Management.Common.ServerConnection> を <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>に設定します。  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出します。 このメソッドが **false**を返す場合、指定された名前が誤っているか、プロファイルがサーバーに存在していません。  
  
4.  <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A> プロパティが <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.User>に設定されていることを確認します。これは、顧客のプロファイルを表します。 <xref:Microsoft.SqlServer.Replication.AgentProfileTypeOption.System> の値が <xref:Microsoft.SqlServer.Replication.AgentProfile.Type%2A>であるプロファイルは削除しないでください。  
  
5.  <xref:Microsoft.SqlServer.Replication.AgentProfile.Remove%2A> メソッドを呼び出して、このオブジェクトで表されるユーザー定義プロファイルをサーバーから削除します。  
  
##  <a name="FollowUp"></a> 補足情報:エージェント パラメーターを変更した後  
エージェント パラメーターの変更は、エージェントの次回起動時に反映されます。 エージェントを継続して実行している場合は、そのエージェントを停止して再起動する必要があります。 SQL Server 2017 CU3 以降では、エージェントを再起動しなくても、一部のエージェント パラメーターの変更が有効になります。 
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェント プロファイル](../../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)   
 [Replication Log Reader Agent](../../../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)   
 [Replication Queue Reader Agent](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)  
  
  
