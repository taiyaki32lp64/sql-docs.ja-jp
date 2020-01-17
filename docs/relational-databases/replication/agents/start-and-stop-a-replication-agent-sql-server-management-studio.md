---
title: レプリケーション エージェントを起動および停止する (SSMS)
description: SQL Server Management Studio とレプリケーション モニターでレプリケーション エージェントの停止を開始する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], stopping
- agents [SQL Server replication], starting
ms.assetid: 97977c4a-8c7c-4a22-9480-69aa812bd1e5
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 70f876d9152e836e12ad0c28e640362b23197190
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321632"
---
# <a name="start-and-stop-a-replication-agent-sql-server-management-studio"></a>レプリケーション エージェントを起動および停止する (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] の **[ジョブ]** フォルダーと **[レプリケーション]** フォルダーから、およびレプリケーション モニターからエージェントを開始および停止します。 以下のエージェントおよびジョブの開始と停止を行うことができます。  
  
-   すべてのパブリケーションで使用されるスナップショット エージェント  
  
-   すべてのトランザクション パブリケーションで使用されるログ リーダー エージェント  
  
-   キュー更新サブスクリプションに有効なトランザクション パブリケーションで使用されるキュー リーダー エージェント  
  
-   トランザクション パブリケーションやスナップショット パブリケーションに対するサブスクリプションを同期するディストリビューション エージェント  
  
-   マージ パブリケーションに対するサブスクリプションを同期するマージ エージェント  
  
-   レプリケーション メンテナンス ジョブ。  
  
 マージ エージェントとディストリビューション エージェントの開始について詳しくは、「[プッシュ サブスクリプションの同期](../../../relational-databases/replication/synchronize-a-push-subscription.md)」および「[プル サブスクリプションの同期](../../../relational-databases/replication/synchronize-a-pull-subscription.md)」をご覧ください。 メンテナンス ジョブについて詳しくは、「[レプリケーション メンテナンス ジョブの実行 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/administration/run-replication-maintenance-jobs-sql-server-management-studio.md)」をご覧ください。  
  
 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
### <a name="to-start-and-stop-a-snapshot-agent-or-log-reader-agent-from-management-studio"></a>Management Studio からスナップショット エージェントまたはログ リーダー エージェントを開始および停止するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でパブリッシャーに接続して、サーバー ノードと **[レプリケーション]** フォルダーを展開します。  
  
2.  **[ローカル パブリケーション]** フォルダーを展開し、パブリケーションを右クリックします。  
  
3.  **[スナップショット エージェントの状態の表示]** または **[ログ リーダー エージェントの状態の表示]** をクリックします。  
  
4.  **[開始]** または **[停止]** をクリックします。  
  
### <a name="to-start-and-stop-a-queue-reader-agent-from-management-studio"></a>Management Studio からキュー リーダー エージェントを開始および停止するには  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でディストリビューターに接続して、サーバー ノードを展開します。  
  
2.  **[SQL Server エージェント]** フォルダーを展開して、 **[ジョブ]** フォルダーを展開します。  
  
3.  エージェントのジョブを右クリックして **[ジョブの開始]** または **[ジョブの停止]** をクリックします。 キュー リーダー エージェントのジョブの名前は、 **[\<ディストリビューター>].\<整数>** という形式になっています。  
  
### <a name="to-start-and-stop-a-snapshot-agent-log-reader-agent-or-queue-reader-agent-from-replication-monitor"></a>レプリケーション モニターからスナップショット エージェント、ログ リーダー エージェント、またはキュー リーダー エージェントを開始および停止するには  
  
1.  左ペインでパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[エージェント]** タブをクリックします。  
  
3.  エージェントを右クリックして **[エージェントの開始]** または **[エージェントの停止]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [レプリケーションの監視](../../../relational-databases/replication/monitor/monitoring-replication.md)   
 [レプリケーション エージェント実行可能ファイルの概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)   
 [レプリケーション エージェントの概要](../../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
