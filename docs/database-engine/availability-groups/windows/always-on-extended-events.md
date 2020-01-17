---
title: 可用性グループの拡張イベントを構成する
description: SQL Server では、Always On 可用性グループに固有の拡張イベントが定義されています。 可用性グループのトラブルシューティングの際、セッション内のこのような拡張イベントを監視すれば、根本原因を容易に診断することができます。
ms.custom: ag-guide, seodec18
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 5950f98a-3950-473d-95fd-cde3557b8fc2
author: rothja
ms.author: jroth
ms.openlocfilehash: d6fdf58703d448e07c9be063b616f90c72f2411d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67991556"
---
# <a name="configure-extended-events-for-always-on-availability-groups"></a>Always On 可用性グループの拡張イベントを構成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server では、Always On 可用性グループに固有の拡張イベントが定義されています。 可用性グループのトラブルシューティングの際、セッション内のこのような拡張イベントを監視すれば、根本原因を容易に診断することができます。 可用性グループの拡張イベントは、次のクエリを使用して表示することができます。  
  
```sql  
SELECT * FROM sys.dm_xe_objects WHERE name LIKE '%hadr%'  
```  
   
##  <a name="BKMK_alwayson_health"></a> Alwayson_health セッション  
 可用性グループを作成し、可用性グループ関連のイベントのサブセットをキャプチャすると、alwayson_health 拡張イベント セッションが自動的に作成されます。 このセッションは、可用性グループをトラブルシューティングする際にすぐに開始することができる有効かつ便利なツールとしてあらかじめ構成されています。 可用性グループの作成ウィザードでは、このウィザードで構成されたすべての参加中の可用性レプリカに対してセッションを自動的に開始します。  
  
> [!IMPORTANT]  
>  この**新しい可用性グループ ウィザード**を使用して可用性グループを作成していない場合、alwayson_health セッションは自動的に開始されない場合があります。 このセッションが開始していない場合は、予期せぬ問題が発生しても、イベント データをキャプチャすることはできません。 セッションを手動で開始してから、セッションのプロパティを設定してセッションが自動的に開始されるように構成する必要があります。  
  
 alwayson_health セッションの定義を表示するには:  
  
1.  **オブジェクト エクスプローラー**で **[管理]** 、 **[拡張イベント]** 、および **[セッション]** の順に展開します。  
  
2.  **[Alwayson_health]** を右クリックし、 **[セッションをスクリプト化]** 、 **[CREATE]** の順にポイントし、 **[新しいクエリ エディター ウィンドウ]** をクリックします。  

alwayson_health でカバーされているイベントの一部については、[拡張イベントのリファレンス](always-on-extended-events.md#BKMK_Reference)を参照してください。  


##  <a name="BKMK_Debugging"></a> デバッグ用の拡張イベント  
 Alwayson_health セッションでカバーされている拡張イベントに加えて、SQL Server では可用性グループ用のさまざまなデバッグ イベントが定義されています。 このような追加の拡張イベントをセッションで利用するには、以下の手順に従います。  
  
1.  **オブジェクト エクスプローラー**で **[管理]** 、 **[拡張イベント]** 、および **[セッション]** の順に展開します。  
  
2.  **[セッション]** を右クリックし、 **[新しいセッション]** をクリックします。 または、 **[Alwayson_health]** を右クリックし、 **[プロパティ]** を選択します。  
  
3.  **[ページの選択]** ウィンドウで **[イベント]** をクリックします。  
  
4.  イベント ライブラリの **[カテゴリ]** 列で **[alwayson]** を選択し、その他のカテゴリをすべてクリアします。  
  
5.  **[チャネル]** 列で、 **[デバッグ]** を選択します。 まだ選択されていない可用性グループの関連イベントがすべて、イベント ライブラリに表示されるようになります。  
  
6.  イベント ライブラリでイベントを強調表示し、 **[>]** ボタンをクリックしてそのイベントをセッションのために選択します。  
  
7.  セッションが終了したら、 **[OK]** をクリックしてセッションを閉じます。 セッションが開始されると、選択したイベントがキャプチャされることを確認してください。  
  
##  <a name="BKMK_Reference"></a> Always On 可用性グループの拡張イベントのリファレンス  
 このセクションでは、可用性グループを監視するために使用される一部の拡張イベントについて説明します。  
  
 [availability_replica_state_change](#BKMK_availability_replica_state_change)  
  
 [availability_group_lease_expired](#BKMK_availability_group_lease_expired)  
  
 [availability_replica_automatic_failover_validation](#BKMK_availability_replica_automatic_failover_validation)  
  
 [error_reported (複数のエラー番号): 転送または接続に問題がある場合](#BKMK_error_reported)  
  
 [data_movement_suspend_resume](#BKMK_data_movement_suspend_resume)  
  
 [alwayson_ddl_executed](#BKMK_alwayson_ddl_executed)  
  
 [availability_replica_manager_state](#BKMK_availability_replica_manager_state)  
  
 [error_reported (1480): データベース レプリカのロールの変更](#BKMK_error_reported_1480)  
  
###  <a name="BKMK_availability_replica_state_change"></a> availability_replica_state_change  
 可用性レプリカの状態が変化したときに発生します。 このイベントは、可用性グループの作成または可用性レプリカの追加によってトリガーすることができます。 失敗した自動フェールオーバーを診断する場合に便利です。 フェールオーバーの各手順をトレースするためにも使用できます。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|availability_replica_state_change|  
|カテゴリ|always on|  
|Channel|運用|  
  
#### <a name="event-fields"></a>イベント フィールド  
  
|[オブジェクト名]|Type_name|[説明]|  
|----------|----------------|-----------------|  
|availability_group_id|guid|可用性グループの ID。|  
|availability_group_name|unicode_string|可用性グループの名前です。|  
|availability_replica_id|guid|可用性レプリカの ID。|  
|previous_state|availability_replica_state|変更前のレプリカのロール。<br /><br /> **有効な値は次のとおりです。**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
|current_state|availability_replica_state|変更後のレプリカのロール。<br /><br /> **有効な値は次のとおりです。**<br /><br /> Primary_Normal<br /><br /> Secondary_Normal<br /><br /> Resolving_Pending_Failover<br /><br /> Resolving_Normal<br /><br /> Primary_Pending<br /><br /> Not_Available|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_replica_state_change  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_group_lease_expired"></a> availability_group_lease_expired  
 クラスターと可用性グループに接続の問題が存在し、リースの有効期限が切れた場合に発生します。 このイベントは可用性グループと基になる WSFC クラスター間の接続が切断されていることを示します。 プライマリ レプリカ上で接続の問題が発生した場合は、このイベントによって自動フェールオーバーが引き起こされるか、または可用性グループがオフラインになる可能性があります。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|availability_group_lease_expired|  
|カテゴリ|always on|  
|Channel|運用|  
  
#### <a name="event-fields"></a>イベント フィールド  
  
|[オブジェクト名]|Type_name|[説明]|  
|----------|----------------|-----------------|  
|availability_group_id|guid|可用性グループの ID。|  
|availability_group_name|unicode_string|可用性グループの名前です。|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT availability_group_lease_expired  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_replica_automatic_failover_validation"></a> availability_replica_automatic_failover_validation  
 自動フェールオーバーによって、プライマリ レプリカとしての可用性レプリカの準備状況が検証され、対象の可用性レプリカが新しいプライマリ レプリカになる準備が整っているかどうかが示される場合に発生します。 たとえば、同期または参加していないデータベースが存在する場合、フェールオーバーの検証では false が返されます。 このイベントは、フェールオーバー中に障害ポイントを示す設計になっています。 自動フェールオーバーは無人操作であるため、この情報は特に自動フェールオーバーに対応するデータベース管理者にとって有用です。 データベース管理者はイベントを検証することで、自動フェールオーバーが失敗した理由を確認できます。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|availability_replica_automatic_failover_validation||  
|カテゴリ|always on|  
|Channel|分析|  
  
#### <a name="event-fields"></a>イベント フィールド  
  
|[オブジェクト名]|Type_name|[説明]|  
|----------|----------------|-----------------|  
|availability_group_id|guid|可用性グループの ID。|  
|availability_group_name|unicode_string|可用性グループの名前です。|  
|availability_replica_id|guid|可用性レプリカの ID。|  
|forced_quorum|validation_result_type|値が TRUE の場合、この可用性レプリカでは自動フェールオーバーは無効になります。<br /><br /> TRUE<br /><br /> FALSE|  
|joined_and_synchronized|validation_result_type|値が FALSE の場合、この可用性レプリカでは自動フェールオーバーは無効になります。<br /><br /> TRUE<br /><br /> FALSE|  
|previous_primary_or_automatic_failover_target|validation_result_type|値が FALSE の場合、この可用性レプリカでは自動フェールオーバーは無効になります。<br /><br /> TRUE<br /><br /> FALSE|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_automatic_failover_validation (  
WHERE (  
[forced_quorum]=(TRUE) OR [joined_and_synchronized]=(FALSE) OR [previous_primary_or_automatic_failover_target]=(TRUE)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
  
```  
  
###  <a name="BKMK_error_reported"></a> error_reported (複数のエラー番号): 転送または接続に問題がある場合  
 フィルター処理した各イベントは、可用性グループが依存しているトランスポートまたはデータベース ミラーリング エンドポイントで接続の問題が発生したことを示します。  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|error_reported<br /><br /> フィルター処理する番号: 35201、35202、35206、35204、35207、9642、9666、9691、9692、9693、28034、28036、28080、28091、33309|  
|カテゴリ|エラー|  
|Channel|管理|  
  
#### <a name="error-numbers-to-filter"></a>フィルター処理するエラー番号  
  
|エラー番号|[説明]|  
|------------------|-----------------|  
|35201|可用性レプリカ '%ls' への接続を確立しようとしているときに接続タイムアウトが発生しました。|  
|35202|可用性グループ '%ls' での、ID [%ls] を持つ可用性レプリカ '%ls' から ID [%ls] を持つ可用性レプリカ '%ls' への接続が正常に確立されました。  このメッセージは情報提供だけを目的としています。 ユーザーによる操作は不要です。|  
|35206|可用性レプリカ '%ls' への確立済みの接続で接続タイムアウトが発生しました。|  
|35204|インスタンス '%ls' とインスタンス '%ls' との接続がエンドポイントのシャットダウンに起因して無効になりました。|  
|タイムアウト + 接続済み|  
|35207|可用性グループ ID '%ls' でのレプリカ ID '%ls' からレプリカ ID '%ls' への接続試行が、エラー %d、重大度 %d、状態 %d で失敗しました。  重大度 %d、状態: %d。 (DBA の使用が適切でない可能性があります。 確認し、問題がある場合は後で取り除いてください)|  
|9642|Service Broker/データベース ミラーリング トランスポートの接続エンドポイントでエラーが発生しました。エラー: %i、状態: %i。 (こちら側のエンドポイントのロール: %S_MSG、相手側のエンドポイントのアドレス: '%.*hs') エラー: %i、状態: %i。 (こちら側のエンドポイントのロール: %S_MSG、相手側のエンドポイントのアドレス: '%.\*hs')|  
|9666|%S_MSG エンドポイントは、状態が disabled または stopped です。|  
|9691|%S_MSG エンドポイントにより、接続のリッスンが停止されました。|  
|9692|ポート %d は他のプロセスで使用中なので、%S_MSG エンドポイントではそのポートでリッスンできません。|  
|9693|次のエラーが発生したので、%S_MSG エンドポイントでは接続をリッスンできませんでした: '%.*ls'。|  
|28034|接続ハンドシェイクが失敗しました。 ログイン '%.*ls' にはエンドポイントでの CONNECT 権限がありません。 状態 %d。|  
|28036|接続ハンドシェイクが失敗しました。 このエンドポイントで使用された証明書が見つかりませんでした: %S_MSG。 master データベースで DBCC CHECKDB を使用して、エンドポイントのメタデータの整合性を確認してください。 状態 %d。|  
|28080|接続ハンドシェイクが失敗しました。 %S_MSG エンドポイントが構成されていません。 状態 %d。|  
|28091|%S_MSG のエンドポイントを認証なしで開始することはサポートされていません。|  
|33309|既定の %S_MSG エンドポイント構成がまだ読み込まれていないので、クラスター エンドポイントを開始できません。|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--Connectivity Error Messages  
[error_number]=(35201)   
OR [error_number]=(35202)   
OR [error_number]=(35204)   
OR [error_number]=(35206)   
OR [error_number]=(35207)   
OR [error_number]=(9642)   
--OR [error_number]=(9666)   
OR [error_number]=(9691)   
OR [error_number]=(9692)   
OR [error_number]=(9693)   
OR [error_number]=(28034)   
OR [error_number]=(28036)   
OR [error_number]=(28080)   
OR [error_number]=(28091)   
OR [error_number]=(33309)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_data_movement_suspend_resume"></a> data_movement_suspend_resume  
 データベース レプリカのデータベース移動が中断または再開されたときに発生します。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|data_movement_suspend_resume|  
|カテゴリ|Always on|  
|Channel|運用|  
  
#### <a name="event-fields"></a>イベント フィールド  
  
||||  
|-|-|-|  
|[オブジェクト名]|Type_name|[説明]|  
|availability_group_id|guid|可用性グループの ID。|  
|availability_group_name|unicode_string|可用性グループの名前 (使用可能な場合)。|  
|availability_replica_id|guid|可用性レプリカの ID。|  
|database_replica_id|guid|可用性データベースの ID。|  
|database_replica_name|unicode_string|可用性データベースの名前です。|  
|database_id|uint32|可用性データベースの ID。|  
|suspend_status|suspend_status_type|中断状態を示す値。<br /><br /> SUSPEND_NULL<br /><br /> RESUMED<br /><br /> SUSPENDED<br /><br /> SUSPENDED_INVALID|  
|suspend_source|suspend_source_type|中断アクションまたは再開アクションのソース。|  
|suspend_reason|unicode_string|データベース レプリカ マネージャー内でキャプチャされた中断の理由。|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT data_movement_suspend_resume (  
WHERE (  
[suspend_status]=(SUSPENDED)or [suspend_status]=(SUSPENDED_INVALID) or   
[suspend_status]=(SUSPEND_NULL)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_alwayson_ddl_executed"></a> alwayson_ddl_executed  
 CREATE、ALTER、DROP などの可用性グループ データ定義言語 (DDL) ステートメントが実行されているときに発生します。 イベントの主な目的は、可用性レプリカでのユーザー アクションの問題を示すこと、または手動フェールオーバー、強制フェールオーバー、データ移動の中断、データ移動の再開などのランタイムの問題が続く運用アクションの開始ポイントを示すことです。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|alwayson_ddl_execution|  
|カテゴリ|always on|  
|Channel|分析|  
  
#### <a name="event-fields"></a>イベント フィールド  
  
|[オブジェクト名]|Type_name|[説明]|  
|----------|----------------|-----------------|  
|availability_group_id|Guid|可用性グループの ID。|  
|availability_group_name|unicode_string|可用性グループの名前です。|  
|ddl_action|alwayson_ddl_action|REATE、ALTER、DROP といった DDL アクションのCREATE、ALTER、または DROP。|  
|ddl_phase|ddl_opcode|BEGIN、COMMIT、ROLLBACK といった DDL 操作のBEGIN、COMMIT、または ROLLBACK。|  
|ステートメントから削除してください。|unicode_string|実行されたステートメントのテキスト。|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT alwayson_ddl_executed  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_availability_replica_manager_state"></a> availability_replica_manager_state  
 可用性レプリカ マネージャーの状態が変化したときに発生します。 このイベントは可用性レプリカ マネージャーのハートビートを示します。 可用性レプリカ マネージャーが正常な状態にない場合は、SQL Server インスタンス内のすべての可用性レプリカがダウンします。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|availability_replica_manager_state_change|  
|カテゴリ|always on|  
|Channel|運用|  
  
#### <a name="event-fields"></a>イベント フィールド  
  
|[オブジェクト名]|Type_name|[説明]|  
|----------|----------------|-----------------|  
|current_state|manager_state|可用性レプリカ マネージャーの現在の状態。<br /><br /> オンライン<br /><br /> Offline<br /><br /> WaitingForClusterCommunication|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
  
ADD EVENT availability_replica_manager_state (  
WHERE ([current_state]=(OFFLINE))  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
###  <a name="BKMK_error_reported_1480"></a> error_reported (1480): データベース レプリカのロールの変更  
 このフィルター処理された error_reported イベントは、可用性レプリカ ロールの変更後に非同期的に発生します。 フェールオーバー プロセス中に、想定したロールを変更できない可用性データベースを示します。  
  
#### <a name="event-information"></a>イベントに関する情報  
  
|[列]|[説明]|  
|------------|-----------------|  
|[オブジェクト名]|error_reported<br /><br /> エラー番号 1480: REPLICATION_TYPE_MSG データベース "DATABASE_NAME" は、REASON_MSG が原因で、"OLD_ROLE" から "NEW_ROLE" にロールを変更中です|  
|カテゴリ|エラー|  
|Channel|管理|  
  
#### <a name="alwaysonhealth-session-definition"></a>alwayson_health セッションの定義  
  
```sql  
CREATE EVENT SESSION [alwayson_health] ON SERVER   
ADD EVENT sqlserver.error_reported(  
    WHERE   
(  
--database replica role change message  
OR [error_number] = (1480)  
  
--database replica runtime error messages  
OR [error_number]=(823)   
OR [error_number]=(824)   
OR [error_number]=(829)  
)  
)  
  
ADD TARGET package0.event_file(SET filename=N'alwayson_health.xel',max_file_size=(5),max_rollover_files=(4),metadatafile=N'alwayson_health.xem')  
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)  
GO  
```  
  
## <a name="next-steps"></a>次の手順  
 [イベント セッション データの表示](https://msdn.microsoft.com/library/hh710068(v=sql.110).aspx)   
