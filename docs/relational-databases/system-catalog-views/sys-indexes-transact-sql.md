---
title: sys. indexes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3d4d307ea18127586ac46b0f6afb973ef62cf6ba
ms.sourcegitcommit: ede04340adbf085e668a2536d4f7114abba14a0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74761481"
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  テーブル、ビュー、テーブル値関数など、テーブル オブジェクトのインデックスまたはヒープごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**object_id**|**通り**|このインデックスが所属するオブジェクトの ID。|  
|**指定**|**sysname**|インデックスの名前。 **name**は、オブジェクト内でのみ一意です。<br /><br /> NULL = ヒープ|  
|**index_id**|**通り**|インデックスの ID。 **index_id**は、オブジェクト内でのみ一意です。<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化インデックス<br /><br /> > 1 = 非クラスター化インデックス|  
|**各種**|**tinyint**|インデックスの種類:<br /><br /> 0 = ヒープ<br /><br /> 1 = クラスター化<br /><br /> 2 = 非クラスター化<br /><br /> 3 = XML<br /><br /> 4 = 空間<br /><br /> 5 = クラスター化列ストアインデックス。 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降。<br /><br /> 6 = 非クラスター化列ストアインデックス。 **適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降。<br /><br /> 7 = 非クラスター化ハッシュインデックス。 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降。|  
|**type_desc**|**nvarchar (60)**|インデックスの種類の説明:<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> クラスター化列ストア: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降**に適用さ**れます。<br /><br /> 非クラスター化列ストア: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]以降**に適用さ**れます。<br /><br /> 非クラスター化ハッシュ: 非クラスター化ハッシュインデックスは、メモリ最適化テーブルでのみサポートされています。 sys.hash_indexes ビューでは、現在のハッシュ インデックスとハッシュ プロパティが表示されます。 詳細については、「 [sys. hash_indexes &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)」を参照してください。 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]以降。|  
|**is_unique**|**bit**|1 = インデックスは一意です。<br /><br /> 0 = インデックスは一意ではありません。<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**data_space_id**|**通り**|インデックスのデータ領域の ID。 データ領域は、ファイル グループまたはパーティション構成です。<br /><br /> 0 = **object_id**はテーブル値関数またはメモリ内インデックスです。|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY は ON です。<br /><br /> 0 = IGNORE_DUP_KEY はオフです。|  
|**is_primary_key**|**bit**|1 = インデックスは PRIMARY KEY 制約の一部です。<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**is_unique_constraint**|**bit**|1 = インデックスは UNIQUE 制約の一部です。<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**fill_factor**|**tinyint**|> 0 = インデックスが作成または再構築されたときに使用される FILLFACTOR のパーセンテージ。<br /><br /> 0 = 既定値<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**is_padded**|**bit**|1 = PADINDEX はオンです。<br /><br /> 0 = PADINDEX はオフです。<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**is_disabled**|**bit**|1 = インデックスは無効です。<br /><br /> 0 = インデックスは無効になっていません。|  
|**is_hypothetical**|**bit**|1 = インデックスは仮想的であり、データへのアクセス パスとして直接使用することはできません。 仮想インデックスは、列レベルの統計を保持しています。<br /><br /> 0 = インデックスは仮想的ではありません。|  
|**allow_row_locks**|**bit**|1 = インデックスは行ロックを許可します。<br /><br /> 0 = インデックスは行ロックを許可しません。<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**allow_page_locks**|**bit**|1 = インデックスはページロックを許可します。<br /><br /> 0 = インデックスはページロックを許可しません。<br /><br /> クラスター化列ストア インデックスの場合、常に 0 です。|  
|**has_filter**|**bit**|1 = インデックスにはフィルターがあり、フィルター定義を満たす行のみが含まれます。<br /><br /> 0 = インデックスにフィルターがありません。|  
|**filter_definition**|**nvarchar (max)**|フィルター選択されたインデックスに含まれる行のサブセットの式。<br /><br /> ヒープまたはフィルター選択されたインデックス以外のインデックスの場合は、NULL です。|  
|**auto_created**|**bit**|1 = インデックスは自動チューニングによって作成されました。<br /><br />0 = インデックスはユーザーによって作成されました。
|**optimize_for_sequential_key**|**bit**|1 = インデックスの最後のページ挿入最適化が有効になっています。<br><br>0 = 既定値。 インデックスの最後のページ挿入最適化が無効になっています。|

> [!NOTE]
> **Optimize_for_sequential_key**ビットは、2019 CTP 3.1 以降のバージョン SQL Server のみでサポートされています。
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="examples"></a>例  
 次の例では、 `Production.Product` [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]データベース内のテーブルのすべてのインデックスを返します。  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>参照  
 [オブジェクトカタログビュー &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Transact-sql&#41;&#40;カタログビュー](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [index_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [xml_indexes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [key_constraints &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. ファイルグループ &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [partition_schemes &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [SQL Server システムカタログに対するクエリについてよく寄せられる質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
