---
title: SQL トレースの最適化 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- time [SQL Server], traces
- SQL Trace, performance
- traces [SQL Server], performance
- performance [SQL Server], trace
ms.assetid: 50944218-925f-4576-aec8-4379846d7681
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3b29965c33270bbf8d9173c55e96af48b9c4f749
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63135537"
---
# <a name="optimize-sql-trace"></a>SQL トレースの最適化
  SQL トレースを実行すると、データを収集するためにシステム リソースが使用されるのでパフォーマンス コストが発生しますが、このコストはさまざまな方法で最小限に抑えることができます。 トレースによって発生するパフォーマンス コストを最小限に抑えるには、次のようにしてください。  
  
-   トレースの実行には、コマンド プロンプトを使用することを検討してください。 グラフィカル ユーザー インターフェイスを使用すると、パフォーマンスが低下します。 詳細については、「[sp_trace_create &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-create-transact-sql)」を参照してください。  
  
-   頻繁に発生するイベントは含めないようにします。 可能な場合は、特定のイベント クラスやフィルターを使用してトレースの範囲を狭くします。 収集するトレース イベントが少ないほど、トレースをサポートするために必要なシステム リソースも少なくて済みます。  
  
-   関連性のあるデータを提供するイベントだけを収集するようにトレースの焦点を絞ります。 たとえば、トレースでデッドロックを特定する場合は、 **Lock:Acquired** イベント クラスではなく **Lock:Deadlock** イベント クラスを使用します。 これらのイベント クラスを両方含めると、取得したすべてのロックをトレースしなければならないため、実行コストが倍増します。  
  
-   重複データは収集しないようにします。 たとえば、 **SQL:BatchStarted** と **SQL:BatchCompleted**を収集する場合は、 **SQL:BatchStarted** イベント クラスのテキスト データだけを収集することにより、結果セットのサイズを最小限に抑えることができます。  
  
-   トレース定義でフィルターを使用します。 たとえば、アドホック クエリの際のパフォーマンスの低下を報告しているユーザーがいる場合は、 **LoginName**に対するフィルターを作成します。 **LoginName** がこのユーザー名と一致するイベントだけを含めるように、フィルターを設定します。  
  
 パフォーマンスに重大な影響を与えるイベントのトレースを実行する必要がある場合は、次のいずれかの方法に従って、サーバーのパフォーマンスに対する影響を最小限に抑えるようにしてください。  
  
-   トレースの実行時間の短縮。 トレースの実行時間の長さは、停止時刻を有効にすることによって調整できます。 これは、イベント クラスの数を制限したり、イベントをフィルター選択したりすることができない場合に特に重要になります。 停止時刻を有効にすると、トレースによって発生するパフォーマンス コストが永続しなくなります。  
  
-   トレース結果のサイズの制限。 トレース結果のサイズの上限は、ファイルの最大サイズに設定できます。 この方法を採用すると、ファイル サイズの上限に達した時点でパフォーマンス コストが発生しなくなります (ファイル ロールオーバーが有効になっていない場合)。  
  
-   返されるイベントの数の制限。 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] を使用すると、トレースをテーブルに保存し、行の最大数を設定することにより、返されるイベントの数を制限することができます。 最大行数に達した後も、 [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)] の画面にはトレース結果が引き続き表示されますが、結果をテーブルに記録することによるコストは発生しなくなります。  
  
## <a name="see-also"></a>参照  
 [トレースへのフィルターの適用](../sql-trace/filter-a-trace.md)  
  
  
