---
title: パフォーマンスの監視とチューニング | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- instances of SQL Server, monitoring performance
- monitoring server performance [SQL Server]
- Database Engine [SQL Server], performance
- monitoring performance [SQL Server], about performance
- server performance [SQL Server]
- monitoring performance [SQL Server]
- database performance [SQL Server], about performance
- tuning databases [SQL Server], about performance
- status information [SQL Server], performance monitoring
- database monitoring [SQL Server], about performance
- monitoring [SQL Server], queries performance
- server performance [SQL Server], about performance
- tuning databases [SQL Server]
- database performance [SQL Server]
- monitoring [SQL Server], server performance
- database monitoring [SQL Server]
- monitoring server performance [SQL Server], about monitoring server performance
ms.assetid: 87f23f03-0f19-4b2e-bfae-efa378f7a0d4
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fd6fdf81a74e015995f5bf9bd5500f196ccf5cc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020250"
---
# <a name="monitor-and-tune-for-performance"></a>パフォーマンスの監視とチューニング
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  データベースを監視する目的は、サーバーのパフォーマンスを評価することです。 適切な監視には、現在のパフォーマンスのスナップショットを定期的にキャプチャして問題の原因となっているプロセスを特定したり、長期にわたって継続的にデータを採取してパフォーマンスの傾向を追跡する作業が必要です。  
  
 データベース パフォーマンスの継続的な評価は、応答時間を最小限にし、スループットを最大限にして、最適なパフォーマンスを実現するために役立ちます。 パフォーマンスを最大限に高めるには、効率的なネットワーク トラフィック、ディスク I/O、および CPU 使用が重要です。 アプリケーションの要件を十分に分析し、データの論理構造と物理構造を理解し、データベースの使用状況を評価し、競合する処理 (オンライン トランザクション処理 (OLTP) と意思決定支援など) の関係を調整する必要があります。  
  
## <a name="monitoring-and-tuning-databases-for-performance"></a>パフォーマンスのためのデータベースの監視とチューニング  
 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] および Microsoft Windows オペレーティング システムでは、データベースの現在の状態を参照したり、状態の変化に伴うパフォーマンスを追跡するためのユーティリティが用意されています。 さまざまなツールや技法を使用して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を監視できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の監視は、次のことに役立ちます。  
  
-   パフォーマンスを向上できるかどうかの判断。 たとえば、頻繁に使用するクエリの応答時間を監視することで、テーブルに対するクエリまたはインデックスの変更が必要かどうかを判断できます。  
  
-   ユーザーの利用状況の評価。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続しようとするユーザーを監視することで、セキュリティが適切に設定されているかどうかを判断し、アプリケーションや開発システムをテストできます。 また、実行時に SQL クエリを監視することで、クエリが正しく作成され、期待どおりの結果が得られているかどうかを判断できます。  
  
-   問題のトラブルシューティングや、ストアド プロシージャなどのアプリケーション コンポーネントのデバッグ。  
  
## <a name="monitoring-in-a-dynamic-environment"></a>動的な環境での監視  
条件を変更すると、パフォーマンスが変化します。 評価では、ユーザー数の増加によるパフォーマンスの変化、ユーザーのアクセス方法と接続方法の変化、データベース コンテンツの増加、クライアント アプリケーションの変化、アプリケーション内のデータの変化、クエリの複雑化、およびネットワーク トラフィックの増加を確認できます。 ツールを使用してパフォーマンスを監視することにより、パフォーマンスの変化を、変化する条件と複雑なクエリに関連付けることができます。 **使用例:**  
  
-   頻繁に使用されるクエリの応答時間を監視することによって、クエリを実行するテーブルに対するクエリまたはインデックスの変更が必要かどうかを判断できます。  
  
-   実行時に [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリを監視することによって、クエリが正しく作成され、期待どおりの結果が得られているかどうかを判断できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続しようとするユーザーを監視することによって、セキュリティが適切に設定されているかどうかを判断でき、アプリケーションまたは開発システムをテストできます。  
  
応答時間は、クエリが処理されていることを視覚的に確認できる形式で、結果セットの先頭行をユーザーに返すのに必要な時間の長さです。 スループットは、指定した時間内にサーバーで処理されたクエリの合計数です。  
  
ユーザーの数が増えるにつれて、サーバーのリソースの競合も増えます。その結果、応答時間が長くなり、全般的なスループットが減少します。  
  
## <a name="monitoring-and-performance-tuning-tasks"></a>監視とパフォーマンス チューニングのタスク  
  
|トピック| タスク|  
|-----------|----------------------|  
|[SQL Server コンポーネントの監視](../../relational-databases/performance/monitor-sql-server-components.md)|利用状況モニター、拡張イベント、および動的管理ビューと関数など、SQL Server コンポーネントを監視するために必要な手順です。|  
|[パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)|ライブ クエリ統計、データベース エンジン チューニング アドバイザーなど、SQL Server で使用可能な監視およびチューニング ツールの一覧を示します。|  
|[クエリ調整アシスタントを使用したデータベースのアップグレード](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)|新しいデータベース互換性レベルにアップグレードする間に、ワークロードのパフォーマンスの安定を維持します。|  
|[クエリ ストアを使用したパフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)|クエリ ストアを使用して、自動的にクエリ、プラン、および実行時統計の履歴をキャプチャし、確認用に保持します。|  
|[パフォーマンスのベースラインの設定](../../relational-databases/performance/establish-a-performance-baseline.md)|パフォーマンスのベースラインの設定方法。|  
|[パフォーマンスの問題の特定](../../relational-databases/performance/isolate-performance-problems.md)|データベースのパフォーマンスの問題を特定します。|  
|[ボトルネックの特定](../../relational-databases/performance/identify-bottlenecks.md)|ボトルネックを特定するために、サーバーのパフォーマンスを監視および追跡します。|  
|[DMV を使用してビューの使用統計とパフォーマンスを確認する](../../relational-databases/performance/use-dmvs-determine-usage-performance-views.md)|クエリのパフォーマンスに関する情報を取得するために使用する方法とスクリプトについて説明します。|  
|[サーバーのパフォーマンスと利用状況の監視](../../relational-databases/performance/server-performance-and-activity-monitoring.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と、Windows のパフォーマンスと利用状況の監視ツールを使用します。|  
|[リソースの使用状況の監視](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)|システム モニター (perfmon とも呼ばれます) を使用して、パフォーマンス カウンターで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスを測定します。|  

  
## <a name="see-also"></a>参照  
 [エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)    
 [実行プランの比較と分析](../../relational-databases/performance/compare-and-analyze-execution-plans.md)    
 [実行プランの表示と保存](../../relational-databases/performance/display-and-save-execution-plans.md)    
  
  
