---
title: 'SQL Server: Broker Activation オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 364fd8e037e2c09afa16294e75096993f861ca20
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987151"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server: Broker Activation オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SQLServer:BrokerActivation** パフォーマンス オブジェクトには、ストアド プロシージャのアクティブ化に関する情報を報告するパフォーマンス カウンターが含まれています。 次の表は、このオブジェクトに含まれているカウンターを示します。  
  
|SQL Server Broker Activation カウンター|[説明]|  
|-------------------------------------------|-----------------|  
|**Stored Procedures Invoked/sec**|インスタンス内のすべてのキュー モニターによって 1 秒間に呼び出されたアクティブ化ストアド プロシージャの合計数が報告されます。|  
|**Task Limit Reached**|キューに登録できる最大数のタスクが既に実行されているために、キュー モニターで新しいタスクの開始に失敗した合計回数が報告されます。|  
|**Task Limit Reached/sec**|キューに登録できる最大数のタスクが既に実行されているために、キュー モニターで 1 秒間に新しいタスクの開始に失敗した回数が報告されます。|  
|**Tasks Aborted/sec**|エラーが発生して終了したか、メッセージを受信できないためにキュー モニターによって中断されたアクティブ化ストアド プロシージャのタスク数が報告されます。|  
|**Tasks Running**|現在実行中のアクティブ化ストアド プロシージャの数が報告されます。|  
|**Tasks Started/sec**|インスタンス内のすべてのキュー モニターによって 1 秒間に開始されたアクティブ化ストアド プロシージャの数が報告されます。|  
  
## <a name="see-also"></a>参照  
 [sys.dm_broker_activated_tasks &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql.md)   
 [sys.dm_broker_queue_monitors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql.md)   
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
