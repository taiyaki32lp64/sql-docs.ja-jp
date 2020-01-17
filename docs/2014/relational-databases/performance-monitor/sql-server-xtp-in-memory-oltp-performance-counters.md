---
title: XTP (インメモリ OLTP) パフォーマンス カウンター |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69b24c96e4833a45038bfcae20f0a5fecd0d2340
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63151137"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>XTP (インメモリ OLTP) パフォーマンス カウンター
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、パフォーマンス モニターがインメモリ OLTP のアクティビティを監視するために使用できるオブジェクトとカウンターが用意されています。  
  
##  <a name="SQLServerPOs"></a> XTP (インメモリ OLTP) パフォーマンス オブジェクト  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトについて説明します。  
  
|パフォーマンス オブジェクト|説明|  
|------------------------|-----------------|  
|[XTP Cursors](../cursors.md)|XTP Cursors パフォーマンス オブジェクトには、XTP エンジンの内部カーソルに関連するカウンターが含まれています。 カーソルとは、XTP エンジンが [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを処理するために使用する、低レベルの構成要素です。 このため、通常はユーザー側でカーソルを直接管理することはありません。|  
|[XTP Garbage Collection](sql-server-xtp-garbage-collection.md)|XTP Garbage Collection パフォーマンス オブジェクトには、XTP エンジンのガベージ コレクターに関連するカウンターが含まれています。|  
|[XTP Phantom Processor](sql-server-xtp-phantom-processor.md)|XTP Phantom Processor パフォーマンス オブジェクトには、XTP エンジンのファントム処理サブシステムに関連するカウンターが含まれています。 このコンポーネントには、SERIALIZABLE 分離レベルで実行されているトランザクション内のファントム行を検出する役割があります。|  
|[XTP ストレージ](sql-server-xtp-storage.md)|XTP ストレージのパフォーマンス オブジェクトには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の XTP ストレージに関連するカウンターが含まれています。|  
|[XTP Transaction Log](sql-server-xtp-transaction-log.md)|XTP Transaction Log パフォーマンス オブジェクトには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の XTP トランザクション ログに関連するカウンターが含まれています。|  
|[XTP Transactions](sql-server-xtp-transactions.md)|XTP Transactions パフォーマンス オブジェクトには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内の XTP エンジン トランザクションに関連するカウンターが含まれています。|  
  
  
