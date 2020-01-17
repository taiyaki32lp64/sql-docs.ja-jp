---
title: sys. tables (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- tables_TSQL
- sys.tables_TSQL
- sys.tables
- tables
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tables catalog view
ms.assetid: 8c42eba1-c19f-4045-ac82-b97a5e994090
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d1a6d6be7a51cf03442bb5576556b10c5c099ab0
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983307"
---
# <a name="systables-transact-sql"></a>sys.tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内のユーザーテーブルごとに1行の値を返します。  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|\<継承された列 >||このビューが継承する列の一覧については、「 [sys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)」を参照してください。|  
|lob_data_space_id|**int**|0 以外の値は、このテーブルのラージ オブジェクト バイナリ (LOB) データを格納するデータ領域 (ファイル グループまたはパーティション構成) の ID です。 LOB データ型の例としては、 **varbinary (max)** 、 **varchar (max)** 、 **geography**、 **xml**などがあります。<br /><br /> 0 = テーブルには LOB データが含まれません。|  
|filestream_data_space_id|**int**|FILESTREAM ファイル グループまたは FILESTREAM ファイル グループから成るパーティション構成のデータ領域 ID です。<br /><br /> FILESTREAM ファイルグループの名前を報告するには、`SELECT FILEGROUP_NAME (filestream_data_space_id) FROM sys.tables`クエリを実行します。<br /><br /> sys.tables は、filestream_data_space_id = data_space_id で次のビューに結合できます。<br /><br /> -sys. ファイルグループ<br /><br /> -sys. partition_schemes<br /><br /> -sys. インデックス<br /><br /> -sys. allocation_units<br /><br /> -sys. fulltext_catalogs<br /><br /> -sys. data_spaces<br /><br /> -sys. destination_data_spaces<br /><br /> -sys. master_files<br /><br /> -sys. database_files<br /><br /> -backupfilegroup (filegroup_id での結合)|  
|max_column_id_used|**int**|このテーブルで使用される列 ID の最大値です。|  
|lock_on_bulk_load|**bit**|テーブルは、一括読み込みにロックされます。 詳細については、「[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。|  
|uses_ansi_nulls|**bit**|テーブルは、SET ANSI_NULLS データベース オプションが ON の場合に作成されます。|  
|is_replicated|**bit**|1 = テーブルは、スナップショット レプリケーションまたはトランザクション レプリケーションを使用してパブリッシュされます。|  
|has_replication_filter|**bit**|1 = テーブルにはレプリケーション フィルターがあります。|  
|is_merge_published|**bit**|1 = テーブルは、マージ レプリケーションを使用してパブリッシュされます。|  
|is_sync_tran_subscribed|**bit**|1 = テーブルは、即時更新サブスクリプションを使用してサブスクライブされます。|  
|has_unchecked_assembly_data|**bit**|1 = テーブルに、前回の ALTER ASSEMBLY で定義が変更されたアセンブリに依存する、持続データが含まれています。 次の DBCC CHECKDB または DBCC CHECKTABLE が正常に完了した後、は0にリセットされます。|  
|text_in_row_limit|**int**|text in row で許可される最大バイト数です。<br /><br /> 0 = text in row オプションは設定されていません。 詳細については、「[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。|  
|large_value_types_out_of_row|**bit**|1 = 大きい値の型は行外に格納されます。 詳細については、「[sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。|  
|is_tracked_by_cdc|**bit**|1 = テーブルで変更データ キャプチャが有効になっています。 詳細については、「 [sys &#40;. sp_cdc_enable_table transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)」を参照してください。|  
|lock_escalation|**tinyint**|テーブルの LOCK_ESCALATION オプションの値です。<br /><br /> 0 = TABLE<br /><br /> 1 = DISABLE<br /><br /> 2 = AUTO|  
|lock_escalation_desc|**nvarchar(60)**|テーブルの lock_escalation オプションについての説明テキストです。 有効値は、TABLE、AUTO、および DISABLE です。|  
|is_filetable|**bit**|**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> 1 = テーブルは FileTable です。<br /><br /> FileTables について詳しくは、「[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)」をご覧ください。|  
|durability|**tinyint**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> 返される値は次のとおりです。<br /><br /> 0 = SCHEMA_AND_DATA<br /><br /> 1 = SCHEMA_ONLY<br /><br /> 値 0 が既定値です。|  
|durability_desc|**nvarchar(60)**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> 使用できる値を次に示します。<br /><br /> SCHEMA_ONLY<br /><br /> SCHEMA_AND_DATA<br /><br /> 値 SCHEMA_AND_DATA は、テーブルが持続性のあるインメモリ テーブルであることを示します。 メモリ最適化テーブルの既定値は SCHEMA_AND_DATA です。 値 SCHEMA_ONLY は、メモリ最適化オブジェクトでは、データベースを再起動した場合にテーブル データの更新内容が保存されないことを示します。|  
|is_memory_optimized|**bit**|**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> 使用できる値を次に示します。<br /><br /> 0 = メモリ最適化ではありません。<br /><br /> 1 = メモリ最適化です。<br /><br /> 値 0 が既定の値です。<br /><br /> メモリ最適化テーブルは、メモリ内のユーザーテーブルです。スキーマは、他のユーザーテーブルと同様にディスクに保存されます。 メモリ最適化テーブルには、ネイティブコンパイルストアドプロシージャからアクセスできます。|  
|temporal_type|**tinyint**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> テーブルの型を表す数値。<br /><br /> 0 = NON_TEMPORAL_TABLE<br /><br /> 1 = HISTORY_TABLE<br /><br /> 2 = SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|temporal_type_desc|**nvarchar(60)**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> テーブルの種類のテキストの説明:<br /><br /> NON_TEMPORAL_TABLE<br /><br /> HISTORY_TABLE<br /><br /> SYSTEM_VERSIONED_TEMPORAL_TABLE|  
|history_table_id|**int**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。<br /><br /> (2, 4) で temporal_type ときに、履歴データを保持するテーブルの object_id を返します。それ以外の場合は、NULL を返します。|  
|is_remote_data_archive_enabled|**bit**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降および [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]<br /><br /> テーブルでは、拡張が有効ながあるかどうかを示します。<br /><br /> 0 = テーブルは Stretch が許可されていません。<br /><br /> 1 = テーブルは、拡張を有効にしました。<br /><br /> 詳細については、「 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)」を参照してください。|  
|is_external|**bit**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]、および [!INCLUDE[sssdwfull](../../includes/sssdwfull-md.md)]。<br /><br /> テーブルが外部テーブルであることを示します。<br /><br /> 0 = テーブルは、外部テーブルではありません。<br /><br /> 1 = テーブルは外部テーブルです。| 
|history_retention_period|**int**|**Applies to**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>History_retention_period_unit で指定された単位で表した、テンポラル履歴の保有期間を表す数値。 |  
|history_retention_period_unit|**int**|**Applies to**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>テンポラル履歴の保有期間の単位の種類を表す数値。 <br /><br />-1: 無制限 <br /><br />3: 日 <br /><br />4: 週 <br /><br />5: 月 <br /><br />6: 年 |  
|history_retention_period_unit_desc|**nvarchar(10)**|**Applies to**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]. <br/><br/>テンポラル履歴保有期間の単位の種類の説明テキスト。 <br /><br />INFINITE <br /><br />[DAY] <br /><br />[WEEK] <br /><br />[MONTH] <br /><br />[YEAR] |  
|is_node|**bit**|**適用対象**: [!INCLUDE[sssql17-md.md](../../includes/sssql17-md.md)] および [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。 <br/><br/>1 = これはグラフノードテーブルです。 <br /><br />0 = これはグラフノードテーブルではありません。 |  
|is_edge|**bit**|**適用対象**: [!INCLUDE[sssql17-md.md](../../includes/sssql17-md.md)] および [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。 <br/><br/>1 = これはグラフのエッジテーブルです。 <br /><br />0 = これは、グラフのエッジテーブルではありません。 |  

## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
 次の例は、主キーを持たないすべてのユーザー テーブルを返します。  
  
```  
SELECT SCHEMA_NAME(schema_id) AS schema_name  
    ,name AS table_name   
FROM sys.tables   
WHERE OBJECTPROPERTY(object_id,'TableHasPrimaryKey') = 0  
ORDER BY schema_name, table_name;  
GO  
  
```  
  
次の例では、一時的なデータがどのように関連する公開することができます。  
   
**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降と [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)]。
  
```  
SELECT T1.object_id, T1.name as TemporalTableName, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema,  
T2.name as HistoryTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema,  
T1.temporal_type_desc  
FROM sys.tables T1  
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id  
ORDER BY T1.temporal_type desc  
```  

次の例は、テンポラル履歴のリテンション期間に関する情報を公開する方法を示しています。  

**Applies to**: [!INCLUDE[sssdsfull](../../includes/sssdsfull-md.md)].  
  
```  
SELECT DB.is_temporal_history_retention_enabled, SCHEMA_NAME(T1.schema_id) AS TemporalTableSchema, 
T1.name as TemporalTableName, SCHEMA_NAME(T2.schema_id) AS HistoryTableSchema, T2.name as HistoryTableName,
T1.history_retention_period, T1.history_retention_period_unit_desc
FROM sys.tables T1  
OUTER APPLY (select is_temporal_history_retention_enabled from sys.databases where name = DB_NAME()) DB
LEFT JOIN sys.tables T2   
ON T1.history_table_id = T2.object_id WHERE T1.temporal_type = 2 
```  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
