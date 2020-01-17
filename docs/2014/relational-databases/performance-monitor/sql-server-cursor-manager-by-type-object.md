---
title: 'SQL Server: Cursor Manager by Type オブジェクト | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35fa15dc6651d8bfd9b6d32cafd00cd47698560b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68206969"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>SQL Server: Cursor Manager by Type オブジェクト
  **SQLServer:Cursor Manager by Type** オブジェクトには、種類別にグループ化されたカーソルを監視するカウンターが用意されています。  
  
 次の表で、SQL Server **Cursor Manager by Type** カウンターについて説明します。  
  
|Cursor Manager by Type カウンター|説明|  
|-------------------------------------|-----------------|  
|**Active cursors**|アクティブなカーソルの数。|  
|**Cache Hit Ratio**|キャッシュ ヒットとキャッシュ参照の比率。|  
|**Cached Cursor Counts**|キャッシュ内の特定種類のカーソルの数。|  
|**Cursor Cache Use Count/sec**|キャッシュされている各種のカーソルが使用された時間。|  
|**Cursor memory usage**|カーソルによって消費されたメモリ量 (KB)。|  
|**Cursor Requests/sec**|サーバーが受け取った SQL カーソル要求の数。|  
|**Cursor worktable usage**|カーソルによって使用された作業テーブルの数。|  
|**Number of active cursor plans**|カーソル プランの数。|  
  
 オブジェクトの各カウンターには、次のインスタンスが含まれています。  
  
|Cursor Manager のインスタンス|説明|  
|-----------------------------|-----------------|  
|**_Total**|すべてのカーソルに関する情報。|  
|**API Cursor**|API カーソルのみに関する情報。|  
|**TSQL Global Cursor**|[!INCLUDE[tsql](../../includes/tsql-md.md)] グローバル カーソルのみに関する情報。|  
|**TSQL Local Cursor**|[!INCLUDE[tsql](../../includes/tsql-md.md)] ローカル カーソルのみに関する情報。|  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;システム モニター&#41;](monitor-resource-usage-system-monitor.md)  
  
  
