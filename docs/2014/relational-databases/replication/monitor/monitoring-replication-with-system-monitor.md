---
title: システム モニターによるレプリケーションの監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2b5d1a63937a11da4703ec4ef0338dee89a5c33f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667307"
---
# <a name="monitoring-replication-with-system-monitor"></a>システム モニターによるレプリケーションの監視
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows のシステム モニターにより、グラフ、図およびレポートを使って、使用しているコンピューターの効率の評価、考えられる問題 (リソース使用の不均衡、ハードウェアの不足、プログラム設計の問題など) の識別とトラブルシューティング、およびハードウェアの追加計画の作成を行うことができます。 詳細については、「[リソースの利用状況の監視 &#40;システム モニター&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md)」を参照してください。  
  
 システム モニターでは、さまざまなプロセスのパフォーマンスについての情報を提供するパフォーマンス オブジェクトおよびカウンターを使用します。 レプリケーション エージェントに関連するカウンターにより、レプリケーション パフォーマンスを計測できます。  
  
|エージェント|パフォーマンス オブジェクト|カウンター|説明|  
|-----------|------------------------|-------------|-----------------|  
|すべてのエージェント|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:Replication Agents|実行中|現在実行されているレプリケーション エージェントの数。|  
|スナップショット エージェント|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション スナップショット|スナップショット:1 秒あたりに配信されたコマンド|ディストリビューターに 1 秒間に配信されたコマンド数。|  
|スナップショット エージェント|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション スナップショット|スナップショット:1 秒あたりに配信されたトランザクション|ディストリビューターに 1 秒間に配信されたトランザクション数。|  
|ログ リーダー エージェント (Log Reader Agent)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション ログ リーダー|ログ リーダー:1 秒あたりに配信されたコマンド|ディストリビューターに 1 秒間に配信されたコマンド数。|  
|ログ リーダー エージェント (Log Reader Agent)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション ログ リーダー|ログ リーダー:1 秒あたりに配信されたトランザクション|ディストリビューターに 1 秒間に配信されたトランザクション数。|  
|ログ リーダー エージェント (Log Reader Agent)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション ログ リーダー|ログ リーダー:配信の遅延|パブリッシャーでトランザクションが適用されてから、ディストリビューターに配信されるまでの現在のミリ秒単位の経過時間。|  
|ディストリビューション エージェント|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーションの配布|Dist:1 秒あたりに配信されたコマンド|サブスクライバーに 1 秒間に配信されたコマンド数。|  
|ディストリビューション エージェント|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーションの配布|Dist:1 秒あたりに配信されたトランザクション|サブスクライバーに 1 秒間に配信されたトランザクション数。|  
|ディストリビューション エージェント|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーションの配布|Dist:配信の遅延|トランザクションがディストリビューターに配信されてから、サブスクライバーで適用されるまでの現在のミリ秒単位の経過時間。|  
|[マージ エージェント]|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション マージ|Conflicts/sec|マージ プロセス中に 1 秒間に発生した競合数。|  
|[マージ エージェント]|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション マージ|Downloaded Changes/sec|パブリッシャーからサブスクライバーに 1 秒間にレプリケートされた行数。|  
|[マージ エージェント]|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:レプリケーション マージ|Uploaded Changes/sec|サブスクライバーからパブリッシャーに 1 秒間にレプリケートされた行数。|  
  
## <a name="see-also"></a>参照  
 [監視 (レプリケーション)](../monitoring-replication.md)  
  
  
