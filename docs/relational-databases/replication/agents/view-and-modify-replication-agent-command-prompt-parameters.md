---
title: エージェント コマンド プロンプト パラメーターの表示および変更
description: SQL Server のさまざまなレプリケーション エージェントによって使用されるコマンド プロンプト パラメーターを表示および変更する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], command prompt parameters
ms.assetid: 45f2e781-c21d-4b44-8992-89f60fb3d022
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6c72c58b0a23f8215d303addfbb2ec9fb65c4489
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321637"
---
# <a name="view-and-modify-replication-agent-command-prompt-parameters"></a>レプリケーション エージェント コマンド プロンプト パラメーターの表示および変更
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  レプリケーション エージェントは、コマンド ライン パラメーターを使用できる実行可能ファイルです。 既定では、エージェントは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント ジョブ ステップで実行されるため、これらのパラメーターは、 **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスを使用して表示および変更できます。 このダイアログ ボックスは、 **の** [ジョブ] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] フォルダーおよびレプリケーション モニター内の **[エージェント]** タブからアクセスできます。 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
> [!NOTE]  
>  エージェント パラメーターの変更は、エージェントの次回起動時に反映されます。 エージェントを継続して実行している場合は、そのエージェントを停止して再起動する必要があります。  
  
 パラメーターは直接変更することもできますが、エージェント プロファイルを使用して変更する方が一般的です。 詳しくは、「 [レプリケーション エージェント プロファイル](../../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
 **[ジョブ]** フォルダーからエージェント ジョブにアクセスする場合は、次の表を使用して、各エージェントで使用できるエージェント ジョブ名とパラメーターを決定してください。  
  
|エージェント|ジョブ名|パラメーターの一覧の参照先|  
|-----------|--------------|------------------------------------|  
|スナップショット エージェント|**\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<整数>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|マージ パブリケーション パーティションに対するスナップショット エージェント|**Dyn_\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<GUID>**|[Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|  
|ログ リーダー エージェント (Log Reader Agent)|**\<パブリッシャー>-\<PublicationDatabase>-\<整数>**|[レプリケーション ログ リーダー エージェント](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|  
|プル サブスクリプションに対するマージ エージェント|**\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<サブスクライバー>-\<SubscriptionDatabase>-\<整数>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|プッシュ サブスクリプションに対するマージ エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|  
|プッシュ サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|プル サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<PublicationDatabase>-\<パブリケーション>-\<サブスクライバー>-\<SubscriptionDatabase>-\<GUID>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|SQL Server 以外のサブスクライバーへのプッシュ サブスクリプションに対するディストリビューション エージェント|**\<パブリッシャー>-\<パブリケーション データベース>-\<パブリケーション>-\<サブスクライバー>-\<整数>**|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|  
|キュー リーダー エージェント (Queue Reader Agent)|**[\<ディストリビューター>].\<整数>**|[レプリケーション キュー リーダー エージェント](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|  
  
 \*Oracle パブリケーションに対するプッシュ サブスクリプションの場合は、 **\<Publisher>-\<PublicationDatabase>** ではなく、 **\<Publisher>-\<Publisher**> になります  
  
 \*\*Oracle パブリケーションに対するプル サブスクリプションの場合は、 **\<Publisher>-\<PublicationDatabase>** ではなく **\<Publisher>-\<DistributionDatabase**> になります  
  
### <a name="to-view-and-modify-replication-agent-command-line-parameters-from-management-studio"></a>Management Studio からレプリケーション エージェント コマンド ライン パラメーターを表示または変更するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]で適切なコンピューターに接続して、サーバー ノードを展開します。  
  
    -   プル サブスクリプションに対するディストリビューション エージェントとマージ エージェントの場合は、サブスクライバーに接続します。  
  
    -   その他のエージェントの場合は、ディストリビューターに接続します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  ジョブを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスの **[ステップ]** ページで、ステップ **[エージェントを実行します]** を選択し、 **[編集]** をクリックします。  
  
5.  **[ジョブ ステップのプロパティ - エージェントを実行します]** ダイアログ ボックスで、 **[コマンド]** フィールドを編集します。  
  
6.  両方のダイアログ ボックスで **[OK]** をクリックします。  
  
### <a name="to-view-and-modify-distribution-agent-and-merge-agent-command-line-parameters-from-replication-monitor"></a>レプリケーション モニターからディストリビューション エージェントとマージ エージェントのコマンド ライン パラメーターを表示および変更するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[すべてのサブスクリプション]** タブをクリックします。  
  
3.  サブスクリプションを右クリックし、 **[詳細表示]** をクリックします。  
  
4.  **[サブスクリプション <SubscriptionName>]** ウィンドウで、 **[アクション]** をクリックし、 **[\<AgentName> ジョブのプロパティ]** をクリックします。  
  
5.  **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスの **[ステップ]** ページで、ステップ **[エージェントを実行します]** を選択し、 **[編集]** をクリックします。  
  
6.  **[ジョブ ステップのプロパティ - エージェントを実行します]** ダイアログ ボックスで、 **[コマンド]** フィールドを編集します。  
  
7.  両方のダイアログ ボックスで **[OK]** をクリックします。  
  
### <a name="to-view-and-modify-snapshot-agent-log-reader-agent-and-queue-reader-agent-command-line-parameters-from-replication-monitor"></a>レプリケーション モニターからスナップショット エージェント、ログ リーダー エージェント、およびキュー リーダー エージェントのコマンド ライン パラメーターを表示および変更するには  
  
1.  レプリケーション モニターの左ペインのパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[エージェント]** タブをクリックします。  
  
3.  グリッド内のエージェントを右クリックし、 **[プロパティ]** をクリックします。  
  
4.  **[ジョブのプロパティ - \<Job>]** ダイアログ ボックスの **[ステップ]** ページで、ステップ **[エージェントを実行します]** を選択し、 **[編集]** をクリックします。  
  
5.  **[ジョブ ステップのプロパティ - エージェントを実行します]** ダイアログ ボックスで、 **[コマンド]** フィールドを編集します。  
  
6.  両方のダイアログ ボックスで **[OK]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの管理](../../../relational-databases/replication/agents/replication-agent-administration.md)   
 [レプリケーション エージェント実行可能ファイルの概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [レプリケーション エージェントの概要](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
