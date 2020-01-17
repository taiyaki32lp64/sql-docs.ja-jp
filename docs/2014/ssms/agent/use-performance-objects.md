---
title: パフォーマンス オブジェクトの使用 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, monitoring
- SQL Server Agent service, monitoring
- SQL Server Agent service, performance objects
- SQL Server Agent, performance objects
- performance objects [SQL Server Agent]
- monitoring [SQL Server], SQL Server Agent
- monitoring [SQL Server Agent]
- performance counters [SQL Server], SQL Server Agent
- counters [SQL Server], SQL Server Agent
ms.assetid: 830b843a-6b2a-4620-a51b-98358e9fc54b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2ccba43aa28cadef1995fab001f66e1f4bebacde
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63245849"
---
# <a name="use-performance-objects"></a>パフォーマンス オブジェクトの使用
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントには、サービスの動作を監視するためのパフォーマンス オブジェクトとパフォーマンス カウンターが含まれています。 パフォーマンス オブジェクトを使用すると、パフォーマンス モニターや Windows ツールを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのバックグラウンド動作を特定できるようになります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスで現在実行されているアクティブなジョブの数を特定して、ブロックされたジョブを特定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのパフォーマンス オブジェクトとパフォーマンス カウンターは、コンピューターにインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスごとに存在します。 パフォーマンス オブジェクトの名前は、各オブジェクトが表す [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに従って付けられます。  
  
 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスのパフォーマンス オブジェクトの命名形式を示しています。  
  
|インスタンスの種類|オブジェクト名です。|  
|-------------------|-----------------|  
|既定|**SQLAgent:** *オブジェクト*:*カウンター*|  
|名前付き|**SQLAgent$**<br /> ***instance_name* :** *object*:*counter*|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントの次のパフォーマンス オブジェクトが含まれています。  
  
|オブジェクト名です。|説明|  
|-----------------|-----------------|  
|[SQLAgent:Jobs](../../relational-databases/performance-monitor/sql-server-agent-jobs-object.md)|開始されたジョブ、成功率、および現在の状態に関するパフォーマンス情報|  
|[SQLAgent:JobSteps](../../relational-databases/performance-monitor/sql-server-agent-jobsteps-object.md)|ジョブ ステップに関する状態情報|  
|[SQLAgent:Alerts](../../relational-databases/performance-monitor/sql-server-agent-alerts-object.md)|警告と通知の数に関する情報|  
|[SQLAgent:Statistics](../../relational-databases/performance-monitor/sql-server-agent-statistics-object.md)|パフォーマンスに関する一般的な情報|  
  
## <a name="see-also"></a>関連項目  
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [システム モニターの起動 &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
  
