---
title: レプリケーションの監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], about monitoring replication
- transactional replication, monitoring
- monitoring [SQL Server replication]
- merge replication monitoring [SQL Server replication]
- snapshot replication [SQL Server], monitoring
- replication [SQL Server], monitoring
- administering replication, monitoring
ms.assetid: f182f43a-6af8-45bc-a708-08d5f7a6984a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e2b3441d98bc9226abce3a49fd28820df6ec99ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666870"
---
# <a name="monitoring-replication"></a>監視 (レプリケーション)
  レプリケーション トポロジの監視は、レプリケーションの配置における重要な側面です。 レプリケーション処理は分散環境で行われるため、レプリケーションに関連するすべてのコンピューターについてその利用状況と状態を追跡することが不可欠です。 レプリケーションの監視には以下のツールを使用できます。  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] Replication Monitor  
  
     レプリケーションの監視を行うにあたり、最も重要なツールがレプリケーション モニターです。すべてのレプリケーションの利用状況がパブリッシャー関連のビューで表示されます。 詳細については、次を参照してください。[レプリケーション モニターでパフォーマンスを監視](monitor/monitor-performance-with-replication-monitor.md)します。  
  
-   [!INCLUDE[msCoName](../../includes/msCoName-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssManStudioFull-md.md)]  
  
     [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] を使用して、レプリケーション モニターにアクセスできます。 また、次に示すエージェントによってログに記録された現在の状態や最後のメッセージを表示したり、各エージェントを開始および停止したりすることができます。ログ リーダー エージェント、スナップショット エージェント、マージ エージェント、ディストリビューション エージェント。 詳細については、「 [Monitor Replication Agents](monitor/monitor-replication-agents.md)」を参照してください。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] およびレプリケーション管理オブジェクト (RMO)  
  
     どちらのインターフェイスでも、ディストリビューターからすべての種類のレプリケーションを監視できます。 マージ レプリケーションでは、サブスクライバーからレプリケーションを監視することもできます。  
  
-   レプリケーション エージェント イベントに対する警告  
  
     レプリケーションには、レプリケーション エージェント イベントに対する定義済みの警告が多数用意されています。また、必要に応じて追加の警告を作成することもできます。 警告を使用して、イベントに対する自動応答のトリガーを起動したり、管理者に通知することができます。 詳細については、「[レプリケーション エージェント イベントに対する警告の使用](agents/use-alerts-for-replication-agent-events.md)」を参照してください。  
  
-   システム モニター  
  
     システム モニターには、レプリケーションに関するさまざまなカウンターが表示されるので、パフォーマンスを監視する場合に便利です。 詳細については、「 [Monitoring Replication with System Monitor](monitor/monitoring-replication-with-system-monitor.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [レプリケーション管理に関する FAQ](administration/frequently-asked-questions-for-replication-administrators.md)   
 [Best Practices for Replication Administration](administration/best-practices-for-replication-administration.md)   

  
  
