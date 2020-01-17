---
title: 拡張イベントのツール
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 811542608a33777a5e44183f65e44d8321a65c63
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75234630"
---
# <a name="extended-events-tools"></a>拡張イベントのツール

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張イベント セッションの作成と管理には、次のツールを使用できます。  
  
-   データ定義言語 (DDL) ステートメント。 拡張イベント セッションの作成および変更に使用できます。  
  
-   動的管理ビュー、カタログ ビュー、およびシステム テーブル。 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用して、セッション データやメタデータを取得することができます。 システム テーブルを使用すると、SQL トレース イベントのクラスや列と等価な既存の拡張イベントを特定できます。  
  
-   オブジェクト エクスプローラーの **[拡張イベント]** ノード。 セッションの開始、停止、削除のほか、セッション テンプレートのインポートとエクスポートを行うことができます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell プロバイダー。 拡張イベント セッションの作成、変更、および管理に使用できる強力なツールです。 詳細については、「 [拡張イベントへの PowerShell プロバイダーの使用](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)」を参照してください。  
  
-   [https://login.microsoftonline.com/consumers/]([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 拡張イベントのトピックに用意されているコード サンプルを作成し、実行することができます。 詳細については、「 [オブジェクト エクスプローラー](../../ssms/object/object-explorer.md)」を参照してください。  
  
 自分が作成したセッション以外にも、サーバーには、既定のシステム正常性セッションが存在します。 このセッションは、パフォーマンスの問題をトラブルシューティングするのに役立つシステム データを収集します。 詳細については、「 [system_health セッションの使用](../../relational-databases/extended-events/use-the-system-health-session.md)」を参照してください。  
  
## <a name="ddl-statements"></a>DDL ステートメント  
 拡張イベント セッションを作成、変更、および削除するには、次の DDL ステートメントを使用します。  
  
|Name|[説明]|  
|----------|-----------------|  
|[CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)|イベントのソース、イベント セッション ターゲット、およびイベント セッション パラメーターを識別する拡張イベント セッション オブジェクトを作成します。|  
|[ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)|イベント セッションの開始および停止、またはイベント セッションの構成変更を行います。|  
|[DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)|イベント セッションを削除します。|  
  
## <a name="catalog-views"></a>カタログ ビュー  
 イベント セッションの作成時に作成されたメタデータを取得するには、次のカタログ ビューを使用します。  
  
|Name|[説明]|  
|----------|-----------------|  
|[sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)|すべてのイベント セッションの定義を一覧表示します。|  
|[sys.server_event_session_actions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql.md)|イベント セッションの各イベントのアクションごとに 1 行のデータを返します。|  
|[sys.server_event_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql.md)|イベント セッションのイベントごとに行を返します。|  
|[sys.server_event_session_fields &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql.md)|イベントおよびターゲットに明示的に設定されたカスタマイズ可能な列ごとに 1 行のデータを返します。|  
|[sys.server_event_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql.md)|イベント セッションのイベント ターゲットごとに 1 行のデータを返します。|  
  
## <a name="dynamic-management-views"></a>動的管理ビュー  
 セッション メタデータおよびセッション データを取得するには、次の動的管理ビューを使用します。 メタデータはカタログ ビューから取得され、セッション データはイベント セッションの開始時と実行時に作成されます。  
  
> [!NOTE]  
>  これらのビューには、セッションが開始されるまでセッション データは格納されません。  
  
|Name|[説明]|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql.md)|セッション ディスパッチャー プールに関する情報を返します。|  
|[sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)|イベント パッケージによって公開されるオブジェクトごとに 1 行のデータを返します。|  
|[sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)|すべてのオブジェクトのスキーマ情報を返します。|  
|[sys.dm_xe_packages &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql.md)|拡張イベント エンジンに登録されているすべてのパッケージを一覧表示します。|  
|[sys.dm_xe_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql.md)|アクティブな拡張イベント セッションに関する情報を返します。|  
|[sys.dm_xe_session_targets &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)|セッション ターゲットに関する情報を返します。|  
|[sys.dm_xe_session_events &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql.md)|セッション イベントに関する情報を返します。|  
|[sys.dm_xe_session_event_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql.md)|イベント セッション アクションに関する情報を返します。|  
|[sys.dm_xe_map_values &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql.md)|内部数値キーをユーザーが判読できるテキストにマッピングします。|  
|[sys.dm_xe_session_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql.md)|セッションにバインドされたオブジェクトの構成値を示します。|  
  
## <a name="system-tables"></a>システム テーブル  
 次のシステム テーブルを使用して、SQL トレース イベントのクラスおよび列と等価な拡張イベントの情報を取得します。  
  
|Name|[説明]|  
|----------|-----------------|  
|[trace_xe_event_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)|SQL トレース イベント クラスに割り当てられている拡張イベントのイベントごとに 1 行のデータを格納します。|  
|[trace_xe_action_map &#40;Transact-SQL&#41;](../../relational-databases/system-tables/extended-events-tables-trace-xe-action-map.md)|SQL トレース列 ID に割り当てられている拡張イベントのアクションごとに 1 行のデータを格納します。|  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 拡張イベント テーブル &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/6d52ff03-f5aa-4f0f-8c98-9b49dc76f94e)   
 [system_health セッションの使用](../../relational-databases/extended-events/use-the-system-health-session.md)   
 [拡張イベントへの PowerShell プロバイダーの使用](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)  
  
  
