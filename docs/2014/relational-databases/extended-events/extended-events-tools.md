---
title: 拡張イベントのツール | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e26bc62f0e6b81b7b4ac8e1361d0a1ac31513ef6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63137050"
---
# <a name="extended-events-tools"></a>拡張イベントのツール
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント セッションの作成と管理には、次のツールを使用できます。  
  
-   データ定義言語 (DDL) ステートメント。 拡張イベント セッションの作成および変更に使用できます。  
  
-   動的管理ビュー、カタログ ビュー、およびシステム テーブル。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、セッション データやメタデータを取得することができます。 システム テーブルを使用すると、SQL トレース イベントのクラスや列と等価な既存の拡張イベントを特定できます。  
  
-   オブジェクト エクスプローラーの **[拡張イベント]** ノード。 セッションの開始、停止、削除のほか、セッション テンプレートのインポートとエクスポートを行うことができます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダー。 拡張イベント セッションの作成、変更、および管理に使用できる強力なツールです。 詳細については、「 [拡張イベントへの PowerShell プロバイダーの使用](use-the-powershell-provider-for-extended-events.md)」を参照してください。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]」を参照してください。 拡張イベントのトピックに用意されているコード サンプルを作成し、実行することができます。 詳細については、「 [オブジェクト エクスプローラー](../../ssms/object/object-explorer.md)」を参照してください。  
  
 自分が作成したセッション以外にも、サーバーには、既定のシステム正常性セッションが存在します。 このセッションは、パフォーマンスの問題をトラブルシューティングするのに役立つシステム データを収集します。 詳細については、「 [system_health セッションの使用](use-the-ssms-xe-profiler.md)」を参照してください。  
  
## <a name="ddl-statements"></a>DDL ステートメント  
 拡張イベント セッションを作成、変更、および削除するには、次の DDL ステートメントを使用します。  
  
|名前|説明|  
|----------|-----------------|  
|[CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)|イベントのソース、イベント セッション ターゲット、およびイベント セッション パラメーターを識別する拡張イベント セッション オブジェクトを作成します。|  
|[ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)|イベント セッションの開始および停止、またはイベント セッションの構成変更を行います。|  
|[DROP EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-event-session-transact-sql)|イベント セッションを削除します。|  
  
## <a name="catalog-views"></a>カタログ ビュー  
 イベント セッションの作成時に作成されたメタデータを取得するには、次のカタログ ビューを使用します。  
  
|名前|説明|  
|----------|-----------------|  
|[sys.server_event_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql)|すべてのイベント セッションの定義を一覧表示します。|  
|[sys.server_event_session_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql)|イベント セッションの各イベントのアクションごとに 1 行のデータを返します。|  
|[sys.server_event_session_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql)|イベント セッションのイベントごとに 1 行のデータを返します。|  
|[sys.server_event_session_fields &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql)|イベントおよびターゲットに明示的に設定されたカスタマイズ可能な列ごとに 1 行のデータを返します。|  
|[sys.server_event_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql)|イベント セッションのイベント ターゲットごとに 1 行のデータを返します。|  
  
## <a name="dynamic-management-views"></a>動的管理ビュー  
 セッション メタデータおよびセッション データを取得するには、次の動的管理ビューを使用します。 メタデータはカタログ ビューから取得され、セッション データはイベント セッションの開始時と実行時に作成されます。  
  
> [!NOTE]  
>  これらのビューには、セッションが開始されるまでセッション データは格納されません。  
  
|名前|説明|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql)|セッション ディスパッチャー プールに関する情報を返します。|  
|[sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)|イベント パッケージによって公開されるオブジェクトごとに 1 行のデータを返します。|  
|[sys.dm_xe_object_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql)|すべてのオブジェクトのスキーマ情報を返します。|  
|[sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)|拡張イベント エンジンに登録されているすべてのパッケージを一覧表示します。|  
|[sys.dm_xe_sessions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql)|アクティブな拡張イベント セッションに関する情報を返します。|  
|[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)|セッション ターゲットに関する情報を返します。|  
|[sys.dm_xe_session_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql)|セッション イベントに関する情報を返します。|  
|[sys.dm_xe_session_event_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql)|イベント セッション アクションに関する情報を返します。|  
|[sys.dm_xe_map_values &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql)|内部数値キーをユーザーが判読できるテキストにマッピングします。|  
|[sys.dm_xe_session_object_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql)|セッションにバインドされたオブジェクトの構成値を示します。|  
  
## <a name="system-tables"></a>システム テーブル  
 次のシステム テーブルを使用して、SQL トレース イベントのクラスおよび列と等価な拡張イベントの情報を取得します。  
  
|名前|説明|  
|----------|-----------------|  
|[trace_xe_event_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/extended-events-tables-trace-xe-event-map)|SQL トレース イベント クラスに割り当てられている拡張イベントのイベントごとに 1 行のデータを格納します。|  
|[trace_xe_action_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/extended-events-tables-trace-xe-action-map)|SQL トレース列 ID に割り当てられている拡張イベントのアクションごとに 1 行のデータを格納します。|  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](../views/views.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)   
 [SQL Server 拡張イベント テーブル &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/system-tables-transact-sql)   
 [system_health セッションの使用](use-the-ssms-xe-profiler.md)   
 [拡張イベントへの PowerShell プロバイダーの使用](use-the-powershell-provider-for-extended-events.md)  
  
  
