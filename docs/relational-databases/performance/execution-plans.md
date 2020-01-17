---
title: 実行プラン | Microsoft Docs
ms.custom: ''
ms.date: 10/28/2015
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server]
- execution plans [SQL Server]
- query execution plans
ms.assetid: 07f8f594-75b4-4591-8c29-d63811d7753f
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 9bf75c2d176c4ea2c596f29f1ddda910e794ae12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68232018"
---
# <a name="execution-plans"></a>実行プラン
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

クエリを実行するには、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] はステートメントを分析し、必要なデータにアクセスする最も効率的な方法を判断する必要があります。 この分析は、クエリ オプティマイザーと呼ばれているコンポーネントによって処理されます。 クエリ オプティマイザーへの入力は、クエリ、データベース スキーマ (テーブル定義やインデックスの定義)、およびデータベース統計で構成されます。 クエリ オプティマイザーの出力がクエリ実行プランです。これは、クエリ プランや単に実行プランと呼ばれることもあります。   

クエリ実行プランは、次の事項を定義しています。 

* 基になるテーブルにアクセスする順序  
  通常、データベース サーバーからベース テーブルにアクセスして結果セットを構築する順序は何とおりもあります。 たとえば、`SELECT` ステートメントが 3 つのテーブルを参照している場合、データベース サーバーは最初に `TableA` にアクセスし、`TableA` のデータを使用して `TableB` から一致する行を抽出します。次に、`TableB` のデータを使用して `TableC` のデータを抽出することができます。 データベースがテーブルにアクセスする際に可能な順序には、次の組み合わせがあります。  
  `TableC`、 `TableB`、 `TableA`、または  
  `TableB`、 `TableA`、 `TableC`、または  
  `TableB`、 `TableC`、 `TableA`、または  
  `TableC`、 `TableA`、 `TableB`  

* 各テーブルからデータを取り出す方法  
  通常、各テーブルのデータにアクセスする方法にも何とおりかあります。 特定のキー値を持つ数行だけが必要な場合、データベース サーバーではインデックスを使用できます。 テーブル内のすべての行が必要な場合は、インデックスを無視してテーブル スキャンを実行できます。 テーブル内のすべての行が必要で、 `ORDER BY`で指定されたキー列のインデックスがある場合、テーブル スキャンではなくインデックス スキャンを行うと、結果セットの並べ替えを個別に行わずに済みます。 テーブルが非常に小さい場合は、テーブルにどのようにアクセスするときでもテーブル スキャンが最も効率的な方法です。

> [!TIP]
> クエリ処理とクエリ実行プランの詳細については、「[クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容  
  
-   [クエリ プロファイリング インフラストラクチャ](../../relational-databases/performance/query-profiling-infrastructure.md)  
  
-   [実行プランの表示と保存](../../relational-databases/performance/display-and-save-execution-plans.md)  
  
-   [実行プランの比較と分析](../../relational-databases/performance/compare-and-analyze-execution-plans.md)  

-   [プラン ガイド](../../relational-databases/performance/plan-guides.md)  

## <a name="see-also"></a>参照  
 [パフォーマンスの監視とチューニング](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [クエリ処理アーキテクチャ ガイド](../../relational-databases/query-processing-architecture-guide.md)    
 [ライブ クエリ統計](../../relational-databases/performance/live-query-statistics.md)     
 [利用状況モニター](../../relational-databases/performance-monitor/activity-monitor.md)     
 [クエリのストアを使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [sys.dm_exec_query_statistics_xml](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-statistics-xml-transact-sql.md)     
 [sys.dm_exec_query_profiles](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-profiles-transact-sql.md)     
 [トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [プラン表示の論理操作と物理操作のリファレンス](../../relational-databases/showplan-logical-and-physical-operators-reference.md)
