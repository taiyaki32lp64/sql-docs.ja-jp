---
title: SQL Server:Buffer Node | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7e99c6e4f28ecef032ff3b793393e5465740156d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63250738"
---
# <a name="sql-serverbuffer-node"></a>SQL Server: Buffer Node
  **Buffer Node** オブジェクトは、 **Buffer Manager** オブジェクトで提供されるカウンターを補完するカウンターを提供します。 このオブジェクトを使用すると、各 NUMA (non-uniform memory access) ノードに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバッファー プール ページの配分を監視することができます。 使用中の NUMA ノードごとに **Buffer Node** オブジェクトのインスタンスがあります。 非 NUMA アーキテクチャでは、 **Buffer Node** オブジェクトのインスタンスが 1 つあります。  
  
## <a name="buffer-node-performance-objects"></a>Buffer Node パフォーマンス オブジェクト  
 次の表で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Node** パフォーマンス オブジェクトについて説明します。  
  
|SQL Server の Buffer Node カウンター|説明|  
|-------------------------------------|-----------------|  
|**Database pages**|データベースの内容が含まれたこのノード上のバッファー プール内のページ数を示します。|  
|**Page life expectancy**|ページが参照されないままこのノードのバッファー プールに存在する最小秒数を示します。|  
|**Local Node page lookups/sec**|このノードによって満たされた、このノードからの参照要求の数を示します。|  
|**Remote Note page lookups/sec**|他のノードによって満たされた、このノードからの参照要求の数を示します。|  
  
 SQL Server が非 NUMA ハードウェアで動作している場合は、 **Buffer Node** オブジェクトのカウンターと **Buffer Manager** オブジェクトのカウンターが一致します。  
  
 NUMA ハードウェアでは、すべての **Buffer Nodes** の各カウンターの合計は、対応する **Buffer Manager**のカウンターに一致します。  
  
> [!NOTE]  
>  カウンター値と合計が正確に一致しない場合があります。これは、カウンターが動的な性質を持っているためと、サンプリング精度によるものです。  
  
## <a name="see-also"></a>参照  
 [SQL Server: Buffer Manager オブジェクト](sql-server-buffer-manager-object.md)   
 [サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [リソースの利用状況の監視 &#40;System Monitor&#41;](monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)  
  
  
