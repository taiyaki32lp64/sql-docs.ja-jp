---
title: SQL Server エージェントの Jobs オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLAgent:Jobs
- Jobs object
ms.assetid: 225b5e2d-4a78-4178-b2b6-b419df83c4aa
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5bd37ab434dbefbb01862f1004ca62e673df0453
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63251029"
---
# <a name="sql-server-agent-jobs-object"></a>SQL Server エージェントの Jobs オブジェクト
  SQL Server エージェントの **Jobs** パフォーマンス オブジェクトには、SQL Server エージェントのジョブについての情報を報告するパフォーマンス カウンターが含まれています。 次の表は、このオブジェクトに含まれているカウンターを示します。  
  
 次の表には **SQLAgent:Jobs** カウンターが含まれています。  
  
|名前|説明|  
|----------|-----------------|  
|**Active Jobs**|このカウンターは、現在実行中のジョブの数を報告します。|  
|**Failed jobs**|このカウンターは、失敗して終了したジョブの数を報告します。|  
|**Job success rate**|このカウンターは、実行済みジョブのうち問題なく完了したジョブの割合を報告します。|  
|**Jobs activated/minute**|このカウンターは、最後の 1 分間に起動されたジョブの数を報告します。|  
|**Queued jobs**|このカウンターは、SQL Server エージェントで実行する準備が整っているジョブで、まだ実行が開始されていないジョブの数を報告します。|  
|**Successful jobs**|このカウンターは、問題なく終了したジョブの数を報告します。|  
  
 オブジェクトの各カウンターには、次のインスタンスが含まれています。  
  
|Instance|説明|  
|--------------|-----------------|  
|**_Total**|すべてのジョブの情報です。|  
|**警告**|警告によって開始されたジョブの情報です。|  
|**Others**|警告またはスケジュールによって開始されたジョブの情報です。 通常、これらのジョブは **sp_start_job**を使用して手動で開始されます。|  
|**スケジュール**|スケジュールによって開始されたジョブの情報です。|  
  
## <a name="see-also"></a>関連項目  
 [ジョブの実装](../../ssms/agent/implement-jobs.md)   
 [パフォーマンス オブジェクトの使用](../../ssms/agent/use-performance-objects.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
