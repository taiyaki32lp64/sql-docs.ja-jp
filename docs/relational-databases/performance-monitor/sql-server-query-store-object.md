---
title: SQL Server, クエリ ストア オブジェクト | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store object
- SQL Server:Query Store
ms.assetid: b4a04acd-0b66-44a5-b72d-1a45b49e13e6
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 08cc5200801b99442c8973583f4ab7caa9ea9fb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140727"
---
# <a name="sql-server-query-store-object"></a>SQL Server, クエリ ストア オブジェクト
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  クエリ ストア オブジェクトは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリソース使用率を監視するカウンターを提供し、クエリ テキスト、オブジェクト (ストアド プロシージャなど) の実行プランとランタイム統計情報、アドホックおよび準備された [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント、トリガーを格納します。  
  
 次の表では、 **SQLServer:Query Store**カウンターについて説明します。  
  
|SQL Server のクエリ ストア カウンター|[説明]|  
|-------------------------------------|-----------------|  
|**Query Store CPU usage (クエリ ストアの CPU 使用率)**|クエリ ストアの CPU の使用率を示します。|  
|**Query Store logical reads (クエリ ストアの論理読み取り数)**|クエリ ストアによって行われた論理読み取りの数を示します。|  
|**Query Store logical writes (クエリ ストアの論理書き込み数)**|クエリ ストアからフラッシュするためにキューに登録されているデータの量を示します。 キューへのアイテムの追加の頻度と遅延 (ランタイム統計情報を表します) は、データ フラッシュ間隔の設定によって制御されます。|  
|**Query Store physical reads (クエリ ストアの物理読み取り数)**|クエリ ストアによって行われた物理読み取りの数を示します。|  
  
 オブジェクトの各カウンターには、次のインスタンスが含まれています。  
  
|クエリ ストアのインスタンス|[説明]|  
|--------------------------|-----------------|  
|**_Total**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのインスタンスのクエリ ストアの情報です。|  
|\<データベース名>|このデータベースのクエリ ストアの情報です。|  
  
## <a name="see-also"></a>参照  
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [クエリ ストアのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)   
 [クエリ ストアのカタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)   
 [リソースの利用状況の監視 &#40;システム モニター&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
