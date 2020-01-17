---
title: 同期スケジュールの指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], synchronizing
- scheduling synchronization [SQL Server replication]
- synchronization [SQL Server replication], schedules
- replication [SQL Server], synchronization
ms.assetid: 97f2535b-ec19-4973-823d-bcf3d5aa0216
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9bfbb62c58efea29df26cb9fc6e632bc4e2b3642
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62630804"
---
# <a name="specify-synchronization-schedules"></a>同期スケジュールの指定
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用して、同期スケジュールを指定する方法について説明します。 サブスクリプションを作成するときに、サブスクリプションのレプリケーション エージェントをいつ実行するかを制御する同期スケジュールを定義できます。 スケジュール設定のパラメーターを指定しなかった場合、サブスクリプションは既定のスケジュールを使用します。  
  
 サブスクリプションは、ディストリビューション エージェント (スナップショット レプリケーションおよびトランザクション レプリケーションの場合) またはマージ エージェント (マージ レプリケーションの場合) で同期されます。 エージェントは継続的に実行、要求時に実行、またはスケジュールで実行できます。  
  
 **このトピックの内容**  
  
-   **同期スケジュールを指定するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
 サブスクリプションの新規作成ウィザードの **[同期スケジュール]** ページで同期スケジュールを指定します。 このウィザードへのアクセスの詳細については、「 [Create a Push Subscription](create-a-push-subscription.md) 」および「 [Create a Pull Subscription](create-a-pull-subscription.md)」を参照してください。  
  
 **[ジョブ スケジュールのプロパティ]** ダイアログ ボックスで同期スケジュールを変更します。このダイアログ ボックスは、 **の** [ジョブ] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] フォルダーおよびレプリケーション モニターのエージェントの詳細ウィンドウから使用できます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
 **[ジョブ]** フォルダーからスケジュールを指定する場合は、次の表でエージェントのジョブ名を確認してください。  
  
|エージェント|ジョブ名|  
|-----------|--------------|  
|プル サブスクリプションに対するマージ エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<SubscriptionDatabase>-\<整数>**|  
|プッシュ サブスクリプションに対するマージ エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|  
|プッシュ サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>** <sup>1</sup>|  
|プル サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<サブスクライバー>-\<サブスクリプション データベース>-\<GUID>** <sup>2</sup>|  
|SQL Server 以外のサブスクライバーへのプッシュ サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|  
  
 <sup>1</sup> Oracle パブリケーションに対するプッシュ サブスクリプションの場合は、" **\<パブリッシャー>-\<パブリケーション データベース>** " ではなく " **\<パブリッシャー>-\<パブリッシャー>** " になります  
  
 <sup>2</sup> Oracle パブリケーションに対するプル サブスクリプションの場合は、" **\<パブリッシャー>-\<パブリケーション データベース>** " ではなく " **\<パブリッシャー>-\<ディストリビューション データベース>** " になります  
  
#### <a name="to-specify-synchronization-schedules"></a>同期スケジュールを指定するには  
  
1.  サブスクリプションの新規作成ウィザードの **[同期スケジュール]** ページで、作成する各サブスクリプションについて、 **[エージェント スケジュール]** ボックスの一覧から以下のいずれかの値を選択します。  
  
    -   **[連続実行する]**  
  
    -   **[要求時にのみ実行する]**  
  
    -   **[\<スケジュールの定義...>]**  
  
2.  **[\<スケジュールの定義...>]** を選択した場合は、 **[ジョブ スケジュールのプロパティ]** ダイアログ ボックスでスケジュールを指定し、 **[OK]** をクリックします。  
  
3.  ウィザードを完了します。  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-replication-monitor"></a>レプリケーション モニターでプッシュ サブスクリプションの同期スケジュールを変更するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  サブスクリプションを右クリックし、 **[詳細表示]** をクリックします。  
  
4.  **サブスクリプション\<SubscriptionName >** ウィンドウで、をクリックして**アクション**、 をクリックし、  **\<AgentName > ジョブのプロパティ**。  
  
5.  **[ジョブのプロパティ - \<JobName>]** ダイアログ ボックスの **[スケジュール]** ページで、 **[編集]** をクリックします。  
  
6.  **[ジョブ スケジュールのプロパティ]** ダイアログ ボックスで、 **[スケジュールの種類]** ボックスの一覧の値を選択します。  
  
    -   エージェントを連続実行するには、 **[SQL Server エージェントの開始時に自動的に開始]** を選択します。  
  
    -   エージェントをスケジュールで実行するには、 **[定期的]** を選択します。  
  
    -   エージェントを要求時に実行するには、 **[指定日時]** を選択します。  
  
7.  **[定期的]** を選択した場合は、エージェントのスケジュールを指定します。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-push-subscription-in-management-studio"></a>Management Studio でプッシュ サブスクリプションの同期スケジュールを変更するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  サブスクリプションに関連付けられているディストリビューション エージェントまたはマージ エージェントのジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ジョブのプロパティ - \<JobName>]** ダイアログ ボックスの **[スケジュール]** ページで、 **[編集]** をクリックします。  
  
5.  **[ジョブ スケジュールのプロパティ]** ダイアログ ボックスで、 **[スケジュールの種類]** ボックスの一覧の値を選択します。  
  
    -   エージェントを連続実行するには、 **[SQL Server エージェントの開始時に自動的に開始]** を選択します。  
  
    -   エージェントをスケジュールで実行するには、 **[定期的]** を選択します。  
  
    -   エージェントを要求時に実行するには、 **[指定日時]** を選択します。  
  
6.  **[定期的]** を選択した場合は、エージェントのスケジュールを指定します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
#### <a name="to-modify-a-synchronization-schedule-for-a-pull-subscription-in-management-studio"></a>Management Studio でプル サブスクリプションの同期スケジュールを変更するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  サブスクリプションに関連付けられているディストリビューション エージェントまたはマージ エージェントのジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ジョブのプロパティ - \<JobName>]** ダイアログ ボックスの **[スケジュール]** ページで、 **[編集]** をクリックします。  
  
5.  **[ジョブ スケジュールのプロパティ]** ダイアログ ボックスで、 **[スケジュールの種類]** ボックスの一覧の値を選択します。  
  
    -   エージェントを連続実行するには、 **[SQL Server エージェントの開始時に自動的に開始]** を選択します。  
  
    -   エージェントをスケジュールで実行するには、 **[定期的]** を選択します。  
  
    -   エージェントを要求時に実行するには、 **[指定日時]** を選択します。  
  
6.  **[定期的]** を選択した場合は、エージェントのスケジュールを指定します。  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
 レプリケーション ストアド プロシージャを使用してプログラムで同期スケジュールを定義できます。 使用するストアド プロシージャは、レプリケーションの種類およびサブスクリプションの種類 (プルまたはプッシュ) によって異なります。  
  
 スケジュールを定義するには、次のスケジュール設定のパラメーターを使用します。これらのパラメーターの動作は、[sp_add_schedule &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-schedule-transact-sql) から継承されます。  
  
-   **@frequency_type** - エージェントのスケジュール設定に使用する頻度の種類。  
  
-   **@frequency_interval** - エージェントを実行する曜日。  
  
-   **@frequency_relative_interval** - エージェントを月単位でスケジュール設定する場合の指定された月の週。  
  
-   **@frequency_recurrence_factor** - 同期から同期の間に発生する頻度の種類の単位の数。  
  
-   **@frequency_subday** - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
-   **@frequency_subday_interval** - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
-   **@active_start_time_of_day** - 指定された日のエージェントの実行を開始する最も早い時刻。  
  
-   **@active_end_time_of_day** - 指定された日のエージェントの実行を開始する最も遅い時刻。  
  
-   **@active_start_date** - エージェント スケジュールが有効になる最初の日。  
  
-   **@active_end_date** - エージェント スケジュールが有効である最後の日。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプル サブスクリプションの同期スケジュールを定義するには  
  
1.  トランザクション パブリケーションに対して新しいプル サブスクリプションを作成します。 詳細については、「 [Create a Pull Subscription](create-a-pull-subscription.md)」を参照してください。  
  
2.  サブスクライバーで、[sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql) を実行します。 **@publisher** 、 **@publisher_db** 、 **@publication** 、およびサブスクライバーのディストリビューション エージェントが **@job_name** と **@password** で実行するときの [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 資格情報を指定します。 サブスクリプションを同期するディストリビューション エージェント ジョブのスケジュールを定義する、上述の同期のパラメーターを指定します。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプッシュ サブスクリプションの同期スケジュールを定義するには  
  
1.  トランザクション パブリケーションに対して新しいプッシュ サブスクリプションを作成します。 詳細については、「 [プッシュ サブスクリプションの作成](create-a-push-subscription.md)」をご覧ください。  
  
2.  サブスクライバーで、[sp_addpushsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql) を実行します。 **@subscriber** 、 **@subscriber_db** 、 **@publication** 、およびサブスクライバーのディストリビューション エージェントが **@job_name** と **@password** で実行するときの Windows 資格情報を指定します。 サブスクリプションを同期するディストリビューション エージェント ジョブのスケジュールを定義する、上述の同期のパラメーターを指定します。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションの同期スケジュールを定義するには  
  
1.  マージ パブリケーションに対して新しいプル サブスクリプションを作成します。 詳細については、「 [Create a Pull Subscription](create-a-pull-subscription.md)」を参照してください。  
  
2.  サブスクライバーで、 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)を実行します。 **@publisher** 、 **@publisher_db** 、 **@publication** 、およびサブスクライバーのマージ エージェントが **@job_name** と **@password** で実行するときの Windows 資格情報を指定します。 サブスクリプションを同期するマージ エージェント ジョブのスケジュールを定義する、上述の同期のパラメーターを指定します。  
  
#### <a name="to-define-the-synchronization-schedule-for-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションの同期スケジュールを定義するには  
  
1.  マージ パブリケーションに対して新しいプッシュ サブスクリプションを作成します。 詳細については、「 [Create a Push Subscription](create-a-push-subscription.md)」を参照してください。  
  
2.  サブスクライバーで、 [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)を実行します。 **@subscriber** 、 **@subscriber_db** 、 **@publication** 、およびサブスクライバーのマージ エージェントが **@job_name** と **@password** で実行するときの Windows 資格情報を指定します。 サブスクリプションを同期するマージ エージェント ジョブのスケジュールを定義する、上述の同期のパラメーターを指定します。  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
 レプリケーションは、SQL&#xA0;Server エージェントを使用して、スナップショットの生成やサブスクリプションの同期など、定期的に発生する動作のジョブをスケジュール設定します。 レプリケーション管理オブジェクト (RMO) をプログラムで使用して、レプリケーション エージェント ジョブのスケジュールを指定できます。  
  
> [!NOTE]  
>  サブスクリプションを作成し、`false` に `CreateSyncAgentByDefault` を指定すると (プル サブスクリプションの既定の動作)、エージェント ジョブは作成されず、スケジュール設定のプロパティは無視されます。 この場合は、アプリケーションによって同期スケジュールを決定する必要があります。 詳細については、「 [Create a Pull Subscription](create-a-pull-subscription.md) 」および「 [Create a Push Subscription](create-a-push-subscription.md)」を参照してください。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプッシュ サブスクリプションを作成するレプリケーション エージェント スケジュールを定義するには  
  
1.  作成するサブスクリプションに対して <xref:Microsoft.SqlServer.Replication.TransSubscription> クラスのインスタンスを作成します。 詳細については、「 [Create a Push Subscription](create-a-push-subscription.md)」を参照してください。  
  
2.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>を呼び出す前に、 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> プロパティの次のフィールドを 1 つ以上設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - エージェントのスケジュール設定時に使用する頻度の種類 (毎日、毎週など)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - エージェントを実行する曜日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - エージェントを月単位でスケジュール設定する場合の指定された月の週。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同期から同期の間に発生する頻度の種類の単位の数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - エージェントの実行を開始する特定の日の最も早い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - エージェントの実行を開始する特定の日の最も遅い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - エージェント スケジュールが有効になっている最初の日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - エージェント スケジュールが有効になっている最後の日。  
  
    > [!NOTE]  
    >  これらのプロパティを指定しなかった場合、既定値が設定されます。  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> メソッドを呼び出してサブスクリプションを作成します。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-transactional-publication"></a>トランザクション パブリケーションに対するプル サブスクリプションを作成するレプリケーション エージェント スケジュールを定義するには  
  
1.  作成するサブスクリプションに対して <xref:Microsoft.SqlServer.Replication.TransPullSubscription> クラスのインスタンスを作成します。 詳細については、「 [Create a Pull Subscription](create-a-pull-subscription.md)」を参照してください。  
  
2.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>を呼び出す前に、 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> プロパティの次のフィールドを 1 つ以上設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - エージェントのスケジュール設定時に使用する頻度の種類 (毎日、毎週など)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - エージェントを実行する曜日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - エージェントを月単位でスケジュール設定する場合の指定された月の週。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同期から同期の間に発生する頻度の種類の単位の数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - エージェントの実行を開始する特定の日の最も早い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - エージェントの実行を開始する特定の日の最も遅い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - エージェント スケジュールが有効になっている最初の日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - エージェント スケジュールが有効になっている最後の日。  
  
    > [!NOTE]  
    >  これらのプロパティを指定しなかった場合、既定値が設定されます。  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> メソッドを呼び出してサブスクリプションを作成します。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-pull-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプル サブスクリプションを作成するレプリケーション エージェント スケジュールを定義するには  
  
1.  作成するサブスクリプションに対して <xref:Microsoft.SqlServer.Replication.MergePullSubscription> クラスのインスタンスを作成します。 詳細については、「 [Create a Pull Subscription](create-a-pull-subscription.md)」を参照してください。  
  
2.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A>を呼び出す前に、 <xref:Microsoft.SqlServer.Replication.PullSubscription.AgentSchedule%2A> プロパティの次のフィールドを 1 つ以上設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - エージェントのスケジュール設定時に使用する頻度の種類 (毎日、毎週など)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - エージェントを実行する曜日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - エージェントを月単位でスケジュール設定する場合の指定された月の週。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同期から同期の間に発生する頻度の種類の単位の数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - エージェントの実行を開始する特定の日の最も早い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - エージェントの実行を開始する特定の日の最も遅い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - エージェント スケジュールが有効になっている最初の日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - エージェント スケジュールが有効になっている最後の日。  
  
    > [!NOTE]  
    >  これらのプロパティを指定しなかった場合、既定値が設定されます。  
  
3.  <xref:Microsoft.SqlServer.Replication.PullSubscription.Create%2A> メソッドを呼び出してサブスクリプションを作成します。  
  
#### <a name="to-define-a-replication-agent-schedule-when-you-create-a-push-subscription-to-a-merge-publication"></a>マージ パブリケーションに対するプッシュ サブスクリプションを作成するレプリケーション エージェント スケジュールを定義するには  
  
1.  作成するサブスクリプションに対して <xref:Microsoft.SqlServer.Replication.MergeSubscription> クラスのインスタンスを作成します。 詳細については、「 [Create a Push Subscription](create-a-push-subscription.md)」を参照してください。  
  
2.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A>を呼び出す前に、 <xref:Microsoft.SqlServer.Replication.Subscription.AgentSchedule%2A> プロパティの次のフィールドを 1 つ以上設定します。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyType%2A> - エージェントのスケジュール設定時に使用する頻度の種類 (毎日、毎週など)。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyInterval%2A> - エージェントを実行する曜日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRelativeInterval%2A> - エージェントを月単位でスケジュール設定する場合の指定された月の週。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencyRecurrenceFactor%2A> - 同期から同期の間に発生する頻度の種類の単位の数。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDay%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.FrequencySubDayInterval%2A> - エージェントを 1 日に複数回実行する場合の頻度の単位。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartTime%2A> - エージェントの実行を開始する特定の日の最も早い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndTime%2A> - エージェントの実行を開始する特定の日の最も遅い時刻。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveStartDate%2A> - エージェント スケジュールが有効になっている最初の日。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationAgentSchedule.ActiveEndDate%2A> - エージェント スケジュールが有効になっている最後の日。  
  
    > [!NOTE]  
    >  これらのプロパティを指定しなかった場合、既定値が設定されます。  
  
3.  <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> メソッドを呼び出してサブスクリプションを作成します。  
  
###  <a name="PShellExample"></a> 例 (RMO)  
 次の例では、マージ パブリケーションに対するプッシュ サブスクリプションを作成して、サブスクリプションを同期するスケジュールを指定します。  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>関連項目  
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [パブリケーションのサブスクライブ](subscribe-to-publications.md)   
 [プッシュ サブスクリプションの同期](synchronize-a-push-subscription.md)   
 [プル サブスクリプションの同期](synchronize-a-pull-subscription.md)   
 [データの同期](synchronize-data.md)  
  
  
