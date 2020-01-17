---
title: SQL Server:Buffer Node | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Buffer Node
- Buffer Node object
ms.assetid: fd3f9f0f-7c38-4cfd-a0c5-ee93dd52d9a5
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 9011394dccf472499c1c8a8bd1023b7c23009883
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987210"
---
# <a name="sql-serverbuffer-node"></a>SQL Server: Buffer Node
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Buffer Node** オブジェクトは、 **Buffer Manager** オブジェクトで提供されるカウンターを補完するカウンターを提供します。 このオブジェクトを使用すると、各 NUMA (non-uniform memory access) ノードに対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバッファー プール ページの配分を監視することができます。 使用中の NUMA ノードごとに **Buffer Node** オブジェクトのインスタンスがあります。 非 NUMA アーキテクチャでは、 **Buffer Node** オブジェクトのインスタンスが 1 つあります。  
  
## <a name="buffer-node-performance-objects"></a>Buffer Node パフォーマンス オブジェクト  
 次の表で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Buffer Node** パフォーマンス オブジェクトについて説明します。  
  
|SQL Server の Buffer Node カウンター|[説明]|  
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
 [SQL Server: Buffer Manager オブジェクト](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [サーバー メモリに関するサーバー構成オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
  
