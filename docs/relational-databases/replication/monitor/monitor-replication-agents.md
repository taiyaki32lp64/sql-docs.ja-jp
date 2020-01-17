---
title: レプリケーション エージェントの監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], agents
- Log Reader Agent, monitoring
- Replication Monitor, agents
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- Snapshot Agent, monitoring
- agents [SQL Server replication], monitoring
- Distribution Agent, monitoring
ms.assetid: d06ed24f-82d7-4b9e-9e40-cc9780476a71
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: aa72ae36463f191ef8f127562d231b2e58480039
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68767719"
---
# <a name="monitor-replication-agents"></a>レプリケーション エージェントの監視
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション モニターを使用すると、レプリケーションの利用状況を体系的に表示でき、特定のエージェントに関する情報を簡単に見つけることもできます。 次の一覧に、各エージェント、各エージェントを利用できるレプリケーション モニターのタブ、およびそれらのタブへのアクセス方法について説明しているトピックへのリンクを示します。  
  
-   以下のエージェントは、レプリケーション モニターでパブリケーションと関連付けられています。  
  
    -   スナップショット エージェント  
  
    -   ログ リーダー エージェント (Log Reader Agent)  
  
    -   キュー リーダー エージェント (Queue Reader Agent)  
  
     これらのエージェントに関連付けられている情報およびタスクにアクセスするには、次のタブを使用します。 **[エージェント]** (各パブリッシャーとパブリケーションで使用可能) と **[警告]** (各パブリケーションで使用可能)。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
-   以下のエージェントは、レプリケーション モニターでサブスクリプションと関連付けられています。  
  
    -   ディストリビューション エージェント  
  
    -   [マージ エージェント]  
  
     これらのエージェントに関連付けられている情報およびタスクにアクセスするには、次のタブを使用します。 **[サブスクリプション ウォッチ リスト]** (各パブリッシャーで使用可能)、または **[すべてのサブスクリプション]** タブ (各パブリケーションで使用可能)。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
## <a name="using-sql-server-management-studio-to-monitor-replication-agents"></a>SQL Server Management Studio を使用してレプリケーション エージェントを監視する  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] には、レプリケーション エージェントの監視用に以下のダイアログ ボックスが用意されています。  
  
-   **[スナップショット エージェントの状態の表示]** ダイアログ ボックス (すべてのパブリケーション用)  
  
-   **[ログ リーダー エージェントの状態の表示]** ダイアログ ボックス (すべてのトランザクション パブリケーション用)  
  
-   **[同期の状態の表示]** ダイアログ ボックス (すべてのサブスクリプション用。このダイアログ ボックスからディストリビューション エージェントおよびマージ エージェントにアクセスできます)  
  
 レプリケーション モニターでは、各エージェントに関する追加情報が表示され、キュー リーダー エージェントが使用されている場合はその監視機能も提供されます。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。
  
#### <a name="to-monitor-the-snapshot-agent-and-log-reader-agent"></a>スナップショット エージェントおよびログ リーダー エージェントを監視するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  パブリケーションを右クリックし、 **[ログ リーダー エージェントの状態の表示]** または **[スナップショット エージェントの状態の表示]** をクリックします。  
  
4.  **[ログ リーダー エージェントの状態の表示]** または **[スナップショット エージェントの状態の表示]** ダイアログ ボックスで、以下の操作を行います。  
  
    -   エージェントの状態を表示します。  
  
    -   必要に応じてエージェントを開始または停止します。  
  
    -   **[監視]** をクリックして **レプリケーション モニター**を起動します。  
  
5.  **[閉じる]** をクリックします。  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-publisher"></a>ディストリビューション エージェントおよびマージ エージェントを監視するには (パブリッシャー側から)  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でパブリッシャーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーを展開します。  
  
3.  監視するサブスクリプションのパブリケーションを展開します。  
  
4.  サブスクリプションを右クリックし、 **[同期の状態の表示]** をクリックします。  
  
5.  **[同期の状態の表示]** ダイアログ ボックスで、以下の操作を行います。  
  
    -   エージェントの状態を表示します。  
  
    -   必要に応じてエージェントを開始または停止します。  
  
    -   プッシュ サブスクリプションの場合、 **[監視]** をクリックして **レプリケーション モニター**を起動します。  
  
    -   プル サブスクリプションの場合、 **[ジョブ履歴の表示]** をクリックして **ログ ファイル ビューアー**を起動します。エージェント ログからの出力が表示されます。  
  
6.  **[閉じる]** をクリックします。  
  
#### <a name="to-monitor-the-distribution-agent-and-merge-agent-from-the-subscriber"></a>ディストリビューション エージェントおよびマージ エージェントを監視するには (サブスクライバー側から)  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でサブスクライバーに接続して、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  監視するサブスクリプションを右クリックして **[同期の状態の表示]** をクリックします。  
  
4.  **[同期の状態の表示]** ダイアログ ボックスで、以下の操作を行います。  
  
    -   エージェントの状態を表示します。  
  
    -   必要に応じてエージェントを開始または停止します。  
  
    -   **[ジョブ履歴の表示]** をクリックして **ログ ファイル ビューアー**を起動します。エージェント ログからの出力が表示されます。  
  
5.  **[閉じる]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーション エージェントの概要](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
