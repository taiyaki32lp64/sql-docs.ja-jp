---
title: 拡張イベントの概要 - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: overview
helpviewer_keywords:
- extended events [SQL Server]
- xe
- XEvents
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4d829b32941ad1bc64df4e2e86cddb26d7468281
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313699"
---
# <a name="extended-events-overview"></a>拡張イベントの概要

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントのアーキテクチャを使用すると、ユーザーは、パフォーマンスの問題のトラブルシューティングや特定に必要最小限のデータを収集できます。 拡張イベントは構成可能で、スケーリングにとても優れています。

拡張イベントの詳細については、「[クイック スタート:SQL Server 拡張イベント](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)」を参照してください。

## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントの利点  

拡張イベントは軽量なパフォーマンス監視システムであり、使用されるパフォーマンス リソースは最小限です。 拡張イベントには、セッション データを作成、変更、表示、分析するためのグラフィカル ユーザー インターフェイスが 2 つ用意されています。 これらのインターフェイスには次の名前が付けられています。

- 新規セッション ウィザード
- 新しいセッション

## <a name="extended-events-concepts"></a>拡張イベントの概念  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベントは、イベントやイベント コンシューマーなどの既存の概念を基にし、Event Tracing for Windows の概念を使用し、新しい概念を導入しています。  
  
 次の表は、拡張イベントにおける各種の概念を示しています。  
  
|トピック|[説明]|  
|-----------|-----------------|  
|[SQL Server 拡張イベント パッケージ](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|オブジェクトを含む拡張イベント パッケージについて説明します。 これらのオブジェクトは、拡張イベント セッションの実行中にデータを取得して処理するために使用されます。|  
|[SQL Server 拡張イベント ターゲット](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|イベント セッション中にデータを受け取ることができるイベント コンシューマーについて説明します。|  
|[SQL Server 拡張イベント エンジン](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|拡張イベント セッションを実装および管理するエンジンについて説明します。|  
|[SQL Server 拡張イベント セッション](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|拡張イベント セッションについて説明します。|  
| &nbsp; | &nbsp; |
  
## <a name="extended-events-architecture"></a>拡張イベントのアーキテクチャ  

拡張イベントは、サーバー システム用の汎用的なイベント処理システムの名前です。 拡張イベント インフラストラクチャでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からのデータを相互に関連付けることができます。さらに、特定の条件下では、オペレーティング システムやデータベース アプリケーションからのデータを相互に関連付けることもできます。 オペレーティング システムのケースでは、拡張イベント出力を Event Tracing for Windows (ETW) に送る必要があります。 ETW は、イベント データをオペレーティング システムまたはアプリケーション イベント データに関連付けます。  

すべてのアプリケーションには、アプリケーションの内部と外部の両方で有用な実行ポイントが存在します。 アプリケーションの内部に目を向けると、非同期処理が、タスクの初回実行時に収集された情報を使ってエンキューされていることがあります。 アプリケーションの外部では、実行ポイントによって監視ユーティリティに情報が提供されます。 この情報は、監視対象アプリケーションの動作やパフォーマンス特性に関するものです。  

 拡張イベントを使用すると、プロセスの外部でイベント データを利用できます。 このデータは通常、次のようなツールやユーザーによって使用されます。  
  
-   トレース ツール (SQL トレース、システム モニターなど)。  
  
-   ログ ツール (Windows イベント ログ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログなど)。  
  
-   製品を管理するユーザー、または製品上でアプリケーションを開発するユーザー。  
  
 拡張イベントの設計には、次の大きな特徴があります。  
  
-   拡張イベント エンジンはイベントの種類に依存しません。 エンジンはイベントの内容による制約を受けないため、あらゆるイベントをあらゆるターゲットにバインドできます。 拡張イベント エンジンの詳細については、「 [SQL Server 拡張イベント エンジン](../../relational-databases/extended-events/sql-server-extended-events-engine.md)」を参照してください。  
  
-   イベントは、イベント コンシューマー (拡張イベントの *ターゲット* ) とは分離されています。 つまり、任意のターゲットが任意のイベントを受け取ることができます。 さらに、ターゲット側では、発生したあらゆるイベントを自動的に処理できるため、追加のイベント コンテキストを提供したりログに記録したりすることが可能となります。 詳細については、「 [SQL Server 拡張イベント ターゲット](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)」を参照してください。  
  
-   イベントは、イベントが発生した際に実行されるアクションとは異なります。 したがって、すべてのイベントには任意のアクションを関連付けることができます。  
  
-   述語を使用すると、イベント データのキャプチャ時に動的にフィルターが適用されます。 動的フィルター処理により、拡張イベント インフラストラクチャの柔軟性が高まります。 詳細については、「 [SQL Server 拡張イベント パッケージ](../../relational-databases/extended-events/sql-server-extended-events-packages.md)」を参照してください。  
  
 拡張イベントはイベント データを同期的に生成します。また、そのデータは非同期的に処理できるため、柔軟なイベント処理が可能となります。 さらに、拡張イベントには、次の機能が用意されています。  
  
-   サーバー システムの枠を越えてイベントを処理する統一的なアプローチ。同時に、ユーザーは特定のイベントを切り分けて、トラブルシューティングに役立てることができます。  
  
-   既存の ETW ツールのサポートと統合。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]に基づく自由な構成が可能なイベント処理メカニズム。  
  
-   アクティブ プロセスを最小限の負荷で動的に監視する機能。  
  
-   パフォーマンスへの体感的な影響を伴わずに動作する既定のシステム正常性セッション。 このセッションは、パフォーマンスの問題をトラブルシューティングするのに役立つシステム データを収集します。 詳細については、「 [system_health セッションの使用](../../relational-databases/extended-events/use-the-system-health-session.md)」を参照してください。  
  
## <a name="extended-events-tasks"></a>拡張イベントのタスク  

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)] を使用して [!INCLUDE[tsql](../../includes/tsql-md.md)] データ定義言語 (DDL) ステートメント、動的管理ビューおよび関数、カタログ ビューを実行することで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 環境の簡単、または複雑な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント トラブルシューティング ソリューションを作成することができます。  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|**オブジェクト エクスプローラー** を使用してイベント セッションを管理します。|[オブジェクト エクスプローラーでのイベント セッションの管理](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|拡張イベント セッションを作成する方法について説明します。|[拡張イベント セッションの作成](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|ターゲット データを表示および更新する方法について説明します。| [SQL Server での拡張イベントからのターゲット データの詳細表示](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント セッションを作成および管理するために、拡張イベントのツールを使用する方法について説明します。|[拡張イベントのツール](../../relational-databases/extended-events/extended-events-tools.md)|  
|拡張イベント セッションを変更する方法について説明します。|[拡張イベント セッションの変更](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|イベントに関連付けられているフィールドの情報を取得する方法について説明します。|[すべてのイベントのフィールドを取得する](https://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|登録パッケージで提供されているイベントを調べる方法について説明します。|[登録パッケージのイベントの表示](https://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|登録パッケージで提供されている拡張イベント ターゲットを確認する方法について説明します。|[登録パッケージの拡張イベント ターゲットの表示](https://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|SQL トレースのイベントとそれに関連した列について、拡張イベントにおける等価なイベントとアクションを確認する方法について説明します。|[SQL トレースのイベント クラスと等価な拡張イベントを確認する](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|CREATE EVENT SESSION または ALTER EVENT SESSION で ADD TARGET 引数を使用する際に設定できるパラメーターを確認する方法について説明します。|[ADD TARGET 引数の構成可能パラメーターの取得](https://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|既存の SQL トレース スクリプトを拡張イベント セッションに変換する方法について説明します。|[既存の SQL トレース スクリプトから拡張イベント セッションへの変換](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|ロックを保持しているクエリ、クエリのプラン、およびロックが取得されたときの [!INCLUDE[tsql](../../includes/tsql-md.md)] スタックを特定する方法について説明します。|[ロックを保持しているクエリの特定](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|データベース パフォーマンスを低下させているロックのソースを特定する方法について説明します。|[ロックの大半を取得しているオブジェクトを見つける](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|拡張イベントを Event Tracing for Windows と共に使用してシステムの使用状況を監視する方法について説明します。|[拡張イベントを使用したシステムの使用状況の監視](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
|拡張イベントに対するカタログ ビューと動的管理ビュー (DMV) の使用。 | [SQL Server の拡張イベントに対するシステム ビューからの SELECT と JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |
| &nbsp; | &nbsp; |

次の Transact-SQL (T-SQL) クエリを使用して、可能なすべての拡張イベントとその説明を一覧表示します。

```sql
SELECT
     obj1.name as [XEvent-name],
     col2.name as [XEvent-column],
     obj1.description as [Descr-name],
     col2.description as [Descr-column]
  FROM
               sys.dm_xe_objects        as obj1
      JOIN sys.dm_xe_object_columns as col2 on col2.object_name = obj1.name
  ORDER BY
    obj1.name,
    col2.name
```


## <a name="code-examples-can-differ-for-azure-sql-database"></a>Azure SQL Database では、コード例が異なる可能性があります。

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>参照

[データ層アプリケーション](../../relational-databases/data-tier-applications/data-tier-applications.md)  
[SQL Server オブジェクトとバージョンの DAC サポート](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)  
[データ層アプリケーションの配置](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)  
[データ層アプリケーションの監視](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)  
&nbsp;  
[拡張イベントの動的管理ビュー](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)  
[拡張イベント カタログ ビュー (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
&nbsp;  
[XELite: XEL ファイルまたはライブ SQL ストリームから XEvents を読み取るためのクロスプラットフォーム ライブラリ](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/)、2019 年 5 月リリース。  
[Read-SQLXEvent PowerShell コマンドレット](https://www.powershellgallery.com/packages/SqlServer.XEvent)、2019 年 6 月リリース。  
[SQL の謎:XEvent セッションの因果関係の追跡とイベント シーケンス (ブログ公開 2019 年 4 月 1 日)](https://bobsql.com/sql-mysteries-causality-tracking-vs-event-sequence-for-xevent-sessions/)  
