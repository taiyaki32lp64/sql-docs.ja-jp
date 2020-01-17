---
title: XTP (インメモリ OLTP) パフォーマンス カウンター
ms.custom: seo-dt-2019
ms.date: 04/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f963d8d7fe186d889856c108de1541110beb16a3
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165510"
---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>SQL Server XTP (インメモリ OLTP) パフォーマンス カウンター
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、パフォーマンス モニターがインメモリ OLTP のアクティビティを監視するために使用できるオブジェクトとカウンターが用意されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降では、オブジェクトとカウンターがマシン上で指定した [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]バージョンのすべてのインスタンス間で共有されます。  
  
 以前は、オブジェクトおよびカウンター名は *XTP Cursors*のように、 **XTP**から始まりました。 現在は、 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]から始まり、名前は次のようなパターンとなります。  
  
-   **SQL Server** *\<バージョン>* **XTP Cursors**  
  
 *\<version>* の値は、2016 のようになります。  
  
##  <a name="SQLServerPOs"></a> SQL Server XTP パフォーマンス オブジェクト  
 次の表では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パフォーマンス オブジェクトについて説明します。  
  
|パフォーマンス オブジェクト|[説明]|  
|------------------------|-----------------|  
|[SQL Server の XTP Cursors](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|SQL Server XTP Cursors パフォーマンス オブジェクトには、インメモリ OLTP エンジンの内部カーソルに関連するカウンターが含まれています。 カーソルとは、インメモリ OLTP エンジンが [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを処理するために使用する、低レベルの構成要素です。 このため、通常はユーザー側でカーソルを直接管理することはありません。|  
|[SQL Server XTP Databases](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|SQL Server XTP Databases パフォーマンス オブジェクトは、インメモリ OLTP データベース固有のカウンターを提供します。|  
|[SQL Server XTP Garbage Collection](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|SQL Server XTP Garbage Collection パフォーマンス オブジェクトには、インメモリ OLTP エンジンのガベージ コレクターに関連するカウンターが含まれています。|  
|[SQL Server 2016 XTP IO ガバナー](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|SQL Server XTP IO ガバナーのパフォーマンス オブジェクトには、インメモリ OLTP IO レート ガバナーに関連するカウンターが含まれています。|
|[SQL Server XTP Phantom Processor](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|SQL Server XTP Phantom Processor パフォーマンス オブジェクトには、インメモリ OLTP エンジンのファントム処理サブシステムに関連するカウンターが含まれています。 このコンポーネントには、SERIALIZABLE 分離レベルで実行されているトランザクション内のファントム行を検出する役割があります。|  
|[SQL Server の XTP ストレージ](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|SQL Server XTP ストレージのパフォーマンス オブジェクトには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインメモリ OLTP のストレージに関連するカウンターが含まれています。|  
|[SQL Server XTP トランザクション ログ](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|SQL Server XTP トランザクション ログ パフォーマンス オブジェクトには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインメモリ OLTP トランザクション ログに関連するカウンターが含まれています。|  
|[SQL Server XTP トランザクション](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|SQL Server XTP トランザクション ログ パフォーマンス オブジェクトには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインメモリ OLTP のエンジン トランザクションに関連するカウンターが含まれています。|  
  
  
