---
title: "SQL Server、Batch Resp Statistics オブジェクト | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLServer:Batch Resp Statistics
ms.assetid: a58e8733-6a8d-4b47-b5cb-042e813d808a
caps.latest.revision: 3
author: dagiro
ms.author: v-dagir
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc35f5f03d3b395fc09765fa8ac5ef8158ad8c51
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-batch-resp-statistics-object"></a>SQL Server、Batch Resp Statistics オブジェクト
**SQLServer:Batch Resp Statistics** パフォーマンス オブジェクトには、SQL Server バッチ応答時間を追跡するカウンターが用意されています。

次の表では、SQL Server の **Batch Resp Statistics** パフォーマンス オブジェクトについて説明します。


|**SQL Server Batch Resp Statistics カウンター**|Description|  
|-------------|-----------------|  
|**Batches >=000000ms & \<000001ms**|応答時間が 0 ミリ秒以上 1 ミリ秒未満の SQL バッチ数|
|**Batches >=000001ms & \<000002ms**|応答時間が 1 ミリ秒以上 2 ミリ秒未満の SQL バッチ数|
|**Batches >=000002ms & \<000005ms**|応答時間が 2 ミリ秒以上 5 ミリ秒未満の SQL バッチ数|
|**Batches >=000005ms & \<000010ms**|応答時間が 5 ミリ秒以上 10 ミリ秒未満の SQL バッチ数|
|**Batches >=000010ms & \<000020ms**|応答時間が 10 ミリ秒以上 20 ミリ秒未満の SQL バッチ数|
|**Batches >=000020ms & \<000050ms**|応答時間が 20 ミリ秒以上 50 ミリ秒未満の SQL バッチ数|
|**Batches >=000050ms & \<000100ms**|応答時間が 50 ミリ秒以上 100 ミリ秒未満の SQL バッチ数|
|**Batches >=000100ms & \<000200ms**|応答時間が 100 ミリ秒以上 200 ミリ秒未満の SQL バッチ数|
|**Batches >=000200ms & \<000500ms**|応答時間が 200 ミリ秒以上 500 ミリ秒未満の SQL バッチ数|
|**Batches >=000500ms & \<001000ms**|応答時間が 500 ミリ秒以上 1,000 ミリ秒未満の SQL バッチ数|
|**Batches >=001000ms & \<002000ms**|応答時間が 1,000 ミリ秒以上 2,000 ミリ秒未満の SQL バッチ数|
|**Batches >=002000ms & \<005000ms**|応答時間が 2,000 ミリ秒以上 5,000 ミリ秒未満の SQL バッチ数|
|**Batches >=005000ms & \<010000ms**|応答時間が 5,000 ミリ秒以上 10,000 ミリ秒未満の SQL バッチ数|
|**Batches >=010000ms & \<020000ms**|応答時間が 10,000 ミリ秒以上 20,000 ミリ秒未満の SQL バッチ数|
|**Batches >=020000ms & \<050000ms**|応答時間が 20,000 ミリ秒以上 50,000 ミリ秒未満の SQL バッチ数|
|**Batches >=050000ms & \<100000ms**|応答時間が 50,000 ミリ秒以上 100,000 ミリ秒未満の SQL バッチ数| 
|**Batches &gt;=100000ms**|応答時間が 100,000 ミリ秒以上の SQL バッチ数| 

オブジェクトの各カウンターには、次のインスタンスが含まれています。  
  
|アイテム|Description|  
|----------|-----------------|  
|**CPU Time:Requests**|要求に対して CPU が使用した時間。|  
|**CPU Time:Total(ms)**|バッチに対して CPU が使用した合計時間。|  
|**Elapsed Time:Requests**|要求の経過時間。|  
|**Elapsed Time:Total(ms)**|バッチの経過時間。|  

## <a name="see-also"></a>参照
[SQL Server の Plan Cache オブジェクト](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md)  
[リソースの利用状況の監視 (システム モニター)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  