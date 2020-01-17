---
title: 管理とトラブルシューティング
ms.date: 06/27/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, managing
- Stretch Database, troubleshooting
- managing Stretch Database
- troubleshooting Stretch Database
ms.assetid: 6334db3e-9297-44df-8d53-211187a95520
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 786ebc0529d9af47c34840e0e2cb11bf2a448fec
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/08/2019
ms.locfileid: "73844607"
---
# <a name="manage-and-troubleshoot-stretch-database"></a>Stretch Database の管理とトラブルシューティング
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database の管理とトラブルシューティングには、この記事で説明するツールとメソッドを使います。  
## <a name="manage-local-data"></a>ローカル データの管理  
  
###  <a name="LocalInfo"></a> Stretch Database が有効なローカル データベースとテーブルに関する情報を取得する  
 カタログ ビュー **sys.databases** と **sys.tables** を開き、Stretch 対応の SQL Server データベースとテーブルに関する情報を確認します。 詳細については、「[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)」と「[sys.tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)」を参照してください。  
 
 SQL Server で Stretch 対応テーブルが使用する領域の量を表示するには、次のステートメントを実行します。
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'LOCAL_ONLY';
GO
 ```
   
## <a name="manage-data-migration"></a>データ移行の管理  
  
### <a name="check-the-filter-function-applied-to-a-table"></a>テーブルに適用されたフィルター関数の確認  
 カタログ ビュー **sys.remote_data_archive_tables** を開き、 **filter_predicate** 列の値を確認し、移行する行を選択するために Strech Database が使用する関数を識別します。 値が null の場合、テーブル全体が移行の対象になります。 詳細については、「[sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)」と「[フィルター関数を使用して、移行する行を選択する](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md)」を参照してください。  
  
###  <a name="Migration"></a> データ移行の状態を確認する  
 Stretch Database モニターでデータ移行を監視するには、SQL Server Management Studio のデータベースで、 **[タスク]、[Stretch]、[モニター]** の順に選択します。 詳細については、「 [データ移行の監視とトラブルシューティング &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)」を参照してください。  
  
 または、動的管理ビュー **sys.dm_db_rda_migration_status** を開いて、移行されたバッチ数とデータ行数を確認します。  
  
###  <a name="Firewall"></a> データ移行のトラブルシューティング  
 トラブルシューティングの提案については、「 [データ移行の監視とトラブルシューティング &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)」を参照してください。  
  
## <a name="manage-remote-data"></a>リモート データの管理  
  
###  <a name="RemoteInfo"></a> Stretch Database に使用されるリモート データベースとテーブルに関する情報を取得する  
 カタログ ビュー **sys.remote_data_archive_databases** と **sys.remote_data_archive_tables** を開いて、移行されたデータが格納されているリモートのデータベースとテーブルに関する情報を参照します。 詳細については、「[sys.remote_data_archive_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md)」と「[sys.remote_data_archive_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-tables.md)」を参照してください。  
 
Azure で Stretch 対応テーブルが使用する領域の量を表示するには、次のステートメントを実行します。
 
 ```sql
USE <Stretch-enabled database name>;
GO
EXEC sp_spaceused '<Stretch-enabled table name>', 'true', 'REMOTE_ONLY';
GO
 ```

### <a name="delete-migrated-data"></a>移行データの削除  
既に Azure に移行したデータを削除する場合は、「 [sys.sp_rda_reconcile_batch](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-batch-transact-sql.md)」に記載された手順に従います。  
  
## <a name="manage-table-schema"></a>テーブル スキーマの管理

### <a name="dont-change-the-schema-of-the-remote-table"></a>リモート テーブルのスキーマは変更しないでください  
 Stretch Database 用に構成された SQL Server テーブルと関連付けてあるリモート Azure テーブルのスキーマは変更しないでください。 特に、列の前やデータ型は変更しないでください。 Stretch Database の機能によって、SQL Server テーブルのスキーマと関連するリモート テーブルのスキーマについて、さまざまな仮定を行います。 リモート スキーマを変更すると、変更したテーブルに対して Stretch Database は機能しなくなります。  

### <a name="reconcile-table-columns"></a>テーブル列の調整  
リモート テーブルから誤って列を削除した場合は、 **sp_rda_reconcile_columns** を実行し、リモート テーブルにはなく Stretch 対応 SQL Server テーブルに存在する列をリモート テーブルに追加します。 詳細については、「 [sys.sp_rda_reconcile_columns](../../relational-databases/system-stored-procedures/sys-sp-rda-reconcile-columns-transact-sql.md)」を参照してください。  
  
  > [!IMPORTANT]
  > **sp_rda_reconcile_columns** がリモート テーブルから誤って削除した列を再作成する場合、削除された列に属していたデータは復元されません。
  
**sp_rda_reconcile_columns** は、Stretch 対応の SQL Server テーブルにはなく、リモート テーブルに存在する列をリモート テーブルから削除しません。 Stretch 対応の SQL Server テーブルに存在しなくなったリモートの Azure テーブルに列が存在している場合、これらの余分な列が Stretch Database の正常な動作を妨げることはありません。 必要に応じて余分の列を手動で削除できます。  
 
## <a name="manage-performance-and-costs"></a>パフォーマンスとコストの管理  
  
### <a name="troubleshoot-query-performance"></a>クエリ パフォーマンスのトラブルシューティング  
  Stretch 対応テーブルを含むクエリの実行時間は、Stretch 対応にする前のテーブルよりも長くかかります。 クエリ パフォーマンスが大幅に低下する場合は、次の問題が発生していないか確認してください。  
  
-   Azure サーバーは、SQL Server とは異なる地域にありますか。 Azure サーバーが SQL Server と同じ地域になるように構成すると、SQL Server のネットワーク待機時間は軽減されます。  
  
-   ネットワークの状態が低下する可能性があります。 最近の問題または停止については、ネットワーク管理者に問い合わせてください。  
  
### <a name="increase-azure-performance-level-for-resource-intensive-operations-such-as-indexing"></a>インデックス作成など、リソースが消費される操作の Azure パフォーマンス レベルを増やします。  
 Stretch Database に構成されている大規模なテーブルに対してビルド、再構築、インデックスの再構成を行い、その間 Azure の移行済みデータに対する高負荷のクエリが予期される場合、操作の期間中に対応するリモート Azure データベースのパフォーマンス レベルを増やすことをお勧めします。 パフォーマンス レベルおよび料金の詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」を参照してください。  
  
### <a name="you-cant-pause-the-sql-server-stretch-database-service-on-azure"></a>Azure で SQL Server Stretch Database サービスを一時停止することはできません  
 適切なパフォーマンスと料金レベルを選択していることを確認します。 リソースを集中的に使用する操作のために一時的にパフォーマンス レベルを上げる場合は、操作の完了後、以前のレベルに復元します。 パフォーマンス レベルおよび料金の詳細については、「 [SQL Server Stretch Database の価格](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/)」を参照してください。  
   
 ## <a name="change-the-scope-of-queries"></a>クエリのスコープの変更  
 Stretch 対応テーブルに対するクエリは、既定ではローカルとリモートの両方のデータを返します。 すべてのユーザーによるすべてのクエリに対するクエリ スコープ、もしくは管理者による 1 つのクエリに対するクエリ スコープのみを変更することができます。  
   
 ### <a name="change-the-scope-of-queries-for-all-queries-by-all-users"></a>すべてのユーザーによるすべてのクエリのクエリ スコープの変更  
 すべてのユーザーによるすべてのクエリ スコープを変更するには、ストアド プロシージャ **sys.sp_rda_set_query_mode**を実行します。 スコープを縮小して、ローカル データだけをクエリするか、すべてのクエリを無効にするか、または既定の設定を復元することができます。 詳細については、「 [sys.sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md)」を参照してください。  
   
 ### <a name="queryHints"></a>管理者による 1 つのクエリに対するクエリ スコープの変更  
 db_owner ロールのメンバーが 1 つのクエリ スコープを変更するためには、**WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = *value*)** クエリ ヒントを SELECT ステートメントに追加します。 REMOTE_DATA_ARCHIVE_OVERRIDE クエリ ヒントには次の値を指定できます。  
 -   **LOCAL_ONLY**。 ローカル データだけをクエリします。  
   
 -   **REMOTE_ONLY**。 リモート データだけをクエリします。  
   
 -   **STAGE_ONLY**。 Stretch Database が移行対象の行をステージングし、移行後に指定した期間に移行済みの行を保持しているテーブル内のデータのみをクエリします。 このクエリ ヒントは、ステージング テーブルをクエリする唯一の方法です。  
  
たとえば、次のクエリではローカルの結果だけが返されます。  
  
 ```sql  
USE <Stretch-enabled database name>;
GO
SELECT * FROM <Stretch_enabled table name> WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = LOCAL_ONLY) WHERE ... ;
GO
```  
   
 ## <a name="adminHints"></a>管理者用の更新と削除を行う  
 既定では、Stretch 対応テーブルで、移行対象の行または既に移行された行に対して、UPDATE 操作または DELETE 操作を実行することはできません。 問題を修正する必要がある場合、**WITH (REMOTE_DATA_ARCHIVE_OVERRIDE = *値*)** クエリ ヒントをステートメントに追加することにより、db_owner ロールのメンバーが UPDATE 操作または DELETE 操作を実行できます。 REMOTE_DATA_ARCHIVE_OVERRIDE クエリ ヒントには次の値を指定できます。  
 -   **LOCAL_ONLY**。 ローカルのデータのみを更新または削除します。  
   
 -   **REMOTE_ONLY**。 リモートのデータのみを更新または削除します。  
   
 -   **STAGE_ONLY**。 Stretch Database が移行対象の行をステージングし、移行後に指定した期間に移行済みの行を保持しているテーブル内のデータのみを更新または削除します。  
  
## <a name="see-also"></a>参照  
 [データ移行の監視とトラブルシューティング &#40;Stretch Database&#41;](../../sql-server/stretch-database/monitor-and-troubleshoot-data-migration-stretch-database.md)   
[Stretch 対応データベースのバックアップ (Stretch Database)](../../sql-server/stretch-database/backup-stretch-enabled-databases-stretch-database.md)  
[Stretch 対応データベースの復元 (Stretch Database)](../../sql-server/stretch-database/restore-stretch-enabled-databases-stretch-database.md)  
  
  
