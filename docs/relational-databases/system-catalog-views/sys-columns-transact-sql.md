---
title: sys. columns (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.columns_TSQL
- sys.columns
- columns_TSQL
- columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.columns catalog view
ms.assetid: 323ac9ea-fc52-4b8c-8a7e-e0e44f8ed86c
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 64b4d3e1eb464481b076af86dbc018be72e93a6f
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981965"
---
# <a name="syscolumns-transact-sql"></a>sys.columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  ビューやテーブルなど、列を持つオブジェクトの列ごとに 1 行のデータを返します。 以下に、列を持つオブジェクトの種類の一覧を示します。  
  
-   テーブル値アセンブリ関数 (FT)  
  
-   インライン テーブル値 SQL 関数 (IF)  
  
-   内部テーブル (IT)  
  
-   システム テーブル (S)  
  
-   テーブル値 SQL 関数 (TF)  
  
-   ユーザー テーブル (U)  
  
-   ビュー (V)  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|object_id|**int**|この列が属するオブジェクトの ID です。|  
|name|**sysname**|列の名前です。 オブジェクト内で一意です。|  
|column_id|**int**|列の ID です。 オブジェクト内で一意です。<br /><br /> 列 ID は連続した値にならないことがあります。|  
|system_type_id|**tinyint**|列のシステム型の ID。|  
|user_type_id|**int**|ユーザーが定義した列の型の ID です。<br /><br /> 型の名前を返すには、この列で [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)カタログ ビューに結合します。|  
|max_length|**smallint**|列の最大長 (バイト単位) です。<br /><br /> -1 = 列のデータ型は**varchar (max)** ,、 **nvarchar (max)** ,、 **varbinary (max)** ,、または**xml**です。<br /><br /> **テキスト**列の場合、max_length 値は16か sp_tableoption ' text in row ' によって設定された値になります。|  
|有効桁数 (precision)|**tinyint**|数値ベースの場合は、列の有効桁数です。それ以外の場合は、0 です。|  
|scale|**tinyint**|数値ベースの場合の列の小数点以下桁数それ以外の場合は0です。|  
|collation_name|**sysname**|文字ベースの場合は、列の照合順序の名前です。それ以外の場合は、NULL です。|  
|is_nullable|**bit**|1 = 列で NULL 値を使用できます。|  
|is_ansi_padded|**bit**|1 = 文字、バイナリ、またはバリアントの場合、列で ANSI_PADDING ON 動作を使用します。<br /><br /> 0 = 列は文字、バイナリ、またはバリアントではありません。|  
|is_rowguidcol|**bit**|1 = 列は宣言された ROWGUIDCOL です。|  
|is_identity|**bit**|1 = 列に id 値がある|  
|is_computed|**bit**|1 = 列は計算列です。|  
|is_filestream|**bit**|1 = 列は FILESTREAM 列です。|  
|is_replicated|**bit**|1 = 列はレプリケートされています。|  
|is_non_sql_subscribed|**bit**|1 = 列は SQL Server 以外のサブスクライバーを持ちます。|  
|is_merge_published|**bit**|1 = 列はマージ パブリッシュされています。|  
|is_dts_replicated|**bit**|1 = 列は [!INCLUDE[ssIS](../../includes/ssis-md.md)] を使用してレプリケートされています。|  
|is_xml_document|**bit**|1 = 内容が完全な XML ドキュメントです。<br /><br /> 0 = コンテンツがドキュメントフラグメントであるか、列のデータ型が**xml**ではありません。|  
|xml_collection_id|**int**|列のデータ型が**xml**で xml が型指定されている場合は0以外の。 この値は、列の検証 XML スキーマ名前空間を含むコレクションの ID です。<br /><br /> 0 = XML スキーマコレクションがありません。|  
|default_object_id|**int**|既定のオブジェクトの ID を指定します。これは、スタンドアロンオブジェクトの[sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)、またはインラインの列レベルの既定の制約のいずれであるかには関係ありません。 インラインの列レベルの既定のオブジェクトの parent_object_id 列は、テーブル自体への参照です。<br /><br /> 0 = 既定値はありません。|  
|rule_object_id|**int**|sys.sp_bindrule を使用して列にバインドするスタンドアロン ルールの ID です。<br /><br /> 0 = スタンドアロン ルールはありません。 列レベルの CHECK 制約については、「 [sys. &#40;check_constraints&#41;transact-sql](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)」を参照してください。|  
|is_sparse|**bit**|1 = 列はスパース列です。 詳細については、「 [スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。|  
|is_column_set|**bit**|1 = 列は列セットです。 詳細については、「 [スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。|  
|generated_always_type|**tinyint**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 列の値が生成されることを示します (システムテーブルの列の場合は常に0になります)。<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> 詳細については、「[テンポラルテーブル&#40;リレーショナルデータベース&#41;](../../relational-databases/tables/temporal-tables.md)」を参照してください。|  
|generated_always_type_desc|**nvarchar(60)**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> `generated_always_type`の値の説明テキスト (常にシステムテーブルの列に対して NOT_APPLICABLE) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 暗号化の種類:<br /><br /> 1 = 決定的な暗号化<br /><br /> 2 = ランダム化暗号化|  
|encryption_type_desc|**nvarchar(64)**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 暗号化の種類の説明。<br /><br /> 化<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 暗号化アルゴリズムの名前。<br /><br /> AEAD_AES_256_CBC_HMAC_SHA_512 のみがサポートされているとします。|  
|column_encryption_key_id|**int**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> CEK の ID です。|  
|column_encryption_key_database_name|**sysname**|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、[!INCLUDE[ssSDW_md](../../includes/sssds-md.md)]。<br /><br /> 列のデータベースと異なる場合、列の暗号化キーが存在するデータベースの名前。 列と同じデータベースに、キーが存在する場合は NULL です。|  
|is_hidden|**bit**|**適用対象**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 列が非表示かどうかを示します。<br /><br /> 0 = 通常、非表示、表示列<br /><br /> 1 = 非表示の列|  
|is_masked|**bit**|**適用対象**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] 以降、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 動的データマスクによって列がマスクされているかどうかを示します。<br /><br /> 0 = 通常、マスクされていない列<br /><br /> 1 = 列はマスクされます。|  


 
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;transact-sql&#41; ](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [all_columns &#40;transact-sql&#41; ](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [system_columns &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
  
