---
title: Stretch Database の拡張イベント
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 70485e74-2e25-4e7e-be6c-9dd1780a42e3
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: be1cc04f4ee684fd2c97dd638038c6ce79d666fd
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844577"
---
# <a name="extended-events-for-stretch-database"></a>Stretch Database の拡張イベント
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


Stretch Database では、トラブルシューティングのための一連の拡張イベントを提供しています。  
  
詳細については、「 [拡張イベント](../../relational-databases/extended-events/extended-events.md)」を参照してください。 トラブルシューティングのために拡張イベント セッションを開始する方法の詳細については、「 [拡張イベント セッションの作成](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)」を参照してください。  
  
## <a name="list-of-extended-events-for-stretch-database"></a>Stretch Database の拡張イベントの一覧  
  
イベント名|イベントの説明   
---------|---------  
remote_data_archive_db_ddl|データをストレッチするためにデータベース T-SQL ddl が処理されると発生します。  
remote_data_archive_provision_operation|プロビジョニング操作の開始または終了時に生じます。  
remote_data_archive_query_rewrite|クエリがストレッチ用に書き直されるときに RelOp_Get が置換されると生じます。  
remote_data_archive_table_ddl|データをストレッチするためにテーブル T-SQL ddl が処理されると発生します。  
remote_data_archive_telemetry|オンプレミス システムでテレメトリ イベントが Azure DB 転送されたときに発生します。  
remote_data_archive_telemetry_rejected|AzureDB 拡張テレメトリ イベントが拒否されたときに発生します  
repopulate_stretch_schema_task_queue_complete|拡張スキーマ タスク キューの再作成の完了をレポートします。  
repopulate_stretch_schema_task_queue_start|拡張スキーマ タスク キューの再作成の開始をレポートします。  
stretch_codegen_errorlog|コード ジェネレーターの出力を報告します  
stretch_codegen_start|拡張コード生成の開始を報告します  
stretch_create_remote_table_start|リモート テーブル作成の開始を報告します  
stretch_database_disable_completed|ALTER DATABASE SET REMOTE_DATA_ARCHIVE OFF コマンドの完了を報告します  
stretch_database_enable_completed|ALTER DATABASE SET REMOTE_DATA_ARCHIVE ON コマンドの完了を報告します  
stretch_database_reauthorize_completed|sp_rda_reauthorize_db spec proc の完了をレポートします  
stretch_index_reconciliation_codegen_completed|拡張リモート インデックス操作用のコード生成の完了を報告します  
stretch_index_update_step_completed|拡張されたインデックス更新操作の期間を報告します  
stretch_migration_debug_trace|移行拡張アクションのデバッグ トレース。  
stretch_migration_dequeue_migration|ストレッチ移行タスクがデータベースに対してデキューされると生成されるイベント。  
stretch_migration_queue_migration|データベースとオブジェクトの移行を開始するためパケットをキューに入れます。  
stretch_migration_requeue_migration|ストレッチ移行タスク パケットがキューに再登録されると生成されるイベント。  
stretch_migration_start_migration|データベースとオブジェクトの移行を開始します。  
stretch_migration_start_unmigration|データベースとオブジェクトの移行取り消しを開始します。  
stretch_remote_column_execution_completed|ストレッチ列用に生成されたコードのリモート実行の完了を報告します  
stretch_remote_column_reconciliation_codegen_completed|ストレッチ リモート列調整用のコード生成の完了をレポートします  
stretch_remote_index_execution_completed|拡張インデックス用に生成されたコードのリモート実行の完了を報告します  
stretch_schema_queue_task|データベースとオブジェクトのスキーマのタスクを処理するためにパケットがキューに入ろうとしているときに報告します。  
stretch_schema_script_execution_completed|拡張スキーマ タスクの処理中に、拡張スクリプトの実行完了をレポートします。  
stretch_schema_script_execution_skipped|拡張スキーマ タスクの処理中に、拡張スクリプトの実行をスキップしたことをレポートします。  
stretch_schema_script_execution_start|拡張スキーマ タスクの処理中に、拡張スクリプトの実行開始をレポートします。  
stretch_schema_task_failed|拡張スキーマ タスクの実行中に拡張スキーマ関数でエラーが発生したことをレポートします。  
stretch_schema_task_skipped|ストレッチ スキーマ関数の段階でストレッチ スキーマ タスクがスキップされることをレポートします。  
stretch_schema_task_start|拡張スキーマ タスク中に、拡張スキーマ機能の開始を報告します。  
stretch_schema_task_succeeded|拡張スキーマ タスクの実行中に拡張スキーマ関数が正常に完了したことをレポートします。  
stretch_sp_migration_get_batch_id|Sp_stretch_get_batch_id を呼び出す  
stretch_sync_metadata_start|移行タスク時のメタデータ チェックの開始を報告します。  
stretch_table_codegen_completed|ストレッチされたテーブルのコード生成の完了を報告します  
stretch_table_complete_data_reconciliation|データベースとオブジェクトのデータ調整を完了します。  
stretch_table_data_reconciliation_event|行のバッチをデータ調整した場合の完了をレポートします  
stretch_table_data_reconciliation_results_event|行の多数のバッチをデータ調整した場合のエラーまたは正常な完了をレポートします  
stretch_table_hinted_admin_delete_event|管理者のヒントを使用するストレッチ削除 DML 操作の実行をレポートします  
stretch_table_hinted_admin_update_event|管理者のヒントを使用するストレッチ更新 DML 操作の実行をレポートします  
stretch_table_provisioning_step_completed|ストレッチされたテーブルのプロビジョニング操作の実行時間を報告します  
stretch_table_query_error|ストレッチ クエリ書き直しの間にスローされたエラーを報告します  
stretch_table_remote_creation_completed|ストレッチされたテーブルのために生成されたコードのリモート実行の完了を報告します  
stretch_table_row_migration_event|行のバッチの移行の完了を報告します  
stretch_table_row_migration_results_event|行の複数のバッチの移行のエラーまたは成功した完了を報告します  
stretch_table_row_unmigration_event|行のバッチの移行取り消しの完了を報告します  
stretch_table_row_unmigration_results_event|行の複数のバッチの移行取り消しのエラーまたは成功した完了を報告します  
stretch_table_start_data_reconciliation|データベースとオブジェクトのデータ調整を開始します。  
stretch_table_unprovision_completed|ストレッチされていないテーブルのローカル リソースの削除の完了を報告します  
stretch_table_validation_error|ユーザーが拡張を有効にした際のテーブルの検証の完了を報告します  
stretch_unprovision_table_start|拡張テーブル プロビジョニング解除の開始を報告します  
  
## <a name="see-also"></a>参照  
[Stretch Database の管理とトラブルシューティング](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  

