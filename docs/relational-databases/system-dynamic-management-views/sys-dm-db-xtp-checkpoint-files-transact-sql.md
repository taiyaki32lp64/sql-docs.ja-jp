---
title: sys.dm_db_xtp_checkpoint_files (Transact-SQL) |Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fb3aa62880de7013cf503e61eb2d86a3454c2350
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026910"
---
# <a name="sysdm_db_xtp_checkpoint_files-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  ファイル サイズ、物理的な場所、トランザクション ID など、チェックポイント ファイルに関する情報を表示します。  
  
> **注:** 現在のチェックポイントが閉じられていない、s の [状態] 列の`ys.dm_db_xtp_checkpoint_files`新しいファイルの UNDER CONSTRUCTION になります。 最後のチェックポイント以降のトランザクション ログ拡張のための十分ながある場合、または発行した場合に、チェックポイントが自動的に閉じられます、`CHECKPOINT`コマンド ([CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md))。  
  
 メモリ最適化ファイル グループは、内部的には、インメモリ テーブルの挿入および削除された行を格納するのに追加専用のファイルを使用します。 これらのファイルには 2 つの種類があります。 データ ファイルには、デルタ ファイルが削除された行への参照が含まれている挿入された行が含まれています。 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 新しいバージョンから大幅に異なるし、下位にあるトピックの説明は[SQL Server 2014](#bkmk_2014)します。  
  
 詳細については、「[メモリ最適化オブジェクト用ストレージの作成と管理](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)」を参照してください。  
  
##  <a name="bkmk_2016"></a> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] およびそれ以降  
 次の表に、列の`sys.dm_db_xtp_checkpoint_files`以降 **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|container_id|**int**|データまたはデルタ ファイルが含まれているコンテナー (sys.database_files で FILESTREAM 型のファイルとして表される) の ID。 内の file_id と結合[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)します。|  
|container_guid|**uniqueidentifier**|で、ルート、データまたはデルタ ファイルがの一部であるコンテナーの GUID です。 File_guid sys.database_files テーブルに結合します。|  
|checkpoint_file_id|**uniqueidentifier**|チェックポイント ファイルの GUID です。|  
|relative_file_path|**nvarchar (256)**|コンテナーにマップされている、ファイルのパスです。|  
|file_type|**smallint**|無料の場合は-1<br /><br /> データ ファイルは 0 です。<br /><br /> デルタ ファイルの場合は 1 です。<br /><br /> ルート ファイルの 2<br /><br /> 大きなデータ ファイルの 3|  
|file_type_desc|**nvarchar(60)**|無料として保守管理されてすべて FREE のファイルは、割り当てに使用できます。 無料のファイルは、システムによって予測されるニーズに応じてサイズを変更できます。 最大サイズは、1 GB です。<br /><br /> データにはデータ ファイルには、メモリ最適化テーブルに挿入された行が含まれます。<br /><br /> 差分にはデルタ ファイルには、削除されたデータ ファイル内の行への参照が含まれます。<br /><br /> ルートにはルート ファイルには、メモリ最適化テーブルとネイティブ コンパイル済みのオブジェクトのシステム メタデータが含まれます。<br /><br /> 大規模なデータの大きなデータ ファイルを含む (n)varchar(max) と varbinary (max) 列と列セグメントはメモリ最適化テーブルの列ストア インデックスの一部であるで挿入された値。|  
|internal_storage_slot|**int**|内部ストレージ配列でのファイルのインデックス。 ルートの場合、または 1 以外の状態を NULL になります。|  
|checkpoint_pair_file_id|**uniqueidentifier**|対応するデータまたはデルタ ファイルです。 ルートの場合は NULL。|  
|file_size_in_bytes|**bigint**|ディスク上のファイルのサイズです。|  
|file_size_used_in_bytes|**bigint**|データ格納中のチェックポイント ファイル ペアについては、この列は、次のチェックポイントの後に更新されます。|  
|logical_row_count|**bigint**|データの場合は、挿入された行の数です。<br /><br /> デルタでは、行の数は、テーブルのドロップのアカウンティングの後に削除されます。<br /><br /> ルートの場合、次のように NULL です。|  
|state|**smallint**|0 - 事前に作成されました。<br /><br /> 1-UNDER CONSTRUCTION<br /><br /> 2 - ACTIVE<br /><br /> 3 - ターゲットをマージします。<br /><br /> 8 - ログの切り捨てを待機しています|  
|state_desc|**nvarchar(60)**|PRECREATED のチェックポイント ファイルの数が事前に割り当てられたトランザクションが実行されているように、新しいファイルを割り当てるときの待機時間を排除または最小限にします。 推定、ワークロードのニーズに応じて、サイズを変更できるこれらのファイルを事前に作成されたが、データはありません。 これは、MEMORY_OPTIMIZED_DATA ファイル グループのデータベースでのストレージ オーバーヘッドです。<br /><br /> UNDER CONSTRUCTION - は、これらのチェックポイント ファイルは、データベースによって生成されたログ レコードに基づいて、登録されている、つまり、作成中と、まだチェックポイントの一部ではないです。<br /><br /> ACTIVE - 終了した前回のチェックポイントからパッケージを挿入または削除された行が含まれます。 領域は、データベースの再起動時にトランザクション ログのアクティブな部分を適用する前に、メモリに読み込まれるテーブルの内容が含まれます。 マージ操作を想定して、メモリ最適化テーブルのメモリ内サイズの約 2 x がトランザクションのワークロード維持するには、これらのチェックポイント ファイルのサイズを見込んでいます。<br /><br /> マージ ターゲット - マージ操作でこれらのチェックポイント ファイルのターゲットは、マージ ポリシーによって識別されたソース ファイルから統合されたデータ行を格納します。 マージをインストールした段階で、MERGE TARGET は ACTIVE 状態に遷移します。<br /><br /> マージがインストールされているし、MERGE TARGET CFP が持続性チェックポイントの場合は、この状態にマージ ソースのチェックポイント ファイルの遷移の一部は、ログの切り捨てを待機しています。 メモリ最適化テーブルでデータベースの正しい動作では、この状態のファイルが必要です。  たとえば、持続性チェックポイントから復元を行う際に、時間をさかのぼる目的で使用されます。|  
|lower_bound_tsn|**bigint**|ファイル内のトランザクションの下限の境界状態 (1, 3) に含まれない場合は null。|  
|upper_bound_tsn|**bigint**|ファイル内のトランザクションの上限状態 (1, 3) に含まれない場合は null。|  
|begin_checkpoint_id|**bigint**|開始チェックポイントの ID です。|  
|end_checkpoint_id|**bigint**|最後のチェックポイントの ID です。|  
|last_updated_checkpoint_id|**bigint**|このファイルを更新する最後のチェックポイントの ID です。|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar(60)**|0 = > UNENCRTPTED<br /><br /> 1 = > 1 のキーで暗号化<br /><br /> 2 = > 2 のキーで暗号化します。 アクティブなファイルのみ有効です。|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 次の表に、列の`sys.dm_db_xtp_checkpoint_files`の **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|container_id|**int**|データまたはデルタ ファイルが含まれているコンテナー (sys.database_files で FILESTREAM 型のファイルとして表される) の ID。 内の file_id と結合[sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)します。|  
|container_guid|**uniqueidentifier**|データまたはデルタ ファイルが含まれているコンテナーの GUID。|  
|checkpoint_file_id|**GUID**|データ ファイルまたはデルタ ファイルの ID。|  
|relative_file_path|**nvarchar (256)**|コンテナーの場所を基準とする、データ ファイルまたはデルタ ファイルの相対パス。|  
|file_type|**tinyint**|0 はデータ ファイルに対応。<br /><br /> 1 はデルタ ファイルに対応。<br /><br /> State 列が 7 に設定されている場合は NULL です。|  
|file_type_desc|**nvarchar(60)**|ファイルの種類:DATA_FILE、DELTA_FILE、または [状態] 列が 7 に設定されている場合は NULL です。|  
|internal_storage_slot|**int**|内部ストレージ配列でのファイルのインデックス。 State 列が 2 または 3 ではない場合は NULL です。|  
|checkpoint_pair_file_id|**uniqueidentifier**|対応するデータ ファイルまたはデルタ ファイル。|  
|file_size_in_bytes|**bigint**|使用されているファイルのサイズ。 State 列が 5、6、または 7 に設定されている場合は NULL です。|  
|file_size_used_in_bytes|**bigint**|使用されているファイルによる使用済みサイズ。 State 列が 5、6、または 7 に設定されている場合は NULL です。<br /><br /> データ格納中のチェックポイント ファイル ペアについては、この列は、次のチェックポイントの後に更新されます。|  
|inserted_row_count|**bigint**|データ ファイル内の行の数。|  
|deleted_row_count|**bigint**|デルタ ファイル内の削除された行の数。|  
|drop_table_deleted_row_count|**bigint**|drop table の影響を受けたデータ ファイル内の行数。 state 列が 1.に等しい場合にデータ ファイルに適用されます。<br /><br /> 削除されたテーブルについて、削除された行数を示します。 drop_table_deleted_row_count の統計情報は、削除されたテーブルの行に関するメモリ ガベージ コレクションが完了し、チェックポイントが作成されてから、コンパイルされます。 テーブルの削除に関する統計情報がこの列に反映される前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動した場合、復旧操作の一環として統計情報が更新されます。 復旧プロセスでは、削除されたテーブルの行は読み込まれません。 削除されたテーブルに関する統計情報は、読み込みフェーズ中にコンパイルされ、復旧が完了するとこの列で報告されます。|  
|state|**int**|0 - 事前に作成されました。<br /><br /> 1-UNDER CONSTRUCTION<br /><br /> 2 - ACTIVE<br /><br /> 3 - ターゲットをマージします。<br /><br /> 4-マージされたソース<br /><br /> 5-必要な FOR バックアップ/HA<br /><br /> 6 - 廃棄 (TOMBSTONE) に移行中<br /><br /> 7-廃棄 (TOMBSTONE)|  
|state_desc|**nvarchar(60)**|PRECREATED の少数のデータとデルタ ファイル ペア、チェックポイント ファイル ペア (Cfp) とも呼ばれますは、事前に割り当てられたトランザクションが実行されているように、新しいファイルを割り当てるときの待機時間を排除または最小限に保持されます。 これらは最大サイズで作成され、データ ファイルのサイズは 128 MB、デルタ ファイルのサイズは 8 MB になりますが、データは含まれません。 CFP の数は、8 を最小として、論理プロセッサまたはスケジューラの数に応じて計算されます (コアにつき 1 個で、最大値なし)。 これは、メモリ最適化テーブルのあるデータベースにおける固定のストレージ オーバーヘッドです。<br /><br /> UNDER CONSTRUCTION の新しく保存する Cfp のセットが挿入され、可能性がある最後のチェックポイント以降のデータ行を削除します。<br /><br /> ACTIVE - この中には、閉じられた前のチェックポイント以降に挿入された行と削除された行が含まれます。 これらの CFP には、データベースの再起動時に、トランザクション ログのアクティブな部分を適用する前に必要とされる、必須である挿入された行と削除された行すべてが含まれます。 マージ操作がトランザクション ワークロードにとって最新であることを想定すると、これらの CFP のサイズは、メモリ最適化されたテーブルのインメモリ サイズの約 2 倍です。<br /><br /> MERGE TARGET -、CFP は、マージ ポリシーによって識別された CFP から統合されたデータ行を格納します。 マージをインストールした段階で、MERGE TARGET は ACTIVE 状態に遷移します。<br /><br /> マージされたソース - 1 回のマージ操作がインストールされている、ソース Cfp は MERGED SOURCE としてマークされます。 マージ ポリシー エバリュエーターは複数のマージを識別できますが、各 CFP はただ 1 つのマージ操作のみに参加できます。<br /><br /> 必要な FOR BACKUP/HA - マージがインストールされると、MERGE TARGET CFP は、持続性チェックポイントの場合は、この状態に遷移の Cfp のマージ ソースの一部です。 この状態にある CFP は、メモリ最適化されたテーブルを持つデータベースを正しく運用するうえで必要とされます。  たとえば、持続性チェックポイントから復元を行う際に、時間をさかのぼる目的で使用されます。 ログの切り捨てポイントが CFP のトランザクション範囲を超えた位置に移動すれば、その CFP をガベージ コレクションの対象としてマークできます。<br /><br /> IN TRANSITION TO TOMBSTONE - これらの Cfp は、インメモリ OLTP エンジンによって不要し、することができますガベージ コレクションします。 この状態は、これらの CFP がバックグラウンド スレッドによって次の状態である TOMBSTONE に遷移されるのを待機していることを示します。<br /><br /> 廃棄 (tombstone) のこれらの Cfp は、filestream ガベージ コレクターによるガベージ コレクションを待機しています。 ([sp_filestream_force_garbage_collection &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|ファイルに含まれているトランザクションの下限。 State 列が 2、3、または 4 以外の場合は null です。|  
|upper_bound_tsn|**bigint**|ファイルに含まれているトランザクションの上限。 State 列が 2、3、または 4 以外の場合は null です。|  
|last_backup_page_count|**int**|最後のバックアップによって決定された論理ページ数。 State 列が 2、3、4、または 5 に設定されている場合に適用されます。 ページ数が不明な場合は NULL。|  
|delta_watermark_tsn|**int**|このデルタ ファイルへの書き込みを行った前回のチェックポイントのトランザクション。 これはデルタ ファイルのウォーターマークです。|  
|last_checkpoint_recovery_lsn|**nvarchar(23)**|引き続きファイルを必要としている前回のチェックポイントの復旧ログ シーケンス番号。|  
|tombstone_operation_lsn|**nvarchar(23)**|tombstone_operation_lsn が、ログの切り捨てに関するログ シーケンス番号より少ない場合は、このファイルは削除されます。|  
|logical_deletion_log_block_id|**bigint**|状態 5 にのみ適用されます。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する `VIEW DATABASE STATE` 権限が必要です。  
  
## <a name="use-cases"></a>ユース ケース  
 次のように、インメモリ OLTP で使用されるストレージを見積もることができます。  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
次のクエリを実行状態とファイルの種類別の記憶域使用率の内訳を参照してください。
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルの動的管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
