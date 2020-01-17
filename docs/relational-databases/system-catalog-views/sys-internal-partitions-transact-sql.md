---
title: internal_partitions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0d1e6e4fa9c88fc67b15a076a6c96a742fd7fdc
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304812"
---
# <a name="sysinternal_partitions-transact-sql"></a>internal_partitions (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  ディスクベーステーブルの列ストアインデックスの内部データを追跡する行セットごとに1行のデータを返します。 これらの行セットは、列ストアインデックスの内部にあり、削除された行、行グループのマッピング、およびデルタストアの行グループを追跡します。 各テーブルパーティションのデータを追跡します。各テーブルには、少なくとも1つのパーティションがあります。 列ストアインデックスを再構築するたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって行セットが再作成されます。   
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|このパーティションのパーティション ID。 これは、データベース内で一意です。|  
|object_id|**int**|パーティションを含むテーブルのオブジェクト ID。|  
|index_id|**int**|テーブルで定義されている列ストアインデックスのインデックス ID。<br /><br /> 1 = クラスター化列ストアインデックス<br /><br /> 2 = 非クラスター化列ストアインデックス|  
|partition_number|**int**|パーティションの数です。<br /><br /> 1 = パーティションテーブルの最初のパーティション、または非パーティションテーブルの1つのパーティション。<br /><br /> 2 = 2 番目のパーティション。|  
|internal_object_type|**tinyint**|列ストアインデックスの内部データを追跡する行セットオブジェクト。<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP-このビットマップインデックスは、列ストアから削除済みとしてマークされている行を追跡します。 ビットマップは、複数の行グループにパーティションを含めることができるため、すべての行グループに対して使用されます。 行は依然として物理的に存在し、列ストアの領域を占有しています。<br /><br /> COLUMN_STORE_DELTA_STORE-単票形式のストレージに圧縮されていない行グループと呼ばれる行のグループを格納します。 各テーブルパーティションには、0個以上のデルタストア行グループを含めることができます。<br /><br /> COLUMN_STORE_DELETE_BUFFER-更新可能な非クラスター化列ストアインデックスの削除を維持するために使用します。 クエリによって基になる行ストアテーブルから行が削除されると、削除バッファーは列ストアから削除を追跡します。 削除された行の数が1048576を超えると、バックグラウンドのタプルムーバースレッドまたは明示的な再編成コマンドによって、delete ビットマップに再びマージされます。  特定の時点で、削除ビットマップと削除バッファーの和集合は、削除されたすべての行を表します。<br /><br /> COLUMN_STORE_MAPPING_INDEX-クラスター化列ストアインデックスにセカンダリ非クラスター化インデックスがある場合にのみ使用されます。 これにより、非クラスター化インデックスキーが列ストアの正しい行グループと行 ID にマップされます。 別の行グループに移動する行のキーのみを格納します。このエラーは、デルタ行グループが列ストアに圧縮され、マージ操作によって2つの異なる行グループの行がマージされた場合に発生します。|  
|Row_group_id|**int**|デルタストアの行グループの ID。 各テーブルパーティションには、0個以上のデルタストア行グループを含めることができます。|  
|hobt_id|**bigint**|内部行セットオブジェクト (HoBT) の ID。 これは、内部行セットの物理的特性に関する詳細情報を取得するために、他の Dmv と結合するのに適したキーです。|  
|rows|**bigint**|このパーティション内の行の概数です。|  
|data_compression|**tinyint**|行セットの圧縮の状態。<br /><br /> 0 = NONE<br /><br /> 1 = 行<br /><br /> 2 = ページ|  
|data_compression_desc|**nvarchar(60)**|各パーティションの圧縮の状態。 行ストア テーブルに指定できる値は、NONE、ROW、および PAGE です。 列ストアテーブルに指定できる値は、列ストアと COLUMNSTORE_ARCHIVE です。|  
|optimize_for_sequential_key|**bit**|1 = パーティションには、最後のページ挿入最適化が有効になっています。<br><br>0 = 既定値。 パーティションで最後のページ挿入の最適化が無効になっています。|
  
## <a name="permissions"></a>アクセス許可  
 `public` ロールのメンバーシップが必要です。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="general-remarks"></a>全般的な解説  
 列ストアインデックスを作成または再構築するたびに、新しい列ストア内部インデックスを再作成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. テーブルのすべての内部行セットを表示する  
 この例では、テーブルのすべての内部列ストア行セットが返されます。 また、hobt_id を使用して、特定の行セットに関する詳細情報を確認することもできます。  
  
```sql  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>参照  
 [オブジェクト カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server システム カタログに対するクエリに関してよくあるご質問](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
