---
title: レプリケーション モニターでのパブリケーションおよびサブスクリプションの状態の表示 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Log Reader Agent, monitoring
- Merge Agent, monitoring
- Queue Reader Agent, monitoring
- publications [SQL Server replication], viewing information
- Snapshot Agent, monitoring
- Distribution Agent, monitoring
- monitoring performance [SQL Server replication], publication status
- monitoring performance [SQL Server replication], subscription status
- subscriptions [SQL Server replication], viewing status
- Replication Monitor, publication and subscription status
ms.assetid: 16590771-9867-463e-a973-36a5c145ac16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9dad3a2c5f7073ea63608ba5234061a3ffa2102c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666967"
---
# <a name="view-publication-and-subscription-status-in-replication-monitor"></a>レプリケーション モニターでのパブリケーションおよびサブスクリプションの状態の表示
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] レプリケーション モニターには、パブリケーションおよびサブスクリプションの状態情報が表示されます。  
  
-   パブリケーションの状態は、そのサブスクリプションの最も優先度の高い状態によって決定されます。 たとえば、あるパブリケーションに対する 1 つのサブスクリプションにエラーが発生し、別のサブスクリプションにはパフォーマンス上の問題がある場合、そのパブリケーションに対してはエラーの状態が表示されます。  
  
-   サブスクリプションの状態は、そのサブスクリプションにサービスを提供するエージェントの状態によって決定されます。 マージ レプリケーションの場合はマージ エージェントです。 トランザクション レプリケーションの場合は、ログ リーダー エージェントまたはディストリビューション エージェントです (優先度の高い方の状態が表示されます。キュー更新サブスクリプションが使用されている場合は、状態はキュー リーダー エージェントによっても決定されます)。 スナップショット レプリケーションの場合は、スナップショット エージェントまたはディストリビューション エージェントです (優先度の高い方の状態が表示されます)。  
  
 以下に、パブリケーションおよびサブスクリプションの状態の値の一覧を示します。 しきい値に達したか、超えた場合にのみ、3 つの状態値が表示されます。  
  
-   有効期限切れサブスクリプション  
  
     この状態値は、すべての種類のレプリケーションに適用されます。 詳細については、「 [レプリケーション モニターのしきい値と警告の設定](set-thresholds-and-warnings-in-replication-monitor.md)」を参照してください。  
  
-   [パフォーマンス クリティカル]  
  
     この状態値は、トランザクション レプリケーションとマージ レプリケーションに適用されます。 詳細については、「[レプリケーション モニターを使用したパフォーマンスの監視](monitor-performance-with-replication-monitor.md)」をご覧ください。  
  
-   [長期マージ]  
  
     この状態値はマージ レプリケーションに適用されます。 詳細については、「[レプリケーション モニターを使用したパフォーマンスの監視](monitor-performance-with-replication-monitor.md)」をご覧ください。  
  
 パブリケーションおよびサブスクリプションの状態の他に、マージ レプリケーションではアーティクル レベルの統計が使用できます。この情報は、マージ フェーズの完了までに要する時間、指定されたアーティクルの処理に費やされた時間、サブスクライバーが使用している接続の種類、およびその他の重要な情報についての詳細を提供します。 統計情報は、レプリケーション モニターの [マージ エージェント] ウィンドウに表示されます。 スナップショット レプリケーションおよびトランザクション レプリケーションでは、ディストリビューション エージェントの処理に関する詳細が提供されます。  
  
 **パブリケーションおよびサブスクリプションの状態を表示するには**  
  
-   レプリケーション モニター:[レプリケーション モニターを使用して情報を表示し、タスクを実行する](view-information-and-perform-tasks-replication-monitor.md)
  
  
## <a name="publication-status-values"></a>パブリケーションの状態の値  
 次の表は、パブリケーションの状態の値と対応するアイコンを優先度順に示しています。  
  
|状態|アイコン|  
|------------|----------|  
|[エラー]|![UI アイコン: エラー](../media/repl-icon-error.gif "UI アイコン: エラー")|  
|[パフォーマンス クリティカル]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[失敗したコマンドの再試行]|![UI アイコン: レプリケーション エージェントの再試行](../media/repl-icon-retry.gif "UI アイコン: レプリケーション エージェントの再試行")|  
|[OK]|なし|  
  
## <a name="subscription-status-values"></a>サブスクリプションの状態値  
 次の表は、サブスクリプションの状態値と対応するアイコンを優先度順に示しています。 サブスクリプションは、" **まもなく期限切れ/期限切れ** " と " **失敗したコマンドの再試行**" など同時に 2 つの状態になることがあります。その場合、最も優先度の高い状態が表示されます。  
  
 状態値 " **パフォーマンス クリティカル**"、" **まもなく期限切れ/期限切れ**"、および " **初期化されていないサブスクリプション** " は警告です。 警告が表示されるとき、レプリケーション モニターにはエージェントが実行中であるかどうかも表示されます。 たとえば、 **[実行中]、[パフォーマンス クリティカル]** という形で状態が表示されます。  
  
### <a name="transactional-subscriptions"></a>トランザクション サブスクリプション  
  
|状態|アイコン|  
|------------|----------|  
|[エラー]|![UI アイコン: エラー](../media/repl-icon-error.gif "UI アイコン: エラー")|  
|[パフォーマンス クリティカル]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|まもなく期限切れ/期限切れ|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[初期化されていないサブスクリプション]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[失敗したコマンドの再試行]|![UI アイコン: レプリケーション エージェントの再試行](../media/repl-icon-retry.gif "UI アイコン: レプリケーション エージェントの再試行")|  
|[実行されていません]|![UI アイコン: レプリケーション エージェントの停止](../media/repl-icon-stopped.gif "UI アイコン: レプリケーション エージェントの停止")|  
|実行中|![UI アイコン: レプリケーション エージェントの実行](../media/repl-icon-running.gif "UI アイコン: レプリケーション エージェントの実行")|  
  
### <a name="merge-subscriptions"></a>マージ サブスクリプション  
  
|状態|アイコン|  
|------------|----------|  
|[エラー]|![UI アイコン: エラー](../media/repl-icon-error.gif "UI アイコン: エラー")|  
|[パフォーマンス クリティカル]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[長期マージ]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|まもなく期限切れ/期限切れ|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[初期化されていないサブスクリプション]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[失敗したコマンドの再試行]|![UI アイコン: レプリケーション エージェントの再試行](../media/repl-icon-retry.gif "UI アイコン: レプリケーション エージェントの再試行")|  
|[同期中]|![UI アイコン: レプリケーション エージェントの実行](../media/repl-icon-running.gif "UI アイコン: レプリケーション エージェントの実行")|  
|同期されていません|![UI アイコン: レプリケーション エージェントの停止](../media/repl-icon-stopped.gif "UI アイコン: レプリケーション エージェントの停止")|  
  
### <a name="snapshot-subscriptions"></a>スナップショット サブスクリプション  
  
|状態|アイコン|  
|------------|----------|  
|[エラー]|![UI アイコン: エラー](../media/repl-icon-error.gif "UI アイコン: エラー")|  
|[まもなく期限切れ/期限切れ]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[初期化されていないサブスクリプション]|![UI アイコン: 警告](../media/repl-icon-warn.gif "UI アイコン: 警告")|  
|[失敗したコマンドの再試行]|![UI アイコン: レプリケーション エージェントの再試行](../media/repl-icon-retry.gif "UI アイコン: レプリケーション エージェントの再試行")|  
|[同期中]|![UI アイコン: レプリケーション エージェントの実行](../media/repl-icon-running.gif "UI アイコン: レプリケーション エージェントの実行")|  
|同期されていません|![UI アイコン: レプリケーション エージェントの停止](../media/repl-icon-stopped.gif "UI アイコン: レプリケーション エージェントの停止")|  
  
## <a name="see-also"></a>参照  
 [レプリケーションの監視](../monitoring-replication.md)  
  
  
