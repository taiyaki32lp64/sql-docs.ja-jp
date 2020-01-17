---
title: 拡張イベント | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 485c748aad8b07a5e8b92a02c03d51a82e5f362a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990703"
---
# <a name="extended-events"></a>拡張イベント
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントのアーキテクチャは高い拡張性と柔軟な構成を備えており、これによってユーザーは、トラブルシューティングまたはパフォーマンスの問題の特定に必要な量の情報を過不足なく収集できます。  
  
 Web サイトで拡張イベントに関する詳細を検索する[SQL Server 拡張イベント](https://blogs.msdn.com/b/extended_events/)します。  
  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントの利点  
 拡張イベントは軽量なパフォーマンス監視システムであり、使用されるパフォーマンス リソースはごくわずかです。 拡張イベントには、セッション データを容易かつ迅速に作成、変更、表示、および分析するためのグラフィカル ユーザー インターフェイスが 2 つ用意されています (**新規セッション ウィザード** と **[新しいセッション]** )。  
  
## <a name="extended-events-concepts"></a>拡張イベントの概念  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントは、イベントやイベント コンシューマーなど、既存の概念を基にして、Event Tracing for Windows の概念や、新しい概念を導入したものです。  
  
 次の表は、拡張イベントにおける各種の概念を示しています。  
  
|トピック|説明|  
|-----------|-----------------|  
|[SQL Server 拡張イベント パッケージ](sql-server-extended-events-packages.md)|拡張イベント パッケージについて説明します。拡張イベント パッケージには、拡張イベント セッションを実行する際、データの取得と処理に使用されるオブジェクトが含まれます。|  
|[SQL Server 拡張イベント ターゲット](../../database-engine/sql-server-extended-events-targets.md)|イベント セッション中にデータを受け取ることができるイベント コンシューマーについて説明します。|  
|[SQL Server 拡張イベント エンジン](sql-server-extended-events-engine.md)|拡張イベント セッションを実装および管理するエンジンについて説明します。|  
|[SQL Server 拡張イベント セッション](sql-server-extended-events-sessions.md)|拡張イベント セッションについて説明します。|  
  
## <a name="extended-events-architecture"></a>拡張イベントのアーキテクチャ  
 拡張イベントは、サーバー システムの汎用的なイベント処理システムです。 拡張イベント インフラストラクチャでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのデータを相互に関連付けることができます。さらに、特定の条件下では、オペレーティング システムやデータベース アプリケーションからのデータを相互に関連付けることもできます。 後者の場合、イベント データをオペレーティング システムまたはアプリケーションのイベント データと相互に関連付けるためには、拡張イベント出力を Event Tracing for Windows (ETW) に送る必要があります。  
  
 すべてのアプリケーションには、アプリケーションの内部と外部の両方で有用な実行ポイントが存在します。 アプリケーションの内部に目を向けると、非同期処理が、タスクの初回実行時に収集された情報を使ってエンキューされていることがあります。 一方、アプリケーションの外部では、実行ポイントは、監視ユーティリティに対し、監視対象アプリケーションの動作やパフォーマンス特性に関する情報を提供します。  
  
 拡張イベントを使用すると、プロセスの外部でイベント データを利用できます。 このデータは通常、次のようなツールやユーザーによって使用されます。  
  
-   トレース ツール (SQL トレース、システム モニターなど)。  
  
-   ログ ツール (Windows イベント ログ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログなど)。  
  
-   製品を管理するユーザー、または製品上でアプリケーションを開発するユーザー。  
  
 拡張イベントの設計には、次の大きな特徴があります。  
  
-   拡張イベント エンジンはイベントの種類に依存しません。 イベントの内容による制約を受けないため、あらゆるイベントをあらゆるターゲットにバインドできます。 拡張イベント エンジンの詳細については、「 [SQL Server 拡張イベント エンジン](sql-server-extended-events-engine.md)」を参照してください。  
  
-   イベントは、イベント コンシューマー (拡張イベントの *ターゲット* ) とは分離されています。 つまり、任意のターゲットが任意のイベントを受け取ることができます。 さらに、ターゲット側では、発生したあらゆるイベントを自動的に処理できるため、追加のイベント コンテキストを提供したりログに記録したりすることが可能となります。 詳細については、「 [SQL Server 拡張イベント ターゲット](../../database-engine/sql-server-extended-events-targets.md)」を参照してください。  
  
-   イベントは、イベントが発生した際に実行されるアクションとは異なります。 したがって、すべてのイベントには任意のアクションを関連付けることができます。  
  
-   述語を使用すると、イベント データのキャプチャ時に動的にフィルターが適用されます。 この機能が拡張イベント インフラストラクチャの柔軟性を高めています。 詳細については、「 [SQL Server 拡張イベント パッケージ](sql-server-extended-events-packages.md)」を参照してください。  
  
 拡張イベントはイベント データを同期的に生成します。また、そのデータは非同期的に処理できるため、柔軟なイベント処理が可能となります。 さらに、拡張イベントには、次の機能が用意されています。  
  
-   サーバー システムの枠を越えてイベントを処理する統一的なアプローチ。同時に、ユーザーは特定のイベントを切り分けて、トラブルシューティングに役立てることができます。  
  
-   既存の ETW ツールのサポートと統合。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]に基づく自由な構成が可能なイベント処理メカニズム。  
  
-   アクティブ プロセスを最小限の負荷で動的に監視する機能。  
  
-   パフォーマンスへの体感的な影響を伴わずに動作する既定のシステム正常性セッション。 このセッションは、パフォーマンスの問題をトラブルシューティングするのに役立つシステム データを収集します。 詳細については、「 [system_health セッションの使用](use-the-ssms-xe-profiler.md)」を参照してください。  
  
## <a name="extended-events-tasks"></a>拡張イベントのタスク  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] データ定義言語 (DDL) ステートメント、動的管理ビューおよび関数、カタログ ビューを実行することで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境の簡単、または複雑な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント トラブルシューティング ソリューションを作成することができます。  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|**オブジェクト エクスプローラー** を使用してイベント セッションを管理します。|[オブジェクト エクスプローラーでのイベント セッションの管理](../../ssms/object/object-explorer.md)|  
|拡張イベント セッションを作成する方法について説明します。|[拡張イベント セッションの作成](../../database-engine/create-an-extended-events-session.md)|  
|ターゲット データを表示および更新する方法について説明します。|[イベント セッション データの表示](../../database-engine/view-event-session-data.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント セッションを作成および管理するために、拡張イベントのツールを使用する方法について説明します。|[拡張イベントのツール](extended-events-tools.md)|  
|拡張イベント セッションを変更する方法について説明します。|[拡張イベント セッションの変更](alter-an-extended-events-session.md)|  
|ターゲット データをコピーまたはエクスポートする方法について説明します。|[ターゲット データのコピーまたはエクスポート](../../database-engine/copy-or-export-target-data.md)|  
|トレース結果ビューを変更してデータの分析方法をカスタマイズする方法について説明します。|[トレース結果の表示の変更](../../database-engine/modify-the-trace-results-view.md)|  
|イベントに関連付けられているフィールドの情報を取得する方法について説明します。|[すべてのイベントのフィールドを取得する](../../database-engine/get-the-fields-for-all-events.md)|  
|登録パッケージで提供されているイベントを調べる方法について説明します。|[登録パッケージのイベントの表示](../../database-engine/view-the-events-for-registered-packages.md)|  
|登録パッケージで提供されている拡張イベント ターゲットを確認する方法について説明します。|[登録パッケージの拡張イベント ターゲットの表示](../../database-engine/view-the-extended-events-targets-for-registered-packages.md)|  
|SQL トレースのイベントとそれに関連した列について、拡張イベントにおける等価なイベントとアクションを確認する方法について説明します。|[SQL トレースのイベント クラスと等価な拡張イベントを確認する](view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|CREATE EVENT SESSION または ALTER EVENT SESSION で ADD TARGET 引数を使用する際に設定できるパラメーターを確認する方法について説明します。|[ADD TARGET 引数の構成可能パラメーターの取得](../../database-engine/get-the-configurable-parameters-for-the-add-target-argument.md)|  
|既存の SQL トレース スクリプトを拡張イベント セッションに変換する方法について説明します。|[既存の SQL トレース スクリプトから拡張イベント セッションへの変換](convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|ロックを保持しているクエリ、クエリのプラン、およびロックが取得されたときの [!INCLUDE[tsql](../../includes/tsql-md.md)] スタックを特定する方法について説明します。|[ロックを保持しているクエリの特定](determine-which-queries-are-holding-locks.md)|  
|データベース パフォーマンスを低下させているロックのソースを特定する方法について説明します。|[ロックの大半を取得しているオブジェクトを見つける](find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|拡張イベントを Event Tracing for Windows と共に使用してシステムの使用状況を監視する方法について説明します。|[拡張イベントを使用したシステムの使用状況の監視](monitor-system-activity-using-extended-events.md)|  
  
## <a name="see-also"></a>参照  
 [[データ層アプリケーション]](../data-tier-applications/data-tier-applications.md)   
 [SQL Server オブジェクトとバージョンの DAC サポート](../data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [データ層アプリケーションの配置](../data-tier-applications/deploy-a-data-tier-application.md)   
 [データ層アプリケーションの監視](../data-tier-applications/monitor-data-tier-applications.md)   
 [拡張イベントの動的管理ビュー](../views/views.md)   
 [拡張イベント カタログ ビュー &#40;TRANSACT-SQL&#41;](~/relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql  
  
  
